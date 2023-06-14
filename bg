package fish;

import java.awt.Color;
import java.awt.Graphics;

public class Bg {

	public void paintSelf(Graphics g,int fishLevel) {
		g.drawImage(GameUtils.background, 0, 0,null);
		switch(GameWin.state) {
		case 0:
			GameUtils.drawWord(g, "开始", Color.GREEN, 80,700,500);
			break;
		case 1:
			GameUtils.drawWord(g, "积分"+GameUtils.count, Color.ORANGE, 50,200,120);
			GameUtils.drawWord(g, "难度"+GameUtils.level, Color.ORANGE, 80,600,120);
			GameUtils.drawWord(g, "等级"+fishLevel, Color.ORANGE, 80,1000,120);
			break;
		case 2:
			GameUtils.drawWord(g, "积分"+GameUtils.count, Color.ORANGE, 50,200,120);
			GameUtils.drawWord(g, "难度"+GameUtils.level, Color.ORANGE, 80,600,120);
			GameUtils.drawWord(g, "等级"+fishLevel, Color.ORANGE, 80,1000,120);
			GameUtils.drawWord(g, "失败", Color.RED,80,700,500);
			break;
		case 3:
			GameUtils.drawWord(g, "积分"+GameUtils.count, Color.ORANGE, 50,200,120);
			GameUtils.drawWord(g, "难度"+GameUtils.level, Color.ORANGE, 80,600,120);
			GameUtils.drawWord(g, "等级"+fishLevel, Color.ORANGE, 80,1000,120);
			GameUtils.drawWord(g, "胜利", Color.RED, 80,700,500);
			break;
		case 4:
			break;
			default:
		}
		
	}

}
