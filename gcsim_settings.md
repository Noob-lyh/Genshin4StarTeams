# gcsim模拟设置及角色面板参考

简单来说，一段gcsim的程序包含四个部分：

1. **模拟条件**  
2. **敌人设置**  
3. **角色面板**  
4. **队伍手法**  

本文档依次给出**模拟条件**、**敌人设置**（这两个部分在模拟时保持不变）、包括所有角色不同流派标准面板的**角色面板**，以及**队伍手法**的说明。  

在team.md中，队伍DPS参考包含的角色面板均从本文档中选取。  

如需投稿，请尽量保持1和2本文档给出的相同。  

## 1. 模拟条件

* 重复设置时新的会覆盖。  
* 模拟持续时间取90秒，即12层半间恰好及格的用时。相比于传统的4循环，这种方式能部分体现队伍的出伤速度（但是总体影响不大）。  

```text
options iteration=1000;     # 模拟次数
options duration=90;        # 每次模拟的持续时间（秒）
options workers=30;         # 并行模拟相关参数（可不管）
options swap_delay=4;       # 60帧下的切人延迟（帧）
```

## 2. 敌人设置

* 预设中一共添加了五个敌人，实际模拟时注释掉其中四个，只保留一个（一般使用第二个，其次第一个）。  
* 五个敌人中，第一个为前方大体积敌人（半径2.5，圆心离原点距离3），第二到五个为前/右/左/后方小体积敌人（半径0.5，圆心离原点距离1），另外角色半径为0.3，位置在原点。  
* 敌人统一使用100级，无限血量，10%全抗性，使用通用掉球设置（每随机480到720帧，即每随机6到12秒，掉落一个1能量的白色微粒）  

```text
#target lvl=100 pos=0,3 radius=2.5 pyro=0.1 dendro=0.1 hydro=0.1 electro=0.1 geo=0.1 anemo=0.1 physical=0.1 cryo=0.1;
target lvl=100 pos=0,1 radius=0.5 pyro=0.1 dendro=0.1 hydro=0.1 electro=0.1 geo=0.1 anemo=0.1 physical=0.1 cryo=0.1;
#target lvl=100 pos=1,0 radius=0.5 pyro=0.1 dendro=0.1 hydro=0.1 electro=0.1 geo=0.1 anemo=0.1 physical=0.1 cryo=0.1;
#target lvl=100 pos=-1,0 radius=0.5 pyro=0.1 dendro=0.1 hydro=0.1 electro=0.1 geo=0.1 anemo=0.1 physical=0.1 cryo=0.1;
#target lvl=100 pos=0,-1 radius=0.5 pyro=0.1 dendro=0.1 hydro=0.1 electro=0.1 geo=0.1 anemo=0.1 physical=0.1 cryo=0.1;
energy every interval=480,720 amount=1;     
```

## 3. 角色面板  

* 角色90级满命（班尼特及御三家除外）天赋999（计算命座前），武器90级精5（不使用限定或月卡武器），副词条标准为20+2n（20条双爆，每种有效词条一般各2条，特殊情况可只取4~6条的某种有效词条）  
* 使用四星圣遗物套装时并未修改词条大小，并不严谨，不过影响不大。  
* 部分角色会有我自己的面板，供参考。圣遗物数据格式略有不同，注意换算。  

### 班尼特

【通用-半输出】5/6命，精1原木刀/精5西风剑，4宗室/4教官充/攻火暴，(5+7)双暴+6生命+6充能  

```text
bennett char lvl=90/90 cons=5/6 talent=9,9,9;
bennett add weapon="sapwoodblade/favoniussword" refine=1/5 lvl=90/90;
bennett add set="noblesseoblige/instructor" count=4;
bennett add stats hp=4780 atk=311 er=0.518/atk%=0.466 pyro%=0.466 cr=0.311;
bennett add stats hp=0 hp%=0.294 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.165 cd=0.462;
```

【我的-20231014】2命，精1原木刀，4宗室充火暴，(5.2+7.6)双暴+5.0生命+4.8充能+8.7攻击  

