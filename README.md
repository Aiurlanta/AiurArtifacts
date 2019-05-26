# 概览
[技能](https://github.com/Aiurlanta/AiurArtifacts#%E6%8A%80%E8%83%BD)<br>
&#8195;[条件](https://github.com/Aiurlanta/AiurArtifacts#%E6%9D%A1%E4%BB%B6)<br>
&#8195;[触发器]()<br>
&#8195;[目标选择器]()
<br>

# 插件简介
一款可自定义物品的Minecraft插件
***
# 技能
一个完整的技能应包含
- 条件（Conditions）
- 触发器（Trigger）
- 目标选择器（TargetSelector）
- 触发概率（Chance）
- 冷却时间（Cooldown）
- 消耗的灵力（Mana）
- 子技能（Skills）
<br>

## 条件
条件用于判断是否处于某种情况<br>
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
<br>

<details>
<summary>条件类型</summary>

### Health－血量
**参数**<br>
－health(h)－血量设定
<br>

```yaml
- "health{h>50%} #血量大于50%"
- "health{h<=50%} #血量小于等于50%"
- "health{h=50%} #血量等于50%"
- "health{h>=10} #血量大于等于10HP"
- "health{h=5} #血量等于5HP"
```
<br>

### EquipmentDetection－装备栏检测
**参数**<br>
- slot(s)－装备栏格子
  - mainHand－主手
  - offHand－副手
- item(i)－物品内部名称
<br>

```yaml
- "Equipment{s=mainhand;i=example1} #检测主手是否拥有物品example1"
```

<br>

</details>
<br>

#### 条件是如何运作的
一个条件分为两个部分<br>
一部分为 与门条件（And），一部分为 或门条件（Or）<br>
与门条件和或门条件下又包含子条件<br>
与门条件下的所有子条件都成立时 与门条件成立<br>
或门条件下只要有其中一个子成立时 或门条件成立<br>
当 与门条件 和 或门条件 两部分都成立时，该条件整体便成立<br>
```yaml
example1:
  And:
  - "BlockDetection{type=water}"
  Or:
  - "health{h>70%}"
  - "health{h<40%}"
#当技能释放者站在水中
#并且技能释放者血量>70%或<40%时条件成立
```
<br>

值得注意的是，当 与门条件 或者 或门条件 为空时，默认它成立<br>
```yaml
example1:
  And:
  - "health{h<=70%}"
  - "health{h>=40%}"
#与门条件（Or）为空，默认成立
#当技能释放者血量在40%-70%之间时条件成立
```
<br>

```yaml
example1:
  Or:
  - "health{h>70%}"
  - "health{h<40%}"
#与门条件（And）为空，默认成立
#当技能释放者血量>70%或者<40%时条件成立
```

#### 条件的对立
在子条件前添加 [!] 即可取其对立<br>
```yaml
example1:
  And:
  - "[!]health{h>=70%}"
#当技能释放者血量<70%时条件成立
```

<br>
条件配置好后即可在技能配置内使用它<br>
```yaml
#技能配置
Conditions:
- "example1"
- "example2"
#example1,example2为条件的内部名称
```
当技能Conditions下的所有条件都成立时才执行技能<br>
<br>
当然，你也可以不使用条件，将其留空即可
<br>
<br>

## 触发器
触发器决定了技能在何时触发
<br>

触发器|参数|何时触发
--|:--:|:--
onDamagedByEntity{type=X}|type(t)－实体类型|被实体攻击时触发
onDamagedByProjectile{pt=X;st=X}|ProjectileType(pt)－抛射物类型<br>ShooterType(st)－射击者类型|被抛射物击中时触发
onDamagedByOther{type=X}|type(t)－伤害类型|其他伤害因素（如摔落,爆炸）
onAttack{type=X}|type(t)－目标实体的类型|近战攻击时触发
onShooting|无|射出箭矢时触发
onShootAttack{type=X}|type(t)－目标实体的类型|射出的箭矢击中目标时触发
onArrowLand|无|箭矢落地时触发
onKillEntity{type=X}|type(t)－死亡实体的类型|杀死实体时触发
<br>

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
<summary>实体类型</summary>

<br>

多实体类型|描述
--|:--
all|所有实体类型
animals|动物类型
livingentity|生物
monster|怪物类型（恶魂，史莱姆除外）
players|玩家类型
projectiles|抛射物（箭，鸡蛋，喷溅药水等）
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

**详细说明**<br>
```yaml
Trigger: "onDamagedByOther{type=fall}"
#当释放者摔落时触发技能

Trigger: "onDamagedByOther{type=void}"
#当释放者掉入虚空时触发
```
当然，type是支持多个多个参数的<br>
填入多种参数时等号后面的参数需要使用中括号[]括起来<br>
并且参数之间需要用英文逗号(,)隔开<br>
```yaml
Trigger: "onDamagedByOther{type=[fall,void]}"
#当释放者摔落或掉入虚空时触发

Trigger: "onAttack{type=[zombie,husk,skeleton,wither]}"
#当释放者攻击的实体类型为
#僵尸，尸壳，骷髅，凋灵时触发
```
同时，你还可以整体剔除某种类型，只需要在前面加[!]即可<br>
```yaml
Trigger: "onAttack{type=[livingentity,[!]zombie,[!]skeleton]}"
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
EntitiesInRadius{r=X}|@EIR{r=X}|将半径内的所有实体作为目标
@LivingEntitiesInRadius{r=X}|@LEIR{r=X}|将半径内的生物作为目标
MobsInRadius{r=X}|@MIR{r=X}|将半径内的生物作为目标
PlayersInRadius{r=X}|@PIR{r=X}|将半径内的玩家作为目标
PlayersInRing{min=X;max=X}||将环内的所有玩家作为目标
PlayersInWorld|@World|将当前世界所有玩家作为目标
PlayersOnServer|@Server|将服务器内的所有玩家作为目标
<br>

- 单坐标目标

目标选择器|缩写|描述
--|:--:|:--
@SelfLocation| |将自己的坐标作为目标
@Location{world(w)=X;x=X;y=X;z=X}| |指定坐标作为目标
<br>

- 多坐标目标

**@RandomLocationsInRing{a=X;min=X;max=X}**<br>
获取环内随机数量坐标作为目标

参数|默认值|描述
--|:--:|:--
amount(a)|1|获取坐标个数
maxradius(max)|3|环的最大半径
minradius(min)|1|环的最小半径
<br>
<br>

## 子技能

例子
```yaml
exampleskill:
  Conditions:
  - "xxx1"
  Trigger: "onDamaged"
  TargetSelector: "Self"
  Mana: 10
  Cooldown: 10
  Chance: 0.5
  Skills:
  - "lightning{d=3}"
```
***
# 技能列表
### Linghtning－雷电
* 召唤雷电至目标位置并造成一定伤害
<br>

参数（缩写）|默认值|描述
--|:--:|:--
damage（d）|3|雷电造成的伤害|
<br>

例子
```yaml
Skills:
- "lightning{d=3}"
```
***
### Potion－药水
* 给予目标特定的药水效果
<br>

参数（缩写）|默认值|描述
--|:--:|:--
type（t）|slow|药水效果类型
duration（d）|100|持续时间（单位:tick）
level（l）|1|药水等级
<br>

例子
```yaml
Skills:
- "potion{t=weakness;d=200;l=3}"
#给予目标虚弱III效果10秒
```
