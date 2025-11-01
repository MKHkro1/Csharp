我现在写的弱究可以完美适配游戏了
就是开局选弱究卡的那个

```C#
[HarmonyPatch(typeof(CreatePlant), "LimTravel")]
public class CreatePlantLimTravelPatch
{
    [HarmonyPostfix]
    public static void Postfix(CreatePlant __instance, PlantType theSeedType, ref bool __result)
    {
        if (theSeedType == theNewPlantType)
        {
            Board board = __instance.board;
            if (board == null)
            {
                __result = false;
                return;
            }
            if (!board.boardTag.enableAllTravelPlant && !board.boardTag.enableTravelPlant)
            {
                __result = true;
                InGameText.Instance.ShowText("该配方仅旅行模式或深渊可用", 3f);
                return;
            }
            TravelMgr travelMgr = TravelMgr.Instance;
            if (travelMgr == null)
            {
                __result = false;
                return;
            }
            if (board.boardTag.isTravel && !IsPlantAllowedInTravelMode(travelMgr, theNewPlantType))
            {
                __result = true;
                InGameText.Instance.ShowText("未选取此植物", 3f);
                return;
            }
            bool isUnlocked = false;
            int index = (int)theNewPlantType;
            if (travelMgr.unlockPlant != null &&
                index >= 0 &&
                index < travelMgr.unlockPlant.Length)
            {
                isUnlocked = travelMgr.unlockPlant[index];
            }
            if (isUnlocked)
            {
                __result = true;
                InGameText.Instance.ShowText("该配方仅旅行模式或深渊可用", 4f);
            }
            else
            {
                __result = false;
            }
        }
    }
    private static bool IsPlantAllowedInTravelMode(TravelMgr travelMgr, PlantType plantType)
    {
        return (travelMgr.ulockTemp != null && travelMgr.ulockTemp.Contains(plantType)) ||
               (travelMgr.weakUltimates != null && travelMgr.weakUltimates.Contains(plantType));
    }
```
前提是需要
TravelMgr.AllWeakUltimatePlants.Add (theNewPlantType);
TheNewPlantType 就换成你想添加的那个弱究植物的植物类型