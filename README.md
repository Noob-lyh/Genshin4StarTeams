# Genshin4StarTeams

* **README.md（简介/本文档）**：原神纯四星队伍综述项目简介。包含**0金队伍DPS排行榜**、纯四星队伍整体简介、配队评价标准、以及四星角色在0金队中的强度评级。  

* **teams.md（正文）**：尽可能收集原神纯四星角色的配队，每个配队包含简介、评分、手法参考、视频参考、gcsim模拟的DPS参考等。  

* **gcsim_settings.md（模拟设置与角色面板参考）**：gcsim模拟的环境及敌人设置，以及gcsim四星角色标准练度参考面板。  

* **gcsim_dictionary.md（词典与手册）**：gcsim中各游戏名词的中文翻译，如果你有编写gcsim代码的需求可以查阅。  

## 一、纯四星0金配队对单DPS排行榜（施工中）  

注1：角色90级满命（班尼特及御三家除外）天赋999（计算命座前），武器90级精5（不使用限定或月卡武器），副词条标准为20+2n（20条双爆，每种有效词条一般各2条，特殊情况可只取4~6条的某种有效词条），模拟的环境设置参考gcsim_teams.md  
注2：经典低金配队DPS参考：雷国/草行久带空气，1金 5w+  

1. 【种门】柯莱 行秋 久岐忍 菲谢尔（行秋双雷超绽-不抢种/抢种），5.78w/4.59w
2. 【增幅】班尼特 香菱 行秋 砂糖（砂糖国家队-6班），5.58w
3. 【增幅】班尼特 香菱 行秋 菲谢尔（皇女国家队），5.14w
4. 【种门】草主 柯莱 行秋 久岐忍（行秋双草超绽），5.12w
5. 【种门】柯莱 芭芭拉 久岐忍 菲谢尔（芭芭拉双雷超绽-不抢种/抢种），4.51w/3.48w
6. 【种门】瑶瑶 行秋 菲谢尔 砂糖（行秋带风超绽/砂糖激绽），4.45w
7. 【激化】砂糖 丽莎 菲谢尔 瑶瑶（砂糖激化-丽莎），4.67w
8. 【种门】草主 柯莱 芭芭拉 久岐忍（芭芭拉双草超绽），4.12w
9. 【增幅】班尼特 香菱 行秋 重云（重云国家队），3.94w
10. 【直伤】砂糖 北斗 菲谢尔 行秋（砂糖武装），3.93w
11. 【激化】砂糖 北斗 菲谢尔 瑶瑶（砂糖激化-北斗），3.90w
12. 【直伤】班尼特 香菱 珐露珊 鹿野院平藏（双风双火），3.69w
13. 【种门】瑶瑶 柯莱 行秋 托马（行秋双草烈绽），3.66w
14. 【增幅】班尼特 香菱 罗莎莉亚 砂糖（融罗），3.62w
15. 【直伤】珐露珊 鹿野院平藏 行秋 久岐忍（珐鹿感电），3.62w
16. 【增幅】班尼特 香菱 重云 罗莎莉亚（双冰双火-重罗），3.60w
17. 【直伤】班尼特 香菱 北斗 菲谢尔（双雷双火），3.52w
18. 【增幅】班尼特 香菱 凯亚 罗莎莉亚（双冰双火-凯罗），3.45w
19. 【直伤】珐露珊 鹿野院平藏 琳妮特 莱依拉（新四星三风），3.32w
20. 【种门】柯莱 行秋 雷泽 班尼特(6)（彩虹雷泽），3.09w
21. 【直伤】琳妮特 北斗 菲谢尔 芭芭拉（琳芭武装），3.06w
22. 【种门】草主 柯莱 芭芭拉 托马（芭芭拉双草烈绽），2.41w
23. 【直伤】凯亚 罗莎莉亚 行秋 砂糖（凯亚永冻-讨龙/金珀），2.35w/2.26w 

## 二、纯四星配队简介

声明：作者入坑版本为2.8，对于之前四星队的发展均为查找相关视频得到，可能因为幸存者偏差而不准确，欢迎指正。  

在1.0~1.6时期，18位老四星角色整体强度相比于现在相当在线，特别是倍率与附着。与此同时，刚开服的深渊难度相比于现在也极低。因此尽管当时整体游戏理解、操作普遍一般，只要四星的练度以及配置足够，基本上均可以达到满星。这导致了很多在现在看来匪夷所思但却能打满的队伍，例如单火香菱等。当然这个时期也出现了很多经典配队，例如知名度最高（起码老玩家群体中）的四星队————重云国家队，以及上限最高的四星队————砂糖国家队。这两只队伍取个交集，就是三位六星战神。  

