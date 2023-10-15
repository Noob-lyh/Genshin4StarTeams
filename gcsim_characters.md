# gcsim角色面板示例

* 均为在队伍代码中使用的配置，每个配置前的备注会指明用于哪个队伍中  
* 默认6命90级角色+精5四星90级武器，天赋9/9/9(计算命座前)  
* 常见特殊情况：班尼特5命、凯亚2命，月卡/限定/精炼收益低的武器精炼酌情  
* 输出角色一般取双暴20词条(暴击头一般9暴击+11爆伤，爆伤头相反)+有效词条各2条。如果有效词条较少，或对某种有效词条需求较大，则取4条该有效词条。特殊情况可以放弃某些词条取更多的另一些词条  
* 使用四星圣遗物套装时并未修改词条大小，因此并不严谨，不过影响不大  
* 部分角色会有我自己的面板，供大家参考。圣遗物数据格式略有不同，注意自己换算  

## 班尼特

```text
# 通用-半输出，5/6命，精1原木刀/精5西风剑，4宗室/4教官充/攻火暴，(5+7)双暴+6生命+6充能
bennett char lvl=90/90 cons=5/6 talent=9,9,9;
bennett add weapon="sapwoodblade/favoniussword" refine=1/5 lvl=90/90;
bennett add set="noblesseoblige/instructor" count=4;
bennett add stats hp=4780 atk=311 er=0.518/atk%=0.466 pyro%=0.466 cr=0.311;
bennett add stats hp=0 hp%=0.294 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.165 cd=0.462;
# 我的-20231014-2命，精1原木刀，4宗室充火暴，(5.2+7.6)双暴+5.0生命+4.8充能+8.7攻击
bennett char lvl=90/90 cons=2 talent=6,10,10;
bennett add weapon="sapwoodblade" refine=1 lvl=90/90;
bennett add set="noblesseoblige" count=4;
bennett add hp=7888 atk=644 def=76 em=19 cr=0.482 cd=0.499 er=0.784 pyro%=0.466;
```

## 香菱

```text
# 通用-渔获绝缘，6命，精5渔获，4绝缘充/攻火暴，(9+11)双暴+2攻击+2精通+2充能
xiangling char lvl=90/90 cons=6 talent=9,9,9;
xiangling add weapon="thecatch" refine=5 lvl=90/90;
xiangling add set="emblemofseveredfate" count=4;
xiangling add stats hp=4780 atk=311 er=0.518/atk%=0.466 pyro%=0.466 cr=0.311;
xiangling add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;
# 我的-20231014，5命，精5渔获，4绝缘充火暴，(10.0+14.6)双暴+2.0攻击+4.8精通+2.2充能
xiangling char lvl=90/90 cons=5 talent=6,10,10;
xiangling add weapon="thecatch" refine=5 lvl=90/90;
xiangling add set="emblemofseveredfate" count=4;
xiangling add stats hp=5433 atk=383 def=81 em=96 cr=0.642 cd=0.964 er=0.641 pyro%=0.466;
```

## 托马

```text
# 烈绽-乐园十文字，6命，精5喜多院十文字，4乐园精精精，10充能
thoma char lvl=90/90 cons=6 talent=9,9,9;
thoma add weapon="kitaincrossspear" refine=5 lvl=90/90;
thoma add set="flowerofparadiselost" count=4;
thoma add stats hp=4780 atk=311 em=187 em=187 em=187;
thoma add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.55 em=0 cr=0 cd=0;
```

## 行秋

