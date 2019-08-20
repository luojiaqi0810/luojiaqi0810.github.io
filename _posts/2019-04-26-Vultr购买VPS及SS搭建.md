---
layout: post
title:	Vultr购买VPS及ss搭建
subtitle: 每月20人民币左右，性价比高
date: 2019-04-26
author: luojiaqi
header-img: img/post-bg-re-vs-ng2.jpg
catalog: true
tags:
    Blog
---

>感谢室友的安利及无私分享。

# 前言
无论是科研还是娱乐还是日常学习，只在墙内会有很多限制。最近实在受不了了，向室友请教了一下又搜了搜网上的教程，自己搭了个梯子。
这里稍作记录，也给有需要的同学做个参考，本文只讨论科学上网，换作它用（比如建站）之类的需要参考别的教程。
# 购买主机
要搭梯子，那么就得买云服务器或者虚拟主机，就得花点小钱。以前我也喜欢免费的，偶尔用一用免费VPN，但经常有关键时刻不好用的情况，终于明白免费的才是最贵的。。


教程第1步：下定决心每月额外花一点点钱。


然后可以考虑租哪个厂商了，想要在保证服务质量的条件下尽量少出血，那么就得花一点点功夫在网上看看别人的评价。


我目前只试过一家，但了解过[Vultr](https://my.vultr.com/)、[Bandwagon](https://bandwagonhost.com/)、[DigitalOcean](https://www.digitalocean.com/)、[VirMach](https://virmach.com/)。

Bandwagon是室友推荐的，他目前正在用，挺稳定的，速度也比较快（比如youtube）。他家曾经有过$19.9/year的套餐，性价比极高，不过早已没货。现在他家最便宜的是$49.99/year

![](http://ww1.sinaimg.cn/large/609af245ly1g2pr6it5mtj20an0bz0tr.jpg)

直接劝退。。。而且有趣的是打开Bandwagon官方主页需要翻墙，而我们是为了翻墙才去打开它的主页。。

DigitalOcean价格和配置跟Bandwagon基本没差，不过Github学生认证会有$50的赠送金额，但有一年有效期。

VirMach的价格低到令人发指，有号称不需要抢的配置。。

![](http://ww1.sinaimg.cn/large/609af245gy1g2ps6tpsijj20re0sl42y.jpg)

不过像这种一年才几刀几十刀的。。。估计用着会很痛苦吧。。价格太便宜所以我也没尝试，不过试错成本低，也可以尝试一下。

Vultr官网只有注册了才能看得到产品，支持支付宝和微信支付（其他大部分厂商也支持），不过用这两种方式充值最低$10起充，而用Paypal则可以$5起充。还有有一个优势是按小时计费，也就是说可以在不使用的时候停止计费，但必须是删除主机（Server Destroy）后才算停止，简单的Server Stop是不会停止计费的。

本人目前用的是Vultr的$3.5/month的套餐。

![](http://ww1.sinaimg.cn/large/609af245gy1g2prrfse6hj20ua085q47.jpg)

这个更便宜的$2.5/month只支持IPv6，目前还不够普及，所以用来科学上网是不现实的。

而这个$3.5/month的套餐是只有新泽西（New Jersey）才有，其他地区都是$5/month.

## vultr账号注册
如果决定选择Vultr,那么先注册一个账号,使用邮箱即可.
## Paypal账号注册
由于Paypal支付可以$5起充,为了减小试错成本,我又注册了个Paypal.注册Paypal需要银联卡.

而且支付的时候选择使用人民币或美元时最后折算出来的价格是不一样的,会略有差别,这个可以注意一下.
## 购买
其实是充值,先把钱冲到Vultr账户里.

购买前要登录[测试网址](https://www.vultr.com/faq/),在最下方测试一下各地区服务器的效果.

用户体验来源于稳定性和速度,缺一不可.上面的测试结果不一定代表真实情况,我就是新建删除重复了七八次才找到好用一点的.

按照网上的评价,日本和洛杉矶好评较多,我一开始就是选择了这两个地方作为试点,官网测试的结果很稳定,速度也快.我用观看youtube作为测试,结果发现这两个地方的机房不行,看一个多小时就会卡,甚至ssh登陆不上.无奈又删除新建了几次发现并无疗效,便决心一个机房一个机房的试.看到新泽西这个$3.5/month的机房时想着试试再说,结果发现便宜的同时居然也挺好用.

所以大家需要自己尝试一番才能找到一个稳定高速的机房.
##创建主机
充值完毕后,你的帐户里至少应该又$5美元了,那么可以开始创建主机了.

点击左边栏的**Servers**

![](http://ww1.sinaimg.cn/large/609af245gy1g2ptytiujnj203c0iq3zz.jpg)

再点击右上角的加号,进入页面

![](http://ww1.sinaimg.cn/large/609af245gy1g2pu0t52fnj21701hm4bs.jpg)

1.选择合适机房(第一次可以就选日本试试效果,如果效果不好就换个机房重复步骤)
我选的是New Jersey,这个必须得自己试,跟你的所在地和运营商都有关系;

2.系统选择,我选的是Ubuntu18.04;

3.套餐选择,我选的是$3.5/month.

其余选项都可以不选,直接点击**Deploy Now**

等待几分钟就好啦.
![running.png](https://i.loli.net/2019/05/22/5ce505a9d891085998.png)
状态显示running就说明已经ok了。
点击进入详细信息查看
![password.png](https://i.loli.net/2019/05/22/5ce50aba6befe21730.png)
马赛克处是IP地址,下面是用户名和密码，后面登陆时会用到。
# 服务器端部署
接下来要使用ssh连接远程主机
linux系统可以直接用ssh连接。windows系统可以使用xshell或其他软件连接。
ssh登陆命令：

`ssh username@IP`

如果提示
```
The authenticity of host ... can't bbe established
...
Are you sure ...(yes/no)?
```
输入`yes`
然后会提示让你输入密码，正确输入密码后就能够完成连接。

## ss安装
输入命令
`git clone https://github.com/Flyzy2005/ss-fly`
`ss-fly/ss-fly.sh -i password 443`
这里的password是shadowsocks的密码，由自己设置；443是端口号，不加默认是1024.
如果需要改密码或者端口，重新执行一边该命令就好了。
## 开启BBR加速
输入命令
`ss-fly/ss-fly.sh -bbr`
# Windows、Linux、Mac、Android、iOS下的ss安装及设置
[ss客户端安装及设置](https://www.flyzy2005.com/fan-qiang/shadowsocks/ss-clients-download/)

