# AiurArtifacts
## 插件简介
> 一款可自定义物品的Minecraft插件
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