```text
# 通用-祭礼攻击沙，6命，精5祭礼剑，4绝缘/4宗室攻水暴，(9+11)双暴+2攻击+2精通+2充能
xingqiu char lvl=90/90 cons=6 talent=9,9,9;
xingqiu add weapon="sacrificialsword" refine=5 lvl=90/90;
xingqiu add set="emblemofseveredfate/noblesseoblige" count=4;
xingqiu add stats hp=4780 atk=311 atk%=0.466 hydro%=0.466 cr=0.311;
xingqiu add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;
# 循环-西风绝缘，6命，精5西风剑，4绝缘攻水暴，(9+11)双暴+6充能
xingqiu char lvl=90/90 cons=6 talent=9,9,9;
xingqiu add weapon="favoniussword" refine=5 lvl=90/90;
xingqiu add set="emblemofseveredfate" count=4;
xingqiu add stats hp=4780 atk=311 atk%=0.466 hydro%=0.466 cr=0.311;
xingqiu add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.297 cd=0.726;
# 我的-20231014，6命，精3祭礼剑，4绝缘攻水爆，(15.9+7.4)双暴+6.3攻击+2.8精通+0充能
xingqiu char lvl=90/90 cons=6 talent=6,10,10; 
xingqiu add weapon="sacrificialsword" refine=3 lvl=90/90;
xingqiu add set="emblemofseveredfate" count=4;
xingqiu add stats hp=6032 atk=821 def=39 em=56 cr=0.525 cd=1.112 er=0 hydro%=0.466;
```

## 芭芭拉

```text
# 通用-海染祭礼/金珀，6命，精5祭礼残章/试作金珀，4海染生生治，4精通+6生命
barbara char lvl=90/90 cons=6 talent=9,9,9;
barbara add weapon="acrificialfragments/prototypeamber" refine=5 lvl=90/90;
barbara add set="oceanhuedclam" count=4;
barbara add stats hp=4780 atk=311 hp%=0.466 hp%=0.466 heal=0.359;
barbara add stats hp=0 hp%=0.294 atk=0 atk%=0 def=0 def%=0 er=0 em=80 cr=0 cd=0;
# 循环-海染西风，6命，精5西风秘典，4海染生生暴，8暴击
barbara char lvl=90/90 cons=6 talent=9,9,9;
barbara add weapon="favoniuscodex" refine=5 lvl=90/90;
barbara add set="oceanhuedclam" count=4;
barbara add stats hp=4780 atk=311 hp%=0.466 hp%=0.466 cr=0.311;
barbara add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0 em=0 cr=0.264 cd=0;
```

## 凯亚

```text
# 融化-龙吟绝缘，2命，精5匣里龙吟，4绝缘充/精/攻冰暴，(9+11)双暴+2攻击+2精通+2充能
kaeya char lvl=90/90 cons=2 talent=9,9,9;
kaeya add weapon="lionsroar" refine=5 lvl=90/90;
kaeya add set="emblemofseveredfate" count=4;
kaeya add stats hp=4780 atk=311 er=0.518/atk%=0.466/em=187 cryo%=0.466 cr=0.311;
kaeya add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;
# 永冻-妖刀冰套，2命，笼钓瓶一心，4冰套攻冰爆，(11+9)双暴+2攻击+2精通+2充能
kaeya char lvl=90/90 cons=2 talent=9,9,9;
kaeya add weapon="kagotsurubeisshin" refine=1 lvl=90/90;
kaeya add set="blizzardstrayer" count=4;
kaeya add stats hp=4780 atk=311 atk%=0.466 cryo%=0.466 cd=0.622;
kaeya add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.363 cd=0.594;
# 我的-20231014，2命，精3匣里龙吟，4绝缘攻冰暴，(5.9+11.8)双暴+2.5攻击+8.9精通+6.2充能
kaeya char lvl=90/90 cons=2 talent=6,10,10;
kaeya add weapon="lionsroar" refine=3 lvl=90/90;
kaeya add set="emblemofseveredfate" count=4;
kaeya add stats hp=5730 atk=746 def=99 em=177 cr=0.505 cd=0.777 er=0.343 cyro%=0.466;
```

## 罗莎莉亚

