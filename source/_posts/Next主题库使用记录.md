---
title: Next主题库使用记录
date: 2019-04-09 13:09:27
tags: tool
categories: 博客make
---
>添加头像设置
添加头像时，需要进入到配置文件_config.yml,找到avatar关键词，设置内容如下
```
avatar: 
  # In theme directory (source/images): /images/avatar.gif
  # In site directory (source/uploads): /uploads/avatar.gif
  # You can also use other linking images.
  url: /uploads/avatar.gif
```
尝试在avatar后直接添加 /uploads/avatar.gif，但是提示url处存在错误❌，此处**uploads文件夹为自己创建**此处测试使用jpg, png, gif格式图片均可正常显示。
<!-- more -->
>添加音乐外链

在侧边栏中添加音乐播放效果时，需要找到音乐外链所对应的网页源码，在theme/next/layout/_macro/sidebar.swig中进行修改，个人看代码这部分其实就是对应着侧边栏的网页源码，因此只需要在自己所想要添加的位置处补充音乐外链源码即可，例如在links下方添加音乐效果：
```
       {% endif %}
      <iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=86 height=86 src="//music.163.com/outchain/player?type=2&id=22636878&auto=1&height=66"></iframe>
      </section>
          {% if theme.custom_file_path.sidebar %}
```
音乐外链获取可以直接在网易云/qq音乐网页端找到所想要播放的歌曲页面，找到音乐外链即可。对于保护权限，不支持的音乐虽然可以获得其id，在代码处替换id即可，可以正常在博客侧边栏显示但仍不可播放。

>出现css加载不出来的问题
之前添加分类、标签、主页等后，发现点击跳转到相应页面时一直出现布局错乱问题。就是文字显示居左侧，部分字体呈现蓝色、图片加载不正常的现象。。找了白天才知道原来是站点配置出错了。。**站点配置文件中的root一定要加/***!!!如果站点是子目录的话,root配置应该是：
```
url: http://yousite.com/blog
root: /blog 
```
如果不是则配置是：
```
url: http://youname.github.io
root: /
```
其实我自己测试过，这种情况下root直接配置为root: /youname.github.io  也是可以正常加载的～～～ 

>关闭评论功能时页面出现404

尝试了关闭about页面的评论功能，但是却发现点击后变成了404，，，，于是，查了一下原因是因为在输入comments时，系统键盘总是以大写开头。还有一定要注意空格哦～