进入2.0，随着永冻雷国两大传奇平民底裤队的出现，深渊难度也开始上升。更加困难的深渊筛选掉了一批数值不足、逻辑不自洽的四星队，但也留下了四星队中堪比永冻雷国的两只传奇队伍————砂糖武装与双冰双火，恰好也是直伤与增幅————这两支四星队几乎霸占了2.0时期的纯四星深渊。是的，没有草系的四星队就是这么枯燥无味，顶多就是找个人换掉行秋，让三位六星战神凑一块。只可惜随着从1.6版本优菈开始的五星伤害命座大膨胀，四星角色打伤害的责任似乎越来越少。整个2.0大版本中实装了7位新四星角色：早柚、九条、托马、五郎、云堇、久岐忍、小鹿，其中九条五郎为专拐，早柚云堇是辅助，托马久岐忍还在等他们的种子，最终只有小鹿可以勉强算得上输出，更不要说风系专拐还远在3.3。因此，2.0大版本几乎很少看到新队伍，可以说是四星队的至暗时刻。  

3.0草体系的实装瞬间拓宽了四星队的选择。绽放系反应超高的元素利用率和剧变反应倍率极大拉高了四星队的下限，尽管草系新四星的附着人均卧龙凤雏，在低练情况下种门仍然能力压一众强力四星队，甚至部分低金队。同时，草体系也为砂糖武装带来了新生，用草系替代行秋后队伍输出模式从直伤变为了上限更高的激化，省下来的行秋则可以在另一队为所欲为，无论是追求上限点秋香合体，还是当一个高效省心的挂水位打种门，都是又有强度又舒适的选择。  

## 三、纯四星配队评价标准

* 主要用以下四个主要指标评价，评分从0到10
* 其中，输出能力主要受四个乘区影响，各乘区的影响大小用极低/低/中/高/极高表示

1.**[输出]**——在合适环境、正常配置、正常练度、较熟练的手法下，阵容的输出能力
> **[环境乘区]**——深渊怪物类型、分布对输出能力的影响（相同输出评分，越低适应性越强）  
> **[配置乘区]**——角色命座、武器类型&精炼等级对输出能力的影响（相同输出评分，越低越适合平民）  
> **[练度乘区]**——角色&武器&天赋等级、圣遗物副词条对输出能力的影响（相同输出评分，越低越适合低练）  
> **[手部乘区]**——循环手法、输出手法、聚怪手法对输出能力的影响（相同输出评分，越低越适合无手玩家）

2.**[生存]**——综合考虑以下各种因素，在较熟练的手法下，阵容的生存能力  
> **[加分]**——足量治疗、盾、减伤、抗打断、高生命/高防御前台，甚至无敌帧、冻结/削韧/击飞、位移等  
> **[扣分]**——极低治疗、自挂内鬼元素、绽放自伤、重击体力消耗、蓄力/站桩

3.**[破盾]**——综合考虑以下两个方面，在较熟练的手法下，阵容的破盾能力  
> **[破盾类型]**——可破盾的种类  
> **[破盾速度]**——对各种可破盾的平均破盾速度  

4.**[成本]**——深渊两队四星队的前提下，组出此队后对另外一队的影响，即评分越低，另一队越好组
> 注意与竞速的成本概念区分！  

**注1**：以下不作为评价标准：出伤速度、转火能力、是否画地为牢、角色培养性价比等。  
**注2**：理论上讲，[生存]，[破盾]也受到环境、配置、练度、手部乘区影响，但是相对不太明显，因此不详细列出这两项评分的乘区  
**注3**：[破盾]不作为影响输出的因素，主要是因为绝大部分时候破不了盾可以换另一路

**例1**：砂糖国家队（砂糖 班尼特 香菱 行秋）  
1.[输出]——10+，纯四星没有对手（上限）  
1.1 [环境乘区]——低，传统带风增幅体系能应对绝大部分情况，火轮随身不怕多动  
1.2 [配置乘区]——高，对香菱4命、行秋6命、高精祭礼剑的需求比较大  
1.3 [练度乘区]——高，对香菱双爆要求较高，同时还要兼顾充能和精通  
1.4 [手部乘区]——高，双扩对手法要求比较细致  
2.[生存]——8，班尼特治疗(+)，行秋减伤(+)抗打断(+)，自挂火(-)  
3.[破盾]——9，水火附着频率都很高，有风；破水/岩盾略有压力  
4.[成本]——10，四个角色都是四星队中出场率很高的存在，另一队的4组队压力极大  

