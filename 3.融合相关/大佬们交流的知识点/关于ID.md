融合究级 id 已经 958 了（）

还有四十多个位置，不慌（？）

电能豌豆 960 估计要撤了

移出 id 9 xx 的话，旅行限制还得另外写一个（）

之前的旅行限制写的是小于 1000 吗（）

900～999 好像
这块都判定究级

嘛，有的搞了

要不干脆把编号搞成一万开头吧（？）

Culib 把所有用到究极的地方全补了一遍（

But lpp 女王还是吃不到，到现在也没修💦

扩 id 还没整好吧（雾
那个 MixData. Data
Mixdata 不是用来注册新配方的吗（）
目前最高 2048（）
Mixdata. Data 是个 2048 x 2048 的数组
我自己写了个注册 id 的插件，死循环不断+1，搞到二十万位没报错（）
二创植物扩 id 要弄融合就得扩 mixdata. Data（）
从一万开始应该可以的……吧？
可以的
2048×2048=4194304
400 万的空间
Id 扩个 3～4 倍其实就够用了
Id 扩个 3～4 倍其实就够用了
但在飘飘觉得不够用之前，二创植物的 id 就会膨胀到把剩余的空间完全占满了吧（）
二创肯定比 lpp 先需要扩（）
限制 id 的从来不是 mixdata. Data 而是 PlantData 的植物数据数组
究极是 900 来着？
不注册关于扩 id 植物的融合 mixdata. Data 完全可以不管

这个多大空间
扩大 plantdata 那个数组 id 2048+的植物就可以存在了
窝记得 plantdata 里有个 2048（？）的一维数组
2048……
Culib 有关于这个的代码
Git 上应该也有关于扩 id 的代码
（窝写了但发布的时候被窝注释了）

窝想补那个 getmixresult（？）

话说，二创植物可以用 xxx : ultimategatling 的方式写吗（）
huh
类名吗
类似mc的mod（？） 
对，写一个类然后继承原本植物
不是说il2cpp不能extend然后override吗 
没用来着

‍不清楚诶
你试试（？）
我没写过，不知道怎么写（）
我到现在为止写的都是原本植物的修改（）

建议 melon（）
[RegisterTypeInIl 2 Cpp]属性注册一下类
那个类继承然后 override 看看（？）

显示找不到植物的 prefab
![3f32995444102507cd0568e50285ff28.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/3f32995444102507cd0568e50285ff28.png)

准备用豌豆的试试（）

为什么这样会显示没有 prefab 呢（思考）
![c0af79d25e792b7b3e7b0d6914c231fa.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/c0af79d25e792b7b3e7b0d6914c231fa.png)

![9ca2b363cb28c8b435d6b884622d3545_720.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/9ca2b363cb28c8b435d6b884622d3545_720.png)
我这是少注册了什么玩意
![1eb4bea52a138dc48856a14253e491b9.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/1eb4bea52a138dc48856a14253e491b9.png)

感觉有点可行性，但缺少了什么必要的东西导致完全不生效

![7d037eb7f4e46292d7766842d9ae99df.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/7d037eb7f4e46292d7766842d9ae99df.png)

确实可行，但是不知道什么原因，会报错

要不直接改改 culib 的代码试试吧（）

Woc？
![9d346994bad2970e3c69ccdc61c1d4a6.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/9d346994bad2970e3c69ccdc61c1d4a6.png)

我已经把 culib 的代码抄了一部分过来了
![445574a09d687cc6d691fab8a2d766e7.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/445574a09d687cc6d691fab8a2d766e7.png)
现在的问题是什么呢
基类的 update 会报错空指针

基类？你用的哪个啊（）Peashooter？

对
[Error  : Il2CppInterop] During invoking native->managed trampoline
Exception: Il2CppInterop.Runtime.Il2CppException: System.NullReferenceException: Object reference not set to an instance of an object.
--- BEGIN IL2CPP STACK TRACE ---
System.NullReferenceException: Object reference not set to an instance of an object.
  at Shooter.Update () [0x00000] in <00000000000000000000000000000000>:0
--- END IL2CPP STACK TRACE ---

   at Il2CppInterop.Runtime.Il2CppException.RaiseExceptionIfNecessary(IntPtr returnedException) in D:\Beta\projects\Il2CppInterop\Il2CppInterop.Runtime\Il2CppException.cs:line 36
   at DMD<Shooter::Update>(Shooter this)
   at (il2cpp -> managed) Update(IntPtr , Il2CppMethodInfo* )

看看 shooter 的 update 用了什么呗
看看是不是什么没初始化

不应该吧，peashooter 应该会把需要的东西初始化一下啊
而且这个说是没有实例好像

你就那么觉得 lpp 的代码那么好吗
（大雾）
反正看一下肯定没错（）
再怎么差，peashooter 也没报错啊（）
行

怪
![3790458bf62eb02b405f8ea830204766.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/3790458bf62eb02b405f8ea830204766.png)

是不是没有 this 导致的错误（）
什么 this
This 指针是 null😰（？）

我也想不到有其他的原因了
那这能有什么问题导致空报错呢
整个 update 截图看看（？）

下面还有一句是 base. Upddate

![6238668b395dd68686a56b93fff623f7.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/6238668b395dd68686a56b93fff623f7.png)

![88e197e0a208b826ce548d7e7d947d8c.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/88e197e0a208b826ce548d7e7d947d8c.png)

![027254d7778aac40cc5a29f3b06e6e8c.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/027254d7778aac40cc5a29f3b06e6e8c.png)

那看看 base. Update 呗（）
还有 PlantShootUpdate
你的意思是让我去 plant. Update 的那一坨史山里面找吗😰





















































