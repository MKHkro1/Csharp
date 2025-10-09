## 情况

在Unity中，如果重复加载相同的ab包 并且加载包之后没有去将assetbundle unload  
或者在assetbundle unload调用几帧内去加载另一个同名的assetbundle。  
就会报错  
```
The AssetBundle ‘Memory’ can’t be loaded because another AssetBundle with the same files is already loaded.
```


只要两个ab包里面的物体的名字 一样，不管这两个ab包里面的物体是否一样，就会报这个错。

## 在一些同名就代表同个物体的项目中的避免方法

可以需要添加检测机制

```C#
AssetBundle[] loadedABs = Resources.FindObjectsOfTypeAll<AssetBundle>(); if (loadedABs != null) { foreach (var item in loadedABs) { if (item.Contains(assetName)) { //Debug.LogError("isExis ----------------------"); existAB = item; } } }
```

去找到之前加载过的assetbundle

上面这个方法只适用于项目中每个assetbundle里面的物体名字不同的情况。  
如果两个ab包的名字完全相同 就会找到之前加载的ab包

意味着如果想加载的ab包的内容不一样 但是名字一样的话  
只能加载第一次加载的ab包的内容

这时我试过了使用hashtable 保存加载的url以及 对应的ab包，  
然后每次加载的时候，通过url来判断是否已经有加载过的ab包。  
这个方法能避免上述问题

如果上述代码被注释了 还是会 报开始时候的错误

还有一个解决办法就是 ab包加载后卸载掉  
这个方法的优点就是能避免上述两种情况  
弊端就是每次加载都需要重新从网上下载

![8b6698e24cc4d2700618b8112431814c.jpg](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/8b6698e24cc4d2700618b8112431814c.jpg)

![da80f5c9303a1f0f1cabda31e4530a38.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/da80f5c9303a1f0f1cabda31e4530a38.png)

重点：AssetBundle.UnloadAllAssetBundles(false);
![6615697f2fb2666efe11341fb27cbe4f.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/6615697f2fb2666efe11341fb27cbe4f.png)


![83c243153de824cfbe02a8336fba668f.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/83c243153de824cfbe02a8336fba668f.png)
