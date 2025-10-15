嘶……僵尸在被冻结状态下死亡会不动，好奇怪的bug

这是漏了啥导致的
![b710962329f99927f3e67f5b75a69870.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/b710962329f99927f3e67f5b75a69870.png)

```C
/覆写fixedupdate方法以防die的重复调用[HarmonyPatch(typeof(Zombie))]0个引用public class ZombiePatch[HarmonyPatch(nameof (Zombie.FixedUpdate))][HarmonyPrefix]0个引用public static bool Prefix(Zombie_instance)ifinstance.theStatus ==ZombieStatus.Dying){returnfalse:returntrue:/T忘记Update里面也有个die了HarmonyPatch(nameof (Zombie.Update))]HarmonyPrefix.
0个引用public static bool Prefix1(Zombie instance)ifinstance.theStatus ==ZombieStatus.Dying)returnfalse:returntrue:
```
TM忘了update里也有个die了
ida直接看die的交叉引用（）

问的是这个（僵尸在被冻结状态下死亡会不动，好奇怪的 bug）

如果僵尸在被冻结的状态下死亡，那么会直接不动了

按理来说也不应该啊
蓝飘飘你为什么要在update里面调用die方法啊，fixedupdate里面不是已经有了吗