```text
bennett char lvl=90/90 cons=2 talent=6,10,10;
bennett add weapon="sapwoodblade" refine=1 lvl=90/90;
bennett add set="noblesseoblige" count=4;
bennett add stats hp=7888 atk=644 def=76 em=19 cr=0.482 cd=0.499 er=0.784 pyro%=0.466;
```

### 香菱

【通用-渔获绝缘】6命，精5渔获，4绝缘充/攻火暴，(9+11)双暴+2攻击+2精通+2充能  

```text
xiangling char lvl=90/90 cons=6 talent=9,9,9;
xiangling add weapon="thecatch" refine=5 lvl=90/90;
xiangling add set="emblemofseveredfate" count=4;
xiangling add stats hp=4780 atk=311 er=0.518/atk%=0.466 pyro%=0.466 cr=0.311;
xiangling add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;
```

【我的-20231014】5命，精5渔获，4绝缘充火暴，(10.0+14.6)双暴+2.0攻击+4.8精通+2.2充能  

```text
xiangling char lvl=90/90 cons=5 talent=6,10,10;
xiangling add weapon="thecatch" refine=5 lvl=90/90;
xiangling add set="emblemofseveredfate" count=4;
xiangling add stats hp=5433 atk=383 def=81 em=96 cr=0.642 cd=0.964 er=0.641 pyro%=0.466;
```

### 托马

【烈绽-乐园十文字】6命，精5喜多院十文字，4乐园精精精，10充能  

```text
thoma char lvl=90/90 cons=6 talent=9,9,9;
thoma add weapon="kitaincrossspear" refine=5 lvl=90/90;
thoma add set="flowerofparadiselost" count=4;
thoma add stats hp=4780 atk=311 em=187 em=187 em=187;
thoma add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.55 em=0 cr=0 cd=0;
```

### 行秋

【通用-祭礼攻击沙】6命，精5祭礼剑，4绝缘/4宗室攻水暴，(9+11)双暴+2攻击+2精通+2充能  

```text
xingqiu char lvl=90/90 cons=6 talent=9,9,9;
xingqiu add weapon="sacrificialsword" refine=5 lvl=90/90;
xingqiu add set="emblemofseveredfate/noblesseoblige" count=4;
xingqiu add stats hp=4780 atk=311 atk%=0.466 hydro%=0.466 cr=0.311;
xingqiu add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;
```

【循环-西风绝缘】6命，精5西风剑/精7祭礼剑(保证刷新E)，4绝缘攻水暴，(9+11)双暴+6充能  

```text
xingqiu char lvl=90/90 cons=6 talent=9,9,9;
xingqiu add weapon="favoniussword/sacrificialsword" refine=5/7 lvl=90/90;
xingqiu add set="emblemofseveredfate" count=4;
xingqiu add stats hp=4780 atk=311 atk%=0.466 hydro%=0.466 cr=0.311;
xingqiu add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.297 cd=0.726;
```

【我的-20231014】6命，精3祭礼剑，4绝缘攻水爆，(15.9+7.4)双暴+6.3攻击+2.8精通+0充能

```text
xingqiu char lvl=90/90 cons=6 talent=6,10,10; 
xingqiu add weapon="sacrificialsword" refine=3 lvl=90/90;
xingqiu add set="emblemofseveredfate" count=4;
xingqiu add stats hp=6032 atk=821 def=39 em=56 cr=0.525 cd=1.112 er=0 hydro%=0.466;
```

### 芭芭拉

【通用-海染】6命，精5祭礼残章/试作金珀/白辰之环，4海染生生治，4精通+6生命  

```text
barbara char lvl=90/90 cons=6 talent=9,9,9;
barbara add weapon="acrificialfragments/prototypeamber/hakushinring" refine=5 lvl=90/90;
barbara add set="oceanhuedclam" count=4;
barbara add stats hp=4780 atk=311 hp%=0.466 hp%=0.466 heal=0.359;
barbara add stats hp=0 hp%=0.294 atk=0 atk%=0 def=0 def%=0 er=0 em=80 cr=0 cd=0;
```

【循环-西风】6命，精5西风秘典，4海染生生暴，8暴击

