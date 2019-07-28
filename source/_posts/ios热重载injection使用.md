---
title: ios热重载injection使用
date: 2019-04-18 10:47:23
tags: iOS开发
---
Injection可以在不重新编译整个程序的情况下，用于观察代码修改后的效果，从而提升开发效率。目前支持模拟器运行调试。
GitHub源码地址为：https://github.com/johnno1962/injectionforxcode.git
上述源码是作为Xcode插件使用Injection，但是自Xcode8以后不支持第三方插件，所以推出了app，可以在AppStore中下载，名字是InjectionIII.
下载完成后运行该工具，在pc右上方可以看到其菜单仅包含7项内容。
![avatar](https://gitee.com/lab601_chenhao/image-bed/raw/master/FileWatch.jpg)
<!-- more -->
> InjectionIII使用

1.InjectionIII应用

在open project选项中选择要运行的项目文件夹后，点击select project directory。要确保File Watcher处于开启状态，即其前方有☑️标示。

2.Xcode应用
（1）Xcode打开需要运行的项目，在AppDelegate.m文件中的application didFinishLaunchingWithOptions函数中添加如下代码，此默认是选择iOS，可依据具体需要选择对应设备代码。这里所用的##Xcode版本为10.1##。

```
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Override point for customization after application launch.
#if DEBUG
    // iOS
    [[NSBundle bundleWithPath:@"/Applications/InjectionIII.app/Contents/Resources/iOSInjection10.bundle"] load];
    // tvOS
    //[[NSBundle bundleWithPath:@"/Applications/InjectionIII.app/Contents/Resources/tvOSInjection.bundle"] load];
    // macOS
    //[[NSBundle bundleWithPath:@"/Applications/InjectionIII.app/Contents/Resources/macOSInjection.bundle"] load];
#endif
    return YES;
}
```
(2)在需要修改的controller.m文件中添加injected方法，下方示例代码表示后期要修改view的背景颜色，可依据实际需求添加相应的修改内容。
```
-(void)injected{
    NSLog(@"I've been injected: %@", self);
    self.view.backgroundColor = [UIColor redColor];
    [self viewDidLoad];
}
```
（3）command+R 运行Xcode程序，此时可以看到输出的log信息里有如下内容：此内容表明链接成功。
```
Injection connected, watching /Users/apple/Desktop/ios_Program/testinjection/**
```
（4）在对应需要修改的controller.m文件界面中点击command+s保存键，此时可以观察到view背景色变为红色。
>说明

InjectionIII只能用于模拟器中使用，而且对于不同的需要修改的view controller都需要添加injected方法。网上也可以找到相应的统一化方法，避免重复添加injected方法。

需要观察的修改内容应该在injected方法中添加，若是要在模拟器观察实际情况还需要在其本应出现的位置进行修改！！！

之前尝试过用injection源码编译，但是会报错误，can not open ～/bin/unhide.sh file for writing

