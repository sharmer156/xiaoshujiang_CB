---
title: 2018-10-18强化学习练就18般武艺,伯克利开源DeepMimic
tags: 
grammar_cjkRuby: true
---

## 强化学习练就18般武艺！伯克利开源DeepMimic

[新智元](javascript:void(0);) _今天_

![](https://mmbiz.qpic.cn/mmbiz_png/UicQ7HgWiaUb0jAUwusDvsnYYKniboXfhUjEua3b5jIemsuOj4dzLFQrOmvicjoNSjea6LkWia94dBh46r7SicUcKic0w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### 

* * *

**  新智元报道  ** 来源：GitHub

### 编辑：肖琴

##### **【新智元导读】** 伯克利BAIR实验室发布的那个会“18般武艺”的DeepMimic模型开源了！DeepMimic使用强化学习技术，用动作捕捉片段训练模型，教会了AI智能体完成24种动作，包括翻跟斗、侧翻跳、投球、高踢腿等等，动作非常流畅自然。

震撼！AI WORLD 2018世界人工智能峰会开场视频

还记得今年4月伯克利BAIR实验室发布的那个会“18般武艺”的**DeepMimic**模型吗？他们使用强化学习技术，用动作捕捉片段训练模型，教会了AI智能体完成24种动作，走路、跑步就不用说了，还包括翻跟斗、侧翻跳、投球、高踢腿等等高能动作。

体会一下：

![](https://mmbiz.qpic.cn/mmbiz_gif/UicQ7HgWiaUb0jAUwusDvsnYYKniboXfhUjxg7iahsQ6mbYJIvTWaZcpejYMiaz0ia8W9NGlVlDUCnauKzMmSqA1l8Jw/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

回旋踢

![](https://mmbiz.qpic.cn/mmbiz_gif/UicQ7HgWiaUb0jAUwusDvsnYYKniboXfhUj2QXCGGfqDM1tvPcibUuCuXjzNkgrwZ2RvfHEBAWWxGuxwSHlOq6ibNDQ/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

跑步

![](https://mmbiz.qpic.cn/mmbiz_gif/UicQ7HgWiaUb0jAUwusDvsnYYKniboXfhUjiaN54kE3icWWb3lSYdib3E0Q4WXWxnfSiaFUq0XXOpCe4ugcibtWpT1tY6A/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

投球

训练每一种动作都需要动作捕捉和深度强化学习，而BAIR的研究者创造了一个全新的系统，教会agent完成复杂、逼真的动作任务。

作者Xue Bin Peng等人将这个系统命名为DeepMimic，比已有工作更进一步的是，他们的目标是在训练一个agent完成特定任务的前提下，使它的动作更贴近真实。他们的论文发表在SIGGRAPH 2018。

![](https://mmbiz.qpic.cn/mmbiz_png/UicQ7HgWiaUb0jAUwusDvsnYYKniboXfhUjTVica5R1Sn7Dfd0QiawU3ZkDQBL1G5nwgEqAt5XgLicqe2v1Zl2J1ZhLg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

除了人形机器人外，他们还训练了Atlas机器人、暴龙、龙等形态的agent。

![](https://mmbiz.qpic.cn/mmbiz_gif/UicQ7HgWiaUb0jAUwusDvsnYYKniboXfhUjOtekgAxLQ06paTf94XYuCaia46Px3LWj7rWzg27AOETeXjicGTvkBQ3g/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

Atlas机器人

整个DeepMimic所需要的input分为三部分：一个被称为Character的Agent模型；希望Agent学习的参考动作（reference motion）；希望Agent完成的任务（task）所定义的reward function。

训练之后会得到一个可以控制Agent同时满足与参考动作相似且可以完成任务的控制器。

![](https://mmbiz.qpic.cn/mmbiz_gif/UicQ7HgWiaUb0jAUwusDvsnYYKniboXfhUjhicemIXUWCdQRic0v0ZRUdIsCbUeXv3aicbxKHloOj8pfsNLeUCKsTX8Q/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

四种翻滚动作

现在，DeepMimic的代码、数据和训练策略已经全部开源，感兴趣的读者不妨试试拿来训练自己的“功夫小子”。

开源代码

SIGGRAPH 2018论文：“DeepMimic: Example-Guided Deep Reinforcement Learning of Physics-Based Character Skills”的代码。这个框架使用强化学习来训练一个模拟人形智能体来模仿来自mocap数据的各种运动技能。

项目页面：

https://xbpeng.github.io/projects/DeepMimic/index.html

![](https://mmbiz.qpic.cn/mmbiz_png/UicQ7HgWiaUb0jAUwusDvsnYYKniboXfhUjLrVAc8RBOpeZpPZcpmhWA3WrX2xwwqaTUWRS8R1sT8LCk7eLpjjWZw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**C++:**

*   Bullet 2.87 (https://github.com/bulletphysics/bullet3/releases)

*   Eigen (http://www.eigen.tuxfamily.org/index.php?title=Main_Page)

*   OpenGL >= 3.2

*   freeglut (http://freeglut.sourceforge.net/)

*   glew (http://glew.sourceforge.net/)

**Python:**

*   PyOpenGL (http://pyopengl.sourceforge.net/)

*   Tensorflow (https://www.tensorflow.org/)

*   MPI4Py (https://mpi4py.readthedocs.io/en/stable/install.html)

**Misc:**

*   SWIG (http://www.swig.org/)

*   MPI

*   Windows: https://docs.microsoft.com/en-us/message-passing-interface/microsoft-mpi

*   Linux: sudo apt install libopenmpi-dev

**Build**

模拟环境是用C++编写的，python包装器使用SWIG构建。要安装python依赖项，请运行

<pre>pip install -r requirements.txt</pre>

请注意，必须在MPI4Py之前安装MPI。

**Windows**

wrapper使用DeepMimicCore.sln构建。

1\. 从配置管理器中选择x64配置。

2\. 在DeepMimicCore的项目属性下，修改要包含的其他包含目录

*   Bullet源目录

*   Eigen包括目录

*   python包含目录

3\. 修改要指定的其他库目录

*   Bullet lib目录

*   python lib目录

使用Release_Swig配置构建DeepMimicCore项目，这应该在DeepMimicCore/. 中生成DeepMimicCore.py。

**Linux**

1\. 通过指定以下内容修改DeepMimicCore中的Makefile，

*   EIGEN_DIR：Eigen包含目录

*   BULLET_INC_DIR：Bullet源目录

*   PYTHON_INC：python包含目录

*   PYTHON_LIB：python lib目录

2\. 建立wrapper，

<pre>make python</pre>

这应该在DeepMimicCore/中生成DeepMimicCore.py

**如何使用**

一旦构建了python wrapper，就可以使用Tensorflow完全在python中完成训练。DeepMimic.py运行用于查看模拟的可视化工具。使用mpi_run.py完成训练，它使用MPI在多个进程之间并行训练。

通过指定提供场景配置的参数文件来运行DeepMimic.py。例如，

<pre>python DeepMimic.py --arg_file args/run_humanoid3d_spinkick_args.txt</pre>

将为“回旋踢”运行一个预训练的policy。同样的,

<pre>python DeepMimic.py --arg_file args/kin_char_args.txt</pre>

将加载并播放mocap片段。

要训练一个策略（policy），请通过指定参数文件和工作进程数来运行mpi_run.py。例如，

<pre>python mpi_run.py --arg_file args/train_humanoid3d_spinkick_args.txt --num_workers 4</pre>

将训练一个策略，使用4个workers进行“回旋踢”。作为训练方案，它会定期打印统计数据并将其记录到output/，以及最新策略的.ckpt。通常需要大约6千万个样本来训练一个策略，而训练16个workers需要一天时间。16个workers可能是框架所能支持的最大workers数量。

args中已经为不同的技能提供了许多参数文件。train_ [something] _args.txt文件是为mpi_run.py设置的，用于训练策略，并为DeepMimic.py设置run_ [something] _args.txt文件以运行其中一个预训练策略。要运行自己的策略，请使用run_ [something] _args.txt的文件之一，并指定要使用--model_file运行的策略。确保引用的动作--motion_file对应于策略所训练的动作，否则策略将无法正常运行。

**接口**

*   右上角的图显示了价值函数的预测

*   单击右键并拖动将平移相机

*   单击左键并拖动将对特定位置处的角色施加力

*   滚轮会放大/缩小

*   按“r”将重置该episode

*   按'l'将重新加载参数文件并重建所有内容

*   按'x'将使用随机的框投向角色

*   按空格将暂停/恢复模拟

*   按’>'将逐步执行模拟

**Mocap Data**

Mocap clips位于data/motions/中。要播放剪辑，首先修改args/kin_char_args.txt并指定要使用的文件--motion_file，然后运行

<pre>python DeepMimic.py --arg_file args/kin_char_args.txt</pre>

动作文件遵循JSON格式。“Loop”字段指定运动是否是循环的。“wrap”指定一个循环运动，该循环将在结束时回到起始点，而“none”指定一旦运动结束就会停止的非循环运动。“Frames”列表中的每个向量指定运动中的关键帧。每个框架具有以下格式：

![](https://mmbiz.qpic.cn/mmbiz_png/UicQ7HgWiaUb0jAUwusDvsnYYKniboXfhUjpicnhfFpDBXnrB2G6hic3f0TibVazaMgcou6KtdXqPeIjwfj46iaQSz93w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

位置以米为单位指定，球面关节的3D旋转指定为四元数（w，x，y，z），转动关节（例如膝关节和肘关节）的1维旋转用弧度的标量表示。根位置和旋转在世界坐标中，但所有其他关节旋转都在关节的局部坐标中。要使用你自己的动作剪辑，请将其转换为类似格式的JSON文件。

项目地址：

https://github.com/xbpeng/DeepMimic

论文地址;

https://xbpeng.github.io/projects/DeepMimic/2018_TOG_DeepMimic.pdf

