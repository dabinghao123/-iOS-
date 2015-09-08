# -----IOS-----代码片段


## 修改图片的颜色
<pre><code>
- (UIImage *)jsq_image:(UIImage *)image maskedWithColor:(UIColor *)maskColor
{
    CGRect imageRect = CGRectMake(0.0f, 0.0f, image.size.width, image.size.height);
    
    UIGraphicsBeginImageContextWithOptions(imageRect.size, NO, image.scale);
    CGContextRef context = UIGraphicsGetCurrentContext();
    
    CGContextScaleCTM(context, 1.0f, -1.0f);
    CGContextTranslateCTM(context, 0.0f, -imageRect.size.height);

    CGContextClipToMask(context, imageRect, image.CGImage);
    CGContextSetFillColorWithColor(context, maskColor.CGColor);
    CGContextFillRect(context, imageRect);
    
    UIImage *newImage = UIGraphicsGetImageFromCurrentImageContext();
    UIGraphicsEndImageContext();
    
    return newImage;
}

</code></pre>


###使用类别旋转图片
<pre>
<code>
- (UIImage*)imageRotatedByDegrees:(CGFloat)degrees
{
    
    CGFloat width = CGImageGetWidth(self.CGImage);
    CGFloat height = CGImageGetHeight(self.CGImage);
    
    CGSize rotatedSize;
    
    rotatedSize.width = width;
    rotatedSize.height = height;
    
    UIGraphicsBeginImageContext(rotatedSize);
    
    CGContextRef bitmap = UIGraphicsGetCurrentContext();
    
    CGContextTranslateCTM(bitmap, rotatedSize.width/2, rotatedSize.height/2);
    CGContextRotateCTM(bitmap, degrees * M_PI / 180);
    CGContextRotateCTM(bitmap, M_PI);
    CGContextScaleCTM(bitmap, -1.0, 1.0);
    
    CGContextDrawImage(bitmap, CGRectMake(-rotatedSize.width/2, -rotatedSize.height/2, rotatedSize.width, rotatedSize.height), self.CGImage);
    UIImage* newImage = UIGraphicsGetImageFromCurrentImageContext();
    UIGraphicsEndImageContext();
    
    return newImage;
}
</code>
</pre>

<pre>
### Push出现卡顿现象
<code>
最近才使用Xcode5 iOS7进行开发，遇到了个小问题，在使用navigation的pushViewController进行push的时候，两个页面间的动画会出现卡顿一下再推出的效果，最后找出，是因为iOS7 viewController背景颜色的问题，其实不是卡顿，是由于透明色颜色重叠后视觉上的问题，只要在新push里设置下背景颜色就好了
    self.view.backgroundColor = [UIColorgrayColor];

找个位置加上就正常显示了。
</code>

</pre>

<pre>
##点到线段的最短距离
<code>
double x1, y1, x2, y2, x3, y3;    
double px = x2 - x1;
double py = y2 - y1;
double som = px * px + py * py;
double u =  ((x3 - x1) * px + (y3 - y1) * py) / som;
if (u > 1) {
    u = 1;
}
if (u < 0) {
    u = 0;
}
//the closest point
double x = x1 + u * px;
double y = y1 + u * py;
double dx = x - x3;
double dy = y - y3;      
double dist = sqrt(dx*dx + dy*dy);
<code>

</pre>
