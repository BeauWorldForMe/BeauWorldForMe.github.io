IPPG 技术其核心思想是利用摄像头替代传统 PPG 技 术中的光电器件来提取人体的脉搏信号。



在信号建模方面,Wang等[7]认为光源照射在皮 肤表面上产生镜面反射,以及在皮肤组织间产生 漫反射。其中镜面反射光线未渗透进皮肤组织, 不携带任何生理信息,通常表现为直流及低频信 号,反映了皮肤表面的肤色、形状等特性;而漫反 射是入射光在人体组织间经过部分吸收后的散射 光,反映了光线在皮肤组织及皮下血管的吸收情 况,是一种近似周期性的变化;除此以外,CCD 器 件本身不可避免地存在噪声,表现为宽频随机噪 声。





脉搏模型的构建和仿真



脉搏波：脉搏波是[心脏](https://baike.baidu.com/item/心脏/587)的搏动(振动)沿动脉血管和[血流](https://baike.baidu.com/item/血流/1724337)向外周传播而形成的，因此其传播速度取决于[传播介质](https://baike.baidu.com/item/传播介质/12715287)的物理和几何性质--动脉的弹性、管腔的大小、血液的密度和粘性等，特别是与[动脉管壁](https://baike.baidu.com/item/动脉管壁/3509369)的弹性、口径和厚度密切相关。

实验发现[动脉血管](https://baike.baidu.com/item/动脉血管/5750230)的弹性越大(即[顺应性](https://baike.baidu.com/item/顺应性/7527284)越大)，则脉搏波的传播速度越小；动脉管径越小，速度越大。故通常沿主动脉到[大动脉](https://baike.baidu.com/item/大动脉/1112683)、再到较小动脉，脉搏波的传播速度越来越大。



命名空间“System.Data”中不存在类型或命名空间名称“SQLite”(是否缺少程序集引用?) (CS0234) - C:\Users\15200\Desktop\dna2oldmemory-master\dna2oldmemory-master\PulseWaveAnalyzer\PulseWaveAnalyzer\model\DBConnector.cs:10,19