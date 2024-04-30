# gcsim教程

最后更新：2024年4月13日  

本教程主要由[gcsim官方文档（英文）](https://docs.gcsim.app/)翻译而来，经过部分修改和排编写成，目的是方便中文用户更加快速地掌握gcsim使用。本教程会忽略官方文档中部分详细内容，如有需要可以查阅官方文档。  

如果你想查阅所有别人上传的队伍模拟，可以到[gcsim数据库](https://simpact.app/database)查看。注意数据库中的DPS会因不同的标准、优化程度以及对游戏性能的合理应用而有所不同，gcsim也鼓励使用者对数据库中已有代码进行修改。  

## 简介

根据官方文档，gcsim是原神的队伍DPS计算/战斗模拟工具。gcsim根据用户输入的任意给定队伍模拟战斗，并计算该队伍造成的总伤害，以及许多其他有用的统计数据，包括：  

* 按角色划分的总体伤害分布
* 按技能对每个角色进行详细的伤害分布
* 能量循环
* 反应计数
* 伤害类型

## 使用哲学

关于gcsim的意义、用途，有很多不同的观点。gcsim数据库中官方给出的观点是：“gcsim的存在并不只是为了得到标准化的理论平均DPS。用户完全可以输入他们认为有用的内容。所以，不要再盲目比较配置的DPS了。你做错了”。  

我的观点是：gcsim主要是用于提供同一标准下各队伍DPS参考的，这也是四星队综述做的事情。由于是同一标准，必然只能选择更加通用的标准，例如理想状态对单打桩，因而无法反映对群能力、对手法的要求、操作难度、容错率等复杂因素，这也使得过分追求gcsim的高DPS或准确DPS没有意义。总之，gcsim的DPS结果只能是一个参考，如果要提供一个队伍的攻略，还需要文字信息、心得分享以及实战视频等，这同样是四星队综述在做的事情。  

当然你也可以有自己的观点。不过无论如何，建议不要将用gcsim捏出高DPS当做学习使用gcsim的最终目标。  

## 准备工作

通常，直接使用[gcsim网页版](https://gcsim.app/simulator)就可以了。网页版支持直接导入你的角色面板，但是模拟运行速度很慢。如果你是重度用户，需要大量运行模拟，那么建议按照如下过程安装gcsim客户端。  

1. 创建工作文件夹，如`D:/gcsim`
2. 从github下载gcsim的发布版，[下载链接](https://github.com/genshinsim/gcsim/releases)。需要下载的文件可以在最新版本(标有带绿色框的Latest)的Assets中找到。注意：
   * Assets中一共有11个文件，包含4种架构的gcsim可执行文件`gcsim_*`以及gcsim服务器可执行文件`server_*`、gcsim源代码`Source code(zip/tar.gz)`以及证书`LICENSE`
   * 对于windows用户，下载`gcsim_windows_amd64.exe`并保存在之前创建的工作文件夹中即可。下载exe文件可能会导致警告，需要手动操作防止被系统误删  
3. 在工作文件夹中创建文本文件`config.txt`，用于编写模拟使用的代码。
4. 在工作文件夹中创建文本文件`run.txt`，内容为`cmd /k gcsim.exe -c="config.txt" -s="true"`
5. 将`run.txt`改名为`run.bat`，这样写完代码后双击此文件就可以开始模拟了。这两步需要系统设置显示文件后缀名，相关问题请百度解决

到此为止，无论是网页版还是客户端，你已经完成了模拟的准备工作，可以开始编写你的第一份模拟代码了。  

一般而言，gcsim模拟代码可以分为两个部分：**环境**和**队伍**。前者设置模拟相关的参数，如模拟次数和时间、敌人配置、打桩环境等；后者则设置队伍自身参数，包括角色面板和手法。在进行多个队伍模拟比较时，通常保持**环境**部分不变，只改变**队伍**部分。  

接下来就简单介绍这两个部分。  

## 第一部分：环境

首先是**gcsim模拟参数**。这部分以options开头，后面跟上设置项名称和数值，例如：  

```text
options iteration=1000;     # 模拟次数1000
options duration=90;        # 每次模拟持续90秒
options swap_delay=4;       # 切人延迟，填写4时约等于30ms的ping
```

然后设置**目标参数**。要新增一个目标时，以`target`为首新建一行，后面跟上这个敌人的参数，例如：  

```text
target lvl=100 hp=100000000 pos=0,1 radius=0.5 resist=0.1;
```

这一行设置了一个等级(lvl)为100，生命值(hp)为100000000即1亿血，中心位置(pos)在(0,1)处，半径(radius)为0.5，所有抗性(七种元素+物理)均为0.1的目标。注意：

* 生命值(hp)可以不指定，此时敌人视为无限血。当所有敌人都被击败，模拟会提前结束
* 角色的默认中心位置为(0,0)，半径为0.3。注意gcsim中没有模型重叠限制。不同的位置关系、半径可能会导致不同的模拟结果

一般而言，gcsim模拟总是使用100级、0.1全抗、血量极高或无限不会导致模拟提前结束的敌人。其他参数（包括敌人数量）一般没有统一规定，如果队伍对这些参数有要求（如多怪、大体积怪等），建议在发布gcsim模拟时说明。  

最后是**环境掉球**，通常如下设置：  

```text
energy every interval=480,720 amount=1;
```

在这个设置中，每随机480到720帧，即每随机8~12秒，平均每随机10秒，环境掉落1个元素微粒。这是gcsim数据库中大部分模拟以及四星队综述使用的设置，也是通用设置。  

## 第二部分：队伍

一般而言队伍中包含4个角色，因此我们首先需要**每个角色的完整面板**。  

如果你希望导入自己的角色，可以参考官方文档中的教程：[导入你自己的角色面板](https://docs.gcsim.app/guides/importing_characters)。  

如果你希望用某种标准得到一个DPS参考，那么这个过程会稍微有点麻烦。通常的做法是复制已有代码中的设置然后进行修改。例如四星队综述中班尼特的一种标准面板如下：  

```text
bennett char lvl=90/90 cons=6 talent=9,9,9;
bennett add weapon="sapwoodblade" refine=1 lvl=90/90;
bennett add set="noblesseoblige" count=4;
bennett add stats hp=4780 atk=311 er=0.518 pyro%=0.466 cr=0.311;
bennett add stats hp=0 hp%=0.294 atk=0 atk%=0 def=0 def%=0 er=0.33 em=0 cr=0.165 cd=0.462;
```

一般一个角色的标准面板为5行或6行，每一行均以该角色名称为首，后续加`char`表示本行设置角色自身参数，加`add`表示本行角色非自身的参数，这两个词建议不要修改。在上述例子中：  

```text
第一行：人物等级90（上限90），命座6，普攻9级，战技9级，爆发9级
第二行：武器原木刀，精炼1，等级90（上限90）
第三行：圣遗物套装：宗室4（如果是2+2，那么这部分需要两行分别描述两个套装）
第四行：圣遗物主词条：4780生命，311攻击，51.8%充能，46.6%火伤，31.1%暴击
第五行：圣遗物副词条：29.4%生命，33%充能，16.5%暴击，46.2%爆伤
```

你可以根据自己的需要修改上述模板中的部分参数。需要注意目前gcsim只能使用英文名称，中英对照可以参考本项目中的`gcsim_dictionary.md`文件。各词条具体值可以参考`附录：标准面板参考`。  

在像上面一样完成所有角色面板设置后，就可以编写**队伍手法**了。  

手法的设置多种多样，这里只介绍最基本的方式。以雷国为例，一种简单的手法是：雷神E，行秋EQ，班尼特EQ，香菱QE，雷神QA至结束，然后开始下一个循环。为了描述这样的循环，首先用active指定起手角色为雷神：  

```text
active raiden;
```

然后，用一个while死循环来实现手法的“循环”，其中“#”号后面的为注释：  

```text
while 1 {
    raiden skill;           # 雷神E
    xingqiu skill, burst;   # 行秋EQ
    bennett skill, burst;   # 班尼特EQ
    xiangling burst, skill; # 香菱QE
    raiden burst;           # 雷神Q
    raiden attack:15;       # 雷神15次A，即完整3套平A
}
```

好，现在你已经知道gcsim模拟代码的两个部分怎么写了，接下来把它们组装到一起，就可以完成你的第一次模拟了！  

## 第一次gcsim模拟

确定最终所有角色面板如下：  

雷电将军0命，天赋999，精5西风长枪，4绝缘充雷暴，(9+11)双暴+2攻击+2精通+2充能  
班尼特6命，天赋999，精1原木刀，4宗室充火暴，(5+7)双暴+6生命+6充能  
香菱6命，天赋999，精5渔获，4绝缘充火暴，(9+11)双暴+2攻击+2精通+2充能  
行秋6命，天赋999，精5西风剑，4绝缘攻水暴，(9+11)双暴+6充能  

现在可以组装你的代码了！

```text

```

## 附录：进阶环境设置

`iteration`：计算最终DPS时模拟次数一般取1000，在调试阶段为了减少运行时间可以减少模拟次数，如100次。

`duration`：在gcsim数据库中，一般不设置模拟持续时间，而是让队伍完整执行四个循环，模拟将会在最后一个动作完成时自动结束。而在四星队综述中，所有模拟持续时间取90秒，即12层半间恰好及格的用时。两种设置方式下最终DPS会有轻微不同，不过一般可以忽略。  

`swap_delay`：在gcsim数据库中，一般取12，即模拟ping约90ms下的切人延迟。四星队综述中取4。同样对DPS的轻微影响一般可忽略，不过需要注意较高的切人延迟可能使得某些比较极限的操作无法实现。  

## 附录：面板标准参考

这里只考虑5星圣遗物，注意所有数字为实际值，例如46.6%大攻击为atk%=0.466。  

主词条的值：  

```text
hp=4780         # 花
atk=311         # 羽
hp%=0.466       # 沙/杯/头
atk%=0.466      # 沙/杯/头
def%=0.583      # 沙/杯/头
em=187          # 沙/杯/头
er=0.518        # 沙
pyro%/hydro%/electro%/cryo%/anemo%/geo%/dendro%=0.466   # 杯
phys%=0.583                                             # 杯
cr=0.311        # 头
cd=0.622        # 头
heal=0.359      # 头
```

然后是8种副词条的值：

```text
hp%=0.0496      # 1条大生命 = 4.96%生命
hp=253.96       # 1条小生命 = 253.96生命
atk%=0.0496     # 1条大攻击 = 4.96%攻击
atk=16.54       # 1条小攻击 = 16.54攻击
def%=0.0620     # 1条大防御 = 6.2%防御
def=19.68       # 1条小防御 = 19.68防御
cr=0.0331       # 1条暴击 = 3.31%暴击
cd=0.0662       # 1条爆伤 = 6.62%爆伤
er=0.0551       # 1条充能 = 5.51%充能
em=19.82        # 1条精通 = 19.82精通
```

## 附录：进阶手法实现

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