```text
# 双冰融化-西风散件，6命，精5西风长枪，2冰2宗室精冰暴，(9+11)双暴+2攻击+2精通+2充能
rosaria char lvl=90/90 cons=6 talent=9,9,9;
rosaria add weapon="favoniuslance" refine=5 lvl=90/90;
rosaria add set="blizzardstrayer" count=2;
rosaria add set="noblesseoblige" count=2;
rosaria add stats hp=4780 atk=311 em=187 cryo%=0.466 cr=0.311;
rosaria add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;
# 单核融化-匣里绝缘，6命，精5匣里灭辰，4绝缘充冰暴，(9+11)双暴+2攻击+2精通+2充能
rosaria char lvl=90/90 cons=6 talent=9,9,9;
rosaria add weapon="dragonsbane" refine=5 lvl=90/90;
rosaria add set="emblemofseveredfate" count=4;
rosaria add stats hp=4780 atk=311 er=0.518 cryo%=0.466 cr=0.311;
rosaria add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;
# 永冻-西风宗室，6命，精5西风长枪，4宗室攻冰暴，(9+11)双暴+2攻击+2精通+2充能
rosaria char lvl=90/90 cons=6 talent=9,9,9;
rosaria add weapon="favoniuslance" refine=5 lvl=90/90;
rosaria add set="noblesseoblige" count=4;
rosaria add stats hp=4780 atk=311 atk%=0.466 cryo%=0.466 cr=0.311;
rosaria add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;
# 我的-20231014，2命，精5西风长枪，2冰2宗室攻冰暴，(9.0+11.2)双暴+2.5攻击+7.0精通+8.1充能
rosaria char lvl=90/90 cons=2 talent=6,10,10;
rosaria add weapon="favoniuslance" refine=5 lvl=90/90;
rosaria add set="blizzardstrayer" count=2;
rosaria add set="noblesseoblige" count=2;
rosaria add stats hp=4780 atk=785 def=140 em=140 cr=0.607 cd=0.738 er=0.447 cyro%=0.466;
```

## 重云

```text
# 融化-饰铁绝缘，6命，精5饰铁之花，4绝缘充/精冰暴，(9+11)双暴+2攻击+2精通+2充能
chongyun char lvl=90/90 cons=6 talent=9,9,9;
chongyun add weapon="mailedflower" refine=5 lvl=90/90;
chongyun add set="emblemofseveredfate" count=4;
chongyun add stats hp=4780 atk=311 er=0.518/em=187 cryo%=0.466 cr=0.311;
chongyun add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;
```

## 菲谢尔

```text
# 通用-剧团绝弦/静谧之曲，6命，精5绝弦/静谧之曲，4剧团攻雷暴，(9+11)双暴+2攻击+2精通+2充能
fischl char lvl=90/90 cons=6 talent=9,9,9; 
fischl add weapon="stringless/songofstillness" refine=5 lvl=90/90;
fischl add set="goldentroupe" count=4;
fischl add stats hp=4780 atk=311 atk%=0.466 electro%=0.466 cr=0.311;
fischl add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;
# 我的-20231014，6命，精5绝弦/静谧之曲，4剧团攻雷暴，(7.2+13.7)双暴+3.2攻击+6.6精通+2.9充能
fischl char lvl=90/90 cons=6 talent=6,10,8; 
fischl add weapon="stringless/songofstillness" refine=5 lvl=90/90;
fischl add set="goldentroupe" count=4;
fischl add stats hp=6163 atk=784 def=35 em=131 cr=0.548 cd=0.901 er=0.162 electro%=0.466;
```

## 北斗

```text
# 砂武/砂激-浪影绝缘，6命，精5浪影阔剑，4绝缘充雷暴，(9+11)双暴+2攻击+2精通+2充能
beidou char lvl=90/90 cons=6 talent=9,9,9;
beidou add weapon="tidalshadow" refine=5 lvl=90/90;
beidou add set="emblemofseveredfate" count=4;
beidou add stats hp=4780 atk=311 er=0.518 electro%=0.466 cr=0.311;
beidou add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;
# 我的-20231014，6命，精5浪影阔剑，4绝缘充雷暴，(11.1+13.2)双暴+3.9攻击+2.9精通+0充能
beidou char lvl=90/90 cons=6 talent=2,10,10; 
beidou add weapon="tidalshadow" refine=5 lvl=90/90;
beidou add set="emblemofseveredfate" count=4;
beidou add stats hp=4780 atk=455 def=194 em=58 cr=0.677 cd=0.870 er=0.518 electro%=0.466;
```

