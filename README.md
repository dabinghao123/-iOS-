# -----IOS-----代码

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
