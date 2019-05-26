# AiurArtifacts
## 插件简介
> 一款可自定义物品的Minecraft插件
***
## 技能
一个完整的技能应包含
- 条件（Conditions）
- 触发器（Trigger）
- 目标选择器（TargetSelector）
- 触发概率（Chance）
- 冷却时间（Cooldown）
- 消耗的灵力（Mana）
- 技能组（Skills）
<br>

#### 条件
一个技能允许同事判断多个条件
```yaml
Conditions:
- "xxx1"
- "xxx2"
#xx1，xxx2为条件的内部名称
#当xxx1，xxx2同时满足时才能触发技能
```
#### 触发器
用于指定技能在何时触发
触发器|缩写|描述
--|:--:|--:
@Self| |将技能释放者自身作为目标
#### 目标选择器
#### 技能组

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
## 技能列表
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