```text
barbara char lvl=90/90 cons=6 talent=9,9,9;
barbara add weapon="favoniuscodex" refine=5 lvl=90/90;
barbara add set="oceanhuedclam" count=4;
barbara add stats hp=4780 atk=311 hp%=0.466 hp%=0.466 cr=0.311;
barbara add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0 em=0 cr=0.264 cd=0;
```

### 凯亚

【融化-龙吟绝缘】2命，精5匣里龙吟，4绝缘充/精/攻冰暴，(9+11)双暴+2攻击+2精通+2充能

```text
kaeya char lvl=90/90 cons=2 talent=9,9,9;
kaeya add weapon="lionsroar" refine=5 lvl=90/90;
kaeya add set="emblemofseveredfate" count=4;
kaeya add stats hp=4780 atk=311 er=0.518/atk%=0.466/em=187 cryo%=0.466 cr=0.311;
kaeya add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;
```

【永冻-妖刀冰套】2命，笼钓瓶一心，4冰套攻冰爆，(11+9)双暴+2攻击+2精通+2充能  

```text
kaeya char lvl=90/90 cons=2 talent=9,9,9;
kaeya add weapon="kagotsurubeisshin" refine=1 lvl=90/90;
kaeya add set="blizzardstrayer" count=4;
kaeya add stats hp=4780 atk=311 atk%=0.466 cryo%=0.466 cd=0.622;
kaeya add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.363 cd=0.594;
```

【我的-20231014】2命，精3匣里龙吟，4绝缘攻冰暴，(5.9+11.8)双暴+2.5攻击+8.9精通+6.2充能  

```text
kaeya char lvl=90/90 cons=2 talent=6,10,10;
kaeya add weapon="lionsroar" refine=3 lvl=90/90;
kaeya add set="emblemofseveredfate" count=4;
kaeya add stats hp=5730 atk=746 def=99 em=177 cr=0.505 cd=0.777 er=0.343 cryo%=0.466;
```

### 罗莎莉亚

【双冰融化-西风散件】6命，精5西风长枪，2冰2宗室精冰暴，(9+11)双暴+2攻击+2精通+2充能  

```text
rosaria char lvl=90/90 cons=6 talent=9,9,9;
rosaria add weapon="favoniuslance" refine=5 lvl=90/90;
rosaria add set="blizzardstrayer" count=2;
rosaria add set="noblesseoblige" count=2;
rosaria add stats hp=4780 atk=311 em=187 cryo%=0.466 cr=0.311;
rosaria add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;
```

【单核融化-匣里绝缘】6命，精5匣里灭辰，4绝缘充冰暴，(9+11)双暴+2攻击+2精通+2充能

```text
rosaria char lvl=90/90 cons=6 talent=9,9,9;
rosaria add weapon="dragonsbane" refine=5 lvl=90/90;
rosaria add set="emblemofseveredfate" count=4;
rosaria add stats hp=4780 atk=311 er=0.518 cryo%=0.466 cr=0.311;
rosaria add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;
```

【永冻-西风宗室】6命，精5西风长枪，4宗室攻冰暴，(9+11)双暴+2攻击+2精通+2充能

```text
rosaria char lvl=90/90 cons=6 talent=9,9,9;
rosaria add weapon="favoniuslance" refine=5 lvl=90/90;
rosaria add set="noblesseoblige" count=4;
rosaria add stats hp=4780 atk=311 atk%=0.466 cryo%=0.466 cr=0.311;
rosaria add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;
```

【我的-20231014】2命，精5西风长枪，2冰2宗室攻冰暴，(9.0+11.2)双暴+2.5攻击+7.0精通+8.1充能

```text
rosaria char lvl=90/90 cons=2 talent=6,10,10;
rosaria add weapon="favoniuslance" refine=5 lvl=90/90;
rosaria add set="blizzardstrayer" count=2;
rosaria add set="noblesseoblige" count=2;
rosaria add stats hp=4780 atk=785 def=140 em=140 cr=0.607 cd=0.738 er=0.447 cryo%=0.466;
```

### 重云

【融化-饰铁绝缘】6命，精5饰铁之花，4绝缘充/精冰暴，(9+11)双暴+2攻击+2精通+2充能  

