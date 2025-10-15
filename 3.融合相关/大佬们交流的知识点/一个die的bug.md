![1c7be9fd781c2da2ea0f4003c9a1113c_720.jpg](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/1c7be9fd781c2da2ea0f4003c9a1113c_720.jpg)
![f7fcc0a31a9e28467770c61b2ea3db1a_720.jpg](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/f7fcc0a31a9e28467770c61b2ea3db1a_720.jpg)

僵尸的防具造成伤害和僵尸本体造成伤害方法
这个不是……解锁场地随机 buff 的问题吗？
应该是触发了游戏原本方法的报错了

报错内容是没有实例
定位在头盔掉落、头盔受到伤害、僵尸受到伤害

应该就是触发随机词条之后销毁这个僵尸，但因为僵尸被牢樱战神吞噬（die 2）之后直接销毁的，系统找不到这个僵尸所以报错了

也有可能牢战在触发吞噬的时候还造成了一次足够破坏头盔的伤害，所以触发了随机词条并报错
![e662f34e5b529ececf85f68764308ef7_720.jpg](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/e662f34e5b529ececf85f68764308ef7_720.jpg)
牢战变呆子了

突然发现毁灭菇类被压爆不会调用 die 方法