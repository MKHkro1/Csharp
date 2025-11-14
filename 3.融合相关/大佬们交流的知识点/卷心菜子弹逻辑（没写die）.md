你知道为什么崩嘛

为什么

```C#
[HarmonyPatch(typeof(Bullet_sunCabbage))]
    public class Bullet_sunCabbagePatch
    {
        [HarmonyPatch(nameof(Bullet_sunCabbage.HitZombie))]
        [HarmonyPrefix]
        public static bool PreHitZombie(Bullet_sunCabbage __instance, ref Zombie zombie)
        {
            if (__instance.theBulletType == theNewBulletType)
            {
                int damage = 1000;
                if (Lawnf.GetPlantCount(theNewPlantType, __instance.board) > 10 && Lawnf.TravelAdvanced(45))
                    zombie.TakeDamage(DmgType.RealDamage, damage, true);
                else
                    zombie.TakeDamage(DmgType.Shieldless, damage);
                __instance.PlaySound(zombie);
                if (__instance.Vy < 0f)
                {
                    if (__instance.hitTimes <= 5)
                    {
                        __instance.Vy = -__instance.Vy * 0.5f;
                        __instance.Vx = __instance.Vx * 0.4f;
                        for (int i = 0; i < 3; i++)
                        {
                            Bullet bullet = CreateBullet.Instance.SetBullet(
                                __instance.transform.position.x,
                                __instance.transform.position.y,
                                __instance.theBulletRow,
                                theNewBulletType,
                                __instance.theMovingWay);
                            float spreadFactor = (i - 1) * 0.3f;
                            bullet.Vy = __instance.Vy * 0.4f;
                            bullet.Vx = __instance.Vx * (0.4f + spreadFactor);
                            bullet.detaVx = __instance.detaVx;
                            bullet.detaVy = __instance.detaVy;
                        }
                    }
                    else
                    {
                        __instance.Vy = -__instance.Vy;
                    }
                }
                CreateItem instance = CreateItem.Instance;
                if (instance != null)
                {
                    Vector3 position = __instance.transform.position;
                    instance.SetCoin(0, 0, 13, 0, position);
                }
                return false;
            }
            return true;
        }
    }
```

现在的是这么写的

If (__instance. HitTimes <= 弹射次数)

把弹射次数改成了五

把每次生成的子弹改成了三个

其他没改

Die 写哪里了

不对，你原版都没有写。这是你原来的嘛

```C#
[HarmonyPatch(typeof(Bullet_sunCabbage))]
    public class Bullet_sunCabbagePatch
    {
        [HarmonyPatch(nameof(Bullet_sunCabbage.HitZombie))]
        [HarmonyPrefix]
        public static bool PreHitZombie(Bullet_sunCabbage __instance,ref Zombie zombie)
        {
            if (__instance.theBulletType == theNewBulletType)
            {
                zombie.TakeDamage(DmgType.Shieldless, __instance.Damage);
                __instance.PlaySound(zombie);
                if (__instance.Vy < 0f)
                {
                    if (__instance.hitTimes <= 2)
                    {
                        __instance.Vy = -__instance.Vy * 0.5f;
                        __instance.Vx = __instance.Vx * 0.4f;
                        Bullet bullet = CreateBullet.Instance.SetBullet(__instance.transform.position.x,__instance.transform.position.y,__instance.theBulletRow,BulletType.Bullet_sunCabbage,__instance.theMovingWay);
                        bullet.detaVx = __instance.detaVx;
                        bullet.detaVy = __instance.detaVy;
                    }
                    else
                    {
                        __instance.Vy = -__instance.Vy;
                    }
                }
                CreateItem instance = CreateItem.Instance;
                if (instance != null)
                {
                    Vector3 position = __instance.transform.position;
                    instance.SetCoin(0, 0, 13, 0, position);
                }
                return false;
            }
            return true;
        }
    }
```

你最开始就没有写这个