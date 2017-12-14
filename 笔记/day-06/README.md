## 计算某个文件\文件夹的大小
```objc
@implementation NSString (XMGExtension)
//- (unsigned long long)fileSize
//{
//    // 总大小
//    unsigned long long size = 0;
//
//    // 文件管理者
//    NSFileManager *mgr = [NSFileManager defaultManager];
//
//    // 文件属性
//    NSDictionary *attrs = [mgr attributesOfItemAtPath:self error:nil];
//
//    if ([attrs.fileType isEqualToString:NSFileTypeDirectory]) { // 文件夹
//        // 获得文件夹的大小  == 获得文件夹中所有文件的总大小
//        NSDirectoryEnumerator *enumerator = [mgr enumeratorAtPath:self];
//        for (NSString *subpath in enumerator) {
//            // 全路径
//            NSString *fullSubpath = [self stringByAppendingPathComponent:subpath];
//            // 累加文件大小
//            size += [mgr attributesOfItemAtPath:fullSubpath error:nil].fileSize;
//        }
//    } else { // 文件
//        size = attrs.fileSize;
//    }
//
//    return size;
//}

- (unsigned long long)fileSize
{
    // 总大小
    unsigned long long size = 0;

    // 文件管理者
    NSFileManager *mgr = [NSFileManager defaultManager];

    // 是否为文件夹
    BOOL isDirectory = NO;

    // 路径是否存在
    BOOL exists = [mgr fileExistsAtPath:self isDirectory:&isDirectory];
    if (!exists) return size;

    if (isDirectory) { // 文件夹
        // 获得文件夹的大小  == 获得文件夹中所有文件的总大小
        NSDirectoryEnumerator *enumerator = [mgr enumeratorAtPath:self];
        for (NSString *subpath in enumerator) {
            // 全路径
            NSString *fullSubpath = [self stringByAppendingPathComponent:subpath];
            // 累加文件大小
            size += [mgr attributesOfItemAtPath:fullSubpath error:nil].fileSize;
        }
    } else { // 文件
        size = [mgr attributesOfItemAtPath:self error:nil].fileSize;
    }

    return size;
}
@end

XMGLog(@"%zd", @"/Users/xiaomage/Desktop".fileSize);
```

## 计算文字的宽度
```objc
CGFloat titleW = [字符串 sizeWithFont:字体大小].width;
CGFloat titleW = [字符串 sizeWithAttributes:@{NSFontAttributeName : 字体大小}].width;
```

## 有透明度的颜色
```objc
[UIColor colorWithRed:1.0 green:1.0 blue:1.0 alpha:0.2];
[UIColor colorWithWhite:1.0 alpha:0.2];
[[UIColor whiteColor] colorWithAlphaComponent:0.2];
```

## viewWithTag:内部的大致实现思路
```objc
@implementation UIView
- (UIView *)viewWithTag:(NSInteger)tag
{
    if (self.tag == tag) return self;

    for (UIView *subview in self.subviews) {
        return [subview viewWithTag:tag];
    }
}
@end
```
