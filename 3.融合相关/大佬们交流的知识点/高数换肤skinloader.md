星炬没法过火可能是因为少添加了组件

另外一个是少加了几个 shoot 分别是1-5

可能是你没有加到对应的位置

```C#
using BepInEx;

using BepInEx.Logging;

using BepInEx.Unity.IL2CPP;

using HarmonyLib;

using System.Collections.Generic;

using System.IO;

using Unity.VisualScripting;

using UnityEngine;

  

namespace SkinLoader;

  

[BepInPlugin(MyPluginInfo.PLUGIN_GUID, MyPluginInfo.PLUGIN_NAME, MyPluginInfo.PLUGIN_VERSION)]

public class Plugin : BasePlugin

{

    internal static new ManualLogSource Log;

    public static string SCAN_PATH = "SkinLoader";

    public static Dictionary<string, List<string>> folderContents = new Dictionary<string, List<string>>();

    public override void Load()

    {

        // Plugin startup logic

        Log = base.Log;

        Log.LogInfo($"Plugin {MyPluginInfo.PLUGIN_GUID} is loaded!");

        new Harmony($"{MyPluginInfo.PLUGIN_NAME}").PatchAll();

    }

  

    public static AssetBundle LoadAssetBundle(string base64String, string path = "")

    {

        AssetBundle assetBundle = null;

        if (!string.IsNullOrEmpty(base64String))

        {

            byte[] assetBundleData = System.Convert.FromBase64String(base64String);

            assetBundle = AssetBundle.LoadFromMemory(assetBundleData);

        }

  

        if (assetBundle == null && !string.IsNullOrEmpty(path))

        {

            assetBundle = AssetBundle.LoadFromFile(path);

        }

  

        if (assetBundle == null)

        {

            Debug.LogError("Failed to load AssetBundle.");

        }

  

        return assetBundle;

    }

  

    public static void ResigerSkin(int plantType,GameObject prefab,GameObject preview)

    {

        PlantType OType = (PlantType)plantType;

        string name = System.Enum.GetName(typeof(PlantType), OType);

        if (name == null)

        {

            name = prefab.name.Substring(name.Length - 6);

        }

        Il2CppSystem.Type PlantComponent = Il2CppSystem.Type.GetType(name);

        if (PlantComponent == null)

        {

            PlantComponent = Il2CppSystem.Type.GetType(folderContents[plantType.ToString()][0]);

        }

        if (PlantComponent == null)

        {

            Log.LogError($"Type Not Found !");

            return;

        }

        prefab.AddComponent(PlantComponent);

        Plant plant = prefab.GetComponent<Plant>();

        plant.shoot = prefab.transform.Find("Shoot");

        prefab.layer = LayerMask.NameToLayer("Plant");

        prefab.tag = "Plant";

        preview.tag = "Preview";

        GameAPP.resourcesManager._plantPrefabs[OType].Add(prefab);

        GameAPP.resourcesManager._plantPreviews[OType].Add(preview);

        if (!GameAPP.resourcesManager.plantSkinDic.ContainsKey(OType))

        {

            GameAPP.resourcesManager.plantSkinDic.Add(OType, 0);

        }

    }

  

    public static bool IsNumericFolderName(string folderName)

    {

        foreach (char c in folderName)

        {

            if (!char.IsDigit(c))

            {

                return false;

            }

        }

        return true;

    }

  

    public static void ScanFolder()

    {

        try

        {

            string[] subDirectories = Directory.GetDirectories(SCAN_PATH);

            foreach (string dir in subDirectories)

            {

                string folderName = Path.GetFileName(dir);

                if (IsNumericFolderName(folderName))

                {

                    string[] files = Directory.GetFiles(dir);

                    List<string> fileNames = new List<string>();

                    foreach (string file in files)

                    {

                        fileNames.Add(Path.GetFileName(file));

                    }

                    folderContents.Add(folderName, fileNames);

                }

            }

  

            Log.LogMessage("-----------------------------SkinLoader-----------------------------");

            foreach (var entry in folderContents)

            {

                string typeString = entry.Key;

                string abFileName = entry.Value[0];

                GameObject prefab = null;

                GameObject preview = null;

                try

                {

                    AssetBundle ab = LoadAssetBundle(null, $"{SCAN_PATH}/{typeString}/{abFileName}");

                    foreach (var item in ab.LoadAllAssets())

                    {

                        GameObject gameObject = item.TryCast<GameObject>();

                        if ((bool)(gameObject?.name.Contains("Prefab", System.StringComparison.OrdinalIgnoreCase)))

                        {

                            prefab = gameObject;

                        }

                        if ((bool)(gameObject?.name.Contains("Preview", System.StringComparison.OrdinalIgnoreCase)))

                        {

                            preview = gameObject;

                        }

                    }

                    if (prefab != null && preview != null)

                    {

                        if (int.TryParse(typeString, out int plantId))

                        {

                            ResigerSkin(plantId, prefab, preview);

                            Log.LogMessage($"PlantType: {typeString}-{abFileName}Skin Was Loaded Successfully");

                        }

                    }

                }

                catch

                {

                    Log.LogError($"PlantType: {typeString}-{abFileName}Skin Was Loaded Failed");

                    continue;

                }

            }

            Log.LogMessage("-----------------------------SkinLoader-----------------------------");

        }

        catch

        {

  

        }

    }

  

    [HarmonyPatch(typeof(ResourcesManager), "SkinListToDic")]

    public class ResourcesManagerLoadSkinPatch

    {

        [HarmonyPrefix]

        public static void Prefix()

        {

            ScanFolder();

        }

    }

}
```

