## 矩形框比较的2个函数
- bool CGRectContainsRect(CGRect rect1, CGRect rect2)
    - 判断rect1是否包含了rect2
- bool CGRectIntersectsRect(CGRect rect1, CGRect rect2)
    - 判断rect1和rect2是否有重叠
    - `注意：rect1和rect2要在同一个坐标系，比较结果才准确`

## 转换坐标系总结
```objc
view2坐标系 : 以view2的左上角为坐标原点
view1坐标系 : 以view1的左上角为坐标原点

CGRect newRect = [view1 convertRect:rect fromView:view2];
// 让rect这个矩形框， 从view2坐标系转换到view1坐标系, 得出一个新的矩形框newRect
// rect和view2的含义 ： 用来确定矩形框原来在哪

CGRect newRect = [view1 convertRect:rect toView:view2];
// 让rect这个矩形框， 从view1坐标系转换到view2坐标系, 得出一个新的矩形框newRect
// rect和view1的含义 ：用来确定矩形框原来在哪
```

## 获得一个控件在window中的位置和尺寸
- 以获得redView在window中的位置和尺寸为例

```objc
CGRect newRect = [[UIApplication sharedApplication].keyWindow convertRect:redView.bounds fromView:redView];
CGRect newRect = [[UIApplication sharedApplication].keyWindow convertRect:redView.frame fromView:redView.superview];
CGRect newRect = [redView convertRect:redView.bounds toView:[UIApplication sharedApplication].keyWindow];
CGRect newRect = [redView.superview convertRect:redView.frame toView:[UIApplication sharedApplication].keyWindow];
CGRect newRect = [redView convertRect:redView.bounds toView:nil];
CGRect newRect = [redView.superview convertRect:redView.frame toView:nil];
```
