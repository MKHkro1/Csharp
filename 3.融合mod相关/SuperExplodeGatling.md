Core
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
      }
}

```

Plant
```C#
namespace SuperExplodeGatling;
[RegisterTypeInIl2Cpp]
public class SuperDoomGaltling:MonoBehaviour
{
    //植物ID，目前还不可以大于2048，也注意不要和游戏内的重复，19：52
    public static int PlantID=1999;
}
```
