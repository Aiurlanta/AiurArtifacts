# 概览
[插件介绍]()<br>
[配置文件config.yml]()<br>
[命令＆限权]()<br>
[神器(Artifact)]()<br>
&#8195;[物品属性]<br>
&#8195;[物品附加信息]<br>
&#8195;[物品选项]()<br>
&#8195;&#8195;[灵魂绑定]<br>
&#8195;&#8195;[自定义耐久]()<br>
[条件(Condition)]()<br>
[特效(Effect)]()<br>
[技能(Skill)](https://github.com/Aiurlanta/AiurArtifacts#%E6%8A%80%E8%83%BD)<br>
&#8195;[触发器]()<br>
&#8195;[目标选择器]()<br>
&#8195;[子技能]()<br>
[条件列表]()<br>
[特效列表]()<br>
[技能列表]()<br>
&#8195;[Lightning－雷电]()<br>
&#8195;[Potion－药水]()<br>
<br>

# 插件简介
AiurArtifacts（AA）插件是一款可自定义物品的插件<br>
可制作出拥有各式各样功能的物品
此插件的主要功能有：
- 自定义属性
   - 名称，介绍，耐久，材质
   - 附魔
   - 属性
   - Flags
   - 药水效果，头颅材质，烟花效果
   - 旗帜条纹，书本内容等
- 灵魂绑定
- 自定义耐久
- 粒子特效
- [技能](https://github.com/Aiurlanta/AiurArtifacts#%E6%8A%80%E8%83%BD)

***

# 神器(Artifact)
在AiurArtifacts里要制作一件神器并不难<br>
我们先来看一下格式:
```yaml
example_name:
  Id: 2
  Data: 0
  Amount: 1
  Display: "display"
  Lore:
  - "lore"
  Enchantments:
  - "<附魔类型>:<等级>"
  Meta:
  Attributes:
  Effects:
  - "<特效内部名称>"
  Skills:
  - "<技能内部名称>"
  Options:
```
我们将其中的选项一个个单独拿出来看
- **example_name**<br>
神器的内部名称，用来区分不同的神器<br>
每一个神器都有一个内部名称<br>
可以根据神器的内部名称来获得神器<br>
名称可以随便取，区分大小写，但切记不要跟其他神器的内部名称重复!<br>
以下 条件，特效，技能的内部名称与此类似!<br>

- **Id**<br>
设置物品种类
可以根据物品id或者材料名称来设置物品<br>
可选择填入 物品数字id 来设置物品<br>
也可以填入 物品英文id 来设置物品<br>
```yaml
Id: 1 #石头
Id: "grass" #草方块
```

- **Data**<br>
设置物品的副Id<br>
用于物品的耐久和方块种类<br>

- **Amount**<br>
设置物品的数量

- **Display**<br>
设置物品的展示名，支持颜色代码＆

- **Lore**<br>
设置物品的lore，支持颜色代码＆

- **Enchantments**<br>
设置物品的附魔<br>
格式为: <附魔类型>:<等级>
```yaml
Enchantments:
- "Durability:3"
#为物品添加 耐久III 附魔
```
值得注意的是，等级不能超过32767!

- **Meta**<br>
设置物品的附加信息<br>
如 头颅材质，药水类型，旗帜条纹<br>
详情见 [物品附加信息]()<br>

- **Effects**<br>
设置物品的特效<br>

- **Skills**<br>
设置物品的技能<br>

- **Options**<br>
这是一个特殊的子选项<br>
可为神器设置更多的属性
详情见 [神器选项]()<br>
<br>

## 物品属性
待编辑...

## 物品附加信息(Meta)
待编辑...

## 物品选项(Options)

### 灵魂绑定
待编辑...
<br>

### 自定义耐久
```yaml
Options:
  Durability:
    Dura: <耐久>
    Break: true #耐久为0时是否清除该物品
```
每一个神器都可以在lore中设置自定义耐久<br>
自定义耐久并不会影响到物品的原版耐久<br>
拿在手上的神器在**破坏方块、攻击生物、射箭**时耐久会减少耐久<br>
穿在身上的神器在**受到除摔落之外的伤害**时耐久会减少<br>
当然，自定义耐久还能根据原版的机制和神器上的耐久附魔进行计算<br>
<br>

***

# 条件
条件主要是为特效和技能所服务的<br>
主要用于判断技能/特效的释放者或目标是否处于某种情况<br>
条件的配置位于./pluhins/AiurArtifacts/Conditions/文件夹内<br>
条件配置格式<br>
```yaml
example: #条件的内部名称
  And: #与门条件
  - "<条件类型>{参数}"
  - "<条件类型>{参数}"
  Or: #或门条件
  - "<条件类型>{参数}"
  - "<条件类型>{参数}"
```
一个条件分为两个部分<br>
一部分为 与门条件（And），一部分为 或门条件（Or）<br>
与门条件和或门条件下又包含子条件<br>
<br>

### 条件是如何运作的
先判断与门条件和或门条件下的所有子条件
若与门条件下的所有子条件都成立时 与门条件成立<br>
若或门条件下只要有其中一个子成立时 或门条件成立<br>
只有当 与门条件 和 或门条件 两部分都成立时，该条件整体便成立<br>
```yaml
example1:
  And:
  - "BlockDetection{type=water}"
  Or:
  - "health{h>70%}"
  - "health{h<40%}"
#当释放者站在水中
#并且血量>70%或<40%时条件成立
```
<br>

值得注意的是，当 与门条件 或者 或门条件 为空时，默认它成立<br>
```yaml
example1:
  And:
  - "health{h<=70%}"
  - "health{h>=40%}"
#与门条件（Or）为空，默认成立
#当血量在40%-70%之间时条件成立
```

<br>

```yaml
example1:
  Or:
  - "health{h>70%}"
  - "health{h<40%}"
#与门条件（And）为空，默认成立
#当血量>70%或者<40%时条件成立
```

### 条件的对立
在子条件前添加 [!] 即可取其对立<br>
```yaml
example1:
  And:
  - "[!]health{h>=70%}"
#当血量<70%时条件成立
```

### 条件的作用对象
前面说了，条件主要是判断技能/特效的释放者或释放的目标是否处于某种情况<br>
先来看一下例子
```yaml
- "health{h>=70%}"
- "caster.health{h>=70%}"
#检测 技能释放者自己 血量是否符合条件

- "target.health{h>=70%}" 
#检测 技能所释放的目标 血量是否符合条件
```
正如例子所示<br>
在条件前加上 caster 即表示检测释放者<br>
在条件前加 target 则表示检测目标<br>
<br>
当然，如果条件前什么也不加，则默认检测释放者<br>


***

# 技能
技能是AiurArtifacts插件的一大特点<br>
可以让玩家释放许多强大的技能<br>

```yaml
exampleskill: #技能内部名称
  Conditions:
  - "<条件内部名>"
  - "<条件内部名>"
  Trigger: "<触发器>"
  TargetSelector: "@<目标选择器>"
  Mana: 10
  Cooldown: 10
  Chance: 0.5
  Skills:
  - "<技能类型>{参数}"
  - "<技能类型>{参数}"
```
如上面例子所示，一个完整的技能由以下几个部分构成
- [条件（Conditions）](https://github.com/Aiurlanta/AiurArtifacts#%E6%9D%A1%E4%BB%B6-1)
- 触发器（Trigger）
- 目标选择器（TargetSelector）
- **触发概率（Chance）**<br>
设置技能触发的概率<br>
可用范围为 0～1<br>
设置为 0.5 则为50%概率触发
- **冷却时间（Cooldown）**<br>
设置技能的冷却时间（单位: 秒）
- **灵力（Mana）**<br>
设置释放技能所需要消耗的能量值<br>
若释放者的灵力值不足，则无法释放技能
- 子技能（Skills）
<br>

## 条件
在技能中灵活运用条件，会使技能更具特色<br>
在技能中使用条件，只需在Conditions下填入条件的内部名称即可
```yaml
Conditions:
- "example1"
- "example2"
#example1,example2为条件的内部名称
```
当技能Conditions下拥有多个条件时，必须要按顺序满足所有条件才能执行技能<br>
若不想在技能中使用条件，只需将Conditions留空即可
<br>

## 触发器
触发器决定了技能在何时触发
<br>

触发器|参数|何时触发
--|:--:|:--
onDamagedByEntity{type=X}|type(t)－[实体类型](https://github.com/Aiurlanta/AiurArtifacts#%E9%99%84%E5%BD%95)|被实体攻击时触发
onDamagedByProjectile{pt=X;st=X}|ProjectileType(pt)－抛射物类型<br>ShooterType(st)－射击者类型|被抛射物击中时触发
onDamagedByOther{type=X}|type(t)－[伤害类型](https://github.com/Aiurlanta/AiurArtifacts#%E9%99%84%E5%BD%95)|其他伤害因素（如摔落,爆炸）
onAttack{type=X}|type(t)－目标实体的类型|近战攻击时触发
onShootArrow|无|射出箭矢时触发
onShootAttack{type=X}|type(t)－目标实体的类型|射出的箭矢击中目标时触发
onArrowLand|无|箭矢落地时触发
onKillEntity{type=X}|type(t)－死亡实体的类型|杀死实体时触发
<br>

**详细说明**<br>
```yaml
Trigger: "onDamagedByOther{type=fall}"
#当释放者摔落时触发技能

Trigger: "onDamagedByOther{type=void}"
#当释放者掉入虚空时触发
```
当然，type是支持多个多个参数的<br>
填入多种参数时参数之间需要用英文逗号( , )隔开<br>
```yaml
Trigger: "onDamagedByOther{type=fall,void}"
#当释放者摔落或掉入虚空时触发

Trigger: "onAttack{type=zombie,husk,skeleton,wither}"
#当释放者攻击的实体类型为
#僵尸，尸壳，骷髅，凋灵时触发
```
同时，你还可以剔除某种类型，只需要在前面加( ! )即可<br>
```yaml
Trigger: "onAttack{type=!zombie,!skeleton}"
#当释放者攻击除僵尸和骷髅以外的所有生物时触发
```
<br>

## 目标选择器
目标用于技能释放的对象<br>
目标选择器则为技能提供目标
一个技能若没有目标则无法正常触发<br>

```yaml
TargetSelector: "@Self"
#为技能设定 父目标
```
当你为一个技能设定了父目标后，其下的所有子技能都使用父目标<br>
当然你也可以为子技能设定另一个目标，这样子技能将不会使用父目标<br>
```yaml
TargetSelector: "@Self" #设定父目标
Skills:
- "lightning{d=1} @PIR{r=5}" #使用子目标@PIR
- "potion{t=slow;d=200;l=1}" #使用父目标@Self
```
- 单生物目标

目标选择器|缩写|描述
--|:--:|:--
@Self| |将技能释放者自身作为目标
@NearestEntity||将最近的实体作为目标
@NearestLivingEntity|@NLE|将最近的生物作为目标
@NearestPlayer||将最近的玩家作为目标
@Mount||将骑乘的生物作为目标
<br>

- 多生物目标

目标选择器|缩写|描述
--|:--:|:--
@EntitiesInRadius{r;t}|@EIR{r=X}|将半径内的所有实体作为目标
@EntitiesInRing{max;min;t}||将环内的所有实体作为目标
@LivingEntitiesInRadius{r;t}|@LEIR{r=X}|将半径内的生物作为目标
@LivingEntitiesInRing{max;min;t}||将环内的生物作为目标
@PlayersInRadius{r}|@PIR{r}|将半径内的玩家作为目标
@PlayersInRing{min;max}||将环内的所有玩家作为目标
@PlayersInWorld|@World|将当前世界所有玩家作为目标
@PlayersOnServer|@Server|将服务器内的所有玩家作为目标
<br>

- 单坐标目标

目标选择器|缩写|描述
--|:--:|:--
@LocationSelf| |将自己的坐标作为目标
@Location{w;x;y;z}| |指定XYZ坐标作为目标
@LocationDeviation{x;y;z}| |以自身为原点选取坐标作为目标
@LocationRandom{r}| |取范围内随机坐标作为目标
<br>

- 多坐标目标

目标选择器|缩写|描述
--|:--:|:--
@LocationRandomInRadius{a=X;min=X;max=X}||获取半径内随机数量坐标作为目标
@LocationRandomInRing{a=X;min=X;max=X}||获取环内随机数量坐标作为目标
<br>
<br>

- 参数说明

参数|默认值|描述
--|:--:|:--
radius(r)|3|半径
type(t)||实体类型
world(w)||世界名
x,y,z|0|XYZ坐标或坐标的偏移量
amount(a)|1|数量
maxradius(max)|3|环的最大半径
minradius(min)|1|环的最小半径
<br>

- 举几个例子
```yaml
TargetSelector: "@LEIR{r=5;type=zombie,husk}"
选取僵尸和尸壳作为目标
```

```yaml
TargetSelector: "@LEIR{r=5;type=!zombie,!husk}"
选取除僵尸和尸壳外的生物作为目标
```
<br>

## 子技能
技能的多样性主要在于子技能的配置
子技能填写格式如下
```yaml
- "<技能类型>{参数}"
- "<技能类型>{参数} @<目标选择器>"
- "<技能类型>{参数} @<目标选择器> ～Condition{<条件>,<条件>}"
- "<技能类型>{参数} @<目标选择器> ～Condition{<条件>,<条件>} <概率>"
```
<br>
如例子所示，我们还能为子技能设定目标，条件和概率<br>
除此之外，我们还可以直接调用其他的技能<br>
```yaml
Skills:
- "skill{s=<技能内部名称>}"
```
值得注意的是，使用skill调用其他技能时<br>
仅仅是调用其子技能，并不会调用其目标选择器，触发器和概率

```yaml
example1:
  Conditions:
  - "example_condition"
  TargetSelector: "@self"
  Chance: 0.7
  Trigger "..."
  Skills:
  - "..."
example2:
  TargetSelector; "@pir{r=3}"
  Skills:
  - "skill{s=example1}"
```
在上述例子example2中，通过skill来调用example1的子技能<br>
并将其子技能逐一释放到@pir{r=3}所选的目标身上

## 例子
### 攻击目标时概率使目标着火10秒
```yaml
# Skill 配置
fireSkill:
  TargetSelector: "@DiTarget"
  Trigger: "onAttack"
  Skills:
  - "Ing{d=200}"
```

<br>

### 箭矢落地雷击效果
```yaml
# Skill 配置
lightningArrow:
  TargetSelector: "@Arrow"
  Trigger: "onArrowLand"
  Skills:
  - "lightning{d=3}"
```
当箭矢落地时100%在箭矢的位置召唤闪电
<br>

***

# 条件列表
### Health－血量条件
<details>
<summary>详细信息</summary>

- 检测血量是否在一定范围内

参数|描述
--|:--
health(h)|血量设定
<br>

```yaml
- "health{h>50%}" #血量大于50%
- "health{h<=50%}" #血量小于等于50%
- "health{h=50%}" #血量等于50%
- "health{h>=10}" #血量大于等于10HP
- "health{h=5}" #血量等于5HP
```
***
</details>

### EquipmentDetection－装备栏检测
<details>
<summary>详细信息</summary>

- 检测装备栏是否拥有某物品

> **缩写** - Equipment<br>

参数|描述|附加信息
--|:--|:--
slot(s)|装备栏格子类型|mainHand－主手<br>offHand－副手<br>helmet－头部<br>boots－脚部
item(i)|物品内部名称|若名称前带有[mm]<br>则检测MythicMobs的物品<br>反之检测AiurArtifacts的物品
<br>

```yaml
- "Equipment{s=mainhand;i=example1}" #检测主手是否拥有AA物品example1
- "Equipment{s=offhand;i=[mm]example1}" #检测副手是否拥有MM物品example1
```
***
</details>

### BlockDetection－方块检测
<details>
<summary>详细信息</summary>

- 检测方块是否符合指定的类型

> **缩写** - Block<br>

参数|默认值|描述
--|:--:|:--
type(t)|stone（石头）|方块类型
x|0|x轴的偏移量
y|0|y轴的偏移量
z|0|z轴的偏移量
<br>

```yaml
- "Block{t=water}" #检测实体是否处在水中
- "Block{t=grass;y=-1}" #实体脚下的方块是否为草方块
```
***
</details>

### 条件
<details>
<summary>详细信息</summary>

***
</details>

***
# 技能列表
### Linghtning－雷电
<details>
<summary>详细信息</summary>

- 召唤雷电至目标位置并造成一定伤害<br>

参数（缩写）|默认值|描述
--|:--:|:--
damage（d）|3|雷电造成的伤害|
<br>

```yaml
Skills:
- "lightning{d=3}"
```
***
</details>

### Potion－药水
<details>
<summary>详细信息</summary>

- 给予目标特定的药水效果<br>

参数（缩写）|默认值|描述
--|:--:|:--
type（t）|slow|[药水类型](https://github.com/Aiurlanta/AiurArtifacts#%E9%99%84%E5%BD%95)
duration（d）|100|持续时间（单位:tick）
level（l）|1|药水等级
<br>

```yaml
Skills:
- "potion{t=weakness;d=200;l=3}"
#给予目标虚弱III效果10秒
```
***
</details>
<br>

***

# 附录
<details>
<summary>伤害因素类型</summary>

<br>

类型|描述
--|:--
entity_attack|实体攻击造成的伤害
fall|摔落造成的伤害
fire|直接接触火焰造成的伤害
fire_tick|身上火焰效果造成的伤害
lava|岩浆造成的伤害
lightning|雷电造成的伤害
magic|魔法造成的伤害（药水等）
projectile|抛射物造成的伤害
suicide|自杀造成的伤害
thorns|荆棘造成的伤害
void|掉入虚空时受到的伤害
wither|凋零效果造成的伤害
</details>
<br>

<details>
<summary>多实体类型</summary>

<br>

多实体类型|描述
--|:--
all|所有实体类型
animals|动物类型
livingentity|生物
monster|怪物类型（恶魂，史莱姆除外）
players|玩家类型
projectiles|抛射物（箭，鸡蛋，喷溅药水等）
</details>
<br>

<details>
<summary>实体类型</summary>

<br>

实体类型|描述
--|:--
ArmorStand|盔甲架
Arrow|箭
Boat|船
Bat|蝙蝠
Blaze|烈焰人
CaveSpider
Chicken
Cow
Creeper|苦力怕
Donkey
Egg
ElderGuardian
EnderCrystal
EnderDragon
Enderman
Endermite
Evoker
Fireball
Ghast
Giant
Guardian
Hose
Husk
IronGolem
LargetFireball
Llama
MagmaCube
Minecart
Mule
MushroomCow
Ocelot
Parrot
Pig
Pigzombie
PolarBear
Rabbit
Sheep
Shulker
ShulkerBullet
Silverfish
Skeleton
SkeletonHorse
Slime
SmallFireball
Snowball
Snowman
Spider
Squid
Stray
Vex
Villager
Vindicator
Witch
Wither
WitherSkeleton|凋灵骷髅
WitherSkull
Wolf
Zombie|僵尸
ZombieHorse
ZombieVillager
</details>
<br>

<details>
<summary>药水类型</summary>

<br>

药水类型|药水ID|描述
--|:--:|:--
Slow|1|缓慢
</details>
