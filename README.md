# DebugWindow
一个在真机上测试时方便查看输出日志的小工具。

> 在我们实际开发中经常要配合测试进行debug，在真机上测试的时候很难看到控制台的输出日志。真机连接在电脑上进行测试的时候还好，但是有些功能测试的时候可能需要程序杀死重新打开。比如在测试推送功能的时候，需要测试程序在杀死的情况下收到推送怎么处理。这个时候很难看到推送内容是什么，要想根据推送内容写具体的处理逻辑就很不方便了。比如程序莫名其妙地闪退了，你想定位bug却很难看到奔溃日志？比如想查看真机上沙盒中保存的某个值？再比如测试人员在测试过程中想查看当前加载的网页的完整链接（包括自己拼接的参数等等）？再比如想动态修改本地保存的一个状态值而不用重启APP？😂这个时候是不是很想来一个不影响程序的正常运行又可以实时查看打印日志的轮子😉？


## 这个小工具实现了以下功能：

- 每次程序启动就新建一个以当前时间命名的日志文件。
- 自定义打印日志的方法，调用后将把日志记录于文件中。
- 重定向NSLog输出日志到文件中，这样你就不用替换到你项目中已有的NSLog()代码啦。
- 重定向程序奔溃日志到文件中。
- 自动根据当前设备信息选择要不要记录日志的同时把日志打印到控制台。
- 方便增删改查当前沙盒中保存的键值对。
- 通过iTunes查看设备上的日志文件。（真机连接iTunes，通过iTunes的设置->应用->文件共享，找到DebugWindow，就可以看到Logs文件夹。）
- 在日志文件中搜索并高亮字符串。

看完介绍是不是心情有点小激动甚至想“来一发”😂？


## 使用方法

- 将DebugWindow文件夹下的类引入你的项目。
- 在程序启动时调用``[YLDebugWindow startDebug]``方法开启日志记录。
- 如果需要自定义打印日志，调用YLLog()方法，你也可以根据自己实际情况修改该方法。
 
## 注意事项

- 建议在往沙盒中存数据的时候将所有key都带上特定前缀，比如我这里是"kYL"开头的，这样在获取沙盒中键值对的时候方便只看自己保存的键值对。
- 默认在模拟器上和真机连接在电脑上的时候是不把NSLog输出和异常输出日志记录到文件中的，如果需要在模拟器上看效果，可以修改YLLogTool的``needRedirect``方法。

## 更新记录

---2017-05-11---

```
- 使用UIWebView替代QLPreviewController来预览日志文件。
- 解决中文乱码问题。
- 在日志文件中搜索并高亮字符串。
- 增删改查当前沙盒中保存的键值对，方便调试。
```


## 效果图

![](https://github.com/lqcjdx/DebugWindow/blob/master/DebugWindow/DebugWindow/log.gif)


## 参考

- [【iOS开发】iOS10 Log调试小工具](http://www.jianshu.com/p/23011d141622)
- [iOS学习笔记40-日志重定向](http://www.jianshu.com/p/aaf49d0d0d98)
- [Search and highlight text in UIWebView](http://www.icab.de/blog/2010/01/12/search-and-highlight-text-in-uiwebview/)
