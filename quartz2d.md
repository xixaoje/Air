### 01-Quartz2D简介
<hr>
####1.什么是Quartz2D?
他是一个二维的绘图引擎,同时支持iOS和Mac系统

####2.Quartz2D能完成的工作
画基本线条,绘制文字,图片,截图, 定义UIView.
#### 3.Quartz2D实例演示.

#### 4.Quartz2D在开发中的价值
当我们的控件样式极其复杂时,可以把控件内部的结构给画出画,就是自定义控件.

####  5.什么是图形上下文,上下文的类型有哪些?[^图片上下文就是数据类型]

图形上下文是用来保存用户绘制的内容状态,并决定绘制到哪个地方的.

用户把绘制好的内容先保存到图形上下文,

然后根据选择的图形上下文的不同,绘制的内容显示到地方也不相同,即输出 标也不相同.


图形上下文的类型有:

Bitmap Graphics Context(位图上下文,图片)

PDF Graphics Context

Window Graphics Context

Layer Graphics Context(`图层上下文`, 定义UIView取得上下文就是图层上下文. UIView之所以能够显示就是因为他内部有一个图层)

Printer Graphics Context

#### 6.如何自定义UIView,步骤是什么?
先得要有上下文,有了上文才能决定把绘制的东西显示到哪个地方去. 其次就是这个上下文必须得和View相关联.才能将内容绘制到View上面.
步骤: 
######1.要先 定定UIView
######2.实现DrawRect方法
######3.在DrawRect方法中取得跟View相关联的上下文.
######4.绘制路径(描述路径长什么样).
######5.把描述好的路径保存到上下文(即:添加路径到上下文)
######6.把上下文的内容渲染到View

```
//1.获取上下文(获取,创建上下文 都 以uigraphics开头)
    CGContextRef ctx = UIGraphicsGetCurrentContext();
    //2.绘制路径
    UIBezierPath *path = [UIBezierPath bezierPath];
    //2.1 设置起点
    [path moveToPoint:CGPointMake(50, 280)];
    //2.2 添加一根线到终点
    [path addLineToPoint:CGPointMake(250, 50)];
    
    //画第二条线
    //    [path moveToPoint:CGPointMake(100, 280)];
    //    [path addLineToPoint:CGPointMake(250, 100)];
    
    //addLineToPoint:把上一条线的终点当作是下一条线的起点
    [path addLineToPoint:CGPointMake(200, 280)];
    
    //上下文的状态
    //设置线的宽度
    CGContextSetLineWidth(ctx, 10);
    //设置线的连接样式
    CGContextSetLineJoin(ctx, kCGLineJoinRound);
    //设置线的顶角样式
    CGContextSetLineCap(ctx, kCGLineCapRound);
    //设置颜色
    [[UIColor redColor] set];
    
    
    
    //3.把绘制的内容添加到上下文当中.
    //UIBezierPath:UIKit框架 ->    CGPathRef:CoreGraphics框架
    CGContextAddPath(ctx, path.CGPath);
    //4.把上下文的内容显示到View上(渲染到View的layer)(stroke fill)
    CGContextStrokePath(ctx);
```
