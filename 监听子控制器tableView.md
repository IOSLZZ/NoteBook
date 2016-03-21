# 监听子控制器tableView
移除的时候需要注意:

如果出现这种错误:

```
 *** Terminating app due to uncaught exception 'NSRangeException', reason: 'Cannot remove an observer for the key path "contentOffset" from because it is not registered as an observer.'
 
```
```
[self.childViewControllers enumerateObjectsUsingBlock:^(__kindof BaseViewController * _Nonnull vc, NSUInteger idx, BOOL * _Nonnull stop) {
        NSLog(@"%@",vc);
        @try {
            if(vc.tableView){
                [vc.tableView removeObserver:self forKeyPath:@"contentOffset"];
                [vc.tableView removeFromSuperview];
            }
        }
        @catch (NSException *exception) {
            NSLog(@"exception:%@",exception);
        }
        @finally {
            NSLog(@"finally");
        }
        
    }];
```