## 久岐忍

```text
# 超绽-伞剑乐园三精，6命，精5东花坊时雨，4乐园精精精，4精通+8生命
kuki char lvl=90/90 cons=6 talent=9,9,9;
kuki add weapon="toukaboushigure" refine=5 lvl=90/90;
kuki add set="flowerofparadiselost" count=4;
kuki add stats hp=4780 atk=311 em=187 em=187 em=187;
kuki add stats hp=0 hp%=0.392 atk=0 atk%=0 def=0 def%=0 er=0 em=80 cr=0 cd=0;
# 治疗-伞剑千岩，6命，精5东花坊时雨，4千岩生生治，4精通+8生命
kuki char lvl=90/90 cons=6 talent=9,9,9;
kuki add weapon="toukaboushigure" refine=5 lvl=90/90;
kuki add set="tenacityofthemillelith" count=4;
kuki add stats hp=4780 atk=311 hp%=0.466 hp%=0.466 hp%=0.466;
kuki add stats hp=0 hp%=0.392 atk=0 atk%=0 def=0 def%=0 er=0 em=80 cr=0 cd=0;
```

## 雷泽

```text
# 彩虹-乐园三精，6命，精5饰铁之花，4乐园精精精，6精通+6充能
razor char lvl=90/90 cons=6 talent=9,9,9;
razor add weapon="mailedflower" refine=5 lvl=90/90;
razor add set="flowerofparadiselost" count=4;
razor add stats hp=4780 atk=311 em=187 em=187 em=187;
razor add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=120 cr=0 cd=0;
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
# 通用-精通风套驾驶员，6命，精5试作金珀/祭礼残章/讨龙英杰谭，4风套精精精，4精通+6充能
sucrose char lvl=90/90 cons=6 talent=9,9,9;
sucrose add weapon="prototypeamber/sacrificialfragments/thrillingtalesofdragonslayers" refine=5 lvl=90/90;
sucrose add set="viridescentvenerer" count=4;
sucrose add stats hp=4780 atk=311 em=187 em=187 em=187;
sucrose add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=80 cr=0 cd=0;
# 我的-20231014，4命，精5试作金珀/祭礼残章/讨龙英杰谭，4风套精精精，4.2精通+10.7充能
sucrose char lvl=90/90 cons=4 talent=3,3,3;
sucrose add weapon="prototypeamber/sacrificialfragments/thrillingtalesofdragonslayers" refine=5 lvl=90/90;
sucrose add set="viridescentvenerer" count=4;
sucrose add stats hp=6120 atk=467 def=199 em=643 cr=0.132 cd=0.140 er=0.589;
```

## 鹿野院平藏

```text
# 通用-速切输出，6命，精5流浪乐章，2风套2角斗攻风暴，(9+11)双暴+4攻击
heizou char lvl=90/90 cons=6 talent=9,9,9;
heizou add weapon="thewidsith" refine=5 lvl=90/90;
heizou add set="viridescentvenerer" count=2;
heizou add set="gladiatorsfinale" count=2;
heizou add stats hp=4780 atk=311 atk%=0.466 anemo%=0.466 cr=0.311;
heizou add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0 em=0 cr=0.297 cd=0.726;
# 珐鹿琳莱-充能速切治疗，6命，精5试作金珀，4宗室攻风暴，(9+11)双暴+4攻击
heizou char lvl=90/90 cons=6 talent=9,9,9;
heizou add weapon="prototypeamber" refine=5 lvl=90/90;
heizou add set="noblesseoblige" count=4;
heizou add stats hp=4780 atk=311 atk%=0.466 anemo%=0.466 cr=0.311;
heizou add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0 em=0 cr=0.297 cd=0.726;
# 我的-20231014，6命，精1流浪乐章，2风套2追忆攻风暴，(12.1+12.4)双爆+7.9攻击+2.1精通
heizou char lvl=90/90 cons=6 talent=8,10,10;
heizou add weapon="thewidsith" refine=1 lvl=90/90;
heizou add set="viridescentvenerer" count=2;
heizou add set="gladiatorsfinale" count=2;
heizou add stats hp=6757 atk=943 def=40 em=42 cr=0.712 cd=0.816 er=0 anemo%=0.466;
```