```text
chongyun char lvl=90/90 cons=6 talent=9,9,9;
chongyun add weapon="mailedflower" refine=5 lvl=90/90;
chongyun add set="emblemofseveredfate" count=4;
chongyun add stats hp=4780 atk=311 er=0.518/em=187 cryo%=0.466 cr=0.311;
chongyun add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;
```

### 菲谢尔

【通用-剧团绝弦/静谧之曲】6命，精5绝弦/静谧之曲，4剧团攻雷暴，(9+11)双暴+2攻击+2精通+2充能  

```text
fischl char lvl=90/90 cons=6 talent=9,9,9; 
fischl add weapon="stringless/songofstillness" refine=5 lvl=90/90;
fischl add set="goldentroupe" count=4;
fischl add stats hp=4780 atk=311 atk%=0.466 electro%=0.466 cr=0.311;
fischl add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;
```

【我的-20231014】6命，精5绝弦/静谧之曲，4剧团攻雷暴，(7.2+13.7)双暴+3.2攻击+6.6精通+2.9充能  

```text
fischl char lvl=90/90 cons=6 talent=6,10,8; 
fischl add weapon="stringless/songofstillness" refine=5 lvl=90/90;
fischl add set="goldentroupe" count=4;
fischl add stats hp=6163 atk=784 def=35 em=131 cr=0.548 cd=0.901 er=0.162 electro%=0.466;
```

### 北斗

【砂武/砂激-浪影绝缘】6命，精5浪影阔剑，4绝缘充雷暴，(9+11)双暴+2攻击+2精通+2充能  

```text
beidou char lvl=90/90 cons=6 talent=9,9,9;
beidou add weapon="tidalshadow" refine=5 lvl=90/90;
beidou add set="emblemofseveredfate" count=4;
beidou add stats hp=4780 atk=311 er=0.518 electro%=0.466 cr=0.311;
beidou add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;
```

【我的-20231014】6命，精5浪影阔剑，4绝缘充雷暴，(11.1+13.2)双暴+3.9攻击+2.9精通+0充能  

```text
beidou char lvl=90/90 cons=6 talent=2,10,10; 
beidou add weapon="tidalshadow" refine=5 lvl=90/90;
beidou add set="emblemofseveredfate" count=4;
beidou add stats hp=4780 atk=455 def=194 em=58 cr=0.677 cd=0.870 er=0.518 electro%=0.466;
```

### 久岐忍

【超绽-伞剑乐园三精】6命，精5东花坊时雨，4乐园精精精，4精通+8生命  

```text
kuki char lvl=90/90 cons=6 talent=9,9,9;
kuki add weapon="toukaboushigure" refine=5 lvl=90/90;
kuki add set="flowerofparadiselost" count=4;
kuki add stats hp=4780 atk=311 em=187 em=187 em=187;
kuki add stats hp=0 hp%=0.392 atk=0 atk%=0 def=0 def%=0 er=0 em=80 cr=0 cd=0;
```

【治疗-伞剑千岩】6命，精5东花坊时雨，4千岩生生治，4精通+8生命  

```text
kuki char lvl=90/90 cons=6 talent=9,9,9;
kuki add weapon="toukaboushigure" refine=5 lvl=90/90;
kuki add set="tenacityofthemillelith" count=4;
kuki add stats hp=4780 atk=311 hp%=0.466 hp%=0.466 hp%=0.466;
kuki add stats hp=0 hp%=0.392 atk=0 atk%=0 def=0 def%=0 er=0 em=80 cr=0 cd=0;
```

### 丽莎

【通用-西风如雷/绝缘】0命，精5西风秘典，4如雷攻雷暴，(9+11)双暴+2攻击+2精通+2充能  

```text
lisa char lvl=90/90 cons=0 talent=9,9,9;
lisa add weapon="favoniuscodex" refine=5 lvl=90/90;
lisa add set="thunderingfury/emblemofseveredfate" count=4;
lisa add stats hp=4780 atk=311 er=0.518 electro%=0.466 cr=0.311;
lisa add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;
```

### 雷泽

【彩虹-乐园三精】6命，精5饰铁之花，4乐园精精精，6精通+6充能  

```text
razor char lvl=90/90 cons=6 talent=9,9,9;
razor add weapon="mailedflower" refine=5 lvl=90/90;
razor add set="flowerofparadiselost" count=4;
razor add stats hp=4780 atk=311 em=187 em=187 em=187;
razor add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=120 cr=0 cd=0;
```

