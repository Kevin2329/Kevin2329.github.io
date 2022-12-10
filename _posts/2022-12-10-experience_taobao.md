---
layout: post
title: "一次淘宝买代码的经历"
date:   2022-12-10
tags: [diary]
comments: true
author: Kevin
---

最近帮好友解决Unity发布到web,ios端无法运行的问题。<br>

网上中文英文搜遍了，也没找到解决方法。在qq群里问，一位群友说用cocos，之前用Unity也遇到这种情况，后面就转cocos了。<br>

<!-- more -->

我于是下载cocos想用cocos重新做一下那个项目，去好友的工作室里一看项目，放弃了这个想法。一开始他也打算用前端播放视频做了。<br>

我因为不会前端，就想着用cocos做播放视频，虽然也没用过cocos但是毕竟是和unity很相似，但也没能做好。<br>

就找淘宝卖家了。第一位技术人员看起来很专业，做的也很快，要价也很便宜，50块。结果全部素材一发过去，他就发了一张体温计38以上的图片，说自己阳了，真的也是够巧的。<br>

卖家叫我退款，我懒得找第二个卖家了，就说“投诉”，要求找第二位技术人员。<br>
    
第二位技术人员来了。要价130，如果做的又快又好倒也没什么，结果上午商讨好的，初稿到五点钟才发过来。中途我说你把这个文件放到网站上，我们手机好测试。结果说“这个预算不包括部署”，我说你有github pages吗，把文件夹拖到仓库里几秒钟就好了，结果他说“你来”，我说“你拿了钱还让我来”，他说“你以为你给了巨款是吧？”。态度极差，是我这辈子见过态度最差的卖家。东西也没弄好，需要取消播放视频的进度条，也不会弄，反倒开始问一开始的需求是什么。“现在js实现了 然后你们过不了关 我就要负责任吗”。应该弄好的东西没弄好，一直在推卸责任。<br>

晚上我在床上就体会到了一个道理，求人不如求己，明天只能由我出手了。<br>

早上本来想早点起来，结果一直在玩手机，加上去拿快递吃早饭，将近十点才开始。<br>

现在要解决的问题就是 播放视频时不可以有进度条，要求像青年大学习那样的，不可以跳过的视频。怎么实现呢，那就去看青年大学习源代码了。<br>
找到视频播放的部分
```html
<video playsinline="isiPhoneShowPlaysinline" webkit-playsinline="isiPhoneShowPlaysinline" 
x5-video-player-type="h5-page" preload="auto"
playerid="89dd846401e8ec49e0b3b027ed7edfdf" 
style="position: absolute; width: 100%; height: 100%; top: 0px; left: 0px; object-fit: contain; z-index: 0; visibility: inherit;" 
data-used="1" data-idx="0" data-fullscreen_handler="true" src="https://a.....></video>
```
起初看这些代码的时候，没什么感觉，没觉得当中有取消进度条的代码，我觉得我要找的应该是control之类的。结果网上一查。原来关键就是这两句
```html
<video playsinline="isiPhoneShowPlaysinline" webkit-playsinline="isiPhoneShowPlaysinline" ...>
```
我把这两句加上去，通过微信扫码，就可以达成青年大学习一样的效果了。<br>

还有一点就是，只能通过微信扫码或者是特定的浏览器才可以，像百度或者夸克，会自动捕获网页中的视频，这些浏览器下打开青年大学习也是可以跳过的。<br>

文件夹传到github pages的仓库，浏览器生成一个二维码，就可以很方便的用手机进行测试了。<br>

如果好友的甲方通过了，我就狠狠地差评，投诉那个卖家，技术人员技术烂、做得慢、态度差、要价高。<br>

因为我一直学习的是游戏开发相关的知识，之前觉得弄前端什么的浪费时间，现在感觉书到用时方恨少啊，不要求深究，但是基本的还是要会的，很多时候能派上大用场。不然只能花钱求人办事了，运气不好的时候，花了钱还办不好。



