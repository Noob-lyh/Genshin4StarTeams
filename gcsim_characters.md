# gcsim角色面板示例

均为在队伍代码中使用的配置，每个配置前的备注会指明用于哪个队伍中  
默认6命90级角色+精5四星90级武器，天赋9/9/9(计算命座前)  
常见特殊情况：班尼特5命、凯亚2命，月卡与限定武器精炼酌情  
输出角色一般取20词条双暴(一般9+11)+4条左右其他有效词条  

## 班尼特

```text
# 通用-半输出，5命，精1原木刀/精5西风剑，4宗室/4教官充火暴，(5+7)双暴+6生命+6充能
# 注：教官是四星圣遗物数值较低，为了严谨理论上应当扣除部分属性
bennett char lvl=90/90 cons=5 talent=9,9,9;
bennett add weapon="favoniussword/sapwoodblade" refine=1 lvl=90/90;
bennett add set="noblesseoblige/instructor" count=4;
bennett add stats hp=4780 atk=311 er=0.518 pyro%=0.466 cr=0.311;
bennett add stats hp=0 hp%=0.294 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.165 cd=0.462;
```

## 香菱

```text
# 通用-渔获绝缘充能沙，6命，精5渔获，4绝缘充火暴，(9+11)双暴+2攻击+2精通+2充能
xiangling char lvl=90/90 cons=6 talent=9,9,9;
xiangling add weapon="thecatch" refine=5 lvl=90/90;
xiangling add set="emblemofseveredfate" count=4;
xiangling add stats hp=4780 atk=311 er=0.518 pyro%=0.466 cr=0.311;
xiangling add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;
```

## 行秋

```text
# 通用-祭礼攻击沙，6命，精5祭礼剑，4绝缘/4宗室攻水暴，(9+11)双暴+2攻击+2充能
xingqiu char lvl=90/90 cons=6 talent=9,9,9;
xingqiu add weapon="sacrificialsword" refine=5 lvl=90/90;
xingqiu add set="emblemofseveredfate/noblesseoblige" count=4;
xingqiu add stats hp=4780 atk=311 atk%=0.466 hydro%=0.466 cr=0.311;
xingqiu add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=0 cr=0.297 cd=0.726;
```

## 凯亚

```text
# 融化-龙吟绝缘充能沙，2命，精5匣里龙吟，4绝缘充冰暴，(9+11)双暴+2攻击+2精通+2充能
kaeya char lvl=90/90 cons=2 talent=9,9,9;
kaeya add weapon="lionsroar" refine=5 lvl=90/90;
kaeya add set="emblemofseveredfate" count=4;
kaeya add stats hp=4780 atk=311 er=0.518 cryo%=0.466 cr=0.311;
kaeya add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;
```

## 罗莎莉亚

```text
# 融化-西风散件精通沙，6命，精5西风长枪，2冰2宗室精冰暴，(9+11)双暴+2攻击+2精通+2充能
rosaria char lvl=90/90 cons=6 talent=9,9,9;
rosaria add weapon="favoniuslance" refine=5 lvl=90/90;
rosaria add set="blizzardstrayer" count=2;
rosaria add set="noblesseoblige" count=2;
rosaria add stats hp=4780 atk=311 em=187 cryo%=0.466 cr=0.311;
rosaria add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;
```

## 菲谢尔

```text
# 砂糖武装-直伤，6命，精5绝弦，4剧团攻雷暴，(9+11)双暴+2攻击+2充能
fischl char lvl=90/90 cons=6 talent=9,9,9; 
fischl add weapon="stringless" refine=5 lvl=90/90;
fischl add set="goldentroupe" count=4;
fischl add stats hp=4780 atk=311 atk%=0.466 electro%=0.466 cr=0.311;
fischl add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=0 cr=0.297 cd=0.726;
```

## 北斗

```text
# 砂糖武装-直伤，6命，精5浪影阔剑，4绝缘充雷暴，(9+11)双暴+2攻击+2充能
beidou char lvl=90/90 cons=6 talent=9,9,9;
beidou add weapon="finaleofthedeep" refine=5 lvl=90/90;
beidou add set="emblemofseveredfate" count=4;
beidou add stats hp=4780 atk=311 er=0.518 electro%=0.466 cr=0.311;
beidou add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=0 cr=0.297 cd=0.726;
```