### 莱伊拉

【通用-千岩挂冰盾辅】6命，精5天目影打刀，4千岩生生生，4生命+10充能  

```text
layla char lvl=90/90 cons=6 talent=9,9,9;
layla add weapon="amenomakageuchi" refine=5 lvl=90/90;
layla add set="tenacityofthemillelith" count=4;
layla add stats hp=4780 atk=311 hp%=0.466 hp%=0.466 hp%=0.466;
layla add stats hp=0 hp%=0.196 atk=0 atk%=0 def=0 def%=0 er=0.55 em=0 cr=0 cd=0;
```

### 砂糖

【通用-精通风套驾驶员】6命，精5试作金珀/祭礼残章/讨龙英杰谭，4风套精精精，4精通+6充能  

```text
sucrose char lvl=90/90 cons=6 talent=9,9,9;
sucrose add weapon="prototypeamber/sacrificialfragments/thrillingtalesofdragonslayers" refine=5 lvl=90/90;
sucrose add set="viridescentvenerer" count=4;
sucrose add stats hp=4780 atk=311 em=187 em=187 em=187;
sucrose add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=80 cr=0 cd=0;
```

【我的-20231014】4命，精5试作金珀/祭礼残章/讨龙英杰谭，4风套精精精，4.2精通+10.7充能  

```text
sucrose char lvl=90/90 cons=4 talent=3,3,3;
sucrose add weapon="prototypeamber/sacrificialfragments/thrillingtalesofdragonslayers" refine=5 lvl=90/90;
sucrose add set="viridescentvenerer" count=4;
sucrose add stats hp=6120 atk=467 def=199 em=643 cr=0.132 cd=0.140 er=0.589;
```

### 鹿野院平藏

【通用-速切输出】6命，精5流浪乐章，2风套2角斗攻风暴，(9+11)双暴+4攻击

```text
heizou char lvl=90/90 cons=6 talent=9,9,9;
heizou add weapon="thewidsith" refine=5 lvl=90/90;
heizou add set="viridescentvenerer" count=2;
heizou add set="gladiatorsfinale" count=2;
heizou add stats hp=4780 atk=311 atk%=0.466 anemo%=0.466 cr=0.311;
heizou add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0 em=0 cr=0.297 cd=0.726;
```

【珐鹿琳莱-充能速切治疗】6命，精5试作金珀，4宗室攻风暴，(9+11)双暴+4攻击  

```text
heizou char lvl=90/90 cons=6 talent=9,9,9;
heizou add weapon="prototypeamber" refine=5 lvl=90/90;
heizou add set="noblesseoblige" count=4;
heizou add stats hp=4780 atk=311 atk%=0.466 anemo%=0.466 cr=0.311;
heizou add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0 em=0 cr=0.297 cd=0.726;
```

【我的-20231014】6命，精1流浪乐章，2风套2追忆攻风暴，(12.1+12.4)双爆+7.9攻击+2.1精通  

```text
heizou char lvl=90/90 cons=6 talent=8,10,10;
heizou add weapon="thewidsith" refine=1 lvl=90/90;
heizou add set="viridescentvenerer" count=2;
heizou add set="gladiatorsfinale" count=2;
heizou add stats hp=6757 atk=943 def=40 em=42 cr=0.712 cd=0.816 er=0 anemo%=0.466;
```

### 珐露珊

【通用-后台风辅】6命，精5西风猎弓，4千岩/4风套攻/充风暴，(12+8)双暴+4充能  

```text
faruzan char lvl=90/90 cons=6 talent=9,9,9;
faruzan add weapon="favoniuswarbow" refine=5 lvl=90/90;
faruzan add set="tenacityofthemillelith/viridescentvenerer" count=4;
faruzan add stats hp=4780 atk=311 atk%=0.466/er=0.518 anemo%=0.466 cr=0.311;
faruzan add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.22 em=0 cr=0.396 cd=0.528;
```

【珐鹿琳莱-站场输出】6命，精5静谧之曲，4剧团攻/充风暴，(12+8)双暴+4充能  