**例2**：砂糖武装（砂糖 北斗 菲谢尔 行秋）  
1.[输出]——9，较高配置练度下，唯一又强又无脑的纯四星队伍  
1.1 [环境乘区]——低，高削抗直伤体系能应对绝大部分情况，输出主要靠砂糖远程平A触发协同，比较简单  
1.2 [配置乘区]——高，对北斗2命、行秋2命、高精金珀的需求比较大，其他命座和精炼等级对输出的提升也很高  
1.3 [练度乘区]——高，北斗皇女行秋都需要高双爆，同时北斗行秋还要兼顾充能和攻击力  
1.4 [手部乘区]——较低，双减伤/抗打断+薄盾+感电+扩散+颠勺，实际对群生存压力低，且输出方式简单  
2.[生存]——8~10，行秋减伤(+)抗打断(+)，北斗减伤(+)抗打断(+)弹反盾(+)，低治疗(-)，较吃体力(-)  
3.[破盾]——8，水雷附着频率都很高，有风；破水雷盾有压力  
4.[成本]——5，砂北皇三人自成一派，主要是抢行秋  

**例3**：芭芭拉双草超绽（草主 柯莱 芭芭拉 久岐忍）  
1.[输出]——6（对群），5（对单），极低成本的满星及格队伍  
1.1 [环境乘区]——中，超绽种门能应对大部分情况，但画地为牢比较严重  
1.2 [配置乘区]——极低，除草主2命外完全没有刚需命座，只需要低精西风就可以循环  
1.3 [练度乘区]——极低，只需要久岐忍90级三精通、双草工具人草套+充能沙+充能武器  
1.4 [手部乘区]——中，需要一定的切人操作保证双草工具人的Q循环和芭芭拉前台挂水时间  
2.[生存]——8~9，芭芭拉高生命前台(+)，芭芭拉治疗(++)，久岐忍治疗(+)，自挂水(-)  
3.[破盾]——6，三个新四星挂元素卧龙凤雏，芭芭拉水附着勉强足够  
4.[成本]——0，久岐忍一带三，完全的废物利用，甚至可以和砂糖国家队互补  

**例4**：芭芭拉双草/带风冻绽（柯莱 草主/砂糖 罗莎莉亚/迪奥娜 芭芭拉）  
1.[输出]——8（对群），3（对单），低成本的满星可冻对群及格队伍  
1.1 [环境乘区]——极高，刚需群怪否则伤害不足，刚需能冻结否则冻绽不成立  
1.2 [配置乘区]——低，比较需要芭芭拉高精祭礼书，此外最好有柯莱2命、砂糖2命、芭芭拉2命、修女2命+高精西风枪  
1.3 [练度乘区]——极低，只需要芭芭拉90级三精通、有人带草套、保证充能即可  
1.4 [手部乘区]——高，需要聚怪手法保证输出，需要一定的切人操作保证草冰角色的Q循环  
2.[生存]——6~7，芭芭拉治疗(+)，冻结(+)，自挂水(-)，绽放自伤(-)  
3.[破盾]——6~7，与芭芭拉超绽类似，但是可带风破盾更灵活  
4.[成本]——1，与芭芭拉超绽类似，同样是低成本配队，偶尔会抢砂糖和修女  

## 四、纯四星配队角色强度评级

T0-四星上限  
> 行秋 班尼特 香菱 砂糖(EXCEL/竞速)  

T1-深渊常客  
> 菲谢尔 北斗 砂糖(实战) 凯亚 罗莎莉亚  

T2-强力对策  
> 鹿野院平藏 珐露珊(6) 瑶瑶 旅行者(草) 柯莱 久岐忍 重云  

T3-偶尔能上  
> 珐露珊(0~5) 琳妮特 芭芭拉 烟绯 丽莎 绮良良 托马 迪奥娜 莱依拉 夏洛蒂  

T4-仅限整活  
> 旅行者(风) 旅行者(雷) 雷泽 菲米尼 卡维 坎蒂丝 早柚 凝光 诺艾尔 五郎 云堇 旅行者(岩)  

T5-难以配队  
> 米卡 多莉 辛焱 安柏 九条  

T6-登峰造极  
> 旅行者(水)  

---

