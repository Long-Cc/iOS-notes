## 控制台可能会输出以下警告信息
- 警告的原因: [UIImage imageNamed:nil]
```objc
CUICatalog: Invalid asset name supplied: (null)
CUICatalog: Invalid asset name supplied: (null)
```

- 警告的原因: [UIImage imageNamed:@""]
```objc
CUICatalog: Invalid asset name supplied:
CUICatalog: Invalid asset name supplied:
```

## 准确判断一个字符串是否有内容
```objc
if (string.length) {

}

/*
错误写法:
if (string) {

}
*/
```

## 替换UITabBarController内部的tabBar
```objc
// 这里的self是UITabBarController
[self setValue:[[XMGTabBar alloc] init] forKeyPath:@"tabBar"];
```

## center和size的设置顺序
- 建议的设置顺序
    - 先设置size
    - 再设置center

## 给系统自带的类增加分类
- 建议增加的分类属性名\方法名前面加上前缀, 比如

```objc
@interface UIView (XMGExtension)
@property (nonatomic, assign) CGFloat xmg_width;
@property (nonatomic, assign) CGFloat xmg_height;
@property (nonatomic, assign) CGFloat xmg_x;
@property (nonatomic, assign) CGFloat xmg_y;
@property (nonatomic, assign) CGFloat xmg_centerX;
@property (nonatomic, assign) CGFloat xmg_centerY;

@property (nonatomic, assign) CGFloat xmg_right;
@property (nonatomic, assign) CGFloat xmg_bottom;
@end
```

## 按钮常见的访问方法
```objc
[button imageForState:UIControlStateNormal].size;
button.currentImage.size;

[button backgroundImageForState:UIControlStateNormal];
button.currentBackgroundImage;

[button titleForState:UIControlStateNormal];
button.currentTitle;

[button titleColorForState:UIControlStateNormal];
button.currentTitleColor;
```

## 设置按钮的内边距
```objc
@property(nonatomic) UIEdgeInsets contentEdgeInsets UI_APPEARANCE_SELECTOR;
@property(nonatomic) UIEdgeInsets titleEdgeInsets;
@property(nonatomic) UIEdgeInsets imageEdgeInsets;
```

## 解决导航控制器pop手势失效
```
self.interactivePopGestureRecognizer.delegate = self;

- (BOOL)gestureRecognizerShouldBegin:(UIGestureRecognizer *)gestureRecognizer
{
    // 手势何时有效 : 当导航控制器的子控制器个数 > 1就有效
    return self.childViewControllers.count > 1;
}
```
