`Use in rider with net 6.`

`You neet to make a SuperExplodeGatling with Unity.`

`You need to rebuild the event every time you end a modification.`

`This mod use in melonloader.`

Unity work
```C#
//推荐将shooter组件往下挪一些
```
SuperExplodeGatling.Csproj
```C#
//此处由于项目过小，需要手动写入
<ItemGroup>
    <EmbeddedResource include="SuperExplodeGatling"<ItemGroup>
```

Core. Cs
```C#
using System.Text;
using Il2CppInterop.Runtime.Injection;
using MelonLoader;
[assembly:MelonInfo(typeof(SuperExplodeGatling.Core),"SuperDoommGatling","1.0.0","likefengzi")]
[assembly:MelonGame("LanPiaoPiao","PlantsVsZombiesRH")]
[assembly:MelonlatformDomain(MelonPlatformDomainAttribute.CompatibleDomains.IL2CPP)]
namespace SuperExplodeGatling;

public class core：MelonMod
{
    public override void OnInitializeMelon()
      {
          //可以输出中文字符
          Console.OutputEncoding = Encoding.UTF8;
          //注册类
          ClassInjector.RegisterTypeInIl2Cpp<SuperExplodeGatling>();
          //读取刚刚的打包文件,获得资源文件
          var ab=CustomCore.GetAssetBundle(System.Reflection.Assembly.GetExecutingAssembly(),"superdoomgatling");
          //注册植物，
          CustomCore.RegisterCustomPlant<SuperGatling,SuperExplodeGatling>(
              //id
              SuperExplodeGatling.PlantID,
              //预制体
              ab.GetAsset<Gameobject>("SuperGatlingPrefab"),
              //预览图
              ab.GetAsset<Gameobject>("SuperGatlingPreview"),
              //配方fusions：
              new List<int,int>{((int)PlantType.SuperGatling,(int)PlantType.UltimateExplodeCannon),
                  ((int)PlantType.UltimateExplodeCannon,(int)PlantType.SuperGatling),
              },
              //attackInterval:
              1.5f
              //produceInterval:
              0,
              //attackDamage:
              1800,
              //maxHealth
              300,
              //cd:
              10f
              //sun:1000
              
          );
          //使用前置库中的一些预制指令，可以添加一些植物属性，额外发挥其他的功能效果
          //添加一些特殊效果,这个是小喷菇模块，可以一个各自叠种三个
          //CustomCore.TypeMgrExtra.isPuff.Add((PlantType)SuperExplodeGatling.PlantID);
          //添加一些特殊效果,这个是磁力系统模块，可以和磁力植物进行链接
          //CustomCore.TypeMgrExtra.IsMagnetPlnts.Add((PlantType)SuperExplodeGatling.PlantID);
          //etc
          //注册图鉴
          Customcore.AddPlantAlmanacStrings(
          UltimateExplodeCannon.PlantID,
          //name:
          //重新构建后，需要重新构建事件（PlantID）
          "超级爆破机枪射手("+SuperExplodeGatling.PlantID+")",
          //description:
          "<color=#0000FF>一次发射6个爆米花子弹<color>\n"+
          "<color=#905000>韧性<color>300\n"+
          "<color=#905000>融合配方<color>超级机枪射手+究极爆破加农炮\n"
          
          );
      }
}

```

SuperExplodeGatling. Cs
```C#
namespace SuperExplodeGatling;
[RegisterTypeInIl2Cpp]
public class SuperDoomGaltling:MonoBehaviour
{
    //植物ID
    public static int PlantID=667;
    //子弹ID
    //注意!!!此处需要核实与前置库对应的子弹序列是否正确！
    public static BulletType BulletID=BulletType.bullet_splat;
    
    public SuperExplodeGatling plant=gameObject.GetComponent<SuperGatling>();
    
    //事件函数：Awake
    //构建事件属性异常只需要把事件属性(平台目标)改为x64，并重新构建所选项目
    //遇到打包资源过小没有将资源打包进，则需要手动添加SuperExplodeGatling.dll进入SuperExplodeGatling.Csproj，然后重新构建事件
    
    private void Awake()
    {
        plant.shoot=plant.gameObject.transform.GetChild(0).FindChild("Shoot");
    }
    //超级机枪射手有一种获得子弹的方法，因此需要对其进行修改
    //但是由于IL2CPP的限制，因此这里不能使用继承，此处不能继承，只能使用Patch
    [HarmonyPatch(typeof(SuperGatling),nameof(SuperGatling.GetBulletType))]
    public class MyClass
    {
        //patch阻断获得子弹方法，使用prefix
        [HarmonoyPrefix]
        //测试发现其并未阻断，需要写REF关键字，ref可以暗引用传递
        public static bool Prefix(SuperGatling __instance,ref BulletType __result)
        {
            //正常情况不阻断
            if(__instance.plantType==SuperExplodeGatling.PlantID)
            {
                //需要重新构建事件
                __result = SuperExplodeGatling.BlletID;
                //return false后，SuperGatling.GetBulletType就不再执行
                return false;
            }
            return true;
        }
    }
    
}
```
