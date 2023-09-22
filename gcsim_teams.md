# gcsim队伍代码

只包含队伍与循环部分，场景设置请看gcsim模板一节  

部分队伍对技能释放顺序要求较高，而轴又比较复杂，gcsim直接循环掉伤害很严重，  
因此这些队伍会在手工确认第二轮循环能成立的情况下，只模拟第一个循环的DPS，  
此时对应DPS会标注循环时长。  

## 班尼特 香菱 行秋 砂糖

班尼特5命，精5原木刀，4教官充火暴，(5+7)双暴+6生命+6充能  
香菱6命，精5渔获，4绝缘充火暴，(9+11)双暴+2攻击+2精通+2充能  
行秋6命，精5祭礼剑，4宗室攻水暴，(9+11)双暴+2攻击+2充能  
砂糖6命，精5讨龙英杰谭，4风套精精精，4精通+6充能  

DPS：(20s)  
0金 4.50w = 4.23w ~ 4.77w (砂糖两轮一Q，单判，行秋不凹蒸发)  

```text
bennett char lvl=90/90 cons=5 talent=9,9,9;
bennett add weapon="sapwoodblade" refine=5 lvl=90/90;
bennett add set="instructor" count=4;
bennett add stats hp=4780 atk=311 er=0.518 pyro%=0.466 cr=0.311;
bennett add stats hp=0 hp%=0.294 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.165 cd=0.462;

xiangling char lvl=90/90 cons=6 talent=9,9,9;
xiangling add weapon="thecatch" refine=5 lvl=90/90;
xiangling add set="emblemofseveredfate" count=4;
xiangling add stats hp=4780 atk=311 er=0.518 pyro%=0.466 cr=0.311;
xiangling add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

xingqiu char lvl=90/90 cons=6 talent=9,9,9;
xingqiu add weapon="sacrificialsword" refine=5 lvl=90/90;
xingqiu add set="noblesseoblige" count=4;
xingqiu add stats hp=4780 atk=311 atk%=0.466 hydro%=0.466 cr=0.311;
xingqiu add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=0 cr=0.297 cd=0.726;

sucrose char lvl=90/90 cons=6 talent=9,9,9;
sucrose add weapon="thrillingtalesofdragonslayers" refine=5 lvl=90/90;
sucrose add set="viridescentvenerer" count=4;
sucrose add stats hp=4780 atk=311 em=187 em=187 em=187;
sucrose add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=80 cr=0 cd=0;

options duration=20;
active xingqiu;
while 1 {
    xingqiu burst, attack;
    bennett burst, attack;
    sucrose attack, skill, dash;
    if .sucrose.burst.ready {
        sucrose burst;
    }
    xiangling attack, burst, skill;
    sucrose skill, dash;
    xingqiu attack, skill, dash;
    if .xingqiu.skill.ready {
      xingqiu attack, skill, dash;
    }
    xingqiu attack:3;
    sucrose attack:4, attack;
    bennett attack, skill;
    xiangling attack:3;
    bennett attack, skill;
    xiangling attack:3;
}
```

备注：雷国，用雷电将军替代砂糖  
雷电将军0命，精5西风枪，4绝缘充雷暴，(9+11)双暴+2攻击+2充能  

DPS：(20s)  
1金 5.27w (教官班尼特，攻击沙香菱，宗室行秋，雷国极致配装)  
1金 5.11w (教官班尼特，充能沙香菱，宗室行秋，即只换砂糖其他不变)  
1金 5.00w (宗室班尼特，攻击沙香菱，绝缘行秋，雷国常见配装)  
1金 4.86w (宗室班尼特，充能沙香菱，绝缘行秋)  

```text
raiden char lvl=90/90 cons=0 talent=9,9,9;
raiden add weapon="favoniuslance" refine=5 lvl=90/90;
raiden add set="emblemofseveredfate" count=4;
raiden add stats hp=4780 atk=311 er=0.518 electro%=0.466 cr=0.311;
raiden add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=0 cr=0.297 cd=0.726;

options duration=20;
active raiden;
while 1 {
    raiden skill;
    xingqiu burst, attack;
    bennett burst, attack, skill;
    xiangling burst, attack, skill;
    xingqiu attack, skill, dash;
    if .xingqiu.skill.ready {
        xingqiu attack, skill, dash;
    }
    raiden burst;
    raiden attack:3, charge, attack:3, charge, attack:3, charge, attack:2;
    bennett attack, skill;
}
```

## 班尼特 香菱 凯亚 罗莎莉亚

