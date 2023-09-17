# gcsim队伍代码

只包含队伍与循环部分，场景设置请看gcsim模板一节

## 砂糖 北斗 菲谢尔 行秋

金箔风套三精通砂糖  
浪影绝缘攻雷暴北斗  
绝弦剧团攻雷暴菲谢尔  
祭礼绝缘攻水暴行秋  
  
DPS：  
0金对单 3.97w，对双，对三 2.87w，对四 2.59w

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

剧团(XX)攻风暴珐露珊  
宗室金珀攻风暴鹿野院平藏  
2角斗2追忆西风攻风暴琳妮特  
千岩天目三生命莱依拉  
  
DPS：  
0金试作 3.04w (无特效)  
0金绝弦 3.11w  
0金静谧 3.23w  
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
