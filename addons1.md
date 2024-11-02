Here are some random examples for creating addons, mods, or items in popular games:

### World of Warcraft Addon (Lua)

```lua
local frame = CreateFrame("Frame")
frame:RegisterEvent("PLAYER_ENTERING_WORLD")
frame:SetScript("OnEvent", function(self, event, ...)
    print("Hello, World of Warcraft!")
end)
```

### Garry's Mod Item (Lua)

```lua
SWEP.PrintName = "Random Blaster"
SWEP.Author = "YourName"
SWEP.Spawnable = true

SWEP.Primary.ClipSize = 10
SWEP.Primary.DefaultClip = 10
SWEP.Primary.Automatic = false
SWEP.Primary.Ammo = "SMG1"

function SWEP:PrimaryAttack()
    if (not self:CanPrimaryAttack()) then return end
    self:ShootBullet(10, 1, 0.02)
    self:TakePrimaryAmmo(1)
end
```

### Minecraft Addon/Mod (Java)

1. Create a new weapon mod for Minecraft using Minecraft Forge.

#### `CustomSword.java`
```java
package com.example.mymod.items;

import net.minecraft.item.Item;
import net.minecraft.item.ItemTier;
import net.minecraft.item.SwordItem;

public class CustomSword extends SwordItem {
    public CustomSword() {
        super(ItemTier.DIAMOND, 10, -2.4F, new Item.Properties().group(ItemGroup.COMBAT));
        setRegistryName("custom_sword");
    }
}
```

2. Register the sword in your `ModItems` class.

```java
public static final RegistryObject<Item> CUSTOM_SWORD = ITEMS.register("custom_sword", CustomSword::new);
```

### Terraria Mod Weapon (C# - tModLoader)

```csharp
using Terraria;
using Terraria.ID;
using Terraria.ModLoader;

public class RandomSword : ModItem
{
    public override void SetDefaults()
    {
        item.damage = 50;
        item.melee = true;
        item.width = 40;
        item.height = 40;
        item.useTime = 20;
        item.useAnimation = 20;
        item.useStyle = ItemUseStyleID.SwingThrow;
        item.knockBack = 6;
        item.value = 10000;
        item.rare = ItemRarityID.Green;
        item.UseSound = SoundID.Item1;
        item.autoReuse = true;
    }

    public override void AddRecipes()
    {
        ModRecipe recipe = new ModRecipe(mod);
        recipe.AddIngredient(ItemID.Wood, 10);
        recipe.AddIngredient(ItemID.IronBar, 5);
        recipe.AddTile(TileID.Anvils);
        recipe.SetResult(this);
        recipe.AddRecipe();
    }
}
```

Each example creates a simple item or addon for the respective platform. You can expand these by adding more features or assets based on the game’s modding framework.