班尼特5命，精1原木刀，4宗室充火暴，(5+7)双暴+6生命+6充能  
香菱6命，精5渔获，4绝缘充火暴，(9+11)双暴+2攻击+2精通+2充能  
凯亚2命，精5匣里龙吟，4绝缘充冰暴，(9+11)双暴+2攻击+2精通+2充能  
罗莎莉亚6命，精5西风长枪，2冰2宗室精冰暴，(9+11)双暴+2攻击+2精通+2充能  

DPS：(15s)  
0金 3.35w  

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
  
DPS：(24s)  
0金 3.10w  

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

options duration=24;
active layla;
while 1{
    layla skill;
    lynette burst, skill;
    faruzan burst, skill;
    heizou burst, attack, charge, skill[hold=1];
    faruzan aim, aim, skill, aim, aim;
    layla skill, burst;
    lynette skill;
    faruzan skill;
    heizou burst, attack, charge, skill[hold=1];
    faruzan aim, aim, skill, aim, aim;
}
```

## 班尼特 香菱 珐露珊 鹿野院平藏

班尼特5命，精5原木刀，4宗室充火暴，(5+7)双暴+6生命+6充能  
香菱6命，精5渔获，4绝缘充火暴，(9+11)双暴+2攻击+2精通+2充能  
珐露珊6命，精5西风猎弓，4风套充风暴，(12+8)双暴+4充能  
鹿野院平藏6命，精5流浪乐章，2风套2角斗攻风暴，(9+11)双暴+4攻击 
  
DPS：(20s)  
0金 3.69w  

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

heizou char lvl=90/90 cons=6 talent=9,9,9;
heizou add weapon="thewidsith" refine=5 lvl=90/90;
heizou add set="viridescentvenerer" count=2;
heizou add set="gladiatorsfinale" count=2;
heizou add stats hp=4780 atk=311 atk%=0.466 anemo%=0.466 cr=0.311;
heizou add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0 em=0 cr=0.297 cd=0.726;

faruzan char lvl=90/90 cons=6 talent=9,9,9;
faruzan add weapon="favoniuswarbow" refine=5 lvl=90/90;
faruzan add set="viridescentvenerer" count=4;
faruzan add stats hp=4780 atk=311 er=0.518 anemo%=0.466 cr=0.311;
faruzan add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.22 em=0 cr=0.396 cd=0.528;

active bennett;
while 1{
    bennett skill, burst;
    faruzan skill, burst;
    xiangling burst, skill;
    heizou attack, charge, burst, skill;
    bennett attack, skill;
    xiangling attack:2;
    bennett attack, skill;
    xiangling attack:2;
    heizou attack, charge, attack:3, skill;
}
```

## 草主 柯莱 行秋 久岐忍

草主6命，精5西风剑，4草套充草暴，(7+9)双爆+4攻击+4充能  
柯莱6命，精5西风猎弓，4草套充草暴，(7+9)双爆+4攻击+4充能  
行秋6命，精5祭礼剑，4绝缘攻水暴，(9+11)双暴+2攻击+2充能  
久岐忍6命，精5东花坊时雨，4乐园精精精，4精通+8生命  

DPS：  
0金 5.15w  

```text
travelerdendro char lvl=90/90 cons=6 talent=9,9,9;
travelerdendro add weapon="favoniussword" refine=5 lvl=90/90;
travelerdendro add set="deepwoodmemories" count=4;
travelerdendro add stats hp=4780 atk=311 er=0.518 dendro%=0.466 cr=0.311;
travelerdendro add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0.22 em=0 cr=0.231 cd=0.594;

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

active travelerdendro;
travelerdendro skill, burst;
xingqiu burst, attack;
kuki skill, dash, attack;
collei skill, attack;
xingqiu attack, skill, dash;
if .xingqiu.skill.ready {
    xingqiu attack, skill, dash;
}
travelerdendro skill;
while 1{
    if .kuki.skill.ready {
        kuki skill, dash, attack;
    } else if .xingqiu.burst.ready {
        xingqiu burst, attack;
    } else if .travelerdendro.skill.ready {
        travelerdendro skill;
    } else if .collei.skill.ready {
        collei skill;
    } else if .travelerdendro.burst.ready {
        travelerdendro burst;
    } else if .collei.burst.ready {
        collei burst;
    } else if .xingqiu.skill.ready {
        xingqiu attack, skill, dash;
        if .xingqiu.skill.ready {
            xingqiu attack, skill, dash;
        }
    } else {
        kuki attack;
    }
}
```

## 草主 柯莱 芭芭拉 久岐忍

