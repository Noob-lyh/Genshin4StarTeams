# gcsim队伍代码

**队伍手法/循环**：

1. 对于一般有轴的队伍，会设计一套能循环的手法，使其长度约等于队伍中CD最长的动作，同时牺牲一些对不上轴的小技能，如香班凯修循环长度为香菱Q的20秒，而每个20秒循环中香菱12秒冷却的E只放一次。此时DPS标注为`(xx秒循环)`。另外一些冷却比较奇怪的技能(如皇女EQ)会在循环中的某些时间点尝试插入，同时在括号中补充说明。  
2. 部分队伍轴复杂、技能释放顺序要求较高、产球随机性大或随机性造成的影响大，gcsim直接循环90秒掉伤害非常严重，不能反映队伍真实DPS，例如各种带祭礼剑行秋的队伍。对于这些队伍，通常会延长循环时间，或者牺牲部分输出，选择更加适合循环的配装(如行秋带西风剑，或者作弊使用精7祭礼剑)。如果实在难以保证gcsim中的循环，会在手工确认第二轮循环能成立的情况下，只模拟第一个循环的DPS，此时其DPS标注为`(xx秒单循环)`，这样的手法只会作为暂时的解决方案，如果有可以循环的手法会马上替换。  
3. 部分队伍轴非常难排，例如各技能冷却不一且没有倍数关系的队伍，如草主+柯莱+水+久岐忍的双草超绽。此时手法为固定起手式+while死循环，每个循环中按照一定的优先级执行某一个已就绪的动作，且DPS标注为`(无轴循环)`。  
4. 模拟时使用90秒打桩，而不是固定4个循环，因此对出伤快或循环短的队伍会较有优势。

**0金配队标准练度对单DPS排行榜(施工中)**：

1. 柯莱 行秋 久岐忍 菲谢尔（行秋双雷超绽-不抢种/抢种），5.78w/4.59w
2. 班尼特 香菱 行秋 砂糖（砂糖国家队-6班），5.58w
3. 班尼特 香菱 行秋 菲谢尔（皇女国家队），5.14w
4. 草主 柯莱 行秋 久岐忍（行秋双草超绽），5.12w
5. 柯莱 芭芭拉 久岐忍 菲谢尔（芭芭拉双雷超绽-不抢种/抢种），4.51w/3.48w
6. 瑶瑶 行秋 菲谢尔 砂糖（行秋带风超绽/砂糖激绽），4.45w
7. 砂糖 丽莎 菲谢尔 瑶瑶（砂糖激化-丽莎），4.67w
8. 草主 柯莱 芭芭拉 久岐忍（芭芭拉双草超绽），4.12w
9. 班尼特 香菱 行秋 重云（重云国家队），3.94w
10. 砂糖 北斗 菲谢尔 行秋（砂糖武装），3.93w
11. 砂糖 北斗 菲谢尔 瑶瑶（砂糖激化-北斗），3.90w
12. 班尼特 香菱 珐露珊 鹿野院平藏（双风双火），3.69w
13. 瑶瑶 柯莱 行秋 托马（行秋双草烈绽），3.66w
14. 班尼特 香菱 罗莎莉亚 砂糖（融罗），3.62w
15. 珐露珊 鹿野院平藏 行秋 久岐忍（珐鹿感电），3.62w
16. 班尼特 香菱 重云 罗莎莉亚（双冰双火-重罗），3.60w
17. 班尼特 香菱 北斗 菲谢尔（双雷双火），3.52w
18. 班尼特 香菱 凯亚 罗莎莉亚（双冰双火-凯罗），3.45w
19. 珐露珊 鹿野院平藏 琳妮特 莱依拉（新四星三风），3.32w
20. 柯莱 行秋 雷泽 班尼特(6)（彩虹雷泽），3.09w
21. 琳妮特 北斗 菲谢尔 芭芭拉（琳芭武装），3.06w
22. 草主 柯莱 芭芭拉 托马（芭芭拉双草烈绽），2.41w
23. 凯亚 罗莎莉亚 行秋 砂糖（凯亚永冻-讨龙/金珀），2.35w/2.26w

注1：经典低金配队DPS参考，1金雷国约5w，1金草行久皇约6.65w。  
注2：后面标*的DPS值表示该DPS为单循环模拟得到。  
注3：主要使用通用面板，班尼特默认5命，凯亚默认2命（实际上无法触发），部分队伍进行针对性换装之后DPS还能提。此外手法不一定为最优，欢迎贡献更加合理/高伤害的手法。  

## gcsim模拟条件与敌人设置

```text
# gcsim模拟的条件设置，重复设置会覆盖
options iteration=1000;     # 模拟次数
options duration=90;        # 每次模拟的持续时间
options workers=30;         # 并行模拟相关参数
options swap_delay=4;       # 切人延迟（部分手法需要修改此值）
```

```text
# gcsim模拟的敌人设置
# 第一个为前方大体积敌人，第二到五个为前/右/左/后方小体积敌人
# 在此文档中，只使用第一或第二个敌人模拟，通常使用第二个小体积敌人
# 敌人默认100级，无限血量，10%全抗
# 使用通用掉球设置
#target lvl=100 pos=0,3 radius=2.5 pyro=0.1 dendro=0.1 hydro=0.1 electro=0.1 geo=0.1 anemo=0.1 physical=0.1 cryo=0.1;
target lvl=100 pos=0,1 radius=0.5 pyro=0.1 dendro=0.1 hydro=0.1 electro=0.1 geo=0.1 anemo=0.1 physical=0.1 cryo=0.1;
#target lvl=100 pos=1,0 radius=0.5 pyro=0.1 dendro=0.1 hydro=0.1 electro=0.1 geo=0.1 anemo=0.1 physical=0.1 cryo=0.1;
#target lvl=100 pos=-1,0 radius=0.5 pyro=0.1 dendro=0.1 hydro=0.1 electro=0.1 geo=0.1 anemo=0.1 physical=0.1 cryo=0.1;
#target lvl=100 pos=0,-1 radius=0.5 pyro=0.1 dendro=0.1 hydro=0.1 electro=0.1 geo=0.1 anemo=0.1 physical=0.1 cryo=0.1;
energy every interval=480,720 amount=1;     
```

