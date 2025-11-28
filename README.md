using System;

public class RotationTranslation
{
    public static (double alphaDeg, double tX, double tY) CalculateRotationTranslation(
        double x, double y, double thetaDeg, 
        double x1, double y1, 
        double x2, double y2, double theta2Deg)
    {
        // 计算旋转角度 alpha（度）
        double alphaDeg = theta2Deg - thetaDeg;

        // 转换为弧度
        double alphaRad = alphaDeg * Math.PI / 180.0;

        // 计算旋转后的中间点 (x', y')
        double cosAlpha = Math.Cos(alphaRad);
        double sinAlpha = Math.Sin(alphaRad);
        double xPrime = x1 + (x - x1) * cosAlpha - (y - y1) * sinAlpha;
        double yPrime = y1 + (x - x1) * sinAlpha + (y - y1) * cosAlpha;

        // 计算平移向量 (t_x, t_y)
        double tX = x2 - xPrime;
        double tY = y2 - yPrime;

        return (alphaDeg, tX, tY);
    }

    public static void Main()
    {
        // 示例输入
        double x = 1, y = 1, thetaDeg = 0; // p1
        double x1 = 0, y1 = 0;             // 旋转中心 A
        double x2 = 0, y2 = 2, theta2Deg = 90; // p2

        var (alphaDeg, tX, tY) = CalculateRotationTranslation(x, y, thetaDeg, x1, y1, x2, y2, theta2Deg);

        Console.WriteLine($"旋转角度: {alphaDeg:F6} 度");
        Console.WriteLine($"平移向量: ({tX:F6}, {tY:F6})");
    }
}