```text
faruzan char lvl=90/90 cons=6 talent=9,9,9;
faruzan add weapon="songofstillness" refine=5 lvl=90/90;
faruzan add set="goldentroupe" count=4;
faruzan add stats hp=4780 atk=311 atk%=0.466/er=0.518 anemo%=0.466 cr=0.311;
faruzan add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.22 em=0 cr=0.396 cd=0.528;
```

【我的-20231014】6命，精5静谧之曲，2风套2追忆攻风暴，(13.2+13.9)双爆+5.2充能+1.1攻击  

```text
faruzan char lvl=90/90 cons=6 talent=10,10,10;
faruzan add weapon="songofstillness" refine=5 lvl=90/90;
faruzan add set="viridescentvenerer" count=2;
faruzan add set="shimenawasreminiscence" count=2;
faruzan add stats hp=5784 atk=733 def=165 em=0 cr=0.747 cd=0.917 er=0.285 anemo%=0.466;
```

### 琳妮特

【通用-风套工具人】6命，精5西风剑，4风套充风暴，(9+11)双暴+4攻击  

```text
lynette char lvl=90/90 cons=6 talent=9,9,9;
lynette add weapon="favoniussword" refine=5 lvl=90/90;
lynette add set="viridescentvenerer" count=4;
lynette add stats hp=4780 atk=311 er=0.518 anemo%=0.466 cr=0.311;
lynette add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0 em=0 cr=0.297 cd=0.726;
```

【珐鹿琳莱-速切嘲讽副C】6命，精5西风剑，2角斗2追忆攻风暴，(9+11)双暴+4攻击  

```text
lynette char lvl=90/90 cons=6 talent=9,9,9;
lynette add weapon="favoniussword" refine=5 lvl=90/90;
lynette add set="gladiatorsfinale" count=2;
lynette add set="shimenawasreminiscence" count=2;
lynette add stats hp=4780 atk=311 atk%=0.466 anemo%=0.466 cr=0.311;
lynette add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0 em=0 cr=0.297 cd=0.726;
```

### 草主

【通用-草套工具人】6命，精5西风剑，4草套充草暴，(7+9)双爆+4攻击+4充能  

```text
travelerdendro char lvl=90/90 cons=6 talent=9,9,9;
travelerdendro add weapon="favoniussword" refine=5 lvl=90/90;
travelerdendro add set="deepwoodmemories" count=4;
travelerdendro add stats hp=4780 atk=311 er=0.518 dendro%=0.466 cr=0.311;
travelerdendro add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0.22 em=0 cr=0.231 cd=0.594;
```

### 柯莱

【通用-草套工具人】6命，精5西风猎弓，4草套充草暴，(7+9)双爆+4攻击+4充能  

```text
collei char lvl=90/90 cons=6 talent=9,9,9;
collei add weapon="favoniuswarbow" refine=5 lvl=90/90;
collei add set="deepwoodmemories" count=4;
collei add stats hp=4780 atk=311 er=0.518 dendro%=0.466 cr=0.311;
collei add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0.22 em=0 cr=0.231 cd=0.594;
```

### 瑶瑶

【通用-治疗】6命，精5公义的酬报，4千岩/4草套生生治，4精通+6生命+6充能  

```text
yaoyao char lvl=90/90 cons=6 talent=9,9,9;
yaoyao add weapon="rightfulreward" refine=5 lvl=90/90;
yaoyao add set="tenacityofthemillelith/deepwoodmemories" count=4;
yaoyao add stats hp=4780 atk=311 hp%=0.466 hp%=0.466 heal=0.359;
yaoyao add stats hp=0 hp%=0.294 atk=0 atk%=0 def=0 def%=0 er=0.33 em=80 cr=0 cd=0;
```

【挂草循环-草套西风】6命，精5西风长枪，4草套生生治，10暴击+6充能  

```text
yaoyao char lvl=90/90 cons=6 talent=9,9,9;
yaoyao add weapon="favoniuslance" refine=5 lvl=90/90;
yaoyao add set="deepwoodmemories" count=4;
yaoyao add stats hp=4780 atk=311 hp%=0.466 hp%=0.466 heal=0.359;
yaoyao add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.33 cd=0;
```