将上面设置调整好后，复制粘贴到gcsim的config.txt中，再在下面粘贴队伍代码，就可以运行gcsim模拟了。  

## 班尼特 香菱 行秋 砂糖

满命班尼特+祭礼行秋，[来源](https://ngabbs.com/read.php?tid=38590510)，注意需要修改切人延迟为1  
班尼特6命，精1原木刀，4教官充火暴，(5+7)双暴+6生命+6充能  
香菱6命，精5渔获，4绝缘充火暴，(9+11)双暴+2攻击+2精通+2充能  
行秋6命，精7祭礼剑(保证刷新E)，4宗室攻水暴，(9+11)双暴+6充能  
砂糖6命，精5讨龙英杰谭，4风套精精精，4精通+6充能  

DPS：(24秒循环)  
0金 5.58w  

```text
bennett char lvl=90/90 cons=6 talent=9,9,9;
bennett add weapon="sapwoodblade" refine=1 lvl=90/90;
bennett add set="instructor" count=4;
bennett add stats hp=4780 atk=311 er=0.518 pyro%=0.466 cr=0.311;
bennett add stats hp=0 hp%=0.294 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.165 cd=0.462;

xiangling char lvl=90/90 cons=6 talent=9,9,9;
xiangling add weapon="thecatch" refine=5 lvl=90/90;
xiangling add set="emblemofseveredfate" count=4;
xiangling add stats hp=4780 atk=311 atk%=0.466 pyro%=0.466 cr=0.311;
xiangling add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

xingqiu char lvl=90/90 cons=6 talent=9,9,9;
xingqiu add weapon="sacrificialsword" refine=7 lvl=90/90;
xingqiu add set="noblesseoblige" count=4;
xingqiu add stats hp=4780 atk=311 atk%=0.466 hydro%=0.466 cr=0.311;
xingqiu add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.297 cd=0.726;

sucrose char lvl=90/90 cons=6 talent=9,9,9;
sucrose add weapon="thrillingtalesofdragonslayers" refine=5 lvl=90/90;
sucrose add set="viridescentvenerer" count=4;
sucrose add stats hp=4780 atk=311 em=187 em=187 em=187;
sucrose add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=80 cr=0 cd=0;

options swap_delay=1;

active xingqiu;
while 1 {
    set_player_pos(0, -1);
    xingqiu burst, attack;
    bennett burst, attack, skill;
    sucrose attack, skill;
    set_player_pos(0, 0);
    sucrose dash;
    wait(25);
    xiangling burst, attack, skill, attack;
    xingqiu swap;
    wait(40);
    xingqiu attack;
    wait(1);
    xingqiu skill, dash, attack, skill, dash, attack;
    xiangling attack:4,charge;
    sucrose attack:1,charge;
    bennett attack:3,skill;
    xiangling attack:3,skill,attack:8;
    wait(6);
}
```

备注：雷国，用雷电将军替代砂糖  
雷电将军0命，精5西风枪，4绝缘充雷暴，(9+11)双暴+2攻击+2充能
行秋词条改为改为20+2n，香菱班尼特不变  
注意队伍充能溢出，换配装DPS还能提升  

DPS：(20秒循环)  
1金 4.88w  

```text
raiden char lvl=90/90 cons=0 talent=9,9,9;
raiden add weapon="favoniuslance" refine=5 lvl=90/90;
raiden add set="emblemofseveredfate" count=4;
raiden add stats hp=4780 atk=311 er=0.518 electro%=0.466 cr=0.311;
raiden add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=0 cr=0.297 cd=0.726;

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

## 班尼特 香菱 行秋 菲谢尔

班尼特5命，精1原木刀，4宗室充火暴，(5+7)双暴+6生命+6充能  
香菱6命，精5渔获，4绝缘充火暴，(9+11)双暴+2攻击+2精通+2充能  
行秋6命，精5西风剑，4绝缘攻水暴，(9+11)双暴+6充能  
菲谢尔6命，精5绝弦，4剧团攻雷暴，(9+11)双暴+2攻击+2精通+2充能  

DPS：(21秒循环，菲谢尔固定时机尝试插入EQ)  
0金 5.14w  

```text
bennett char lvl=90/90 cons=5 talent=9,9,9;
bennett add weapon="sapwoodblade" refine=1 lvl=90/90;
bennett add set="instructor" count=4;
bennett add stats hp=4780 atk=311 er=0.518 pyro%=0.466 cr=0.311;
bennett add stats hp=0 hp%=0.294 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.165 cd=0.462;

xiangling char lvl=90/90 cons=6 talent=9,9,9;
xiangling add weapon="thecatch" refine=5 lvl=90/90;
xiangling add set="emblemofseveredfate" count=4;
xiangling add stats hp=4780 atk=311 er=0.518 pyro%=0.466 cr=0.311;
xiangling add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

xingqiu char lvl=90/90 cons=6 talent=9,9,9;
xingqiu add weapon="favoniussword" refine=5 lvl=90/90;
xingqiu add set="emblemofseveredfate" count=4;
xingqiu add stats hp=4780 atk=311 atk%=0.466 hydro%=0.466 cr=0.311;
xingqiu add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.297 cd=0.726;

fischl char lvl=90/90 cons=6 talent=9,9,9; 
fischl add weapon="stringless" refine=5 lvl=90/90;
fischl add set="goldentroupe" count=4;
fischl add stats hp=4780 atk=311 atk%=0.466 electro%=0.466 cr=0.311;
fischl add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

fn try_summon_oz_with_attack2(){
    if .fischl.oz == 0 {
        if .fischl.skill.ready {
            fischl attack:2, skill;
        } else if .fischl.burst.ready {
            fischl burst;
        }
    }
}

active xingqiu;
while 1 {
    xingqiu burst, attack;
    bennett burst, attack, skill;
    try_summon_oz_with_attack2();
    xiangling attack, burst, attack, skill;
    try_summon_oz_with_attack2();
    while !.xingqiu.skill.ready {
        xingqiu attack;
    }
    xingqiu attack, skill, dash;
    xingqiu attack:3;
    try_summon_oz_with_attack2();
    bennett attack, skill;
    xiangling attack:3;
    try_summon_oz_with_attack2();
    while !.bennett.skill.ready {
        xingqiu attack;
    }
    bennett skill;
    xiangling attack:3;
    try_summon_oz_with_attack2();
    while !.xingqiu.burst.ready {
        xingqiu attack;
    }
}
```

## 班尼特 香菱 行秋 重云

班尼特5命，精1原木刀，4宗室充火暴，(5+7)双暴+6生命+6充能  
香菱6命，精5渔获，4绝缘充火暴，(9+11)双暴+2攻击+2精通+2充能  
行秋6命，精5西风剑，4绝缘攻水暴，(9+11)双暴+6充能  
重云6命，精5饰铁之花，4绝缘充冰暴，(9+11)双暴+2攻击+2精通+2充能  

DPS：(18秒循环)  
0金 3.94w  

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

xingqiu char lvl=90/90 cons=6 talent=9,9,9;
xingqiu add weapon="favoniussword" refine=5 lvl=90/90;
xingqiu add set="emblemofseveredfate" count=4;
xingqiu add stats hp=4780 atk=311 atk%=0.466 hydro%=0.466 cr=0.311;
xingqiu add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.297 cd=0.726;

chongyun char lvl=90/90 cons=6 talent=9,9,9;
chongyun add weapon="mailedflower" refine=5 lvl=90/90;
chongyun add set="emblemofseveredfate" count=4;
chongyun add stats hp=4780 atk=311 er=0.518 cryo%=0.466 cr=0.311;
chongyun add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

active chongyun;
while 1 {
    chongyun skill;
    xingqiu burst, attack;
    bennett burst, skill;
    xiangling attack, burst, attack, skill;
    chongyun burst;
    xingqiu attack, skill, dash;
    xingqiu attack:3;
    bennett attack, skill;
    while !.bennett.skill.ready {
        xingqiu attack;
    }
    bennett skill;
    xiangling attack:3;
}
```

## 班尼特 香菱 凯亚 罗莎莉亚

班尼特5，精1原木刀，4宗室攻火暴，(5+7)双暴+6生命+6充能  
香菱6命，精5渔获，4绝缘攻火暴，(9+11)双暴+2攻击+2精通+2充能  
凯亚2命，精5匣里龙吟，4绝缘精冰暴，(9+11)双暴+2攻击+2精通+2充能  
罗莎莉亚6命，精5西风长枪，2冰2宗室精冰暴，(9+11)双暴+2攻击+2精通+2充能  

DPS：(20秒循环)  
0金 3.45w  

```text
bennett char lvl=90/90 cons=5/6 talent=9,9,9;
bennett add weapon="sapwoodblade" refine=1 lvl=90/90;
bennett add set="noblesseoblige" count=4;
bennett add stats hp=4780 atk=311 atk%=0.466 pyro%=0.466 cr=0.311;
bennett add stats hp=0 hp%=0.294 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.165 cd=0.462;

xiangling char lvl=90/90 cons=6 talent=9,9,9;
xiangling add weapon="thecatch" refine=5 lvl=90/90;
xiangling add set="emblemofseveredfate" count=4;
xiangling add stats hp=4780 atk=311 atk%=0.466 pyro%=0.466 cr=0.311;
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

## 班尼特 香菱 重云 罗莎莉亚

班尼特5命，精1原木刀，4宗室攻火暴，(5+7)双暴+6生命+6充能  
香菱6命，精5渔获，4绝缘充火暴，(9+11)双暴+2攻击+2精通+2充能  
重云6命，精5饰铁之花，4绝缘精冰暴，(9+11)双暴+2攻击+2精通+2充能  
罗莎莉亚6命，精5西风长枪，2冰2宗室精冰暴，(9+11)双暴+2攻击+2精通+2充能  

DPS：(17秒循环)  
0金 3.60w  

```text
bennett char lvl=90/90 cons=6 talent=9,9,9;
bennett add weapon="sapwoodblade" refine=1 lvl=90/90;
bennett add set="noblesseoblige" count=4;
bennett add stats hp=4780 atk=311 atk%=0.466 pyro%=0.466 cr=0.311;
bennett add stats hp=0 hp%=0.294 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.165 cd=0.462;

xiangling char lvl=90/90 cons=6 talent=9,9,9;
xiangling add weapon="thecatch" refine=5 lvl=90/90;
xiangling add set="emblemofseveredfate" count=4;
xiangling add stats hp=4780 atk=311 er=0.518 pyro%=0.466 cr=0.311;
xiangling add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

chongyun char lvl=90/90 cons=6 talent=9,9,9;
chongyun add weapon="mailedflower" refine=5 lvl=90/90;
chongyun add set="emblemofseveredfate" count=4;
chongyun add stats hp=4780 atk=311 em=187 cryo%=0.466 cr=0.311;
chongyun add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

rosaria char lvl=90/90 cons=6 talent=9,9,9;
rosaria add weapon="favoniuslance" refine=5 lvl=90/90;
rosaria add set="blizzardstrayer" count=2;
rosaria add set="noblesseoblige" count=2;
rosaria add stats hp=4780 atk=311 em=187 cryo%=0.466 cr=0.311;
rosaria add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

active chongyun;
while 1 {
    chongyun skill;
    bennett burst, skill;
    rosaria skill, burst;
    xiangling burst, skill;
    bennett skill;
    chongyun burst;
    rosaria skill;
    xiangling attack:2;
    bennett attack, skill;
    xiangling attack:2;
    rosaria skill;
    xiangling attack:2;
}
```

## 班尼特 香菱 罗莎莉亚 砂糖

班尼特5命，精1原木刀，4宗室充火暴，(5+7)双暴+6生命+6充能  
香菱6命，精5渔获，4绝缘充火暴，(9+11)双暴+2攻击+2精通+2充能  
罗莎莉亚6命，精5匣里灭辰，4绝缘充冰暴，(9+11)双暴+2攻击+2精通+2充能  
砂糖6命，精5讨龙英杰谭，4风套精精精，4精通+6充能  

DPS：(20秒循环)  
0金 3.62w  

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

rosaria char lvl=90/90 cons=6 talent=9,9,9;
rosaria add weapon="dragonsbane" refine=5 lvl=90/90;
rosaria add set="emblemofseveredfate" count=4;
rosaria add stats hp=4780 atk=311 er=0.518 cryo%=0.466 cr=0.311;
rosaria add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

sucrose char lvl=90/90 cons=6 talent=9,9,9;
sucrose add weapon="thrillingtalesofdragonslayers" refine=5 lvl=90/90;
sucrose add set="viridescentvenerer" count=4;
sucrose add stats hp=4780 atk=311 em=187 em=187 em=187;
sucrose add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=80 cr=0 cd=0;

active bennett;
while 1 {
    bennett burst, skill;
    sucrose skill, dash;
    rosaria attack, skill, burst;
    sucrose attack;
    xiangling burst, skill;
    bennett attack, skill;
    rosaria attack, skill;
    sucrose attack;
    bennett attack, skill;
    xiangling attack:3;
    rosaria attack, skill;
    bennett skill;
    xiangling attack:3;
}
```

## 砂糖 北斗 菲谢尔 瑶瑶

砂糖6命，精5祭礼残章，4风套精精精，4精通+6充能  
北斗6命，精5浪影阔剑，4绝缘充雷暴，(9+11)双暴+2攻击+2精通+2充能  
菲谢尔6命，精5绝弦，4剧团攻雷暴，(9+11)双暴+2攻击+2精通+2充能  
瑶瑶6命，精5公义的酬报，4千岩生生治，4精通+6生命+6充能  

DPS：(无轴循环)  
0金 3.90w  

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
beidou add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

fischl char lvl=90/90 cons=6 talent=9,9,9; 
fischl add weapon="stringless" refine=5 lvl=90/90;
fischl add set="goldentroupe" count=4;
fischl add stats hp=4780 atk=311 atk%=0.466 electro%=0.466 cr=0.311;
fischl add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

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

## 砂糖 丽莎 菲谢尔 瑶瑶

砂糖6命，精5白辰之环，4风套精精精，4精通+6充能  
丽莎0命，精5西风秘典，4如雷攻雷暴，(9+11)双暴+2攻击+2精通+2充能  
菲谢尔6命，精5绝弦，4剧团攻雷暴，(9+11)双暴+2攻击+2精通+2充能  
瑶瑶6命，精5公义的酬报，4千岩生生治，4精通+6生命+6充能  

DPS：(无轴循环)  
0金 4.67w  

```text
sucrose char lvl=90/90 cons=6 talent=9,9,9;
sucrose add weapon="hakushinring" refine=5 lvl=90/90;
sucrose add set="viridescent" count=4;
sucrose add stats hp=4780 atk=311 em=187 em=187 em=187;
sucrose add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=80 cr=0 cd=0;

lisa char lvl=90/90 cons=0 talent=9,9,9;
lisa add weapon="favoniuscodex" refine=5 lvl=90/90;
lisa add set="thunderingfury" count=4;
lisa add stats hp=4780 atk=311 er=0.518 electro%=0.466 cr=0.311;
lisa add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

fischl char lvl=90/90 cons=6 talent=9,9,9; 
fischl add weapon="stringless" refine=5 lvl=90/90;
fischl add set="goldentroupe" count=4;
fischl add stats hp=4780 atk=311 atk%=0.466 electro%=0.466 cr=0.311;
fischl add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

yaoyao char lvl=90/90 cons=6 talent=9,9,9;
yaoyao add weapon="rightfulreward" refine=5 lvl=90/90;
yaoyao add set="tenacityofthemillelith" count=4;
yaoyao add stats hp=4780 atk=311 hp%=0.466 hp%=0.466 heal=0.359;
yaoyao add stats hp=0 hp%=0.294 atk=0 atk%=0 def=0 def%=0 er=0.33 em=80 cr=0 cd=0;

active yaoyao;
yaoyao skill;
lisa burst, attack;
sucrose burst, attack, skill;
fischl skill;
while 1 {

    if .fischl.oz == 0 {
        if .fischl.skill.ready {
            fischl skill;
        } else if .fischl.burst.ready {
            fischl burst;
        }
    } 
    
    if .lisa.burst.ready {
        lisa attack, burst;
    } else if .sucrose.burst.ready {
        sucrose burst, attack;
    } else if .yaoyao.skill.ready {
        yaoyao skill;
    } else if .sucrose.skill.ready {
        sucrose attack, skill, dash;
    } else {
        lisa attack:3;
        sucrose attack:3;
    }
}
```

## 砂糖 北斗 菲谢尔 行秋

砂糖6命，精5试作金珀，4风套精精精，4精通+6充能  
北斗6命，精5浪影阔剑，4绝缘充雷暴，(9+11)双暴+2攻击+2精通+2充能  
菲谢尔6命，精5静谧之曲，4剧团攻雷暴，(9+11)双暴+2攻击+2精通+2充能  
行秋6命，精5祭礼剑，4绝缘攻水暴，(9+11)双暴+2攻击+2精通+2充能  
  
DPS：(无轴循环)  
0金 3.93w  

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
beidou add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

fischl char lvl=90/90 cons=6 talent=9,9,9; 
fischl add weapon="songofstillness" refine=5 lvl=90/90;
fischl add set="goldentroupe" count=4;
fischl add stats hp=4780 atk=311 atk%=0.466 electro%=0.466 cr=0.311;
fischl add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

xingqiu char lvl=90/90 cons=6 talent=9,9,9;
xingqiu add weapon="sacrificialsword" refine=5 lvl=90/90;
xingqiu add set="emblemofseveredfate" count=4;
xingqiu add stats hp=4780 atk=311 atk%=0.466 hydro%=0.466 cr=0.311;
xingqiu add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

active sucrose;
sucrose burst;
xingqiu burst, attack;
fischl skill;
sucrose attack, skill, dash;
beidou attack, skill, burst;
xingqiu attack, skill, dash;
if .xingqiu.skill.ready {
    xingqiu attack, skill, dash;
}
while 1 {

    if .fischl.oz == 0 {
        if .fischl.skill.ready {
            fischl skill, attack;
        } else if .fischl.burst.ready {
            fischl burst;
            sucrose attack;
            fischl attack, skill[recast=1];
        }
    }

    if .xingqiu.burst.ready {
        xingqiu burst, attack;
    } else if .sucrose.burst.ready {
        sucrose burst, attack;
    } else if .beidou.burst.ready {
        beidou burst, attack;
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

## 琳妮特 北斗 菲谢尔 芭芭拉

琳妮特6命，精5西风剑，4风套充风暴，(9+11)双暴+4攻击  
北斗6命，精5浪影阔剑，4绝缘充雷暴，(9+11)双暴+2攻击+2精通+2充能  
菲谢尔6命，精5静谧之曲，4剧团攻雷暴，(9+11)双暴+2攻击+2精通+2充能  
芭芭拉6命，精5白辰之环，4海染生生治，4精通+6生命  

DPS：(无轴循环)  
0金 3.06w  

```text
lynette char lvl=90/90 cons=6 talent=9,9,9;
lynette add weapon="favoniussword" refine=5 lvl=90/90;
lynette add set="viridescentvenerer" count=4;
lynette add stats hp=4780 atk=311 er=0.518 anemo%=0.466 cr=0.311;
lynette add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0 em=0 cr=0.297 cd=0.726;

fischl char lvl=90/90 cons=6 talent=9,9,9; 
fischl add weapon="songofstillness" refine=5 lvl=90/90;
fischl add set="goldentroupe" count=4;
fischl add stats hp=4780 atk=311 atk%=0.466 electro%=0.466 cr=0.311;
fischl add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

beidou char lvl=90/90 cons=6 talent=9,9,9;
beidou add weapon="tidalshadow" refine=5 lvl=90/90;
beidou add set="emblemofseveredfate" count=4;
beidou add stats hp=4780 atk=311 er=0.518 electro%=0.466 cr=0.311;
beidou add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

barbara char lvl=90/90 cons=6 talent=9,9,9;
barbara add weapon="hakushinring" refine=5 lvl=90/90;
barbara add set="oceanhuedclam" count=4;
barbara add stats hp=4780 atk=311 hp%=0.466 hp%=0.466 heal=0.359;
barbara add stats hp=0 hp%=0.294 atk=0 atk%=0 def=0 def%=0 er=0 em=80 cr=0 cd=0;

fn try_summon_oz_with_attack(){
    if .fischl.oz == 0 {
        if .fischl.skill.ready {
            fischl attack, skill;
        } else if .fischl.burst.ready {
            fischl burst;
        }
    }
}

options iteration=100;
active beidou;
beidou skill;
lynette burst;
let e = f();
barbara skill, dash, attack;
beidou burst;
try_summon_oz_with_attack();
barbara attack:3, dash;
while 1 {

    try_summon_oz_with_attack();

    if ( f()-e > 600 ) {
        if .lynette.skill.ready {
            lynette skill, attack:3;
        } else if .lynette.burst.ready {
            lynette burst;
        }
        let e = f();
    }

    if .beidou.burst.ready {
        beidou burst, attack;
    } else if .beidou.skill.ready {
        beidou skill, attack;
    } else if .barbara.skill.ready {
        barbara skill, jump, attack:3;
    } else {
        barbara attack:3, dash;
    }
}
```

## 凯亚 罗莎莉亚 行秋 砂糖

凯亚2命，笼钓瓶一心，4冰套攻冰爆，(11+9)双暴+2攻击+2精通+2充能  
罗莎莉亚6命，精5西风长枪，2冰2宗室精冰暴，(9+11)双暴+2攻击+2精通+2充能  
行秋6命，精5祭礼剑，4绝缘/4宗室攻水暴，(9+11)双暴+2攻击+2精通+2充能  
砂糖6命，精5试作金珀，4风套精精精，4精通+6充能  

DPS：(20秒循环)  
0金 2.35w (砂糖换讨龙)  
0金 2.26w  

```text
kaeya char lvl=90/90 cons=2 talent=9,9,9;
kaeya add weapon="kagotsurubeisshin" refine=1 lvl=90/90;
kaeya add set="blizzardstrayer" count=4;
kaeya add stats hp=4780 atk=311 atk%=0.466 cryo%=0.466 cd=0.622;
kaeya add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.363 cd=0.594;

rosaria char lvl=90/90 cons=6 talent=9,9,9;
rosaria add weapon="favoniuslance" refine=5 lvl=90/90;
rosaria add set="noblesseoblige" count=4;
rosaria add stats hp=4780 atk=311 atk%=0.466 cryo%=0.466 cr=0.311;
rosaria add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

xingqiu char lvl=90/90 cons=6 talent=9,9,9;
xingqiu add weapon="sacrificialsword" refine=5 lvl=90/90;
xingqiu add set="emblemofseveredfate" count=4;
xingqiu add stats hp=4780 atk=311 atk%=0.466 hydro%=0.466 cr=0.311;
xingqiu add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

sucrose char lvl=90/90 cons=6 talent=9,9,9;
sucrose add weapon="prototypeamber" refine=5 lvl=90/90;
sucrose add set="viridescentvenerer" count=4;
sucrose add stats hp=4780 atk=311 em=187 em=187 em=187;
sucrose add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=80 cr=0 cd=0;

active xingqiu;
while 1 {
    xingqiu burst, attack;
    sucrose attack;
    if .sucrose.burst.ready {
        sucrose burst;
    }
    kaeya attack, skill, attack;
    rosaria skill, attack, burst;
    sucrose attack, skill, dash;
    kaeya attack, skill, burst, attack;
    xingqiu attack, skill, dash;
    if .xingqiu.skill.ready {
        xingqiu attack, skill, dash;
    }
    xingqiu attack:3;
    rosaria skill, attack;
    kaeya skill, attack;
    sucrose attack:4;
}
```

## 班尼特 香菱 北斗 菲谢尔

班尼特5命，精1原木刀，4宗室充火暴，(5+7)双暴+6生命+6充能  
香菱6命，精5渔获，4绝缘充火暴，(9+11)双暴+2攻击+2精通+2充能  
北斗6命，精5浪影阔剑，4绝缘充雷暴，(9+11)双暴+2攻击+2精通+2充能  
菲谢尔6命，精5绝弦，4剧团攻雷暴，(9+11)双暴+2攻击+2精通+2充能  

DPS：(20秒循环，菲谢尔固定时机尝试插入EQ)  
0金 3.52w  

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

beidou char lvl=90/90 cons=6 talent=9,9,9;
beidou add weapon="tidalshadow" refine=5 lvl=90/90;
beidou add set="emblemofseveredfate" count=4;
beidou add stats hp=4780 atk=311 er=0.518 electro%=0.466 cr=0.311;
beidou add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

fischl char lvl=90/90 cons=6 talent=9,9,9; 
fischl add weapon="stringless" refine=5 lvl=90/90;
fischl add set="goldentroupe" count=4;
fischl add stats hp=4780 atk=311 atk%=0.466 electro%=0.466 cr=0.311;
fischl add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

fn try_summon_oz_with_attack(){
    if .fischl.oz == 0 {
        if .fischl.skill.ready {
            fischl attack:2, skill;
        } else if .fischl.burst.ready {
            fischl burst, attack;
        }
    }
}

active bennett;
while 1 {
    bennett burst, skill;
    try_summon_oz_with_attack();
    xiangling attack, burst, attack, skill;
    beidou attack, skill, burst, attack;
    try_summon_oz_with_attack();
    bennett attack, skill;
    xiangling attack:3;
    try_summon_oz_with_attack();
    while !.bennett.skill.ready {
        bennett attack;
    }
    bennett skill;
    xiangling attack:3;
    try_summon_oz_with_attack();
    beidou skill[counter=2], attack:2;
}
```

## 珐露珊 鹿野院平藏 行秋 久岐忍

珐露珊6命，精5静谧之曲，4剧团充风暴，(12+8)双暴+4充能  
鹿野院平藏6命，精5流浪乐章，2风套2角斗攻风暴，(9+11)双暴+4攻击  
行秋6命，精5西风剑，4绝缘攻水暴，(9+11)双暴+6充能  
久岐忍6命，精5东花坊时雨，4千岩生生治，4精通+8生命  

DPS：  
0金 3.62w  

```text
faruzan char lvl=90/90 cons=6 talent=9,9,9;
faruzan add weapon="songofstillness" refine=5 lvl=90/90;
faruzan add set="goldentroupe" count=4;
faruzan add stats hp=4780 atk=311 er=0.518 anemo%=0.466 cr=0.311;
faruzan add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.22 em=0 cr=0.396 cd=0.528;

heizou char lvl=90/90 cons=6 talent=9,9,9;
heizou add weapon="thewidsith" refine=5 lvl=90/90;
heizou add set="viridescentvenerer" count=2;
heizou add set="gladiatorsfinale" count=2;
heizou add stats hp=4780 atk=311 atk%=0.466 anemo%=0.466 cr=0.311;
heizou add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0 em=0 cr=0.297 cd=0.726;

xingqiu char lvl=90/90 cons=6 talent=9,9,9;
xingqiu add weapon="favoniussword" refine=5 lvl=90/90;
xingqiu add set="emblemofseveredfate" count=4;
xingqiu add stats hp=4780 atk=311 atk%=0.466 hydro%=0.466 cr=0.311;
xingqiu add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.297 cd=0.726;

kuki char lvl=90/90 cons=6 talent=9,9,9;
kuki add weapon="toukaboushigure" refine=5 lvl=90/90;
kuki add set="tenacityofthemillelith" count=4;
kuki add stats hp=4780 atk=311 hp%=0.466 hp%=0.466 hp%=0.466;
kuki add stats hp=0 hp%=0.392 atk=0 atk%=0 def=0 def%=0 er=0 em=80 cr=0 cd=0;

active xingqiu;
while 1 {
    xingqiu burst, attack;
    kuki skill, dash, attack;
    faruzan burst, attack, skill;
    heizou burst, attack, charge, attack, skill;
    faruzan attack, aim, attack, aim, attack, skill;
    xingqiu attack, skill, dash;
    xingqiu attack:3;
    heizou attack, charge, attack:3, skill;
    faruzan attack, aim, attack, aim;
}
```

## 珐露珊 鹿野院平藏 琳妮特 莱依拉

珐露珊6命，精5静谧之曲，4剧团攻风暴，(12+8)双暴+4充能  
鹿野院平藏6命，精5试作金珀，4宗室攻风暴，(9+11)双暴+4攻击  
琳妮特6命，精5西风剑，2角斗2追忆攻风暴，(9+11)双暴+4攻击  
莱依拉6命，精5天目影打刀，4千岩生生生，4生命+10充能  
  
DPS：(24秒循环)  
0金 3.32w  

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
行秋6命，精5祭礼剑，4绝缘攻水暴，(9+11)双暴+2攻击+2精通+2充能  
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
xingqiu add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

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
行秋6命，精5祭礼剑，4绝缘攻水暴，(9+11)双暴+2攻击+2精通+2充能  
久岐忍6命，精5东花坊时雨，4乐园精精精，4精通+8生命  
菲谢尔6命，精5绝弦，4剧团攻雷暴，(9+11)双暴+2攻击+2精通+2充能  

DPS：(无轴循环)  
0金对单 4.59w (小体积怪，皇女抢种子)  
0金对单 5.78w (大体积怪，皇女不抢种子)  

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
xingqiu add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

kuki char lvl=90/90 cons=6 talent=9,9,9;
kuki add weapon="toukaboushigure" refine=5 lvl=90/90;
kuki add set="flowerofparadiselost" count=4;
kuki add stats hp=4780 atk=311 em=187 em=187 em=187;
kuki add stats hp=0 hp%=0.392 atk=0 atk%=0 def=0 def%=0 er=0 em=80 cr=0 cd=0;

fischl char lvl=90/90 cons=6 talent=9,9,9; 
fischl add weapon="stringless" refine=5 lvl=90/90;
fischl add set="goldentroupe" count=4;
fischl add stats hp=4780 atk=311 atk%=0.466 electro%=0.466 cr=0.311;
fischl add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

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

## 柯莱 芭芭拉 久岐忍 菲谢尔

柯莱6命，精5西风猎弓，4草套充草暴，(7+9)双爆+4攻击+4充能  
芭芭拉6命，精5祭礼残章/试作金珀，4海染生生治，4精通+6生命  
久岐忍6命，精5东花坊时雨，4乐园精精精，4精通+8生命  
菲谢尔6命，精5绝弦，4剧团攻雷暴，(9+11)双暴+2攻击+2精通+2充能  

DPS：(无轴循环)  
0金对单 3.48w (小体积怪，皇女抢种子)  
0金对单 4.51w (大体积怪，皇女不抢种子)  

```text
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

fischl char lvl=90/90 cons=6 talent=9,9,9; 
fischl add weapon="stringless" refine=5 lvl=90/90;
fischl add set="goldentroupe" count=4;
fischl add stats hp=4780 atk=311 atk%=0.466 electro%=0.466 cr=0.311;
fischl add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

active collei;
collei burst;
barbara attack, skill, jump;
kuki skill, dash;
fischl skill;
while 1 {

    if .fischl.oz == 0 {
        if .fischl.skill.ready {
            fischl skill, attack;
        } else if .fischl.burst.ready {
            fischl burst, attack;
        }
    }

    if .kuki.skill.ready {
        kuki skill;
    } else if .collei.skill.ready {
        collei skill, attack;
    } else if .collei.burst.ready {
        collei burst;
    } else if .barbara.skill.ready {
        barbara skill;
    } else {
        barbara attack:3, dash;
    }

}
```

## 瑶瑶 行秋 菲谢尔 砂糖

瑶瑶6命，精5西风长枪，4草套生生治，10暴击+6充能  
行秋6命，精5西风剑，4绝缘攻水暴，(9+11)双暴+6充能  
菲谢尔6命，精5绝弦，4剧团攻雷暴，(9+11)双暴+2攻击+2精通+2充能  
砂糖6命，精5祭礼残章，4风套精精精，4精通+6充能  

DPS：(无轴循环)  
0金 4.45w  

```text
yaoyao char lvl=90/90 cons=6 talent=9,9,9;
yaoyao add weapon="favoniuslance" refine=5 lvl=90/90;
yaoyao add set="deepwoodmemories" count=4;
yaoyao add stats hp=4780 atk=311 hp%=0.466 hp%=0.466 heal=0.359;
yaoyao add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.33 cd=0;

xingqiu char lvl=90/90 cons=6 talent=9,9,9;
xingqiu add weapon="favoniussword" refine=5 lvl=90/90;
xingqiu add set="emblemofseveredfate" count=4;
xingqiu add stats hp=4780 atk=311 atk%=0.466 hydro%=0.466 cr=0.311;
xingqiu add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.297 cd=0.726;

fischl char lvl=90/90 cons=6 talent=9,9,9; 
fischl add weapon="stringless" refine=5 lvl=90/90;
fischl add set="goldentroupe" count=4;
fischl add stats hp=4780 atk=311 atk%=0.466 electro%=0.466 cr=0.311;
fischl add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=40 cr=0.297 cd=0.726;

sucrose char lvl=90/90 cons=6 talent=9,9,9;
sucrose add weapon="sacrificialfragments" refine=5 lvl=90/90;
sucrose add set="viridescent" count=4;
sucrose add stats hp=4780 atk=311 em=187 em=187 em=187;
sucrose add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=80 cr=0 cd=0;

active xingqiu;
xingqiu burst, attack;
sucrose attack:2;
fischl skill, attack;
yaoyao skill;
sucrose attack, skill, dash, burst;
xingqiu attack, skill, dash, attack:3;
while 1 {

    if .fischl.oz == 0 {
        if .fischl.skill.ready {
            fischl attack, skill;
        } else if .fischl.burst.ready {
            fischl burst;
        }
    }

    if .xingqiu.burst.ready {
        xingqiu burst, attack;
    } else if .xingqiu.skill.ready {
        xingqiu attack, skill, dash, attack:3;
    } else if .yaoyao.skill.ready {
        yaoyao skill, attack;
    }  else if .sucrose.burst.ready {
        sucrose burst, attack;
    } else if .sucrose.skill.ready {
        sucrose attack, skill, dash;
    } else if .yaoyao.burst.ready {
        yaoyao burst, attack, dash, attack, dash, attack, dash, attack, dash;
    } else {
        sucrose attack:3, dash;
    }
}
```

## 瑶瑶 柯莱 行秋 托马

瑶瑶6命，精5西风长枪，4草套生生治，10暴击+6充能  
柯莱6命，精5西风猎弓，4草套充草暴，(7+9)双爆+4攻击+4充能  
行秋6命，精5西风剑，4绝缘攻水暴，(9+11)双暴+6充能  
托马6命，精5喜多院十文字，4乐园精精精，10充能  

DPS：(20秒循环)  
0金 3.66w  

```text
yaoyao char lvl=90/90 cons=6 talent=9,9,9;
yaoyao add weapon="favoniuslance" refine=5 lvl=90/90;
yaoyao add set="deepwoodmemories" count=4;
yaoyao add stats hp=4780 atk=311 hp%=0.466 hp%=0.466 heal=0.359;
yaoyao add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.33 cd=0;

collei char lvl=90/90 cons=6 talent=9,9,9;
collei add weapon="favoniuswarbow" refine=5 lvl=90/90;
collei add set="deepwoodmemories" count=4;
collei add stats hp=4780 atk=311 er=0.518 dendro%=0.466 cr=0.311;
collei add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0.22 em=0 cr=0.231 cd=0.594;

xingqiu char lvl=90/90 cons=6 talent=9,9,9;
xingqiu add weapon="favoniussword" refine=5 lvl=90/90;
xingqiu add set="emblemofseveredfate" count=4;
xingqiu add stats hp=4780 atk=311 atk%=0.466 hydro%=0.466 cr=0.311;
xingqiu add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.297 cd=0.726;

thoma char lvl=90/90 cons=6 talent=9,9,9;
thoma add weapon="kitaincrossspear" refine=5 lvl=90/90;
thoma add set="flowerofparadiselost" count=4;
thoma add stats hp=4780 atk=311 em=187 em=187 em=187;
thoma add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.55 em=0 cr=0 cd=0;

active yaoyao;
while 1 {
    yaoyao attack, skill, attack:2;
    xingqiu burst, attack, skill, dash, attack:3;
    thoma burst, attack, skill, attack:2;
    yaoyao burst, 
        attack:2, dash,
        attack:2, dash,
        attack:2, dash,
        attack:2;
    collei attack, skill, attack, burst;
    xingqiu attack:2, dash,
        attack:2, dash,
        attack:2;
    yaoyao attack:2, dash, attack;
}
```

## 草主 柯莱 芭芭拉 托马

草主6命，精5西风剑，4草套充草暴，(7+9)双爆+4攻击+4充能  
柯莱6命，精5西风猎弓，4草套充草暴，(7+9)双爆+4攻击+4充能  
芭芭拉6命，精5西风秘典，4海染生生暴，8暴击  
托马6命，精5喜多院十文字，4乐园精精精，10充能  

DPS：(20秒循环，芭芭拉站场平A时若E冷却完毕则释放)  
0金 2.41w  

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
barbara add weapon="favoniuscodex" refine=5 lvl=90/90;
barbara add set="oceanhuedclam" count=4;
barbara add stats hp=4780 atk=311 hp%=0.466 hp%=0.466 cr=0.311;
barbara add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0 em=0 cr=0.264 cd=0;

thoma char lvl=90/90 cons=6 talent=9,9,9;
thoma add weapon="kitaincrossspear" refine=5 lvl=90/90;
thoma add set="flowerofparadiselost" count=4;
thoma add stats hp=4780 atk=311 em=187 em=187 em=187;
thoma add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.55 em=0 cr=0 cd=0;

fn barbara_attack_with_try_skill() {
    if .barbara.skill.ready {
        barbara attack, skill, jump;
    } else {
        barbara attack:4;
    }
}

active travelerdendro;
while 1 {
    travelerdendro skill, burst;
    barbara_attack_with_try_skill();
    thoma burst, skill, attack:3;
    barbara_attack_with_try_skill();
    collei burst, attack;
    barbara_attack_with_try_skill();
    travelerdendro skill, attack;
    barbara_attack_with_try_skill();
    collei skill, attack;
    barbara_attack_with_try_skill();
    barbara_attack_with_try_skill();
    collei attack:2;
    travelerdendro attack:2;
}
```

## 柯莱 行秋 雷泽 班尼特(6)

柯莱6命，精5西风猎弓，4草套充草暴，(7+9)双爆+4攻击+4充能  
行秋6命，精5西风剑，4绝缘攻水暴，(9+11)双暴+6充能  
雷泽6命，精5饰铁之花，4乐园精精精，6精通+6充能  
班尼特6命，精5西风剑，4宗室充火暴，(5+7)双暴+6生命+6充能  

DPS：(21秒循环)  
0金 3.09w  

```text
collei char lvl=90/90 cons=6 talent=9,9,9;
collei add weapon="favoniuswarbow" refine=5 lvl=90/90;
collei add set="deepwoodmemories" count=4;
collei add stats hp=4780 atk=311 er=0.518 dendro%=0.466 cr=0.311;
collei add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0.22 em=0 cr=0.231 cd=0.594;

xingqiu char lvl=90/90 cons=6 talent=9,9,9;
xingqiu add weapon="favoniussword" refine=5 lvl=90/90;
xingqiu add set="emblemofseveredfate" count=4;
xingqiu add stats hp=4780 atk=311 atk%=0.466 hydro%=0.466 cr=0.311;
xingqiu add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.297 cd=0.726;

razor char lvl=90/90 cons=6 talent=9,9,9;
razor add weapon="mailedflower" refine=5 lvl=90/90;
razor add set="flowerofparadiselost" count=4;
razor add stats hp=4780 atk=311 em=187 em=187 em=187;
razor add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=120 cr=0 cd=0;

bennett char lvl=90/90 cons=6 talent=9,9,9;
bennett add weapon="favoniussword" refine=5 lvl=90/90;
bennett add set="noblesseoblige" count=4;
bennett add stats hp=4780 atk=311 er=0.518 pyro%=0.466 cr=0.311;
bennett add stats hp=0 hp%=0.294 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.165 cd=0.462;

active razor;
while 1 {
    razor skill, dash, attack;
    xingqiu burst, attack, skill, dash;
    collei skill, attack, burst;
    bennett attack, burst, skill;
    razor skill, dash, attack, burst,
        attack, skill, dash,
        attack:3, dash,
        attack:3, dash,
        attack:2, skill, dash,
        attack:3, dash,
        attack:3;
    bennett skill, attack:2;
}
```
