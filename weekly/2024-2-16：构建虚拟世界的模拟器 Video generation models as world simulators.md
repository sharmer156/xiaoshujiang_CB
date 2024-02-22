---
title: 2024-2-16：构建虚拟世界的模拟器 Video generation models as world simulators
tags: 
grammar_cjkRuby: true
---


视频生成模型：构建虚拟世界的模拟器 [译]
原文：Video generation models as world simulators
我们致力于在视频数据上开展生成模型的大规模训练。具体来说，我们针对不同时长、分辨率和宽高比的视频及图像，联合训练了基于文本条件的扩散模型。我们采用了一种 Transformer 架构，这种架构能够处理视频和图像潜在编码的时空片段。我们的最大型号模型，Sora，能生成高质量的一分钟视频。我们的研究显示，扩展视频生成模型的规模是向着创建能够模拟物理世界的通用工具迈出的有前途的一步。

本技术报告主要介绍了两方面内容：(1) 我们如何将各种类型的视觉数据转化为统一的表示形式，从而实现生成模型的大规模训练；(2) 对 Sora 模型能力和局限性的定性评价。报告中没有包含模型和实施的详细信息。

之前的很多研究都探讨过利用各种方法对视频数据进行生成模型的建模，包括循环网络 1,2,3，生成对抗网络 4,5,6,7，自回归 Transformer 8,9 以及扩散模型 10,11,12。这些研究通常关注于特定类别的视觉数据，较短的视频，或是固定尺寸的视频。Sora 是一种对视觉数据进行广义建模的模型，它能够生成各种时长、宽高比和分辨率的视频和图像，最长可达一分钟的高清视频。

视觉数据的创新转化：补片技术
受到大语言模型（LLM）在处理互联网规模数据、培养全能技能方面成功经验的启发，13,14 我们探索了如何将类似的优势应用于视觉数据的生成模型。大语言模型通过使用 tokens —— 一种统一处理代码、数学及多种自然语言的高效方式 —— 实现了模态间的无缝转换。在本研究中，我们引入了视觉领域的对应物：视觉补片（patches）。研究表明，补片是一种高效的视觉数据表现形式，15,16,17,18 它们能极大地提升生成模型处理多样化视频和图像数据的能力。

图 1: 补片示意图
图 1: 补片示意图

具体来说，我们通过先将视频数据压缩到低维度潜在空间，19 再将其分解成时空补片，从而实现视频到补片的转化。

视频压缩网络
我们开发了一种降维技术，20 该技术能够处理原始视频数据，并生成在时间和空间上都进行了压缩的潜在表征。Sora 在这种压缩的潜在空间中接受训练，并能够生成新的视频内容。此外，我们还开发了一个解码器，能够将这些潜在表征还原为像素级的视频图像。

时空补片技术
通过对压缩后的视频输入进行处理，我们能够提取出一系列的时空补片，这些补片在模型中扮演着类似于 Transformer Tokens 的角色。值得一提的是，这套方案同样适用于图像处理，因为从本质上来说，图像可以被视为单帧的视频。采用基于补片的表现形式，Sora 能够适应不同分辨率、持续时间及宽高比的视频和图像。在生成新视频内容时，我们可以通过将这些随机初始化的补片按照需要的大小排列成网格，来控制最终视频的大小和形式。

视频生成的 Transformer 扩展技术
Sora 是一种扩散模型21,22,23,24,25；它能够接受带有噪声的图像块（及条件信息如文本提示）作为输入，并被训练以预测出原始的“清晰”图像块。值得注意的是，Sora 属于扩散型 Transformer26。Transformer 技术在多个领域，包括语言建模13,14、计算机视觉15,16,17,18以及图像生成27,28,29中都展现出了卓越的扩展能力。

图 Diffusion
图 Diffusion

本研究发现，扩散型 Transformer 同样能在视频模型领域高效扩展。下文中，我们通过对比训练过程中固定种子和输入条件下的视频样本，展示了训练资源增加带来的样本质量显著提升。

基础计算

4 倍计算

16 倍计算

