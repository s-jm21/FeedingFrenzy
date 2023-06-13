package fish;

import java.awt.*;
import java.awt.event.*;
import javax.swing.JFrame;


public class GameWin extends JFrame{
	//游戏状态：0游戏未开始 1游戏中 2通关失败 3游戏成功 4暂停
	//游戏默认状态
	static int state=0;
	
	Image offScreenImage;
	//设置宽高
	int width=1440;
	int height=900;
	
	
	double random;
	//计数器
	int time=0;
	
	//背景
	Bg bg=new Bg();
	
	//敌方鱼类
	Enamy enamy;
	
	//boss类
	Enamy boss;
	//是否生成boss
	boolean isboss=false;
	
	
	//我方鱼类
	Myfish myFish=new Myfish();
	
	public void launch() {
		this.setSize(width, height);//设置窗口大小
		this.setLocationRelativeTo(null);//设置窗口在屏幕居中位置
		
		this.setTitle("Feeding Frenzy");
		this.setDefaultCloseOperation(EXIT_ON_CLOSE);;
		this.setVisible(true);//设置窗口可见
		
		this.addMouseListener(new MouseAdapter(){
			public void mouseClicked(MouseEvent e) {
				super.mouseClicked(e);
				if(e.getButton()==1&&state==0) {
					state=1;
					repaint();//重新绘制窗口；
				}
				if(e.getButton()==1&&state==2||state==3) {
					reGame();
					state=1;
				}
			}
		});
	
	//键盘移动
		this.addKeyListener(new KeyAdapter() {
			//按下
			public void keyPressed(KeyEvent e) {
				super.keyPressed(e);
				
				if(e.getKeyCode()==38) {
					GameUtils.UP=true;
				}
				if(e.getKeyCode()==40) {
					GameUtils.DOWN=true;
				}
				if(e.getKeyCode()==37) {
					GameUtils.LEFT=true;
				}
				if(e.getKeyCode()==39) {
					GameUtils.RIGHT=true;
				}
				if(e.getKeyCode()==32) {
					switch(state) {
					case 1:
						state=4;
						GameUtils.drawWord(getGraphics(),"游戏暂停",Color.RED,50,20,400);
						break;
					case 4:
						state=1;
						break;
					}
				}
			}
			//松开
			public void keyReleased(KeyEvent e) {
				super.keyReleased(e);
				if(e.getKeyCode()==38) {
					GameUtils.UP=false;
				}
				if(e.getKeyCode()==40) {
					GameUtils.DOWN=false;
				}
				if(e.getKeyCode()==37) {
					GameUtils.LEFT=false;
				}
				if(e.getKeyCode()==39) {
					GameUtils.RIGHT=false;
				}
			}
		});
		
	//循环调用
	while(true) {
		repaint();
		time++;
		try {
			Thread.sleep(40);
		}catch(InterruptedException e) {
			e.printStackTrace();
		}
	}
	}
	public void paint(Graphics g){
		
		//懒加载模式初始化对象
		offScreenImage=createImage(width,height);
		Graphics gImage=offScreenImage.getGraphics(); //获取图片对应的画笔图像，把组件绘制到新的图片中
		//设置背景图片
		bg.paintSelf(gImage,myFish.level);
		switch (state) {
		case 0:
			break;
		case 1:
			myFish.paintSelf(gImage);
			logic();
			for(Enamy enamy:GameUtils.EnamyList) {
				enamy.paintSelf(gImage);
			}
			if(isboss) {
				boss.x=boss.x+boss.dir*boss.speed;
				boss.paintSelf(gImage);
				if(boss.x<0) {
					gImage.setColor(Color.RED);
					gImage.fillRect(boss.x, boss.y,2400, boss.height);
				}
			}
			
			break;
		case 2:
			for(Enamy enamy:GameUtils.EnamyList) {
				enamy.paintSelf(gImage);
			}
			if(isboss) {
				boss.paintSelf(gImage);
			}
			break;
		case 3:
			myFish.paintSelf(gImage);
			break;
		case 4:
			return;
			default:
		
		}
		//把内存当中绘制好的新图片，一次性绘制到主窗口中
		g.drawImage(offScreenImage,0,0,null);
	}
	
	void logic() {
		//关卡难度
		if(GameUtils.count<5) {
			GameUtils.level=0;
			myFish.level=1;
		}else if(GameUtils.count<=15) {
			GameUtils.level=1;
		}else if(GameUtils.count<=50) {
			GameUtils.level=2;
			myFish.level=2;
		}else if(GameUtils.count<=150) {
			GameUtils.level=3;
			myFish.level=3;
		}else if(GameUtils.count<=300) {
			GameUtils.level=4;
			myFish.level=3;
		}else if(GameUtils.count>300) {
			state=3;
		}
		
		//生成鱼
		random=Math.random();
		switch(GameUtils.level) {
		case 4:
			if(time%60==0) {
				if(random>0) {
					boss=new Enamy_Boss();
					isboss=true;
				} 
			}
			
		case 3:
			if(time%10==0) {
				if(random>0.5) {
					enamy=new EnamyLeft();
				}else {
				    enamy=new EnamyRight();
				}
				GameUtils.EnamyList.add(enamy);
			}
		case 2:
			if(time%30==0) {
				if(random>0.5) {
					enamy=new EnamyLeft3();
				}else {
				    enamy=new EnamyRight3();
				}
				GameUtils.EnamyList.add(enamy);
			}
		
		case 1:
			if(time%20==0) {
				if(random>0.5) {
					enamy=new EnamyLeft2();
				}else {
				    enamy=new EnamyRight2();
				}
				GameUtils.EnamyList.add(enamy);
			}
		case 0:
			if(time%10==0) {
				if(random>0.5) {
					enamy=new EnamyLeft();
				}else {
				    enamy=new EnamyRight();
				}
				GameUtils.EnamyList.add(enamy);
			}
			break;
			default:
		}
		
		//定义移动方向
		for(Enamy enamy:GameUtils.EnamyList) {
			enamy.x=enamy.x+enamy.dir*enamy.speed;
		
			if(isboss) {
				if(boss.getRec().intersects(getBounds())) {
			       enamy.x=-200;
				   enamy.y=-200;
				  }
				if(boss.getRec().intersects(myFish.getRec())) {
					state=2;
				}
			}
		
			//我方鱼与敌方鱼碰撞检测
			if(myFish.getRec().intersects(enamy.getRec())) {
				if(myFish.level>=enamy.type) {
					System.out.println("碰撞了");
					enamy.x=-200;
				    enamy.y=-200;
				    GameUtils.count=GameUtils.count+enamy.count;
				}else {
					state=2;
				}
				
				
			}
			
			}
	}
	//重新开始
	void reGame() {
		GameUtils.EnamyList.clear();
		time=0;
		myFish.level=1;
		GameUtils.count=0;
		myFish.x=700;
		myFish.y=500;
		myFish.width=50;
		myFish.height=50;
		boss=null;
		isboss=false;
		
		
	}
	public static void main(String args[]) {
		GameWin gameWin=new GameWin();
		gameWin.launch();
	}

}
