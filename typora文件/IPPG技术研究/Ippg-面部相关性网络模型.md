代码：

```python
import os
import sys
from time import time
import datetime
import cv2
import numpy as np
import scipy.fftpack as fftpack
import shutil
from matplotlib import image
import scipy.signal as signal
from PIL import Image
import IPPG_1, IPPG_2, IPPG_3, IPPG_4, IPPG_5, IPPG_6, pic_delete_edge, IPPG_7, IPPG_8
import keyboard

def main_menu():
    now = datetime.datetime.now()
    print(now)
    print("                       **主菜单**")
    print("                       1--将视频转为图像序列存储")
    print("                       2--使用欧拉影像放大处理视频")
    print("                       3--将欧拉影像放大后的视频转为图像序列存储")
    print("                       4--对3中所得图像序列进行面部宏观信息的可视化")
    print("                       5--对1中所得图像序列进行面部分区切片")
    print("                       6--对5中所得裁剪黑边")
    print("                       7--对6中所得面部重新定位坐标，并进行三种相关性地形图成像...")
    print("                       8--计算血氧饱和度...")
    print("                       9--IPPG结果参数计算...")
    print("                       q--svm分类预测(还没写)...")
    print("                       0--退出程序")
    key_get = input("\n请输入按键选择要进行的计算内容 >>> ")

    if key_get == '1':
        print("将视频转为图像序列存储...")
        now1 = datetime.datetime.now()
        IPPG_1.video2pic(path_1 + "1.mp4", path_3)  # 将视频转为图像序列存储到path_3
        now2 = datetime.datetime.now()
        print("耗时" + str(('%.2f' % (now2.timestamp() - now1.timestamp()))) + "秒")
    elif key_get == '2':
        print("使用欧拉影像放大处理视频...")
        now1 = datetime.datetime.now()
        IPPG_2.magnify_color(path_1 + "1.mp4", 0.7, 4, path_2)
        now2 = datetime.datetime.now()
        print("耗时" + str(('%.2f' % (now2.timestamp() - now1.timestamp()))) + "秒")
    elif key_get == '3':
        print("将欧拉影像放大后的视频转为图像序列存储...")
        now1 = datetime.datetime.now()
        IPPG_1.video2pic(path_2 + "2.mp4", path_4)  # 将欧拉影像放大后的视频转为图像序列存储到path_4
        now2 = datetime.datetime.now()
        print("耗时" + str(('%.2f' % (now2.timestamp() - now1.timestamp()))) + "秒")
    elif key_get == '4':
        print("对1、3中所得图像序列分别进行面部宏观信息的可视化...")
        now1 = datetime.datetime.now()
        IPPG_3.file_sortToNormalized(path_3, path_5+"beforeEVM\\", fps, dataType=dataType)   # 可视化在path5的两个文件夹内
        now2 = datetime.datetime.now()
        print("对1耗时" + str(('%.2f' % (now2.timestamp() - now1.timestamp()))) + "秒")
        IPPG_3.file_sortToNormalized(path_4, path_5+"afterEVM\\", fps, dataType=dataType)
        now3 = datetime.datetime.now()
        print("对3耗时" + str(('%.2f' % (now3.timestamp() - now2.timestamp()))) + "秒")
    elif key_get == '5':
        print("对1中所得图像序列进行面部分区切片以及ptt计算...")
        now1 = datetime.datetime.now()
        cal_ptt = True
        img_path, LEN, center_all, tri_list =IPPG_4.dir_record_analysis(path_3, path_5, path_6, fps,
                                   dataType1=dataType, dataType2=dataType, cal_ptt=cal_ptt)
        now2 = datetime.datetime.now()
        print("耗时" + str(('%.2f' % (now2.timestamp() - now1.timestamp()))) + "秒")
    elif key_get == '6':
        print("裁剪黑边...")
        now1 = datetime.datetime.now()
        pic_delete_edge.main(path_5+"face\\", path_7+"face_new\\", dataType1=dataType)
        print("裁剪完成。")
        now2 = datetime.datetime.now()
        print("耗时" + str(('%.2f' % (now2.timestamp() - now1.timestamp()))) + "秒")
    elif key_get == '7':
        print("对6中所得面部重新定位坐标，并进行三种相关性地形图成像...")
        now1 = datetime.datetime.now()
        IPPG_7.dir_record_again(path_7, path_8, fps=fps, dataType1=dataType)  # 速度比较慢
        now2 = datetime.datetime.now()
        print("耗时" + str(('%.2f' % (now2.timestamp() - now1.timestamp()))) + "秒")
    elif key_get == '8':
        print("计算血氧饱和度...")
        now1 = datetime.datetime.now()
        IPPG_5.cal_spo2(path_3, fps, dataType=dataType)
        now2 = datetime.datetime.now()
        print("耗时" + str(('%.2f' % (now2.timestamp() - now1.timestamp()))) + "秒")
    elif key_get == '9':
        print("IPPG结果参数计算...")
        now1 = datetime.datetime.now()
        IPPG_8.cal_ippg(path_5+"slice\\", path_9, fps, dataType=dataType)  # 计算,datatype根据文件夹修改
        now2 = datetime.datetime.now()
        print("耗时" + str(('%.2f' % (now2.timestamp() - now1.timestamp()))) + "秒")
    elif key_get == 'q':
        print("svm分类预测(还没写)...")
        now1 = datetime.datetime.now()
        now2 = datetime.datetime.now()
        print("耗时" + str(('%.2f' % (now2.timestamp() - now1.timestamp()))) + "秒")
    elif key_get == '0':
        print("退出程序...")
        now2 = datetime.datetime.now()
        print("程序运行总时长：" + str(('%.2f' % (now2.timestamp() - now.timestamp()))) + "秒")
        sys.exit()
    else:
        print("按键输入不符合要求，请重新输入！")

'''
调参Fs（根据视频）
'''
fps = 25
dataType = ".bmp"
'''
path设置
'''
path_0 = "I:\\1\\250668997543202816\\"  # 原始图像序列地址
path_1 = "E:\\code_path\\path_1\\"  # 原始视频存储地址
path_2 = "E:\\code_path\\path_2\\"  # 欧拉影像放大后视频存储地址
path_3 = "E:\\code_path\\path_3\\"  # 原始视频转图片序列存储地址
path_4 = "E:\\code_path\\path_4\\"  # 欧拉影像放大后视频转图片序列存储地址
path_5 = "E:\\code_path\\path_5\\"  # 面部宏观信息可视化结果的存储地址&面部切片
path_6 = "E:\\code_path\\path_6\\"  # PTT计算结果-可视化
path_7 = "E:\\code_path\\path_7\\"  # 裁剪黑边后面部存储地址
path_8 = "E:\\code_path\\path_8\\"  # 相关性地形图结果存储地址
path_9 = "E:\\code_path\\path_9\\"  # IPPG结果参数存储地址
# path_test = "E:\\code_path\\path_test\\"  # 测试path



if __name__ == '__main__':
    print("--------------------------------------Begin!--------------------------------------")
    '''
    注意事项：
    1.运行时使用键盘选择所要进行的计算内容,视频文件放到path_1，命名为1.mp4
    2.运行前需要按上面path块创建文件夹
    3.包含有图像序列的文件夹中的序列内容需要清除，防止下次运行时序列比前次短造成运算错误
    4.有图像序列的文件夹分布在path_3、path_4、path_5、path_7中
    '''
    while True:
        main_menu()




```

