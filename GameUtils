package fish;

import java.awt.Color;
import java.awt.Font;
import java.awt.Graphics;
import java.awt.Image;
import java.awt.Toolkit;
import java.util.ArrayList;
import java.util.List;

public class GameUtils {
	//方向
	static boolean UP=false;
	static boolean DOWN=false;
	static boolean LEFT=false;
	static boolean RIGHT=false;
	
	//分数
	static int count=0;
	
	//等级
	static int level=0;
	
	//敌方鱼类集合
	public static List<Enamy>EnamyList=new ArrayList<>();
	//背景图
	public static Image background=Toolkit.getDefaultToolkit().createImage("D:\\eclipse\\FeedingFrenzy\\image\\Ocean.jpg");
	//敌方鱼类
	public static Image enamyl1=Toolkit.getDefaultToolkit().createImage("D:\\eclipse\\FeedingFrenzy\\image\\Enamy1.png");
	public static Image enamyr1=Toolkit.getDefaultToolkit().createImage("D:\\eclipse\\FeedingFrenzy\\image\\Enamy1.png");
	public static Image enamyl2=Toolkit.getDefaultToolkit().createImage("D:\\eclipse\\FeedingFrenzy\\image\\Enamy2.png");
	public static Image enamyr2=Toolkit.getDefaultToolkit().createImage("D:\\eclipse\\FeedingFrenzy\\image\\Enamy2.png");
	public static Image enamyl3=Toolkit.getDefaultToolkit().createImage("D:\\eclipse\\FeedingFrenzy\\image\\Enamy3.jpg");
	public static Image enamyr3=Toolkit.getDefaultToolkit().createImage("D:\\eclipse\\FeedingFrenzy\\image\\Enamy3.jpg");
	public static Image bossing=Toolkit.getDefaultToolkit().createImage("D:\\eclipse\\FeedingFrenzy\\image\\Enamy4.jpg");
	
	//我方鱼类
	public static Image MyfishimgR=Toolkit.getDefaultToolkit().createImage("D:\\eclipse\\FeedingFrenzy\\image\\myfish.jpg");
	public static Image MyfishimgL=Toolkit.getDefaultToolkit().createImage("D:\\eclipse\\FeedingFrenzy\\image\\myfish.jpg");
	
	//绘制文字的工具类
	public static void drawWord(Graphics g,String str,Color color,int size,int x,int y) {
		g.setColor(color);
		g.setFont(new Font("仿宋",Font.BOLD,size));
		g.drawString(str,x,y);
		
	}

	

}