## 珐露珊

```text
# 通用-后台风辅，6命，精5西风猎弓，4千岩/4风套攻/充风暴，(12+8)双暴+4充能
faruzan char lvl=90/90 cons=6 talent=9,9,9;
faruzan add weapon="favoniuswarbow" refine=5 lvl=90/90;
faruzan add set="tenacityofthemillelith/viridescentvenerer" count=4;
faruzan add stats hp=4780 atk=311 atk%=0.466/er=0.518 anemo%=0.466 cr=0.311;
faruzan add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.22 em=0 cr=0.396 cd=0.528;
# 珐鹿琳莱-站场输出，6命，精5静谧之曲，4剧团攻/充风暴，(12+8)双暴+4充能
faruzan char lvl=90/90 cons=6 talent=9,9,9;
faruzan add weapon="songofstillness" refine=5 lvl=90/90;
faruzan add set="goldentroupe" count=4;
faruzan add stats hp=4780 atk=311 atk%=0.466/er=0.518 anemo%=0.466 cr=0.311;
faruzan add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.22 em=0 cr=0.396 cd=0.528;
# 我的-20231014，6命，精5静谧之曲，2风套2追忆攻风暴，(13.2+13.9)双爆+5.2充能+1.1攻击
faruzan char lvl=90/90 cons=6 talent=10,10,10;
faruzan add weapon="songofstillness" refine=5 lvl=90/90;
faruzan add set="viridescentvenerer" count=2;
faruzan add set="shimenawasreminiscence" count=2;
faruzan add stats hp=5784 atk=733 def=165 em=0 cr=0.747 cd=0.917 er=0.285 anemo%=0.466;
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

## 草主

```text
# 通用-草套工具人，6命，精5西风剑，4草套充草暴，(7+9)双爆+4攻击+4充能
travelerdendro char lvl=90/90 cons=6 talent=9,9,9;
travelerdendro add weapon="favoniussword" refine=5 lvl=90/90;
travelerdendro add set="deepwoodmemories" count=4;
travelerdendro add stats hp=4780 atk=311 er=0.518 dendro%=0.466 cr=0.311;
travelerdendro add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0.22 em=0 cr=0.231 cd=0.594;
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

## 瑶瑶

```text
# 通用-治疗，6命，精5公义的酬报，4千岩/4草套生生治，4精通+6生命+6充能
yaoyao char lvl=90/90 cons=6 talent=9,9,9;
yaoyao add weapon="rightfulreward" refine=5 lvl=90/90;
yaoyao add set="tenacityofthemillelith/deepwoodmemories" count=4;
yaoyao add stats hp=4780 atk=311 hp%=0.466 hp%=0.466 heal=0.359;
yaoyao add stats hp=0 hp%=0.294 atk=0 atk%=0 def=0 def%=0 er=0.33 em=80 cr=0 cd=0;
# 挂草循环-草套西风，6命，精5西风长枪，4草套生生治，10暴击+6充能
yaoyao char lvl=90/90 cons=6 talent=9,9,9;
yaoyao add weapon="favoniuslance" refine=5 lvl=90/90;
yaoyao add set="deepwoodmemories" count=4;
yaoyao add stats hp=4780 atk=311 hp%=0.466 hp%=0.466 heal=0.359;
yaoyao add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.33 cd=0;
```
