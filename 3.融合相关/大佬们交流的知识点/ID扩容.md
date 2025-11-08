话说ID能超过2048吗？

目前貌似不能吧

咕咕咕，现在可以了（）

id扩容的lib窝好像没推到git

id扩容……可以写进前置库里不

本来就是写进lib的（）

诶？那我把ID改成2049（不是）

并非，窝其实都没传过

能发一下吗，我还是喜欢用六位ID

😰

https://github.com/lizhanyu-leaf/MelonLodderRHCreate

做的一个读JSON的

就是写json放进指定目录就可以做二创

好哦

迟早能看见basemod（）

WC，我就随便一试，居然扩成功了

666，盲猜扩PlantDataĕ

只扩这个还不行

还得扩MixData.disMixDatas

这些报错是啥啊
![3af2814a7286fafb0213bf50c1a789dc.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/3af2814a7286fafb0213bf50c1a789dc.png)

null，FixedUpdate用的什么东西是null

主包尝试过扩MixData.data吗

啊？
话说我可以Patch CustomCore的RegisterCustomPlant函数吗？

emm，为什么要patch（）

热扩展（），直接整那么大的空间好像会占用内存来着（）

```C#
#region 自动扩容
// 扩容plantData
if (CustomCore.CustomPlants.Count > 0)
{
    long size_plantData = (int)CustomCore.CustomPlants.Keys.Max() < PlantDataLoader.plantData.Length ? PlantDataLoader.plantData.Length : (int)CustomCore.CustomPlants.Keys.Max();
    PlantDataLoader.PlantData_[] plantData = new PlantDataLoader.PlantData_[size_plantData + 1];
    Array.Copy(PlantDataLoader.plantData, plantData, PlantDataLoader.plantData.Length);
    PlantDataLoader.plantData = plantData;
}

// 扩容particlePrefab
if (CustomCore.CustomParticles.Count > 0)
{
    long size_particlePrefab = (int)CustomCore.CustomParticles.Keys.Max() < GameAPP.particlePrefab.Length ? GameAPP.particlePrefab.Length : (int)CustomCore.CustomParticles.Keys.Max();
    GameObject[] particlePrefab = new GameObject[size_particlePrefab + 1];
    Array.Copy(GameAPP.particlePrefab, particlePrefab, GameAPP.particlePrefab.Length);
    GameAPP.particlePrefab = particlePrefab;
}

// 扩容spritePrefab
if (CustomCore.CustomSprites.Count > 0)
{
    long size_spritePrefab = CustomCore.CustomSprites.Keys.Max() < GameAPP.spritePrefab.Length ? GameAPP.spritePrefab.Length : CustomCore.CustomSprites.Keys.Max();
    Sprite[] spritePrefab = new Sprite[size_spritePrefab + 1];
    Array.Copy(GameAPP.spritePrefab, spritePrefab, GameAPP.spritePrefab.Length);
    GameAPP.spritePrefab = spritePrefab;
}

// 扩容data融合数组
if (CustomCore.CustomPlants.Count > 0)
{
    var arr = MixData.data.Cast<Il2CppSystem.Array>();
    long max = (int)CustomCore.CustomPlants.Keys.Max() + 1;
    var length_0 = arr.GetLength(0) < max ? max : arr.GetLength(0);
    var length_1 = arr.GetLength(1) < max ? max : arr.GetLength(1);
    var length = length_0 < length_1 ? length_1 : length_0;
    var type = arr.GetValue(0, 0).GetIl2CppType();
    var result = Il2CppSystem.Array.CreateInstance(type, length, length);
    Il2CppSystem.Array.Copy(arr, result, arr.Length);
    MixData.data = result;
}

// 扩容disMixDatas拆分数组
if (CustomCore.CustomPlants.Count > 0)
{
    long size_disMixDatas = (int)CustomCore.CustomPlants.Keys.Max() < MixData.disMixDatas.Length ? MixData.disMixDatas.Length : (int)CustomCore.CustomPlants.Keys.Max();
    MixData.DisMixData[] disMixDatas = new MixData.DisMixData[size_disMixDatas + 1];
    Array.Copy(MixData.disMixDatas, disMixDatas, MixData.disMixDatas.Length);
    MixData.disMixDatas = disMixDatas;
}

// 扩容randomData随机融合数组
if (CustomCore.CustomPlants.Count > 0)
{
    var arr = MixData.randomData.Cast<Il2CppSystem.Array>();
    long max = (int)CustomCore.CustomPlants.Keys.Max() + 1;
    var length_0 = arr.GetLength(0) < max ? max : arr.GetLength(0);
    var length_1 = arr.GetLength(1) < max ? max : arr.GetLength(1);
    var length = length_0 < length_1 ? length_1 : length_0;
    var type = arr.GetValue(0, 0).GetIl2CppType();
    var result = Il2CppSystem.Array.CreateInstance(type, length, length);
    Il2CppSystem.Array.Copy(arr, result, arr.Length);
    MixData.randomData = result;
}
#endregion
```

其实已经写了扩容的代码来着（）

阿巴阿巴

感觉最高 ID 不能超过 65535（）

65536 x 65536 大小的二维数组

吓哭了

而且占内存挺大的（）

不过 MixData. Data 和 MixData. RandomData 好像可以不扩）

对的（）

但是要弄融合配方就必须扩（）

Mixdata 不是有个 add 吗

《啊？》

Addordered，添加有序配方
好像是这个名字来着

我只知道不扩的话如果有 ID 超大的植物在场那么可以融合的植物就不会发光了（）

还真有啊（）

我那个简化配方就是用这个写的

还有一个添加无序配方的

![dac5fcd7128a8303b65a301f81458ef2.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/dac5fcd7128a8303b65a301f81458ef2.png)

就是在 order 前面加个 un

第一个是底座，第二个是融合植物，第三个是结果植物

那这个会自动扩容吗🤔

不知道啊，我添加过一大堆原有植物的配方，比如机枪+三线＝炮台这样的

好像之前什么版本还有 GetMixResult（？）

IDA 启动（）

Bullet. Die 然后 set 几个阳光？

![e934aa437775c549d6e70a1162414edb_720.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/e934aa437775c549d6e70a1162414edb_720.png)
不发光但是依旧可以融合（）

你怎么加的

CustomCore. RegisterCustomPlant

culib 直接 Cast<Il2CppSystem.Array>() 然后 SetValue 的

怪不得

哦... 那俩二维数组的扩展就不能把 ID 超过 2048 的植物当作合成素材了（）