视频的多样化持续时间、分辨率和宽高比
传统的图像和视频生成方法通常会将视频调整至标准尺寸，例如 4 秒长的视频以 256x256 的分辨率进行处理。我们发现，直接在视频的原始尺寸上进行训练能带来多重好处。

灵活的采样能力
Sora 能够生成各种尺寸的视频，包括宽屏的 1920x1080p、竖屏的 1080x1920 以及介于两者之间的任何格式。这使得 Sora 能够直接为不同设备制作符合其原生宽高比的内容。此外，它还允许我们在生成全分辨率内容之前，快速地以较低尺寸原型化内容，所有这些都能通过同一模型实现。

构图与布局的优化
我们的实验表明，在视频的原生宽高比上进行训练，能够显著提升视频的构图与布局质量。我们将 Sora 与另一个训练模型进行了对比，后者将所有训练视频裁剪为正方形，这是训练生成模型时的常规做法。与被裁剪成正方形的模型（左侧）相比，Sora 生成的视频（右侧）展现了更佳的构图效果，有时候裁剪成正方形的模型生成的视频中主题只能部分展示。而 Sora 则能够更好地捕捉完整的场景。

语言理解
开发能够从文字生成视频的系统，我们需要大量的视频及其对应的文字说明。我们采用了 DALL·E 330 中引入的一种重新标注技术，并将其应用于视频。首先，我们训练了一个能够生成详细描述的模型，然后利用这个模型为训练集里的所有视频创建文字说明。我们发现，使用描述性强的视频说明进行训练，不仅能提高文字的准确度，还能显著提升视频的整体质量。

就像 DALL·E 3 一样，我们还使用 GPT 把用户的简短提示转化成详尽的说明，再将这些说明送给视频生成模型。这一过程使得 Sora 能够根据用户的指令，制作出高品质的视频。

图片和视频的提示功能
我们网站上的所有示例和展示的视频，都是从文字转化而来。不过，Sora 还能接受图片或已有视频作为输入。这项功能让 Sora 能够完成各种图片和视频编辑任务，比如制作无缝循环视频、给静态图片添加动画效果、延长视频的播放时间等。

让 DALL·E 图片动起来
只需一张图片和一个提示，Sora 就能创造出视频。下面展示了一些基于 DALL·E 231 和 DALL·E 330 图片生成的视频示例。


一只戴着贝雷帽和黑色高领衫的柴犬。


一个包含各种怪兽的家庭的平面设计风格插画。其中有一个毛茸茸的棕色怪兽，一个光滑的黑色怪兽配有触角，一个斑点绿色怪兽，以及一个小巧的带有圆点的怪兽，它们在愉快的环境中互动。


形成“SORA”字样的逼真云朵图像。


在一个装饰华丽的历史大厅里，一道巨大的海浪正准备冲击而来。两位冲浪者抓住机会，巧妙地驾驭着海浪。

视频时间延伸
Sora 同样能够把视频往前或往后延伸。下面是四个视频，它们都是从一个生成的视频片段开始，向后延伸。因此，尽管这四个视频的开头各不相同，但它们最终都汇聚于同一个结尾。

利用这种技术，我们能够将视频向前或向后扩展，创造出完美的无限循环效果。

视频到视频的创新编辑
扩散模型为基于文本提示的图像和视频编辑开辟了新天地。接下来，我们利用这些创新方法之一，SDEdit,32 对 Sora 进行应用。这项技术赋予了 Sora 力量，让它能够不需要任何预先示例，就能改变视频中的风格和环境。

输入视频

将设置更改为郁郁葱葱的丛林。

将设置更改为 1920 年代，使用旧学校的 captureRejectionSymbol。确保保持红色。

使其在水下。

将视频设置更改为不同于山脉的场景？也许是约书亚树？

将视频放置在太空中，并有一条彩虹路。

保持视频相同，但使其成为冬天。

用粘土动画风格制作。

用炭笔画风格重新创作，确保是黑白的。

将设置更改为赛博朋克。

将视频更改为中世纪主题。

使其有恐龙。

用像素艺术风格重写视频。

视频之间的流畅过渡
我们还可以利用 Sora 把两个风格迥异的视频平滑连接起来，使它们之间能够自然过渡，仿佛融为一体。在下方的示例中，你会看到，中间的视频巧妙地融合了左右两侧视频的元素。