T0  
行秋：低配即可挂水，高配还有不错的对单直伤。稳定减伤。  
班尼特：巨量攻击拐+治疗，双冰双火队还可以通过e打不少直伤。  
香菱：稳定后台挂火，纯四星最高上限配队砂国，0命伤害爆炸，高命更加爆炸。  

---

T1  
菲谢尔：砂北皇核心之一，激化队的灵魂。  
北斗：砂北皇核心之二，稳定减伤，对双倍率怪，E上限高。  
砂糖：砂北皇核心之三，削抗+聚怪+挂元素+协同攻击发射器+精通拐。  
凯亚/罗莎莉亚：双冰双火常用，整体伤害不如带行秋但是够用。  

---

T2  
鹿野院平藏：砂国代餐鹿国，省下砂糖组成砂北皇。高命时带珐露珊也可以速切。  
珐露珊(6)：风系伤命打配队。  
瑶瑶：砂北皇+瑶瑶激化队，伤害比砂武略低，但生存压力低且能省下行秋。也可以进单/双草行秋种门。  
旅行者(草)/柯莱：低配种门后台挂草位。保证充能和正确的轴时附着量勉强够用，但最大问题是画地为牢。  
久岐忍：低配种门核心，可用低配置解决一些boss从而省出强力角色给另一路，但上限较低。  
重云：双冰双火可选，倍率低产球少，但是可附魔破盾快。  

---

T3  
珐露珊(0~5)：充能压力大，四星风C持续输出乏力，输出上限不足。  
芭芭拉：低配种门前台挂水位，代替行秋。超绽放中直伤对单吃亏，对群效果还可以，有治疗专打流血狗。原绽放尽管水环被削仍有足够伤害，前提是环境合适。  
烟绯：最强火前台，但最大的问题也在于是前台，难以跟香菱竞争。烈绽较冷门且刚需行秋。  
丽莎：雷前/后台，蓄力E受害者，但是有Q减防后台效果不查，前台超激化打桩DPS也不低。  
绮良良：草盾，蓄力E受害者，四命前毫无后台挂草能力，但超激化队表现尚可。  
托马：火盾+火后台，由于四星队塞不下纯辅一般打烈绽。由于西风枪的高白值和没有祭礼枪，充能精通很难兼顾，1秒间隔上限还可以，真对群比超绽舒服。  
迪奥娜：冰盾奶，功能性强，但由于纯四星永冻伤害比较拉胯，出场率较低。但偶尔能进冻绽放，6命加精通也有应用场景。  
莱依拉：冰盾，大多数时候为迪奥娜下位，但是唯一能带千岩的四星盾辅，有时有特殊左右。  
夏洛蒂：治疗冰法，可作为超绽驾驶员，或冻绽冰位等。  

---

T4  
旅行者(风)：实在没风系角色时的聚怪选择，用于对付骗骗花、镀金旅团等。  
旅行者(雷)：练度碾压时的充能插件，比如雷主国家队等。  
雷泽：物理大剑，平民不友好。可以玩超绽/彩虹。  
菲米尼：物理大剑，平民不友好。可以当超绽驾驶员。  
卡维：草前台。打种门设计矛盾，打输出伤害不足，大部分时候只能当前台挂草工具人。  
坎蒂丝：水后台+水附魔，范围挂水效果还可以，满命可在种门中勉强代替行秋，蒸发体系比较吃厨力。  
早柚：风奶+泥头车，泥头车强制站场且无法协同攻击，属于人下人机制，但娱乐效果尚可。  
凝光：岩速切，对单暴力，但索敌高血压。  
诺艾尔：岩站场大剑主C，比较刚需满命，平民不友好，练度需求高，属于老玩家/华馆常客的玩具。  
五郎：岩辅，四星纯岩队组件之一，命座需求大。  
云堇：岩辅，四星纯岩队组件之一。  
旅行者(岩)：岩辅，四星纯岩队不常见的组件，倍率不错，甚至能拐暴击，但岩柱过胖导致体验很差。  

---

T5  
米卡：物理辅，压力给到主C，同时还有修女这种强力竞争对手。  
多莉：雷充能拐+奶，但雷直伤的砂北皇不缺充能治疗，超激化没位置，后台挂雷对伤害贡献又没有。  
辛焱：火盾/物理大剑，前者不重要可替换角色多，后者平民不友好。  
安柏：火弓，嘲讽+充能拐+高频挂火，但是确实干不过香班。  
九条：雷攻击(爆伤)拐，过于充能大户，机制勉强，可以强行就业纯雷。  

---

T6  
旅行者(水)：强度反向登顶，整活一骑绝尘。

---
