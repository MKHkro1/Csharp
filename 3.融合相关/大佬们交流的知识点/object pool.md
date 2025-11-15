概率变子弹

这下必须好好看看了

玄学（）

会不会是那个复制组件的问题🤔

窝必须品鉴一下生成子弹的代码

估计还是石山（）

看到BulletPoolManager的时候窝差点把可乐喷出来

飘的代码水平： ？（细节一坨偶合 + 中式英语）

孩子们这并不好笑

我觉得飘肯定不懂 SOLID

主包的散装C # 看不懂对象池 （）

主包开发过unity游戏吗（）

那包没有的啊（）

这种代码那肯定看不懂

很正常（）

不管了全部喂给ds（（（）））

被ObjectPool肘击了

看不懂对象池吗

怎么改这个ObjectPool啊（）

改哪部分

比如换子弹的时候要把子弹对应的objectpool的东西换成皮肤的子弹

窝怎么换啊（）

窝不太了解飘飘代码

你得看飘飘怎么写的

```C#
using UnityEngine; 
using UnityEngine.Pool; 
public class BuiltInPoolExample : 
MonoBehaviour 
{ public GameObject bulletPrefab; private IObjectPool objectPool; void Start() { // 初始化对象池 objectPool = new ObjectPool( createFunc: () => Instantiate(bulletPrefab), // 创建时 actionOnGet: (obj) => obj.SetActive(true), // 获取时 actionOnRelease: (obj) => obj.SetActive(false), // 回收时 actionOnDestroy: (obj) => Destroy(obj), // 销毁时 collectionCheck: true, // 集合检查，防止重复回收，默认开启[citation:3] defaultCapacity: 10, // 默认容量 maxSize: 20 // 最大容量，超出后新对象将被销毁而非入池 ); } public GameObject GetBullet() { return objectPool.Get(); } public void ReturnBullet(GameObject bullet) { objectPool.Release(bullet); } }
```

正常来说类似这种

