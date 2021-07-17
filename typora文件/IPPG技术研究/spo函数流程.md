```python
if cal_ox == True:
    try:
        cal_spo2("I:\\1\\250669964074422272") # 热力图，根据相关性来算的？
    except:
        pass
```

```python
def cal_spo2(path = "I:\\1\\250668997543202816"):
	recent_sequence_path = path + "\\" + "slice1"  # 保存路径
    calculate_oxygen(recent_sequence_path)
```

```python
def calculate_oxygen(path):
    dataType = ".bmp"
    pathDir = os.listdir(path)
    LEN = 0
    for i, tmp in enumerate(pathDir):
        if dataType in tmp:
            LEN += 1
            if LEN == 1:
                first_img = i
    pathDir = pathDir[first_img: first_img + LEN]
    CNum = len(pathDir)
    print(pathDir)

    R_channel_1 = []
    B_channel_1 = []
    SPO2=[]

    for i in range(0,  CNum):
        img = imread(os.path.join(path, pathDir[i]))
        # RAC = list(map(float, RAC))
        # PixYmax = 1760
        # PixYmin = 250
        # PixXmin = 200
        # PixXmax = 680
        # img = img[PixYmin:PixYmax, PixXmin:PixXmax, :]
        # PixN = 150;
        # PixXmin = 1457;
        # PixYmin = 220
        # img = img[PixXmin:PixXmin + PixN, PixYmin:PixYmin + PixN, :]

        h, w, _ = img.shape
        print(h, w)
        pixels_num = h*w

        R_temp = img[:, :, 2]
        R_channel = np.sum(R_temp)
        R_channel_1.append(R_channel / pixels_num)
        B_temp = img[:, :, 0]
        B_channel = np.sum(B_temp)
        B_channel_1.append(B_channel / pixels_num)

    print("R_channel_1:", R_channel_1)
    R_channel_1 = np.array(R_channel_1, dtype=float)
    R_channel_f = filtersignal(R_channel_1, [0.7, 3], 20, 2, filtertype="bandpass")
    # print("R_channel_f", R_channel_f) 有值
    B_channel_1 = np.array(B_channel_1, dtype=float)
    B_channel_f = filtersignal(B_channel_1, [0.7, 3], 20, 2, filtertype="bandpass")


    RAC_10 = pd.Series(R_channel_f).rolling(window=10).std()
    # print("中间：", RAC_10)
    # print(type(RAC_10))
    RAC_10 = RAC_10[0:len(RAC_10):40]
    BAC_10 = pd.Series(B_channel_f).rolling(window=10).std()
    BAC_10 = BAC_10[0:len(BAC_10):40]


    RDC = pd.Series(R_channel_1).rolling(window=10).mean()
    RDC = RDC[0:len(RDC):40]
    BDC = pd.Series(B_channel_1).rolling(window=10).mean()
    BDC = BDC[0:len(BDC):40]

    #print(RAC_10,RDC)
    RDC = np.array(RDC)
    BDC = np.array(BDC)
    RAC_10 = np.array(RAC_10)
    BAC_10 = np.array(BAC_10)
    print("RAC_10:", RAC_10, "RDC:", RDC)
    R = [a / b for a, b in zip([c / d for c, d in zip(RAC_10, RDC)], [c / d for c, d in zip(BAC_10, BDC)])]

    for i in range(0,len(R)):
        a = -14.16*R[i]+108.24
        SPO2.append(a)

    SPO2 = np.array(SPO2)
    text_save(path+"\\spo2.txt", SPO2)
```

+ 这个SPO2只是记录了两个值，作用就这些



+ 计算相关性的地方在20200910_face的200~214行

  + ```python
    """step4: calc correlation img"""
    也是找像素进行遍历。
    ```

  + ```python
    tmp = HR_seg_ez(DataAll1, t2, fs=FPS, PixN=blockAllPixN, PixXmin=indX,
                       PixYmin=indY, CHROM_s=False, method='None', show=False)
    '''
         预处理：
             摆脱异常值。
             带通滤波器，无边缘效应
             使用均值中心定标技术降低信号趋势[3]
         （无条件的，因为这通常是必需的步骤，并且没有害处）
    
    '''
    '成分提取方法0：CHROM +自适应小波，直接使用iwave'
    
             '''MethodA：CHROM，可用于颜色信号提取以估计心率[3] [6]
    ```



+ correlate（）函数
  + 计算相关性，原始波和当前波，使用互相关
  + 内部是np.correlate()
  + 原始波iwave里放的是额头处ippg信号。
  + **为啥返回负值呢？**
    + 负相关，使用的是互相关得到的第一个值代替像素块的值。
+ 不得不提他的切片过程
  + 先把原图像进行cv.resize，缩小为原先尺寸的1/4，mode是INTER AREA，用像素面积关系重采样
  + 这种插值模式太方便了！
  + 简化算法，还能求得区域均值。

+ 看脉搏传输速度和血流传输速度