图像的魔法般创造
Sora 的能力不仅限于视频，它还能创造出令人惊叹的图像。我们通过在一个时间仅为一帧的空间网格里排列高斯噪声块来完成这一魔法。这样，Sora 能够创造出各种尺寸的图像，最大分辨率达到了 2048x2048。


秋日中，一位女士的特写肖像，细节惊人，景深浅得令人称奇。


一片生机勃勃的珊瑚礁，色彩斑斓的鱼类和海洋生物穿梭其间。


在苹果树下的年轻老虎的数字艺术作品，展现了哑光画风中的细致美。


一座雪覆盖的山村，温馨的小屋和北极光的展现，细节精致，仿佛用 dslr 拍摄的 50mm f/1.2 镜头下的画面。

涌现的模拟能力
我们发现，在大规模训练下，视频模型展示出了一系列引人注目的涌现能力。这些功能让 Sora 有能力在一定程度上模拟现实世界中的人、动物和环境。这种能力的涌现，并不需要对三维空间、物体等有任何特定的预设偏好 —— 它们纯粹是由数据规模驱动的结果。

三维空间的连贯性。 Sora 能生成带有动态视角变化的视频。当摄像机位置和角度变动时，视频中的人物和场景元素能够在三维空间中保持连贯移动。

远距离连续性与物体持久性。 在生成长视频时，保持时间上的连续性一直是个挑战。我们观察到，Sora 通常能够有效处理短距离和长距离的依赖关系。比如，即使人物、动物或物体被遮挡或移出画面，我们的模型也能保持它们的连续存在。同样，它能在同一视频样本中多次展示同一角色，确保其外观贯穿始终。

与世界的互动。 Sora 有时能模拟出简单地影响世界状态的行为。例如，画家在画布上留下的笔触随时间持久存在，或者某人吃汉堡留下的咬痕。

数字世界的模拟。 Sora 还能模拟数字化过程，如视频游戏。它能在控制 Minecraft 游戏角色进行基本操作的同时，高质量渲染游戏世界及其动态。仅需通过提及“Minecraft”等字样的提示，即可激发这些能力的展现。

这些功能展示了，不断扩大视频模型的规模，是发展出能高度模拟物理及数字世界——包括其中的物体、动物和人——的高级模拟器的一条有前景的路径。

讨论
作为一个模拟器，Sora 当前还有许多局限。比如，它无法精确模拟像玻璃破碎这样的基本物理互动。有些互动，比如吃东西，并不总能正确反映物体状态的改变。我们在OpenAI Sora 介绍页中详细列出了模型的其它常见失误，包括长时间视频样本中出现的不一致性或物体的突然出现等问题。

我们相信，Sora 现有的能力展现了，继续扩展视频模型的规模是朝向开发出能够精准模拟物理和数字世界以及其中的物体、动物和人类的高级模拟器的一条充满希望的途径。

References
Srivastava, Nitish, Elman Mansimov, and Ruslan Salakhudinov. "Unsupervised learning of video representations using lstms." International conference on machine learning. PMLR, 2015.

Chiappa, Silvia, et al. "Recurrent environment simulators." arXiv preprint arXiv:1704.02254 (2017).

Ha, David, and Jürgen Schmidhuber. "World models." arXiv preprint arXiv:1803.10122 (2018).

Vondrick, Carl, Hamed Pirsiavash, and Antonio Torralba. "Generating videos with scene dynamics." Advances in neural information processing systems 29 (2016).

Tulyakov, Sergey, et al. "Mocogan: Decomposing motion and content for video generation." Proceedings of the IEEE conference on computer vision and pattern recognition. 2018.

Clark, Aidan, Jeff Donahue, and Karen Simonyan. "Adversarial video generation on complex datasets." arXiv preprint arXiv:1907.06571 (2019).

Brooks, Tim, et al. "Generating long videos of dynamic scenes." Advances in Neural Information Processing Systems 35 (2022): 31769-31781.

Yan, Wilson, et al. "Videogpt: Video generation using vq-vae and transformers." arXiv preprint arXiv:2104.10157 (2021).

