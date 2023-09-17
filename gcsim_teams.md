# gcsim队伍代码

只包含队伍与循环部分，场景设置请看gcsim模板一节

## 班尼特 香菱 凯亚 罗莎莉亚

班尼特5命，精1原木刀，4宗室充火暴，(5+7)双暴+6生命+6充能  
香菱6命，精5渔获，4绝缘充火暴，(9+11)双暴+2攻击+2精通+2充能  
凯亚2命，精5匣里龙吟，4绝缘充冰暴，(9+11)双暴+2攻击+2精通+2充能  
罗莎莉亚6命，精5西风长枪，2冰2宗室精冰暴，(9+11)双暴+2攻击+2精通+2充能  

DPS：  
0金冗余充能 3.21w （代码使用）  
0金压低充能 3.63w （班尼特香菱攻击沙，凯亚精通沙）  

```text
bennett char lvl=90/90 cons=5 talent=9,9,9;
bennett add weapon="sapwoodblade" refine=1 lvl=90/90;
bennett add set="noblesseoblige" count=4;
bennett add stats hp=4780 atk=311 er=0.518 pyro%=0.466 cr=0.311;
bennett add stats hp=0 hp%=0.294 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.165 cd=0.462;

xiangling char lvl=90/90 cons=6 talent=9,9,9;
xiangling add weapon="thecatch" refine=5 lvl=90/90;
xiangling add set="emblemofseveredfate" count=4;
xiangling add stats hp=4780 atk=311 er=0.518 pyro%=0.466 cr=0.311;
xiangling add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

kaeya char lvl=90/90 cons=2 talent=9,9,9;
kaeya add weapon="lionsroar" refine=5 lvl=90/90;
kaeya add set="emblemofseveredfate" count=4;
kaeya add stats hp=4780 atk=311 er=0.518 cryo%=0.466 cr=0.311;
kaeya add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

rosaria char lvl=90/90 cons=2 talent=9,9,9;
rosaria add weapon="favoniuslance" refine=5 lvl=90/90;
rosaria add set="blizzardstrayer" count=2;
rosaria add set="noblesseoblige" count=2;
rosaria add stats hp=4780 atk=311 em=187 cryo%=0.466 cr=0.311;
rosaria add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

active rosaria;
while 1 {
  rosaria skill;
  bennett burst, skill;
  rosaria burst;
  xiangling burst, skill;
  kaeya skill, burst;
  rosaria skill, attack;
  bennett attack, skill;
  xiangling attack:2;
  kaeya attack, skill;
  rosaria attack, skill;
  bennett attack, skill;
  xiangling attack:2;
  kaeya skill;
}
```

## 砂糖 北斗 菲谢尔 行秋

砂糖6命，精5试作金珀，4风套精精精，4精通+6充能  
北斗6命，精5浪影阔剑，4绝缘充雷暴，(9+11)双暴+2攻击+2充能  
菲谢尔6命，精5绝弦，4剧团攻雷暴，(9+11)双暴+2攻击+2充能  
行秋6命，精5祭礼剑，4绝缘攻水暴，(9+11)双暴+2攻击+2充能  
  
DPS：  
0金对单 3.82w
0金对双 3.34w
0金对三 2.87w
0金对四 2.59w

```text
sucrose char lvl=90/90 cons=6 talent=9,9,9;
sucrose add weapon="prototypeamber" refine=5 lvl=90/90;
sucrose add set="viridescent" count=4;
sucrose add stats hp=4780 atk=311 em=187 em=187 em=187;
sucrose add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=80 cr=0 cd=0;

beidou char lvl=90/90 cons=6 talent=9,9,9;
beidou add weapon="finaleofthedeep" refine=5 lvl=90/90;
beidou add set="emblemofseveredfate" count=4;
beidou add stats hp=4780 atk=311 er=0.518 electro%=0.466 cr=0.311;
beidou add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=0 cr=0.297 cd=0.726;

fischl char lvl=90/90 cons=6 talent=9,9,9; 
fischl add weapon="stringless" refine=5 lvl=90/90;
fischl add set="goldentroupe" count=4;
fischl add stats hp=4780 atk=311 atk%=0.466 electro%=0.466 cr=0.311;
fischl add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=0 cr=0.297 cd=0.726;

xingqiu char lvl=90/90 cons=6 talent=9,9,9;
xingqiu add weapon="sacrificialsword" refine=5 lvl=90/90;
xingqiu add set="emblemofseveredfate" count=4;
xingqiu add stats hp=4780 atk=311 atk%=0.466 hydro%=0.466 cr=0.311;
xingqiu add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=0 cr=0.297 cd=0.726;

active xingqiu;
xingqiu burst, attack;
fischl skill, attack;
sucrose attack, skill, dash, attack, burst, dash;
beidou attack, skill, attack, burst;
while 1 {
  if .xingqiu.burst.ready {
    xingqiu burst, attack;
  } else if .beidou.burst.ready {
    beidou burst, attack;
  } else if .sucrose.burst.ready {
    sucrose burst, attack;
  } else if .fischl.oz == 0 {
    if .fischl.skill.ready {
      fischl skill, attack;
    } else if .fischl.burst.ready {
      fischl burst, attack;
    }
  } else if .xingqiu.skill.ready {
    xingqiu attack, skill, dash;
    if .xingqiu.skill.ready {
      xingqiu attack, skill, dash;
    }
  } else if .beidou.skill.ready {
    beidou skill, attack;
  } else if .sucrose.skill.ready {
    sucrose attack, skill, dash;
  } else {
    sucrose attack:3, dash;
  }
}
```

