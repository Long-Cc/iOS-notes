## 属性名注意点
- 对象属性名不能以new开头
```objc
@property (nonatomic, strong) NSMutableArray<XMGComment *> *newComments;
```

## 常见错误
```objc
-[__NSArray0 objectForKeyedSubscript:]: unrecognized selector sent to instance 0x7fb738c01870
// 错误地将NSArray当做NSDictionary来使用了
```

## block细节
- 如果【block内部】使用【外部声明的强引用】访问【对象A】, 那么【block内部】会自动产生一个【强引用】指向【对象A】
- 如果【block内部】使用【外部声明的弱引用】访问【对象A】, 那么【block内部】会自动产生一个【弱引用】指向【对象A】