Wu, Chenfei, et al. "Nüwa: Visual synthesis pre-training for neural visual world creation." European conference on computer vision. Cham: Springer Nature Switzerland, 2022.

Ho, Jonathan, et al. "Imagen video: High definition video generation with diffusion models." arXiv preprint arXiv:2210.02303 (2022).

Blattmann, Andreas, et al. "Align your latents: High-resolution video synthesis with latent diffusion models." Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition. 2023.

Gupta, Agrim, et al. "Photorealistic video generation with diffusion models." arXiv preprint arXiv:2312.06662 (2023).

Vaswani, Ashish, et al. "Attention is all you need." Advances in neural information processing systems 30 (2017).↩︎

Brown, Tom, et al. "Language models are few-shot learners." Advances in neural information processing systems 33 (2020): 1877-1901.↩︎

Dosovitskiy, Alexey, et al. "An image is worth 16x16 words: Transformers for image recognition at scale." arXiv preprint arXiv:2010.11929 (2020).↩︎

Arnab, Anurag, et al. "Vivit: A video vision transformer." Proceedings of the IEEE/CVF international conference on computer vision. 2021.↩︎

He, Kaiming, et al. "Masked autoencoders are scalable vision learners." Proceedings of the IEEE/CVF conference on computer vision and pattern recognition. 2022.↩︎

Dehghani, Mostafa, et al. "Patch n'Pack: NaViT, a Vision Transformer for any Aspect Ratio and Resolution." arXiv preprint arXiv:2307.06304 (2023).↩︎

Rombach, Robin, et al. "High-resolution image synthesis with latent diffusion models." Proceedings of the IEEE/CVF conference on computer vision and pattern recognition. 2022.

Kingma, Diederik P., and Max Welling. "Auto-encoding variational bayes." arXiv preprint arXiv:1312.6114 (2013).

Sohl-Dickstein, Jascha, et al. "Deep unsupervised learning using nonequilibrium thermodynamics." International conference on machine learning. PMLR, 2015.

Ho, Jonathan, Ajay Jain, and Pieter Abbeel. "Denoising diffusion probabilistic models." Advances in neural information processing systems 33 (2020): 6840-6851.

Nichol, Alexander Quinn, and Prafulla Dhariwal. "Improved denoising diffusion probabilistic models." International Conference on Machine Learning. PMLR, 2021.

Dhariwal, Prafulla, and Alexander Quinn Nichol. "Diffusion Models Beat GANs on Image Synthesis." Advances in Neural Information Processing Systems. 2021.

Karras, Tero, et al. "Elucidating the design space of diffusion-based generative models." Advances in Neural Information Processing Systems 35 (2022): 26565-26577.

Peebles, William, and Saining Xie. "Scalable diffusion models with transformers." Proceedings of the IEEE/CVF International Conference on Computer Vision. 2023.

Chen, Mark, et al. "Generative pretraining from pixels." International conference on machine learning. PMLR, 2020.

Ramesh, Aditya, et al. "Zero-shot text-to-image generation." International Conference on Machine Learning. PMLR, 2021.

Yu, Jiahui, et al. "Scaling autoregressive models for content-rich text-to-image generation." arXiv preprint arXiv:2206.10789 2.3 (2022): 5.

Betker, James, et al. "Improving image generation with better captions." Computer Science. https://cdn.openai.com/papers/dall-e-3. pdf 2.3 (2023): 8↩︎

Ramesh, Aditya, et al. "Hierarchical text-conditional image generation with clip latents." arXiv preprint arXiv:2204.06125 1.2 (2022): 3.

Meng, Chenlin, et al. "Sdedit: Guided image synthesis and editing with stochastic differential equations." arXiv preprint arXiv:2108.01073 (2021).

Authors
Tim Brooks
Bill Peebles
Connor Holmes
Will DePue
Yufei Guo
Li Jing
David Schnurr
Joe Taylor
Troy Luhman
Eric Luhman
Clarence Wing Yin Ng
Ricky Wang
Aditya Ramesh
Acknowledgments
Citation
Please cite as OpenAI et al., and use the following bibtex for citation: https://openai.com/bibtex/videoworldsimulators2024.bib