```python
from lib.ppgfunc import *
from lib.heartpy import *
import copy
from matplotlib import gridspec
from matplotlib import image as imgaaa
import cv2

def corr_analysis(path, path1, center_all, tri_list, FPS=30, LEN = 150, dataType = '.bmp'):
    #center_all是面部各分区的中心点坐标
    print("--------------------------------------面部相关性地形图成像分析开始--------------------------------------")
    print('对信号重采样...')
    # 面部各点 对于面部所有点的均值进行的相关性成像，不再相对于额头ROI
    # FileDir_1 = path+"slice"  # 额头ROI
    # FileDir_face = path + "face"  # 全脸
    FileDir_face = path  # 全脸(带掩膜)
    dataName = 'pic_'

    Show = True
    # filePath_1 = os.path.join(FileDir_1, dataName + str(1) + dataType) # 额头ROI
    # filePath_1 = os.path.join(FileDir_1, dataName + str(1) + dataType) # 额头ROI
    # filePath_face = os.path.join(FileDir_face, dataName + str(1) + dataType) # 全脸
    filePath_face = os.path.join(FileDir_face, dataName + str(1) + dataType) # 全脸
    """step1: 从地址中加载数据"""
    # img_1 = cv2.imread(filePath_1)  # 额头ROI
    img_face = cv2.imread(filePath_face)  # 全脸

    # DataAll_1, t1 = loadAllData(fileDir=FileDir_1, dataName=dataName, dataType=dataType,
    #                           img=img_1, Len=LEN, fs=FPS, show=Show)    # 额头ROI

    DataAll_face, t2 = loadAllData(fileDir=FileDir_face, dataName=dataName, dataType=dataType,
                              img=img_face, Len=LEN, fs=FPS, show=Show)    # 全脸

    """step2: 制作参考区域并获取IPPG数据"""
    # 相关性参考信号--全脸
    pix_num = 0
    ttt = np.zeros(np.shape(DataAll_face[1, 1, 1, :]))
    for ix, indX in enumerate(np.arange(0, img_face.shape[0])):
        print(str(ix)+"_loop1")
        for iy, indY in enumerate(np.arange(0, img_face.shape[1])):
            tmp_0 = DataAll_face[ix, iy, 1, :]  # 应该是一个1*len的信号
            # ttt = np.zeros([len(tmp_0),1])
            if np.sum(tmp_0) != 0:
                pix_num += 1
                for j in range(0,len(tmp_0)):
                    ttt[j] = ttt[j] + tmp_0[j]
    iwave = ttt/float(pix_num)
    print("参考区域信号：面部均值")
    # 各部分IPPG信号获取
    blockAllPixN = 60  # 100#50 #window size of (X,Y) to be averaged 块大小
    blockMovPixN = 1  # 50#10#2 #sliding window size 步长

    AmpImaging = np.zeros([int((img_face.shape[0] - blockAllPixN) / blockMovPixN + 1),
                           int((img_face.shape[1] - blockAllPixN) / blockMovPixN) + 1])

    for ix, indX in enumerate(np.arange(0, img_face.shape[0] - blockAllPixN + 1, blockMovPixN)):
        print(str(ix)+"_loop2")
        for iy, indY in enumerate(np.arange(0, img_face.shape[1] - blockAllPixN + 1, blockMovPixN)):
            tmpp = DataAll_face[indX:indX+blockAllPixN,indY:indY+blockAllPixN,1,:]
            tmpp = tmpp.mean(axis=0)
            tmp = tmpp.mean(axis=0)
            # print("tmp::::", tmp)
            # print(tmp.shape)
            # print("type", type(tmp))
            if np.sum(tmp) == 0:
                # var_mean = 0
                AmpImaging[ix, iy] = 0
            else:
                # test = correlate(iwave.real, tmp)
                # AmpImaging[ix, iy] = correlate(iwave.real, tmp)[0]
                # tmp = ptt_0918.butter_bandpass_filter(tmp, low, high, FPS)
                AmpImaging[ix, iy] = np.correlate(iwave, tmp)

    plt.figure(figsize=(12, 10))
    gs = gridspec.GridSpec(3, 4, wspace=0, hspace=0.1)

    tmp_2 = copy.deepcopy(AmpImaging)
    tmp_2[tmp_2 == 0] = np.nan
    # AmpImaging[AmpImaging == 0] = np.nanmedian(tmp_2)
    # plt.imshow(AmpImaging)
    # plt.show()
    # print("AmpImaging = ", AmpImaging)
    # print("AmpImaging 's shape = ", AmpImaging.shape)
    # cv2.imwrite(path1 + 'corr_1.jpg', AmpImaging)
    imgaaa.imsave(path1 + 'corr_1.png', AmpImaging, cmap='hot')
    imgaaa.imsave(path1 + 'corr_2.png', AmpImaging, cmap='jet')
    imgaaa.imsave(path1 + 'corr_3.png', AmpImaging, cmap='Greys')
    print("点成像完成。")

    # center_all是中心点矩阵 按照三角形的顺序索引，center_all[i]
    # tri_list是三角形顶点，用tri_list[i]索引
    # 各块IPPG信号获取

    block_tmp = np.zeros([len(center_all), 1])
    img_block = np.zeros([img_face.shape[0], img_face.shape[1]])
    for i in range(len(center_all)):
        x1, x2, y1, y2 = center_all[i][0]-30, center_all[i][0]+30, center_all[i][1]-30, center_all[i][1]+30
        if x1 < 0:
            x1 = 0
        if x2 > img_face.shape[1]:
            x2 = img_face.shape[1]-1
        if y1 < 0:
            y1 = 0
        if y2 > img_face.shape[0]:
            y2 = img_face.shape[0]-1
        # tmppp = DataAll_face[x1:x2, y1:y2, 1, :]
        tmppp = DataAll_face[y1:y2, x1:x2, 1, :]
        tmppp = np.nanmean(tmppp, axis=0)
        tmppp = np.nanmean(tmppp, axis=0)
        # tmppp = tmppp.mean(axis=0).mean(axis=0)
        # tmppp = tmppp.mean()

        block_tmp[i] = np.correlate(iwave, tmppp)


    tmp_3 = copy.deepcopy(block_tmp)
    tmp_3[tmp_3 == 0] = np.nan
    block_tmp[block_tmp == 0] = np.nanmedian(tmp_3) # 0置为均值，缩小数值范围
    for j in range(len(block_tmp)):
        block_tmp[j] = (block_tmp[j]-min(block_tmp))/(max(block_tmp)-min(block_tmp)) # 归一化

    for i in range(len(tri_list)):
        if(block_tmp[i]==np.nan):
            block_tmp[i] = 0
        cv2.fillConvexPoly(img_block, tri_list[i], block_tmp[i])

    imgaaa.imsave(path1 + 'corr_block_1.png', img_block, cmap='hot')
    imgaaa.imsave(path1 + 'corr_block_2.png', img_block, cmap='jet')
    imgaaa.imsave(path1 + 'corr_block_3.png', img_block, cmap='Greys')
    print("块成像完成。")

    # 相关性-面网络
    # net_tmp1 = np.zeros([len(center_all), 1])
    net_tmp_mid = np.zeros([len(center_all), len(center_all)])

    for i in range(len(center_all)):
        print(str(i) + "_loop3")
        for j in range(i, len(center_all)):
            x1, x2, y1, y2 = center_all[i][0] - 30, center_all[i][0] + 30, center_all[i][1] - 30, center_all[i][1] + 30
            m1, m2, n1, n2 = center_all[j][0] - 30, center_all[j][0] + 30, center_all[j][1] - 30, center_all[j][1] + 30
            if x1 < 0:
                x1 = 0
            if x2 > img_face.shape[1]:
                x2 = img_face.shape[1] - 1
            if y1 < 0:
                y1 = 0
            if y2 > img_face.shape[0]:
                y2 = img_face.shape[0] - 1
            if m1 < 0:
                m1 = 0
            if m2 > img_face.shape[1]:
                m2 = img_face.shape[1] - 1
            if n1 < 0:
                n1 = 0
            if n2 > img_face.shape[0]:
                n2 = img_face.shape[0] - 1
            tmppp_i = DataAll_face[y1:y2, x1:x2, 1, :]
            tmppp_i = np.nanmean(tmppp_i, axis=0)
            tmppp_i = np.nanmean(tmppp_i, axis=0)
            tmppp_j = DataAll_face[n1:n2, m1:m2, 1, :]
            tmppp_j = np.nanmean(tmppp_j, axis=0)
            tmppp_j = np.nanmean(tmppp_j, axis=0)
            if j != i:
                net_tmp_mid[i][j] = np.correlate(tmppp_i, tmppp_j)
    # 上面会得到一个net_tmp_mid 上三角矩阵，第一行是第一个点对所有点的相关性，第二行是第二个点对其他...以此类推
    # tmp_4 = copy.deepcopy(net_tmp_mid)
    # tmp_4[tmp_4 == 0] = np.nan
    # net_tmp_mid[net_tmp_mid == 0] = np.nanmedian(tmp_4)  # 0置为均值，缩小数值范围
    net_tmp_mid[net_tmp_mid == 0] = np.nan
    for i in range(len(center_all)):
        for j in range(len(center_all)):
            # if net_tmp_mid[i][j] != np.nan:
            net_tmp_mid[i][j] = (net_tmp_mid[i][j]-np.nanmin(np.nanmin(net_tmp_mid)))/(np.nanmax(np.nanmax(net_tmp_mid))-np.nanmin(np.nanmin(net_tmp_mid)))# 归一化

    img_4 = np.zeros(img_face.shape)
    img_4 = img_4.astype(np.uint8)  # 转换数据类型，img4用作掩膜
    for i in range(len(center_all)):
        for j in range(len(center_all)):
            if net_tmp_mid[i][j] >= 0.95:
                # cv2.line(img_4, (center_all[i][0], center_all[i][1]), (center_all[j][0], center_all[j][1]), net_tmp_mid[i][j])
                cv2.line(img_4, (center_all[i][1], center_all[i][0]), (center_all[j][1], center_all[j][0]), (255, 255, 255))

    face_block1 = cv2.imread(path1 + 'corr_block_2.png')
    face_block2 = cv2.imread(path1 + 'corr_block_3.png')
    masked_1 = cv2.add(img_face, img_4)  # 将图片混叠
    masked_2 = cv2.add(face_block1, img_4)  # 将图片混叠
    masked_3 = cv2.add(face_block2, img_4)  # 将图片混叠

    # cv2.imwrite("E:\\code_path\\path_5\\added_up.jpg", masked)
    cv2.imwrite(path1 + 'corr_net_1.jpg', masked_1)
    cv2.imwrite(path1 + 'corr_net_2.jpg', masked_2)
    cv2.imwrite(path1 + 'corr_net_3.jpg', masked_3)
    print("面网络成像完成。")
    print("--------------------------------------相关性分析结束。--------------------------------------")

def loadAllData(fileDir, dataName, dataType='.png', img=np.zeros([1000,1000,3]), Len=500, fs=30, show=True):
    '''
    load the image intact data from the file

    :return: Data, t
    '''
    Data = np.zeros([img.shape[0], img.shape[1], img.shape[2], Len])
    for i in range(0, Len):
        filePath = os.path.join(fileDir, dataName + str(i) + dataType)
        image = cv2.imread(filePath)
        print(str(i)+"_loop0")
        image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB) #for nir /colr
        Data[:, :, :, i] = image
        if show:
            if i == Len:
                # 只显示最后一张图
                plt.figure()
                plt.imshow(image)
                plt.title("The origin data")
                # plt.show()
    t = np.linspace(0, Len / fs, Len)
    return Data, t


def plotData(Data, t, show, title="data"):
    r, c = Data.shape
    colors = plt.cm.jet(np.linspace(0, 1, r))
    if r >= 6:
        r = 0
    if show:
        plt.figure()
        plt.subplot(r + 1, 1, 1)

        for i in range(0, Data.shape[0]):
            plt.plot(t, Data[i, :], c=colors[i, :])
        plt.legend(range(0, Data.shape[0]), loc=2)
        plt.title(title)

        for i in range(r):
            plt.subplot(r + 1, 1, i + 2)
            plt.plot(t, Data[i, :], c=colors[i, :])

def SegData(DataAll=np.zeros([1000,1000,3, 300]), t=np.zeros([1000,1]), indX=([10, 30]), indY=([10, 30]), show=True):
    '''
    image segmentation data from the DataAll
    :return: Data, t
    '''
    Data = DataAll[indX[0]:indX[1], indY[0]:indY[1], :]
    temp = np.mean(Data, axis=1)
    Data = np.mean(temp, axis=0)

    if show:
        try:
            plt.gcf()
            plt.figure(1)
        except Exception as exception:
            plt.figure(1)
            plt.imshow(DataAll[:,:,:,1]/255)

        plt.plot(range(indY[0],indY[1]), np.ones([indY[1]-indY[0],1])*indX[0], '-', linewidth=5, color='firebrick')
        plt.plot(range(indY[0],indY[1]), np.ones([indY[1]-indY[0],1])*indX[1], '-', linewidth=5, color='firebrick')
        plt.plot(np.ones([indX[1]-indX[0],1])*indY[0], range(indX[0],indX[1]), '-', linewidth=5, color='firebrick')
        plt.plot(np.ones([indX[1]-indX[0],1])*indY[1], range(indX[0],indX[1]), '-', linewidth=5, color='firebrick')

        plt.figure()
        plt.imshow(DataAll[indX[0]:indX[1], indY[0]:indY[1], :, 1]/255)
        plt.title("segmentation: "+ str(indX) + str(indY))
        plotData(Data, t, show=show, title="Data_Original")
    return Data, t

```

