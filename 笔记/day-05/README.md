## CocoaPods
- Podfile.lock文件
    - 最后一次更新Pods时, 所有第三方框架的版本号
- 常用指令的区别
    - pod install
        - 会根据Podfile.lock文件中列举的版本号来安装第三方框架
        - 如果一开始Podfile.lock文件不存在, 就会按照Podfile文件列举的版本号来安装第三方框架
        - 安装框架之前, 默认会执行pod repo update指令
    - pod update
        - 将所有第三方框架更新到最新版本, 并且创建一个新的Podfile.lock文件
        - 安装框架之前, 默认会执行pod repo update指令
    - pod install --no-repo-update
    - pod update --no-repo-update
        - 安装框架之前, 不会执行pod repo update指令

## 利用SDWebImage设置UIButton的图片
- 正确用法

```objc
[button sd_setImageWithURL:[NSURL URLWithString:url] forState:UIControlStateNormal placeholderImage:image];
```

## 解决tableView设置tableFooterView时contentSize不正确的问题
```objc
tableView.tableFooterView = footerView;
// 重新刷新数据(会重新计算contentSize)
[tableView reloadData];
```

## 查找字符串的常见方法
```objc
// 如果range.location == 0, 说明是以searchString开头
// 如果range.location == NSNotFound或者range.length == 0, 说明没找到对应的字符串
- (NSRange)rangeOfString:(NSString *)searchString;
// 是否以str开头
- (BOOL)hasPrefix:(NSString *)str;
// 是否以str结尾
- (BOOL)hasSuffix:(NSString *)str;
// 是否包含了str(不管头部\中间\尾部)
- (BOOL)containsString:(NSString *)str;
```

## 计算总行数\总页数
```objc
总数 : 2476
每页显示的最大数量 : 35
总页数 :  (2476 + 35 - 1) / 35
pagesCount = (总数  +  每页显示的最大数量 - 1) / 每页显示的最大数量

总数 : 1660
每一行显示的最大数量 : 30
总行数 : (1660 + 30 - 1) / 30
rowsCount = (总数  +  每行显示的最大数量 - 1) / 每行显示的最大数量
```
