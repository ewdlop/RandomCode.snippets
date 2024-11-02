Creating a **Slay the Spire** mod typically requires using the **ModTheSpire** tool and the **BaseMod** library, both of which are essential for modding the game. Here's a simple example for creating a new card mod using **Java**.

### 1. Setup with ModTheSpire and BaseMod

- Download **ModTheSpire** and **BaseMod**.
- Follow the steps to set up your modding environment, including configuring your IDE (IntelliJ IDEA or Eclipse) with the BaseMod library.

### 2. Example Mod: Create a New Card

#### `NewCard.java`

```java
package mymod.cards;

import com.megacrit.cardcrawl.cards.AbstractCard;
import com.megacrit.cardcrawl.characters.AbstractPlayer;
import com.megacrit.cardcrawl.monsters.AbstractMonster;
import com.megacrit.cardcrawl.actions.common.DamageAction;
import com.megacrit.cardcrawl.actions.common.DamageInfo;
import com.megacrit.cardcrawl.dungeons.AbstractDungeon;
import com.megacrit.cardcrawl.core.CardCrawlGame;
import com.megacrit.cardcrawl.localization.CardStrings;
import basemod.abstracts.CustomCard;

public class NewCard extends CustomCard {

    public static final String ID = "mymod:NewCard";
    public static final String NAME = "Power Strike";
    public static final String DESCRIPTION = "Deal 10 damage.";
    public static final String IMG_PATH = "img/cards/NewCard.png";
    
    private static final CardStrings cardStrings = CardCrawlGame.languagePack.getCardStrings(ID);

    private static final int COST = 1;
    private static final int DAMAGE = 10;

    public NewCard() {
        super(ID, NAME, IMG_PATH, COST, DESCRIPTION, CardType.ATTACK,
              CardColor.RED, CardRarity.BASIC, CardTarget.ENEMY);
        this.baseDamage = DAMAGE;
    }

    @Override
    public void use(AbstractPlayer p, AbstractMonster m) {
        AbstractDungeon.actionManager.addToBottom(
            new DamageAction(m, new DamageInfo(p, this.damage, this.damageTypeForTurn))
        );
    }

    @Override
    public void upgrade() {
        if (!this.upgraded) {
            upgradeName();
            upgradeDamage(5); // Increase damage by 5 on upgrade
        }
    }

    @Override
    public AbstractCard makeCopy() {
        return new NewCard();
    }
}
```

### 3. Register the Card

In your main mod file (for example, `MyMod.java`), you need to register the card with BaseMod:

```java
package mymod;

import basemod.BaseMod;
import basemod.interfaces.PostInitializeSubscriber;
import basemod.interfaces.EditCardsSubscriber;
import com.megacrit.cardcrawl.cards.AbstractCard;
import mymod.cards.NewCard;

public class MyMod implements PostInitializeSubscriber, EditCardsSubscriber {

    public MyMod() {
        BaseMod.subscribe(this);
    }

    @Override
    public void receivePostInitialize() {
        // Custom initialization code, if needed
    }

    @Override
    public void receiveEditCards() {
        BaseMod.addCard(new NewCard()); // Register the new card
    }
}
```

### 4. Add Card Assets

- Create a folder for images, e.g., `img/cards/`.
- Place your card image in that folder, and reference it in the `IMG_PATH` variable in `NewCard.java`.

### 5. Packaging the Mod

- Compile your mod and package it as a `.jar` file.
- Place the `.jar` file in the `mods` folder of **Slay the Spire**.
- Launch the game using **ModTheSpire**, and your mod should appear!

### 6. Testing and Expanding

- You can add more features like custom relics, events, characters, or even completely new mechanics by following the same pattern.
- Test your mod frequently to ensure everything works smoothly.

