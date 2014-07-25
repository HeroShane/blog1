---
layout: post
title: 格式示范
categories:
    - 测试1
    - 测试2
    - 测试3
tags:
    - tips
    - demo
    - example
    - 秋
    - 东
excerpt: 书写规范示例    
---

文章摘要文章摘要文章摘要文章摘要文章摘要文章摘要文章摘要文章摘要文章摘要文章摘要文章摘要文章摘要文章摘要文章摘要文章摘要

![]({{ site.baseurl }}images/2014-07-22-firstimg.jpg)

插入图片

## 插入超链接

插入超链

[超链接](https://heroshane.com)

## 粗体

打開 **粗体1 － 粗体2 － 粗体3**

擦擦擦擦擦擦擦**統計統計統計**，擦擦擦擦擦擦擦**時間時間時間**，擦擦擦擦擦擦擦**待機待機待機待機**。

## 引用

>引用文字引用文字引用文字引用文字，引用文字引用文字引用文字

## 插入代码

``` sh
osascript -e 'display notification "Lorem ipsum dolor sit amet" with title "Title"'
```
后半部分其实是 `AppleScript` ，`osascript`则用于在命令行运行 `AppleScript`。

接着用 `sleep` 命令设置多久后运行，所以最终的命令如下：

```sh
sleep 1200; osascript -e 'display notification "赶快走开" with title "休息时间" sound name "Sosumi"'
```
1200的单位是秒，即20分钟。

<img src="{{ site.baseurl }}images/2014-07-22-secondimg.jpg" width="350">

接下来可以把这个命令写入[dotfiles](https://heroshane.com)，方便的定制时间，显示文字以及声音。

## 引用小图

底下有朋友留言提到了[超链](https://heroshane.com)，它的作用是根据你的作息，在临睡前几小时会慢慢将你电脑屏幕中的蓝光去掉变为暖色，有助入睡。

底下有朋友留言提到了[超链](https://heroshane.com)，它的作用是根据你的作息，在临睡前几小时会慢慢将你电脑屏幕中的蓝光去掉变为暖色，有助入睡。免费:punch:

## 连续多图

[![](http://shane-pic.qiniudn.com/ad84858fa0ec08faf7fe3ba859ee3d6d54fbda4e.jpg)](http://www.flickr.com/photos/ztpala/13023827185/)

[![](http://shane-pic.qiniudn.com/D52588D9B4BAEECE84BFBFB41E.jpg)](http://www.flickr.com/photos/ztpala/13024212034)

[![](http://shane-pic.qiniudn.com/4da04da98226cffc04d05794bb014a90f703ea00.jpg)](http://www.flickr.com/photos/ztpala/13023818675)

[![](http://shane-pic.qiniudn.com/04b19045d688d43f60ce4ba37d1ed21b0ff43bab.jpg)](http://www.flickr.com/photos/ztpala/13023818675)

## 代码高亮

object-c代码片段1：

{% highlight objc %}
[self.activityManager startActivityUpdatesToQueue:self.queue
                                      withHandler:^(CMMotionActivity *activity) {
                                          self.lastActivityDate = activity.startDate;
                                      }];
{% endhighlight %}

object-c代码片段2：

{% highlight objc %}
- (void) observeValueForKeyPath:(NSString *)keyPath ofObject:(id)object
                         change:(NSDictionary *)change context:(void *)context
{
    if (object == self.model && [keyPath isEqualToString:@"lastActivityDate"]) {
        dispatch_async(dispatch_get_main_queue(), ^{
            self.lastActivityDateLabel = @"xxx";
        });
    }
}
{% endhighlight %}

## 代码引用块

<blockquote class="twitter-tweet" lang="en">
<p>郭冬临这个名字突然高大上起来 <a href="https://twitter.com/search?q=%23%E6%9D%83%E5%8A%9B%E7%9A%84%E6%B8%B8%E6%88%8F&amp;src=hash">#权力的游戏</a>
</p>&mdash; Tao (@ztpala) <a href="https://twitter.com/ztpala/statuses/431283349517500416">February 6, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

我的twitter

<blockquote class="twitter-tweet" lang="zh-cn"><p>我的twitter小推文，娃哈哈~_~ <a href="http://t.co/iayI7tAFN2">pic.twitter.com/iayI7tAFN2</a></p>&mdash; HeroShane (@superheroshane) <a href="https://twitter.com/superheroshane/statuses/491623324053561345">2014年7月22日</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

## 序号

类型1：

1. 一一一一一一一一一
2. 二二二二二二二二二
3. 四四四四四四四四四

类型2：

* [超链1](https://heroshane.com)

* [超链2](https://heroshane.com)

* [超链3](https://heroshane.com)

* [超链4](https://heroshane.com)

* [超链5](https://heroshane.com)

## 超链粗体&文字中引用

一百年来，《性与性格》一直在被研究和争论。一百年来，《性与性格》一直在被研究和争论。一百年来，《性与性格》一直在被研究和争论。[普通超链](https://heroshane.com)，也就是每次需要建立新项目，就用命令 `touch "task name"` 一百年来，《性与性格》一直在被研究和争论。一百年来，《性与性格》一直在被研究和争论。一百年来，《性与性格》一直在被研究和争论。一百年来，《性与性格》一直在被研究和争论。

一百年来，《性与性格》一直在被研究和争论。一百年来，《性与性格》一直在被研究和争论。一百年来，《性与性格》一直在被研究和争论。一百年来，《性与性格》一直在被研究和争论。一百年来，《性与性格》一直在被研究和争论。一百年来，《性与性格》一直在被研究和争论。 **[粗体超链](https://heroshane.com)**, 一百年来，《性与性格》一直在被研究和争论。一百年来，《性与性格》一直在被研究和争论。一百年来，《性与性格》一直在被研究和争论。一百年来，《性与性格》一直在被研究和争论。

从哲学、逻辑学、伦理学和心理学等多个角度对这些问题进行了反传统的探讨 `平安三段` ，进行了反传统的探讨 `平安四段` ，进行了反传统的探讨 `鐵騎一段` 。进行了反传统的探讨 `燕飛` 进行了反传统的探讨。

## 综合引用

如果你用[Dropbox](http://db.tt/H7ei7k2)存放和同步[Jekyll]({% post_url 2014-07-22-picpost %})的代码和文章，那么最好进行一些设置防止运行Jekyll时Dropbox大量更新而~~烧毁~~烧热你的电脑。

Dropbox的 **Selective Sync** 可以让你选择性的同步某些文件夹：

`Preferences` - `Advanced` - `Selective Sync` - `Change Settings`

Jekyll用 `_site` 这个文件夹来存放生成好的静态文件，这也是为什么 `.gitignore` 里会默认加入它。

所以最好也在上述的Dropbox选择性同步里将这个文件夹排除，以防止每次build网站时都同步大量的新文件，这天已经够热的了:

>1. 引用自： [#用Dropbox选择性同步Jekyll](http://ztpala.com/2013/07/17/dropbox-selective-sync-jekyll/) <small>[the blog of Tao Zhang](http://ztpala.com/)</small>
>2. 引用自： [#用Gollum搭建基于Git的Wiki](http://ztpala.com/2012/02/01/gollum-git-backed-wiki/) <small>[the blog of Tao Zhang](http://ztpala.com/)</small>
>3. 引用自： [#Git Submodule](http://ztpala.com/2012/01/20/git-submodule/) <small>[the blog of Tao Zhang](http://ztpala.com/)</small>

## 插入框架

instagram推出了在網頁中嵌入照片/影片的功能，順便在這裏測試一下

<iframe src="//instagram.com/p/buUYQUIBnp/embed/" width="612" height="710" frameborder="0" scrolling="no" allowtransparency="true"></iframe>

## 引用gist

引用gist引用gist引用gist引用gist引用gist引用gist

<script src="https://gist.github.com/1619708.js?file=navigation.js"></script>

<s>不用插件的话可以直接用官方gist嵌入方法</s> 现在可以直接插入gist，方法如下：

{% highlight text %}
{% raw %}
{% gist 12345 %}
{% endraw %}
{% endhighlight %}

shane-script

<script src="https://gist.github.com/HeroShane/af6a56246c47b5531757.js"></script>

shane-https

https://gist.github.com/af6a56246c47b5531757.git