## 久岐忍

```text
# 超绽-伞剑乐园三精，6命，精5东花坊时雨，4乐园精精精，4精通+8生命
kuki char lvl=90/90 cons=6 talent=9,9,9;
kuki add weapon="toukaboushigure" refine=5 lvl=90/90;
kuki add set="flowerofparadiselost" count=4;
kuki add stats hp=4780 atk=311 em=187 em=187 em=187;
kuki add stats hp=0 hp%=0.392 atk=0 atk%=0 def=0 def%=0 er=0 em=80 cr=0 cd=0;
```

## 莱伊拉

```text
# 通用-千岩挂冰盾辅，6命，精5天目影打刀，4千岩生生生，4生命+10充能
layla char lvl=90/90 cons=6 talent=9,9,9;
layla add weapon="amenomakageuchi" refine=5 lvl=90/90;
layla add set="tenacityofthemillelith" count=4;
layla add stats hp=4780 atk=311 hp%=0.466 hp%=0.466 hp%=0.466;
layla add stats hp=0 hp%=0.196 atk=0 atk%=0 def=0 def%=0 er=0.55 em=0 cr=0 cd=0;
```

## 砂糖

```text
# 通用-精通风套驾驶员，6命，精5试作金珀/讨龙英杰谭，4风套精精精，4精通+6充能
sucrose char lvl=90/90 cons=6 talent=9,9,9;
sucrose add weapon="prototypeamber/thrillingtalesofdragonslayers" refine=5 lvl=90/90;
sucrose add set="viridescentvenerer" count=4;
sucrose add stats hp=4780 atk=311 em=187 em=187 em=187;
sucrose add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=80 cr=0 cd=0;
```

## 鹿野院平藏

```text
# 珐鹿琳莱-充能速切治疗，6命，精5试作金珀，4宗室攻风暴，(9+11)双暴+4攻击
heizou char lvl=90/90 cons=6 talent=9,9,9;
heizou add weapon="prototypeamber" refine=5 lvl=90/90;
heizou add set="noblesseoblige" count=4;
heizou add stats hp=4780 atk=311 atk%=0.466 anemo%=0.466 cr=0.311;
heizou add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0 em=0 cr=0.297 cd=0.726;
```

## 珐露珊

```text
# 珐鹿琳莱-站场输出，6命，精5静谧之曲，4剧团攻风暴，(12+8)双暴+4充能
faruzan char lvl=90/90 cons=6 talent=9,9,9;
faruzan add weapon="songofstillness" refine=5 lvl=90/90;
faruzan add set="goldentroupe" count=4;
faruzan add stats hp=4780 atk=311 atk%=0.466 anemo%=0.466 cr=0.311;
faruzan add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.22 em=0 cr=0.396 cd=0.528;
```

## 琳妮特

```text
# 珐鹿琳莱-速切嘲讽副C，6命，精5西风剑，2角斗2追忆攻风暴，(9+11)双暴+4攻击
lynette char lvl=90/90 cons=6 talent=9,9,9;
lynette add weapon="favoniussword" refine=5 lvl=90/90;
lynette add set="gladiatorsfinale" count=2;
lynette add set="shimenawasreminiscence" count=2;
lynette add stats hp=4780 atk=311 atk%=0.466 anemo%=0.466 cr=0.311;
lynette add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0 em=0 cr=0.297 cd=0.726;
```

## 柯莱

```text
# 通用-草套工具人，6命，精5西风猎弓，4草套充草暴，(7+9)双爆+4攻击+4充能
collei char lvl=90/90 cons=6 talent=9,9,9;
collei add weapon="favoniuswarbow" refine=5 lvl=90/90;
collei add set="deepwoodmemories" count=4;
collei add stats hp=4780 atk=311 er=0.518 dendro%=0.466 cr=0.311;
collei add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0.22 em=0 cr=0.231 cd=0.594;
```
