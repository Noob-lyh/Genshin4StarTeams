# gcsim教程

## 1. gcsim使用流程

第一步：[从github下载gcsim](https://github.com/genshinsim/gcsim/releases)，点击最新版的Assets下的gcsim.exe即可保存，注意下载exe可能会导致浏览器警告，手动选择保留即可。（注：最新版似乎有自动更新功能，但还没试过）  

第二步：把gcsim.exe移动到工作文件夹中，当然下载的时候就可以指定。

第三步：在工作文件夹中创建文本文件run.txt，此文件内容如下（如果没有后缀名，请百度解决）。完成输入后将文件改名为run.bat，这样写完代码后双击此文件就可以开始模拟了。  

```text
cmd /k gcsim.exe -c="config.txt" -s="true"
```

第四步：在工作文件夹中创建文本文件config.txt用于保存模拟使用的代码。一般gcsim模拟代码包含四个部分：**模拟条件、敌人设置、角色面板和队伍手法**，接下来就依次介绍这四个部分。  

第五步：双击run.bat，开始模拟。  

## 2. 模拟条件

* 重复设置时新的会覆盖。  
* 本项目中所有模拟持续时间取90秒，即12层半间恰好及格的用时。相比于传统的4循环，这种方式能部分体现队伍的出伤速度（但是总体影响不大）。  

```text
options iteration=1000;     # 模拟次数
options duration=90;        # 每次模拟的持续时间（秒）
options workers=30;         # 并行模拟相关参数（可不管）
options swap_delay=4;       # 60帧下的切人延迟（帧）
```

## 2. 敌人设置

* 预设中一共添加了五个敌人，实际模拟时注释掉其中四个，只保留一个（一般使用第二个，其次第一个）。  
* 五个敌人中，第一个为前方大体积敌人（半径2.5，圆心离原点距离3），第二到五个为前/右/左/后方小体积敌人（半径0.5，圆心离原点距离1），另外角色半径为0.3，位置在原点。  
* 敌人统一使用100级，无限血量，10%全抗性，使用通用掉球设置（每随机480到720帧，即每随机6到12秒，掉落一个1能量的白色微粒）  

```text
#target lvl=100 pos=0,3 radius=2.5 pyro=0.1 dendro=0.1 hydro=0.1 electro=0.1 geo=0.1 anemo=0.1 physical=0.1 cryo=0.1;
target lvl=100 pos=0,1 radius=0.5 pyro=0.1 dendro=0.1 hydro=0.1 electro=0.1 geo=0.1 anemo=0.1 physical=0.1 cryo=0.1;
#target lvl=100 pos=1,0 radius=0.5 pyro=0.1 dendro=0.1 hydro=0.1 electro=0.1 geo=0.1 anemo=0.1 physical=0.1 cryo=0.1;
#target lvl=100 pos=-1,0 radius=0.5 pyro=0.1 dendro=0.1 hydro=0.1 electro=0.1 geo=0.1 anemo=0.1 physical=0.1 cryo=0.1;
#target lvl=100 pos=0,-1 radius=0.5 pyro=0.1 dendro=0.1 hydro=0.1 electro=0.1 geo=0.1 anemo=0.1 physical=0.1 cryo=0.1;
energy every interval=480,720 amount=1;     
```

## 3. 角色面板  

建议复制模板然后进行修改，以班尼特为例：  

```text
bennett char lvl=90/90 cons=6 talent=9,9,9;
bennett add weapon="sapwoodblade" refine=5 lvl=90/90;
bennett add set="noblesseoblige" count=4;
bennett add stats hp=4780 atk=311 er=0.518 pyro%=0.466 cr=0.311;
bennett add stats hp=0 hp%=0.294 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.165 cd=0.462;
```

第一到第五行包含的信息分别为：  
等级90，命座6，天赋999  
武器原木刀，精炼5，等级90  
套装宗室4  
增加圣遗物属性：4780生命（花主词条），311攻击（羽主词条），51.8%充能（沙主词条），46.6%火伤（杯主词条），31.1%暴击（头主词条）  
增加圣遗物属性：29.4%生命，33%充能，16.5%暴击，46.2%爆伤（均为副词条）  

按照此模板编写其他角色面板即可，需要对应英语时可以查阅gcsim_dictionary.md  

## 4. 队伍手法

手法的设置多种多样，本文档中主要使用两种：固定长度循环与无轴循环。在设置具体角色行动前，需要使用如下代码，指定起手角色：  

```text
active chA;
```

对于固定长度循环而言，通常使用如下while死循环的方式，当然也可以用for循环指定循环次数：

```text
while 1 {
    chA xxx;
    chB xxx;
    chC xxx;
    chD xxx;
}
```

对于无轴循环，通常使用固定起手式 + while死循环优先选择的方式：

```text
chA xxx;
chB xxx;
chC xxx;
chD xxx;
while 1 {
    if .chA.xxx.ready {
        chA xxx;
    } else if .chB.xxx.ready {
        chB xxx;
    } else if ... {
        ...
    } else {
        ...
    }
}
```

一个固定长度循环的例子是香菱班尼特重云罗莎莉亚（双冰双火）。起手角色为重云，循环手法为“重云E，班尼特QE，罗莎莉亚EAQ，香菱AQE，罗莎莉亚E，班尼特E，香菱AA，重云Q，罗莎莉亚AE，班尼特E，香菱AA”，代码可写为：  

```text
active chongyun;
while 1 {
    chongyun skill;
    bennett burst, skill;
    rosaria skill, attack, burst;
    xiangling attack, burst, skill;
    rosaria skill;
    bennett skill;
    xiangling attack:2;
    chongyun burst;
    rosaria attack, skill;
    bennett skill;
    xiangling attack:2;
}
```

一个无轴循环的例子为草主柯莱行秋久岐忍（行秋双草超绽），起手为草主EQ，行秋QA，久岐忍E闪A，柯莱EA，行秋EA闪EA闪，草主E，此后哪里亮了点哪里，优先级为久岐忍E>行秋Q>草主E>柯莱E>草主Q>柯莱Q>行秋E，如果以上技能都未就绪，则久岐忍站场平A。  

```text
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

实际手法可能更加复杂，例如烟绯蒸发队中烟绯只有奇数轮放Q，因此while循环中的长度为正常的两倍，包括一次烟绯放Q的循环和一次烟绯不放Q的循环；例如队伍中有皇女的情况，找时间放奥兹相当麻烦；例如某些手法精度要求较高的队伍，如砂国，需要大量使用设置角色位置、等待若干帧后行动的代码。  