## 珐露珊 鹿野院平藏 琳妮特 莱依拉

珐露珊6命，精5静谧之曲，4剧团攻风暴，(12+8)双暴+4充能  
鹿野院平藏6命，精5试作金珀，4宗室攻风暴，(9+11)双暴+4攻击  
琳妮特6命，精5西风剑，2角斗2追忆攻风暴，(9+11)双暴+4攻击  
莱依拉6命，精5天目影打刀，4千岩生生生，4生命+10充能  
  
DPS：  
0金试作 3.04w (无特效)  
0金绝弦 3.11w  
0金静谧 3.23w (代码使用)  
1金若水 3.44w  
1金天空 3.48w  
1金魔术 3.66w  

```text
faruzan char lvl=90/90 cons=6 talent=9,9,9;
faruzan add weapon="songofstillness" refine=5 lvl=90/90;
faruzan add set="goldentroupe" count=4;
faruzan add stats hp=4780 atk=311 atk%=0.466 anemo%=0.466 cr=0.311;
faruzan add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.22 em=0 cr=0.396 cd=0.528;

heizou char lvl=90/90 cons=6 talent=9,9,9;
heizou add weapon="prototypeamber" refine=5 lvl=90/90;
heizou add set="noblesseoblige" count=4;
heizou add stats hp=4780 atk=311 atk%=0.466 anemo%=0.466 cr=0.311;
heizou add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0 em=0 cr=0.33 cd=0.66;

lynette char lvl=90/90 cons=6 talent=9,9,9;
lynette add weapon="favoniussword" refine=5 lvl=90/90;
lynette add set="gladiatorsfinale" count=2;
lynette add set="shimenawasreminiscence" count=2;
lynette add stats hp=4780 atk=311 atk%=0.466 anemo%=0.466 cr=0.311;
lynette add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0 em=0 cr=0.33 cd=0.66;

layla char lvl=90/90 cons=6 talent=9,9,9;
layla add weapon="amenomakageuchi" refine=5 lvl=90/90;
layla add set="tenacityofthemillelith" count=4;
layla add stats hp=4780 atk=311 hp%=0.466 hp%=0.466 hp%=0.466;
layla add stats hp=0 hp%=0.196 atk=0 atk%=0 def=0 def%=0 er=0.55 em=0 cr=0 cd=0;

active layla;
while 1{
 layla skill, burst;
 lynette burst, skill;
 faruzan burst, skill;
 heizou burst, attack, charge, skill[hold=1];
 faruzan aim, aim, skill, aim, aim;

 layla skill, burst;
 lynette skill;
 faruzan skill, aim;
 heizou burst, attack, charge, skill[hold=1];
 faruzan aim, skill, aim, aim;
}
```

## 柯莱 行秋 久岐忍 菲谢尔

柯莱6命，精5西风猎弓，4草套充草暴，(7+9)双爆+4攻击+4充能  
行秋6命，精5祭礼剑，4绝缘攻水暴，(9+11)双暴+2攻击+2充能  
久岐忍6命，精5东花坊时雨，4乐园精精精，4精通+8生命  
菲谢尔6命，精5绝弦，4剧团攻雷暴，(9+11)双暴+2攻击+2充能  

DPS：  
0金 4.35w  

```text
collei char lvl=90/90 cons=6 talent=9,9,9;
collei add weapon="favoniuswarbow" refine=5 lvl=90/90;
collei add set="deepwoodmemories" count=4;
collei add stats hp=4780 atk=311 er=0.518 dendro%=0.466 cr=0.311;
collei add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0.22 em=0 cr=0.231 cd=0.594;

xingqiu char lvl=90/90 cons=6 talent=9,9,9;
xingqiu add weapon="sacrificialsword" refine=5 lvl=90/90;
xingqiu add set="emblemofseveredfate" count=4;
xingqiu add stats hp=4780 atk=311 atk%=0.466 hydro%=0.466 cr=0.311;
xingqiu add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=0 cr=0.297 cd=0.726;

kuki char lvl=90/90 cons=6 talent=9,9,9;
kuki add weapon="toukaboushigure" refine=5 lvl=90/90;
kuki add set="flowerofparadiselost" count=4;
kuki add stats hp=4780 atk=311 em=187 em=187 em=187;
kuki add stats hp=0 hp%=0.392 atk=0 atk%=0 def=0 def%=0 er=0 em=80 cr=0 cd=0;

fischl char lvl=90/90 cons=6 talent=9,9,9; 
fischl add weapon="stringless" refine=5 lvl=90/90;
fischl add set="goldentroupe" count=4;
fischl add stats hp=4780 atk=311 atk%=0.466 electro%=0.466 cr=0.311;
fischl add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=0 cr=0.297 cd=0.726;

active xingqiu;
xingqiu burst, attack;
fischl skill, attack;
collei skill, attack;
kuki skill, attack;
xingqiu skill, attack;
if .xingqiu.skill.ready {
  xingqiu skill, attack;
}
collei burst, attack;
while 1 {
  if .xingqiu.burst.ready {
    xingqiu burst, attack;
  } else if .fischl.oz == 0 {
    if .fischl.skill.ready {
      fischl skill, attack;
    } else if .fischl.burst.ready {
      fischl burst, attack;
    }
  } else if .kuki.skill.ready {
    kuki skill, attack;
  } else if .xingqiu.skill.ready {
    xingqiu skill, attack;
    if .xingqiu.skill.ready {
      xingqiu skill, attack;
    }
  } else if .collei.burst.ready {
    collei burst, attack;
  } else if .collei.skill.ready {
    collei skill, attack;
  } else {
    kuki attack;
  }
}
```
