## 自动拉伸问题
- 从xib中加载进来的控件的`autoresizingMask`属性值默认是
    - `UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight`
- 如果一个控件显示出来的大小和当初设置的frame大小不一致,有可能是因为`autoresizingMask`属性值包含了`UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight`,解决方案

```objc
控件.autoresizingMask = UIViewAutoresizingNone;
```
