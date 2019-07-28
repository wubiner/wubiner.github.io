---
title: iOS第三方库管理工具CocoaPods
date: 2019-04-08 20:43:52
tags:
 - tools
categories: ios开发
---
CocoaPods是辅助iOS开发过程中所需要使用的第三库的管理，使用该工具可以免去手动添加lib，下载framework的操作，并且还可以维护其更新。

> 1.安装（需先安装最新版ruby环境）

安装rvm

终端输入：
```
curl -L https://get.rvm.io | bash -s stable 
source ~/.rvm/scripts/rvm 
```
<!-- more -->
检查一下是否安装正确 ：
```
rvm -v 
```
![avatar](https://img-blog.csdnimg.cn/20190401191011434.png)

成功显示rvm已安装版本后查询已知ruby版本
```
rvm list known
```
![avatar](https://img-blog.csdnimg.cn/20190401191111449.png)
图中可以看到最新ruby版本是2.6.0，所以接下来安装2.6.0版本ruby。一定要在此处__安装最新版本__，，不然之后还是无法使用pods。
```
rvm install 2.6.0
```
安装结束需要更改ruby的源地址，以供在国内使用。目前应该使用的是<https://gems.ruby-china.com/>，之前自己在网上搜资料，搜到的是淘宝，还有<https://gems.ruby-china.org/>，淘宝那个有说无法使用，自己试的是china.org结果发现后续仍会报错，搜资料才知道后缀现在改为 __*.com*__。
```
gem sources --remove https://rubygems.org/

gem source -a https://gems.ruby-china.com/
```

替换成功后安装cocoapods，最好是使用以下语句哦，不然会出现无权限报错。
```

sudo gem install -n /usr/local/bin cocoapods
```

安装顺利的话执行pod setup，这个好像时间会比较久。。
```

pod setup
```

成功后会提示如果需要更新可以执行以下语句
```

sudo gem install cocoapods --pre
```

以上步骤未报错的话，应该安装没问题了，注意一定要安装__最新版ruby__哦，如果不是最新版就直接从rvm list known语句开始重来一次，，还有那个源地址一定要是<https://gems.ruby-china.com/>。这两点都是极易报错的地方呢。
>2.使用

在Xcode项目文件夹下添加profile文件，它的内容是添加项目所需要的第三方库名。可以使用vim profile打开编辑。以下图为例
![avatar](https://img-blog.csdnimg.cn/20190401192816951.png)
在该profile文件路径下执行pod install,即可将上述所需第三方库下载到工程中，并且可以直接使用，无需进行参数配置。
```
pod install
```

PS:自己是因为要打开<https://github.com/Aufree/ESTMusicPlayer>工程所以才接触到cocoapods，有兴趣的朋友也可以用这个工程试一试～这个工程是一款音乐播放器～



