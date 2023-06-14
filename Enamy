package fish;

import java.awt.Graphics;
import java.awt.Image;
import java.awt.Rectangle;

public class Enamy {
	//图片
	Image img;
	//物体坐标
	int x;
	int y;
	int width;
	int height;
	//移动速度
	int speed;
	//方向：从左向右1，从左向右-1
	int dir=1;
	//类型
	int type;
	//分值
	int count;
	//绘制自身方法
	public void paintSelf(Graphics g) {
		g.drawImage(img, x, y, width, height,null);
	}
	//获取自身矩形用于碰撞
	public Rectangle getRec() {
		return new Rectangle(x,y,width,height);
	}

}
