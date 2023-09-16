# gcsim_configs

## 角色标准面板

标注输出打法的，一般取20词条双暴+少量攻击力/精通/充能等  
标注工具人打法的，词条相应降低

### 珐露珊

```text
# 站场输出，六命，精五静谧之曲，战技套攻风暴，(12+8)双暴+4充能
faruzan char lvl=90/90 cons=6 talent=9,13,13;
faruzan add weapon="songofstillness" refine=5 lvl=90/90;
faruzan add set="goldentroupe" count=4;
faruzan add stats hp=4780 atk=311 atk%=0.466 anemo%=0.466 cr=0.311;
faruzan add stats hp=0 hp%=0 atk=0 atk%=0 def=0 def%=0 er=0.22 em=0 cr=0.396 cd=0.528;
```

### 鹿野院平藏

```text
# 工具人速切，一命，精五试作金珀，宗室套攻风暴，(5+5)双暴+4攻击
Heizou char lvl=81/90 cons=1 talent=6,8,8;
Heizou add weapon="prototypeamber" refine=5 lvl=80/90;
Heizou add set="noblesseoblige" count=4;
Heizou add stats hp=4780 atk=311 atk%=0.466 anemo%=0.466 cr=0.311;
Heizou add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0 em=0 cr=0.165 cd=0.33;
```

### 琳妮特

```text
# 珐鹿琳莱队工具人，零命，精1西风剑，绝缘充攻暴，(5+5)双暴+4攻击
Lynette char lvl=81/90 cons=0 talent=6,8,8;
Lynette add weapon="favoniussword" refine=1 lvl=80/90;
Lynette add set="emblemofseveredfate" count=4;
Lynette add stats hp=4780 atk=311 er=0.518 atk%=0.466 cr=0.311;
Lynette add stats hp=0 hp%=0 atk=0 atk%=0.196 def=0 def%=0 er=0 em=0 cr=0.165 cd=0.33;
```

### 莱伊拉

```text
# 珐鹿琳莱队工具人，二命，精5天目影打刀，千岩生生生，4生命+8充能
```

## 队伍模拟代码

```text
options iteration=1000 duration=90 swap_delay=4;
target lvl=100 resist=0.1 particle_threshold=250000 particle_drop_count=1;

active CH;

while 1 {
 [rotation]
}
```
