# gcsim队伍代码

只包含队伍与循环部分，场景设置请看gcsim模板一节  

关于队伍手法/循环：  

1. 对于一般有轴的队伍，会设计一套能循环的手法，使其长度约等于队伍中CD最长的动作，同时牺牲一些对不上轴的小技能，如香班凯修循环长度为香菱Q的20秒，而每个20秒循环中香菱12秒冷却的E只放一次。此时DPS标注为(xx秒循环)。  
2. 部分队伍轴复杂、技能释放顺序要求较高、随机性大或随机性造成的影响大，gcsim直接循环90秒掉伤害非常严重，不能反映队伍真实DPS，如祭礼剑行秋的砂国，如果压了充能祭礼没刷新会严重影响循环和伤害。对于这些队伍，会在手工确认第二轮循环能成立的情况下，只模拟第一个循环的DPS，此时其DPS标注为(xx秒单循环)。  
3. 部分队伍轴非常难排，例如各种带皇女的配队(因为E+Q续奥兹的轴长为25秒)，以及一些各技能冷却不一且没有倍数关系的队伍，如草主+柯莱+水+久岐忍的双草超绽。此时手法为固定起手式+while死循环，每个循环中按照一定的优先级执行某一个已就绪的动作，且DPS标注为(无轴循环)。  

## 0金配队标准练度理论DPS排行榜(施工中)

注1：经典低金配队DPS参考——1金雷国约5w，1金草行久皇约6.65w。  
注2：主要使用通用面板，部分队伍进行针对性换装之后DPS还能提。  

1. 柯莱 行秋 久岐忍 菲谢尔（双雷行秋超绽1），5.72w（大体积怪，皇女不抢种子）
2. 班尼特 香菱 行秋 砂糖（砂糖国家队1），5.22w（班6命/砂秒双扩不开Q/香双判/行秋E双蒸）
3. 草主 柯莱 行秋 久岐忍（双草行秋超绽），5.12w
4. 班尼特 香菱 行秋 砂糖（砂糖国家队2），4.49w（班5命/砂简易双扩三轮一Q/香单判/行秋E不凹蒸发）
5. 柯莱 行秋 久岐忍 菲谢尔（双雷行秋超绽2），4.46w（小体积怪，皇女抢种子）
6. 草主 柯莱 芭芭拉 久岐忍（双草芭芭拉超绽），4.12w
7. 砂糖 北斗 菲谢尔 瑶瑶/行秋（砂糖武装/激化），3.83w
8. 班尼特 香菱 珐露珊 鹿野院平藏（双风双火），3.69w
9. 班尼特 香菱 凯亚 罗莎莉亚（双冰双火），3.34w ~ 3.45w（班5命/6命）
10. 珐露珊 鹿野院平藏 琳妮特 莱依拉（新四星三风队），3.10w

## 班尼特 香菱 行秋 砂糖

班尼特5命，精5原木刀，4教官充火暴，(5+7)双暴+6生命+6充能  
香菱6命，精5渔获，4绝缘充火暴，(9+11)双暴+2攻击+2精通+2充能  
行秋6命，精5祭礼剑，4宗室攻水暴，(9+11)双暴+2攻击+2充能  
砂糖6命，精5讨龙英杰谭，4风套精精精，4精通+6充能  

