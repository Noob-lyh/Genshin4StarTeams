# gcsim_tutorial_cn

## 模板

只展示常用功能，详见：<https://docs.gcsim.app/guides/>

```text
# simulation time
options iteration=1000 duration=90 swap_delay=4;

# enemy setting
target lvl=100 resist=0.1 particle_threshold=250000 particle_drop_count=1;

# character
CH char lvl=90/90 cons=0 talent=10,10,10;
CH add weapon="" refine=1 lvl=90/90;
CH add set="" count=4;
CH add stats hp=4780 atk=311 [??] [pyro%=0.466] [cr=0.311];
CH add stats hp= hp%= atk= atk%= def= def%= er= em= cr= cd=;

# starting character
active CH;

# rotation
while 1 {
 [rotation]
}
```

## 词典

详见：<https://docs.gcsim.app/reference>  

### 元素及角色

部分角色名为简称/多种可用名称之一，程序中用全小写即可

```text
火(Pyro)：安柏(Amber)，班尼特(Bennett)，迪希雅(Dehya)，迪卢克(Diluc)，胡桃(Hutao)，可莉(Klee)，林尼(Lyney)，托马(Thoma)，香菱(Xiangling)，辛焱(Xinyan)，烟绯(Yanfei)，宵宫(Yoimiya)

水(Hydro)：神里绫人(Ayato)，芭芭拉(Barbara)，坎蒂丝(Candace)，珊瑚宫心海(Kokomi)，莫娜(Mona)，妮露(Nilou)，达达利亚(Tartaglia)，行秋(Xingqiu)，夜兰(Yelan)

雷(Electro)：北斗(Beidou)，赛诺(Cyno)，多莉(Dori)，菲谢尔(Fischl)，刻晴(Keqing)，久岐忍(Kuki)，丽莎(Lisa)，雷电将军(Raiden)，雷泽(Razor)，九条裟罗(Sara)，八重神子(Yae)

冰(Cyro)：俄洛伊(Aloy)，神里绫华(Ayaka)，重云(Chongyun)，迪奥娜(Diana)，优菈(Eula)，甘雨(Ganyu)，凯亚(Kaeya)，莱依拉(Layla)，米卡(Mika)，七七(Qiqi)，罗莎莉亚(Rosaria)，申鹤(Shenhe)

风(Anemo)：珐露珊(Faruzan)，鹿野院平藏(Heizou)，琴(Jean)，万叶(Kazuha)，琳妮特(Lynette)，早柚(Sayu)，砂糖(Sucrose)，温迪(Venti)，流浪者(Wanderer)，魈(Xiao)

岩(Geo)：阿贝多(Albedo)，五郎(Gorou)，荒泷一斗(itto)，凝光(Ningguang)，诺艾尔(Noelle)，云堇(YunJin)，钟离(Zhongli)

草(Dendro)：艾尔海森(Alhaitham)，白术(Baizhu)，柯莱(Collei)，卡维(Kaveh)，绮良良(Kirara)，纳西妲(Nahida)，提纳里(Tighnari)，瑶瑶(YaoYao)

旅行者：traveler/aethor/lumine + 元素名称，例如风荧(lumineanemo)

物理(Phys)，通用伤害加成(dmg%)
```

### 武器

```text
// 五星
单手剑：
双手剑：
长柄武器：
弓：
法器：

// 四星
单手剑：
双手剑：
长柄武器：
弓：静谧之曲(songofstillness)
法器：

// 三星
单手剑：
双手剑：
长柄武器：
弓：
法器：

// 二星、一星
单手剑：
双手剑：
长柄武器：
弓：
法器：
```

### 圣遗物

```text

```

### 其他游戏名词

```text
等级(lvl)，命座(cons)，精炼(refine)，天赋(talent)

小生命/小攻击/小防御(hp/def/atk)
大生命/大攻击/大防御(hp%/def%/atk%)
元素精通(em)，元素充能效率(er)，
暴击率(cr)，暴击伤害(cd)，
火元素伤害加成(pyro%)，其他伤害加成同理，见元素及角色一节
治疗加成(heal)
攻速加成(atkspd%)
注：所有百分比的数据均转化为小数

普攻(attack)，普攻n次(attack:n)
重击(charge)，瞄准射击(aim)
低空下落攻击(low_plunge)，高空下落攻击(high_plunge)
冲刺(dash)，跳跃(jump)，步行(walk)，等待(wait)
元素战技(skill)
元素爆发(burst)
切人(swap)
```
