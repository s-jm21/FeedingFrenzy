package fish;

import java.awt.Graphics;
import java.awt.Image;
import java.awt.Rectangle;

public class Myfish {
	//图片
	Image img=GameUtils.MyfishimgL;
	//坐标
	int x=700;
	int y=500;
	int width=50;
	int height=50;
	//移动速度
	int speed=20;
	//等级
	int level=1;
	
	void logic() {
		if(GameUtils.UP) {
			y=y-speed;
		}
		if(GameUtils.DOWN) {
			y=y+speed;
		}
		if(GameUtils.LEFT) {
			x=x-speed;
			img=GameUtils.MyfishimgL;
		}
		if(GameUtils.RIGHT) {
			x=x+speed;
			img=GameUtils.MyfishimgR;
		}
	}
	
	
	//绘制自身方法
	public void paintSelf(Graphics g) {
		logic();
		g.drawImage(img, x, y, width+GameUtils.count, height+GameUtils.count,null);
	}
	//获取自身矩形的方法用于碰撞检测
	public Rectangle getRec() {
		return new Rectangle(x,y,width+GameUtils.count,height+GameUtils.count);
	}

}
