# gcsim角色面板示例

均为在队伍代码中使用的配置，每个配置前的备注会指明用于哪个队伍中  
默认6命90级角色+精5四星90级武器，天赋9/9/9(计算命座前)，输出角色一般取20词条双暴+少量其他有效词条

## 珐露珊

```text
# 珐鹿琳莱-站场输出，6命，精5静谧之曲，战技套攻风暴，(12+8)双暴+4充能
faruzan char lvl=90/90 cons=6 talent=9,9,9;
faruzan add weapon="songofstillness" refine=5 lvl=90/90;
faruzan add set="goldentroupe" count=4;
faruzan add stats hp=4780 atk=311 atk%=0.466 anemo%=0.466 cr=0.311;
faruzan add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.22 em=0 cr=0.396 cd=0.528;
```

## 鹿野院平藏

```text
# 珐鹿琳莱-速切治疗，6命，精5试作金珀，宗室套攻风暴，(10+10)双暴+4攻击
heizou char lvl=90/90 cons=6 talent=9,9,9;
heizou add weapon="prototypeamber" refine=5 lvl=90/90;
heizou add set="noblesseoblige" count=4;
heizou add stats hp=4780 atk=311 atk%=0.466 anemo%=0.466 cr=0.311;
heizou add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0 em=0 cr=0.33 cd=0.66;
```

## 琳妮特

```text
# 珐鹿琳莱-嘲讽副C，6命，精5西风剑，绝缘充攻暴，(10+10)双暴+4攻击
lynette char lvl=90/90 cons=6 talent=9,9,9;
lynette add weapon="favoniussword" refine=1 lvl=90/90;
lynette add set="emblemofseveredfate" count=4;
lynette add stats hp=4780 atk=311 er=0.518 atk%=0.466 cr=0.311;
lynette add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0 em=0 cr=0.33 cd=0.66;
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
