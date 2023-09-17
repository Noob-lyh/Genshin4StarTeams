# gcsim角色面板示例

均为在队伍代码中使用的配置，每个配置前的备注会指明用于哪个队伍中  
默认6命90级角色+精5四星90级武器，天赋9/9/9(计算命座前)，输出角色一般取20词条双暴+少量其他有效词条

## 行秋

```text
# 砂糖武装-输出，6命，精5祭礼剑，绝缘套攻水暴，(9+11)双暴+2攻击+2充能
xingqiu char lvl=90/90 cons=6 talent=9,9,9;
xingqiu add weapon="sacrificialsword" refine=5 lvl=90/90;
xingqiu add set="emblemofseveredfate" count=4;
xingqiu add stats hp=4780 atk=311 atk%=0.466 hydro%=0.466 cr=0.311;
xingqiu add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=0 cr=0.297 cd=0.726;
```

## 菲谢尔

```text
# 砂糖武装-输出，6命，精5绝弦，战技套攻雷暴，(9+11)双暴+2攻击+2充能
fischl char lvl=90/90 cons=6 talent=9,9,9; 
fischl add weapon="stringless" refine=5 lvl=90/90;
fischl add set="goldentroupe" count=4;
fischl add stats hp=4780 atk=311 atk%=0.466 electro%=0.466 cr=0.311;
fischl add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=0 cr=0.297 cd=0.726;
```

## 北斗

```text
# 砂糖武装-输出，6命，精5浪影阔剑，绝缘充雷暴，(9+11)双暴+2攻击+2充能
beidou char lvl=90/90 cons=6 talent=9,9,9;
beidou add weapon="finaleofthedeep" refine=5 lvl=90/90;
beidou add set="emblemofseveredfate" count=4;
beidou add stats hp=4780 atk=311 er=0.518 electro%=0.466 cr=0.311;
beidou add stats hp=0 hp%=0 atk=0 atk%=0.098 def=0 def%=0 er=0.11 em=0 cr=0.297 cd=0.726;
```

## 莱伊拉

```text
# 珐鹿琳莱-千岩挂冰盾辅，6命，精5天目影打刀，千岩生生生，4生命+10充能
layla char lvl=90/90 cons=6 talent=9,9,9;
layla add weapon="amenomakageuchi" refine=5 lvl=90/90;
layla add set="tenacityofthemillelith" count=4;
layla add stats hp=4780 atk=311 hp%=0.466 hp%=0.466 hp%=0.466;
layla add stats hp=0 hp%=0.196 atk=0 atk%=0 def=0 def%=0 er=0.55 em=0 cr=0 cd=0;
```

## 砂糖

```text
# 砂糖武装-驾驶员，6命，精5试作金珀，风套三精通，4精通+6充能
sucrose char lvl=90/90 cons=6 talent=9,9,9;
sucrose add weapon="prototypeamber" refine=5 lvl=90/90;
sucrose add set="viridescent" count=4;
sucrose add stats hp=4780 atk=311 em=187 em=187 em=187;
sucrose add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.33 em=80 cr=0 cd=0;
```

## 鹿野院平藏

```text
# 珐鹿琳莱-速切治疗，6命，精5试作金珀，宗室套攻风暴，(9+11)双暴+4攻击
heizou char lvl=90/90 cons=6 talent=9,9,9;
heizou add weapon="prototypeamber" refine=5 lvl=90/90;
heizou add set="noblesseoblige" count=4;
heizou add stats hp=4780 atk=311 atk%=0.466 anemo%=0.466 cr=0.311;
heizou add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0 em=0 cr=0.297 cd=0.726;
```

## 珐露珊

```text
# 珐鹿琳莱-站场输出，6命，精5静谧之曲，战技套攻风暴，(12+8)双暴+4充能
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
