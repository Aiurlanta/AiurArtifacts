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
- 技能组（Skills）
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
一个条件分为两个部分<br>
一部分为 与门条件（And），一部分为 或门条件（Or）<br>
- 与门条件（And）下的所有子条件都成立时 与门条件（And）成立<br>
- 或门条件（Or）下只要有其中一个子成立时 或门条件（Or）成立<br>
当 与门条件（And）和 或门条件（Or）两部分都成立时，该条件整体才成立<br>
```yaml
Conditions:
  And:
  - "health{h<=70%}"
  - "health{h>=40%}"
#当技能释放者血量在40%-70%之间时条件成立
```
<br>

```yaml
Conditions:
  Or:
  - "health{h>70%}"
  - "health{h<40%}"
#当技能释放者血量>70%或者<40%时条件成立
```
#### 条件的对立
在子条件前添加 [!] 即可取其对立
```yaml
Conditions:
  And:
  - "[!]health{h>=70%}"
#当技能释放者血量<70%时条件成立
```

<br>
条件配置好后可在技能配置内使用它

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
用于指定技能在何时触发
<br>

触发器|参数|何时触发
--|:--:|:--
onDamagedByEntity{type=X}|type(t)－实体类型|被实体攻击时触发
onDamagedByOther{type=X}|type(t)－伤害类型|其他伤害因素（如摔落,爆炸）
onAttack{type=X}|type(t)－目标实体的类型|近战攻击时触发
onShooting|无|射出箭矢时触发
onShootAttack{type=X}|type(t)－目标实体的类型|射出的箭矢击中目标时触发
onArrowLand|无|箭矢落地时触发
onKillEntity{type=X}|type(t)－死亡实体的类型|杀死实体时触发

## 目标选择器
用于选择目标
<br>

目标选择器|缩写|描述
--|:--:|:--
Self| |将技能释放者自身作为目标

## 技能组

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
