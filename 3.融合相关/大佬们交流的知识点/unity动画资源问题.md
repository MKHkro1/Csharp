有个很抽象的问题

排查出来是资源的问题

不是程序的问题

代码全删了还有问题

（）

Unity 打包资源给我看一眼（？）

![b9de5c3650c1dcf69ec4a5a0de4eeb90.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/b9de5c3650c1dcf69ec4a5a0de4eeb90.png)

窝写了个新的动画就这样了

这个去掉是正常的吗

删了动画正常了

感觉像是没引用到这个动画导致的

（？）

![62f905a563fa94ff2c4750916b76c7e6.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/62f905a563fa94ff2c4750916b76c7e6.png)

是不是这个切换的线有什么讲究（）

点一下看看

这个白色的线点一下

![8de781079dce46774597467901c696d4.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/8de781079dce46774597467901c696d4.png)

有啥问题吗

![e316350f0a2002539c520ad14a215e52.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/e316350f0a2002539c520ad14a215e52.png)

（？）

这个方面窝不会（悲

群里问问吧，窝是没招了


你换成这个 Trigger

这个来触发

然后跳过动画播放时间

再连条线回到 idle 上，不用加其他的东西

就连回去就行

触发动画就是

Plant. Anim. SetTtigger（"你的动画触发器的名字"）
