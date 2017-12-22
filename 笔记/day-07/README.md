## addObject:和addObjectsFromArray:的区别
```objc
self.topics = @[20, 19, 18]
moreTopics = @[17, 16, 15]

self.topics = @[20, 19, 18, @[17, 16, 15]]
[self.topics addObject:moreTopics];

self.topics = @[20, 19, 18, 17, 16, 15]
[self.topics addObjectsFromArray:moreTopics];
```

## 服务器分页的做法
```objc
服务器数据库的数据 = @[23, 22, 21, 20, 19, 18, 17, 16, 15, 14, 13, 12, 11, 10]


第1页数据 == @[20, 19, 18, 17, 16]

做法1:
发送page参数 : page=2
第2页数据 == @[18, 17, 16, 15, 14]

做法2:
发送maxid参数 : maxid=16
第2页数据 == @[15, 14, 13, 12, 11]
```

## 集成MJRefresh
- [github](https://github.com/CoderMJLee/MJRefresh)
- 基本用法

```objc
self.tableView.mj_header = [MJRefreshNormalHeader headerWithRefreshingTarget:self refreshingAction:@selector(loadNewTopics)];
[self.tableView.mj_header beginRefreshing];

self.tableView.mj_footer = [MJRefreshAutoNormalFooter footerWithRefreshingTarget:self refreshingAction:@selector(loadMoreTopics)];
```

## 利用AFN取消请求
```objc
// 取消所有请求
for (NSURLSessionTask *task in self.manager.tasks) {
    [task cancel];
}

// 取消所有请求
[self.manager.tasks makeObjectsPerformSelector:@selector(cancel)];

// 关闭NSURLSession + 取消所有请求
// NSURLSession一旦被关闭了, 就不能再发请求
[self.manager invalidateSessionCancelingTasks:YES];

// 注意: 一个请求任务被取消了(cancel), 会自动调用AFN请求的failure这个block, block中传入error参数的code是NSURLErrorCancelled
```

## UIAlertController
```objc
UIAlertController *controller = [UIAlertController alertControllerWithTitle:nil message:nil preferredStyle:UIAlertControllerStyleActionSheet];

[controller addAction:[UIAlertAction actionWithTitle:@"收藏" style:UIAlertActionStyleDefault handler:^(UIAlertAction * _Nonnull action) {
    NSLog(@"点击了[收藏]按钮");
}]];

[controller addAction:[UIAlertAction actionWithTitle:@"举报" style:UIAlertActionStyleDestructive handler:^(UIAlertAction * _Nonnull action) {
    NSLog(@"点击了[举报]按钮");
}]];

[controller addAction:[UIAlertAction actionWithTitle:@"取消" style:UIAlertActionStyleCancel handler:^(UIAlertAction * _Nonnull action) {
    NSLog(@"点击了[取消]按钮");
}]];

//    [controller addTextFieldWithConfigurationHandler:^(UITextField * _Nonnull textField) {
//        textField.textColor = [UIColor redColor];
//    }];

[self.window.rootViewController presentViewController:controller animated:YES completion:nil];
```