DPS：(20秒单循环，简易双扩手法，香菱火轮单判，行秋不凹蒸发)  
0金 4.69w (砂糖有Q)  
0金 4.49w (砂糖三轮一Q平均值)  
0金 4.39w (砂糖无Q，用E冲刺代替)  

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
    sucrose burst;                  # sucrose burst ready
    #sucrose skill, dash;           # sucrose burst not ready
    xiangling attack, burst, skill;
    sucrose attack, dash;
    xingqiu attack, skill, dash;
    if .xingqiu.skill.ready {
      xingqiu attack, skill, dash;
    }
    xingqiu attack:3;
    sucrose attack;
    bennett attack, skill;
    xiangling attack:3;
    bennett attack, skill;
    xiangling attack:3;
    bennett attack, skill;
    xiangling attack:3;
}
```

备注1：砂糖秒双扩不开Q + 6命班 + 火轮双判 + 行秋E双蒸，来源<https://gcsim.app/db/hQBtQgpwhp6w#>  
使用时要去掉默认的90秒模拟时长以及默认敌人设定。  

DPS：(~24秒循环)  
0金 5.22w  

```text
options swap_delay=12;
target lvl=100 resist=0.1 pos=-2.4,0 radius=2;
active xingqiu;
for let i = 0; i < 4; i = i + 1 {
    set_player_pos(1.2,0);# 0.8 < 1.2 ≤ 1.6
    xingqiu burst,attack;
    wait(3);
    bennett burst,attack,skill;
    sucrose attack;
    wait(7);
    sucrose skill,dash;
    xiangling attack,skill,dash,attack,burst;
    xingqiu skill;
    let e = .xingqiu.skill.ready;
    if(e) {
        xingqiu skill;
    }
    xingqiu dash;
    set_player_pos(0,0);
    if(!e) {
        xingqiu attack:3;
    }
    bennett attack:3,skill;
    xingqiu attack:2;
    bennett attack:2,skill,attack;
    xiangling attack:3,skill,dash,attack;
    bennett skill,attack;
    xiangling attack:3;
    bennett attack:3,skill;
    if(e) {
        xiangling attack,dash;
    }else {
        xingqiu attack:2;
        sucrose skill,dash,attack;
        xingqiu attack,dash;
    }
}
```

备注2：雷国，用雷电将军替代砂糖  
雷电将军0命，精5西风枪，4绝缘充雷暴，(9+11)双暴+2攻击+2充能  

DPS：(20秒单循环，香菱火轮单判，行秋不凹蒸发)  
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

班尼特5/6命，精1原木刀，4宗室攻火暴，(5+7)双暴+6生命+6充能  
香菱6命，精5渔获，4绝缘充火暴，(9+11)双暴+2攻击+2精通+2充能  
凯亚2命，精5匣里龙吟，4绝缘精冰暴，(9+11)双暴+2攻击+2精通+2充能  
罗莎莉亚6命，精5西风长枪，2冰2宗室精冰暴，(9+11)双暴+2攻击+2精通+2充能  

DPS：(20秒循环)  
0金 3.45w (班尼特6命)  
0金 3.34w (班尼特5命)  

```text
bennett char lvl=90/90 cons=5/6 talent=9,9,9;
bennett add weapon="sapwoodblade" refine=1 lvl=90/90;
bennett add set="noblesseoblige" count=4;
bennett add stats hp=4780 atk=311 atk%=0.466 pyro%=0.466 cr=0.311;
bennett add stats hp=0 hp%=0.294 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.165 cd=0.462;

xiangling char lvl=90/90 cons=6 talent=9,9,9;
xiangling add weapon="thecatch" refine=5 lvl=90/90;
xiangling add set="emblemofseveredfate" count=4;
xiangling add stats hp=4780 atk=311 er=0.518 pyro%=0.466 cr=0.311;
xiangling add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

kaeya char lvl=90/90 cons=2 talent=9,9,9;
kaeya add weapon="lionsroar" refine=5 lvl=90/90;
kaeya add set="emblemofseveredfate" count=4;
kaeya add stats hp=4780 atk=311 em=187 cryo%=0.466 cr=0.311;
kaeya add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

rosaria char lvl=90/90 cons=6 talent=9,9,9;
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

## 砂糖 北斗 菲谢尔 瑶瑶