草主6命，精5西风剑，4草套充草暴，(7+9)双爆+4攻击+4充能  
柯莱6命，精5西风猎弓，4草套充草暴，(7+9)双爆+4攻击+4充能  
芭芭拉6命，精5试作金珀，4海染生生治，4精通+6生命  
久岐忍6命，精5东花坊时雨，4乐园精精精，4精通+8生命  

注：代码中手法难度较大且全程贴身，对实战DPS的参考价值有限  

DPS：  
0金 4.12w  

```text
travelerdendro char lvl=90/90 cons=6 talent=9,9,9;
travelerdendro add weapon="favoniussword" refine=5 lvl=90/90;
travelerdendro add set="deepwoodmemories" count=4;
travelerdendro add stats hp=4780 atk=311 er=0.518 dendro%=0.466 cr=0.311;
travelerdendro add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0.22 em=0 cr=0.231 cd=0.594;

collei char lvl=90/90 cons=6 talent=9,9,9;
collei add weapon="favoniuswarbow" refine=5 lvl=90/90;
collei add set="deepwoodmemories" count=4;
collei add stats hp=4780 atk=311 er=0.518 dendro%=0.466 cr=0.311;
collei add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0.22 em=0 cr=0.231 cd=0.594;

barbara char lvl=90/90 cons=6 talent=9,9,9;
barbara add weapon="prototypeamber" refine=5 lvl=90/90;
barbara add set="oceanhuedclam" count=4;
barbara add stats hp=4780 atk=311 hp%=0.466 hp%=0.466 heal=0.359;
barbara add stats hp=0 hp%=0.294 atk=0 atk%=0 def=0 def%=0 er=0 em=80 cr=0 cd=0;

kuki char lvl=90/90 cons=6 talent=9,9,9;
kuki add weapon="toukaboushigure" refine=5 lvl=90/90;
kuki add set="flowerofparadiselost" count=4;
kuki add stats hp=4780 atk=311 em=187 em=187 em=187;
kuki add stats hp=0 hp%=0.392 atk=0 atk%=0 def=0 def%=0 er=0 em=80 cr=0 cd=0;

active travelerdendro;
travelerdendro skill, burst;
barbara attack, skill, jump;
kuki skill, dash;
barbara attack:4;
travelerdendro skill;
while 1{
    if .kuki.skill.ready {
        kuki skill, dash;
    } else if .barbara.skill.ready {
        barbara attack, skill, jump;
    } else if .travelerdendro.skill.ready {
        travelerdendro skill;
    } else if .collei.skill.ready {
        collei skill;
    } else if .travelerdendro.burst.ready {
        travelerdendro burst;
    } else if .collei.burst.ready {
        collei burst;
    } else {
        barbara attack:4;
    }
}
```

## 柯莱 行秋 久岐忍 菲谢尔

柯莱6命，精5西风猎弓，4草套充草暴，(7+9)双爆+4攻击+4充能  
行秋6命，精5祭礼剑，4绝缘攻水暴，(9+11)双暴+2攻击+2充能  
久岐忍6命，精5东花坊时雨，4乐园精精精，4精通+8生命  
菲谢尔6命，精5绝弦，4剧团攻雷暴，(9+11)双暴+2攻击+2充能  

DPS：  
0金对单 4.46w (小体积怪，皇女抢种子)  
0金对单 5.72w (大体积怪，皇女不抢种子)  

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
        xingqiu attack, skill, dash;
        if .xingqiu.skill.ready {
            xingqiu attack, skill, dash;
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

备注：草行久皇，草神换柯莱  
纳西妲0命，精5祭礼书残章，4草套精精精，(3+5)双暴+4精通  

DPS：  
1金对单 5.30w (小体积怪，皇女抢种子)  
1金对单 6.65w (大体积怪，皇女不抢种子)  

```text
nahida char lvl=90/90 cons=0 talent=9,9,9;
nahida add weapon="sacrificialfragments" refine=5 lvl=90/90;
nahida add set="deepwoodmemories" count=4;
nahida add stats hp=4780 atk=311 em=187 em=187 em=187;
nahida add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0 em=80 cr=0.099 cd=0.33;

active nahida;
nahida skill, burst;
fischl skill;
xingqiu burst, attack;
kuki skill, attack;
nahida attack:3, dash, attack:3, dash;
xingqiu skill, attack, dash;
if .xingqiu.skill.ready {
  xingqiu skill, attack, dash;
}
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
        xingqiu attack, skill, dash;
        if .xingqiu.skill.ready {
            xingqiu attack, skill, dash;
        }
    } else if .nahida.skill.ready {
        nahida attack:3, skill;
    } else if .nahida.burst.ready {
        nahida attack, burst;
    } else {
        nahida attack:3, dash;
    }
}
```
