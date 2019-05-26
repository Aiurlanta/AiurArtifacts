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
条件组的配置位于./pluhins/AiurArtifacts/Conditions/文件夹内<br>
条件组的配置见例子<br>
```yaml
example:
  And:
  - "<条件类型>{参数}"
  - "<条件类型>{参数}"
  Or:
  - "<条件类型>{参数}"
  - "<条件类型>{参数}"
```
一个条件分为两个部分
一个是 与门条件（And），一部分是 或门条件（Or）<br>
与门条件（And）需要所有条件成立<br>
或门条件（Or）只需要其中一个成立即可<br>
当 与门条件（And）和 或门条件（Or）两者成立，该条件整体才成立<br>
当技能中的Conditions下的所有条件满足时才可执行技能
```yaml
Conditions:
- "xxx1"
- "xxx2"
#xx1，xxx2为条件的内部名称
#当xxx1，xxx2同时满足时才能触发技能
```
## 触发器
用于指定技能在何时触发
<br>

触发器|缩写|描述
--|:--:|--:
Self| |将技能释放者自身作为目标
## 目标选择器
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

参数（缩写）|描述|默认值
--|:--:|--:
damage（d）|雷电造成的伤害|3HP
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

参数（缩写）|描述|默认值
--|:--:|--:
type（t）|药水类型|缓慢效果
duration（d）|持续时间（单位:tick）|100
level（l）|药水等级|1
<br>

例子
```yaml
Skills:
- "potion{t=weakness;d=200;l=3}"
#给予目标虚弱III效果10秒
```
