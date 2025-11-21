不是为什么不能补Plant.DieEvent啊

这就和补shooter的shoot1一样吧（）

@鲑鱼可以试试OnDestroy 然后加几个判断？

找到解决方法了（）

怎么解决的

补的重写的DieEvent（）

这样的话不是所有植物都能补吧

本来就不是补所有植物（）

OnDestroy：
@此刻春和景明_ 不行啊

convey 美 [kənˈveɪ] 英 [kənˈveɪ] v. 传达；表达；传递；运输；输送；转移（财产权利）；转让（所有权）；传送；搬运；传播；传送信息；传递思想；传递感情

传送带关卡

ondestory连预览图也会判定的

prefix @‍ if (__instance.dying){ 亡语逻辑 }

应该是可以的我没测试

这么搞会不会被压的时候不会触发，贴图消失了才触发

是的

你测测

绕了个大弯结果还得补那个（）（）Plant. DieReason

气死了

![6767cbf52df539c9a852933ebecef6ec.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/6767cbf52df539c9a852933ebecef6ec.png)

奇怪

但可以补Plant.Die

diereason是个枚举啊

你补这玩意干嘛

窝是sb


DieEvent（）

![60d5fd3504d5133ac67f96e07a27478b.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/60d5fd3504d5133ac67f96e07a27478b.png)
乐

我就说嘛，diereason是个枚举，不可能被补的

@鲑鱼这个默认有实现

但是dieevent没有实现

只要是有方法体的虚方法都可以patch



