# gcsim模板

## 模拟条件与敌人属性设置

```text
# conditions
options iteration=100;
options duration=90;
options swap_delay=4;
options workers=30;

# enemies
target lvl=100 pos=0,1 radius=0.5 pyro=0.1 dendro=0.1 hydro=0.1 electro=0.1 geo=0.1 anemo=0.1 physical=0.1 cryo=0.1;
# target lvl=100 pos=1,0 radius=0.5 pyro=0.1 dendro=0.1 hydro=0.1 electro=0.1 geo=0.1 anemo=0.1 physical=0.1 cryo=0.1;
# target lvl=100 pos=-1,0 radius=0.5 pyro=0.1 dendro=0.1 hydro=0.1 electro=0.1 geo=0.1 anemo=0.1 physical=0.1 cryo=0.1;
# target lvl=100 pos=0,-1 radius=0.5 pyro=0.1 dendro=0.1 hydro=0.1 electro=0.1 geo=0.1 anemo=0.1 physical=0.1 cryo=0.1;
energy every interval=480,720 amount=1;
```

## 队伍循环设置示例

```text
active nahida;
while 1 {
 switch 1{
    case .nahida.skill.ready && .nahida.swap.ready && .debuff.res.t0.nahida-e == 0:
        nahida skill;
    case .nahida.burst.ready && .nahida.swap.ready && .status.nahida-q < 180 &&
            .xingqiu.status.xingqiuburst == 0 && .yelan.status.yelanburst == 0:
        nahida burst;
    case .xingqiu.burst.ready && .xingqiu.swap.ready && .status.nahida-q > 300:
        xingqiu burst, attack;
        if .kuki.burst.ready {
            kuki swap;
        } else {
            yelan swap;
        }
    case .kuki.burst.ready && .kuki.swap.ready:
        kuki burst;
        if .xingqiu.status.xingqiuburst > 0 || .yelan.status.yelanburst > 0{
            kuki attack;
        }
    case .xingqiu.status.xingqiuburst > 0 && .xingqiu.status.xingqiuburst < 600
            && .xingqiu.skill.ready && .xingqiu.swap.ready:
        if .nahida.onfield {
            nahida charge;
        }
        xingqiu attack, skill, dash, attack:2;
    case .yelan.burst.ready && .yelan.swap.ready &&
            .xingqiu.status.xingqiuburst > 0 && .status.nahida-q > 300:
        yelan burst, attack;
    case .yelan.skill.ready && .yelan.swap.ready:
        yelan skill, attack:4;
    case .kuki.skill.ready && .kuki.swap.ready:
        if .nahida.onfield {
            nahida charge;
        }
        kuki skill, dash;
        if .xingqiu.status.xingqiuburst > 0 || .yelan.status.yelanburst > 0{
            kuki attack;
        }
    case .kuki.onfield && !.kuki.swap.ready:
        kuki attack;
    case .xingqiu.onfield && !.xingqiu.swap.ready:
        xingqiu attack;
    case .yelan.onfield && !.yelan.swap.ready:
        yelan attack;
    case .nahida.onfield:
        if .nahida.normal > 3 {
            nahida dash;
        } else if .nahida.skill.ready && .nahida.normal > 2 {
            nahida skill;
        } else {
            nahida attack;
        }
    default:
        nahida attack;
 }
}
```