```python
import os
from time import time
import datetime
import cv2
import numpy as np
import scipy.fftpack as fftpack
import shutil
from matplotlib import image
import scipy.signal as signal
from PIL import Image
import dlib
from scipy.signal import find_peaks
import matplotlib.pyplot as plt
from itertools import combinations
from matplotlib import gridspec
import copy
from skimage import io
import IPPG_4, IPPG_6, pic_delete_edge

def dir_record_again(path0, path1, fps=25, dataType1=".bmp"):
    print(">>>面部重定位、分区开始>>>")
    mask = "E:\\code_path\\path_6\\mask.bmp"
    im = io.imread(mask)
    mask2 = pic_delete_edge.corp_margin(im)
    io.imsave("E:\\code_path\\path_6\\mask2.bmp", mask2)
    face_path = path0 + "face_new\\"
    dataName = "pic_"
    # img = cv2.imread(face_path+dataName+str(0)+dataType1)


    tri_list, center_all = IPPG_4.return_new_cen("E:\\code_path\\path_6\\mask2.bmp")
    # 可视化呀！
    '''plot triangle'''
    img2 = cv2.imread("E:\\code_path\\path_6\\mask2.bmp")
    img3 = np.zeros(img2.shape)
    img3 = img3.astype(np.uint8)  # 转换数据类型，img3用作掩膜
    for i in range(len(tri_list)):
        # tri_list[i]是个array
        cv2.line(img3, (tri_list[i][0][0], tri_list[i][0][1]), (tri_list[i][1][0], tri_list[i][1][1]), (255, 255, 255),
                 2)  # cv2.line(image, start_point, end_point, color, thickness) 每个列表的第一个点和第二个点连线
        cv2.line(img3, (tri_list[i][0][0], tri_list[i][0][1]), (tri_list[i][2][0], tri_list[i][2][1]), (255, 255, 255),
                 2)  # 每个列表的第一个点和第三个点连线
        cv2.line(img3, (tri_list[i][1][0], tri_list[i][1][1]), (tri_list[i][2][0], tri_list[i][2][1]), (255, 255, 255),
                 2)  # 每个列表的第二个点和第三个点连线

    masked = cv2.add(img2, img3)  # 将图片混叠
    cv2.imwrite(path0+"added_up_new.jpg", masked)

    pathDir = os.listdir(face_path)
    LEN = 0
    first_img = 0
    for i, tmp in enumerate(pathDir):
        # print(i, tmp)
        if dataType1 in tmp:
            LEN += 1

    IPPG_6.corr_analysis(face_path, path1, center_all, tri_list, FPS=fps, LEN=LEN - 1, dataType=dataType1)
```

<img src="G:\课程缓存\生理系统建模与仿真\大作业\2019229134马者威龙大作业\1.jpg" alt="1" style="zoom:33%;" />

<img src="G:\课程缓存\生理系统建模与仿真\大作业\2019229134马者威龙大作业\Filter_Data_bandpass.png" alt="Filter_Data_bandpass" style="zoom:33%;" />

<img src="G:\课程缓存\生理系统建模与仿真\大作业\2019229134马者威龙大作业\2.jpg" alt="2" style="zoom:33%;" />

<img src="G:\课程缓存\生理系统建模与仿真\大作业\2019229134马者威龙大作业\3.jpg" alt="3" style="zoom:33%;" />

<img src="G:\课程缓存\生理系统建模与仿真\大作业\2019229134马者威龙大作业\4.jpg" alt="4" style="zoom:33%;" />

<img src="G:\课程缓存\生理系统建模与仿真\大作业\2019229134马者威龙大作业\corr_block_2.png" alt="corr_block_2" style="zoom:33%;" />

<img src="G:\课程缓存\生理系统建模与仿真\大作业\2019229134马者威龙大作业\corr_net_3.jpg" alt="corr_net_3" style="zoom:33%;" />

