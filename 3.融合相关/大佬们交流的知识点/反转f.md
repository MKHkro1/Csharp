我这么写除了套的多点没有别的问题吧？
![5d012417c8d97f68f2ffbd8a487de574.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/5d012417c8d97f68f2ffbd8a487de574.png)
```C
[HarmonyPatch(typeof(Input))]0个引用public class MousePatch[HarmonyPatch (nameof (Input.GetMouseButtonDown))][HarmonyPostfix]0个引用public static void Postfix(ref int button,bool result)if(button ==1&result)Vector2 mouseposition Camera.main.ScreenToWorldPoint (Input.mousePosition):RaycastHit2D[]hit Physics2D.RaycastAll(mouseposition,Vector2.zero):for (int i=0;i<hit.Length:itt)if (hit[i].collider.TryGetComponent (out Plant plant))if (plant.wheatType !=0)plant.wheatTime 31f:plant.WheatUpdate(:continue:if(hit[i].collider.TryGetComponent (out Mower mower))if(!mower.started){mower.StartMove(
```
建议反转 if

就反了一个
![5f8278149279b8a4ed98a9d812d8bdd5.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/5f8278149279b8a4ed98a9d812d8bdd5.png)
```C
[HarmonyPatch(typeof(Input))]0个用public class MousePatch[HarmonyPatch(nameof (Input.GetMouseButtonDown))][HarmonyPostfix]0个引用public static void Postfix(ref int button,boolresult)if(button !1!result)return:Vector2 mouseposition Camera.main.ScreenToWorldPoint(Input.mousePosition):RaycastHit2D[]hit Physics2D.RaycastAll(mouseposition,Vector2.zero):for (int i=0:i<hit.Length:i+)if (hit[i].collider.TryGetComponent (out Plant plant))if (plant.wheatType !=0)plant.wheatTime 31f;plant.WheatUpdateO;continue:if (hit[i].collider.TryGetComponent(out Mowermower))if(!mower.started)mower.StartMove():
```
问题是我右击之后它掉卡了

我好像知道了
Wheattime 的问题

原本功能是右击大麦之后变身

不，你不改这个 wheattime 是没法变身的

不用手动 update 吧

Wheattime 要大于等于 31 才会变身
不用 update 只能在有僵尸的时候变身

对的啊
窝好像也懂了

那 ida 看看交叉引用的 wheatupdate

原位置有植物了，然后尝试 setplant
看看 lpp 怎么写的，怎么调用的 wheatupdate

怎么看交叉引用
按 x 的那个？
Y
![2ac27c1adcabb81983c73fab752d7ad9.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/2ac27c1adcabb81983c73fab752d7ad9.png)
实际上 plant 的 plantupdate 引用了 wheatupdate
我也不知道为啥 ida 有时候看不全

 反射通过 string 调用就看不到
  虚函数调用吧（？）
  窝不知道. Jpg

我没看到其他相关的内容……
是不是我 continue 或者循环的问题

哦，怪不得
右击之后有一瞬间是两个植物在一块的

我右击一次实际上是触发了两个植物的变身，所以会多一张卡