砂糖6命，精5祭礼残章，4风套精精精，4精通+6充能  
北斗6命，精5浪影阔剑，4绝缘充雷暴，(9+11)双暴+2攻击+2充能  
菲谢尔6命，精5绝弦，4剧团攻雷暴，(9+11)双暴+2攻击+2充能  
瑶瑶6命，精5公义的酬报，4千岩生生治，4精通+6生命+6充能  

DPS：(无轴循环)  
0金 3.83w  

```text
sucrose char lvl=90/90 cons=6 talent=9,9,9;
sucrose add weapon="sacrificialfragments" refine=5 lvl=90/90;
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

yaoyao char lvl=90/90 cons=6 talent=9,9,9;
yaoyao add weapon="rightfulreward" refine=5 lvl=90/90;
yaoyao add set="tenacityofthemillelith" count=4;
yaoyao add stats hp=4780 atk=311 hp%=0.466 hp%=0.466 heal=0.359;
yaoyao add stats hp=0 hp%=0.294 atk=0 atk%=0 def=0 def%=0 er=0.33 em=80 cr=0 cd=0;

active yaoyao;
yaoyao skill;
fischl skill;
sucrose attack, skill, burst;
beidou burst, skill, attack;
while 1 {

    if .fischl.oz == 0 {
        if .fischl.skill.ready {
            fischl skill, attack;
        } else if .fischl.burst.ready {
            fischl burst, attack;
        }
    } 
    
    if .beidou.burst.ready {
        beidou burst, attack;
    } else if .sucrose.burst.ready {
        sucrose burst, attack;
    } else if .yaoyao.skill.ready {
        yaoyao skill, attack;
    } else if .beidou.skill.ready {
        beidou skill, attack;
    } else if .sucrose.skill.ready {
        sucrose attack, skill, dash;
    } else {
        sucrose attack:3, dash;
    }
}
```

## 砂糖 北斗 菲谢尔 行秋

砂糖6命，精5试作金珀，4风套精精精，4精通+6充能  
北斗6命，精5浪影阔剑，4绝缘充雷暴，(9+11)双暴+2攻击+2充能  
菲谢尔6命，精5绝弦，4剧团攻雷暴，(9+11)双暴+2攻击+2充能  
行秋6命，精5祭礼剑，4绝缘攻水暴，(9+11)双暴+2攻击+2充能  
  
DPS：(无轴循环)  
0金 3.83w  

```text
sucrose char lvl=90/90 cons=6 talent=9,9,9;
sucrose add weapon="prototypeamber" refine=5 lvl=90/90;
sucrose add set="viridescent" count=4;
sucrose add stats hp=4780 atk=311 em=187 em=187 em=187;
sucrose add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=80 cr=0 cd=0;

beidou char lvl=90/90 cons=6 talent=9,9,9;
beidou add weapon="tidalshadow" refine=5 lvl=90/90;
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

    if .fischl.oz == 0 {
        if .fischl.skill.ready {
            fischl skill, attack;
        } else if .fischl.burst.ready {
            fischl burst, attack;
        }
    }

    if .xingqiu.burst.ready {
        xingqiu burst, attack;
    } else if .beidou.burst.ready {
        beidou burst, attack;
    } else if .sucrose.burst.ready {
        sucrose burst, attack;
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
  
DPS：(24秒单循环)  
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

班尼特5命，精1原木刀，4宗室充火暴，(5+7)双暴+6生命+6充能  
香菱6命，精5渔获，4绝缘充火暴，(9+11)双暴+2攻击+2精通+2充能  
珐露珊6命，精5西风猎弓，4风套充风暴，(12+8)双暴+4充能  
鹿野院平藏6命，精5流浪乐章，2风套2角斗攻风暴，(9+11)双暴+4攻击  
  
DPS：(20秒循环)  
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

DPS：(无轴循环)  
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

注：此无轴循环难度较大且需要全程贴身，对实战DPS的参考价值有限  

DPS：(无轴循环)  
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

DPS：(无轴循环)  
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

DPS：(无轴循环)  
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
