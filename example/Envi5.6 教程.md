## Envi5.6 教程

[TOC]





### 处理sentinel-2数据

[下载数据 欧空局：](https://scihub.copernicus.eu/dhus/#/home)

打开文件xml，选择10m
### 图像预处理
#### 图像裁剪

> Subset Data from ROIs	



####  图像重叠

在envi软件里导入相应波段的可见光和近红外tif文件

右侧搜索`Build Layer Stack`，选择要导入的波段

<p align="center">   <img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240926_1135.png" alt="Image Description 1" style="display:inline-block; zoom:50%; margin:10px;">   <img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240926_1141.png" alt="Image Description 2" style="display:inline-block; zoom:50%; margin:10px;">

然后进行坐标系统选择，选择第一个，然后选择相应数据，我默认选蓝光的

<p align="center">   <img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240926_1143.png" alt="Image Description 1" style="display:inline-block; zoom:50%; margin:10px;">   <img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240926_1144.png" alt="Image Description 2" style="display:inline-block; zoom:50%; margin:10px;">


最后重采样使用最近邻即可，输出数据保留数据型号和日期.dat

<p align="center">   <img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240926_1201.png" alt="Image Description 1" style="display:inline-block; zoom:50%; margin:10px;">   <img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240926_1202.png" alt="Image Description 2" style="display:inline-block; zoom:50%; margin:10px;">

<p align="center"><img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240926_1203.png" style="zoom:50%;" /></p>
附landsat5/7/8波段：

<p align="center">
    <img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240926_1133.png" alt="LANDSAT5" title="LANDSAT5" width="70%" />
    <br />
    <strong>LANDSAT5</strong>
</p>


<p align="center">    
	<img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240926_1131.png" alt="LANDSAT7" title="LANDSAT7" width="70%" />   
	<br />    
	<strong>LANDSAT7</strong>
</p>



<p align="center">
    <img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240926_1126.png" alt="LANDSAT8" title="LANDSAT8" width="70%" />
    <br />
    <strong>LANDSAT8</strong>
</p>

#### 图像镶嵌

[【ENVI】图像拼接/图像镶嵌的方法]( https://www.bilibili.com/video/BV1H8411v7cy/?share_source=copy_web&vd_source=d3bc36021115afc7e44de23cb21085db)

> 这是5.3版本的，大体上差不多

### 图像分类处理

在完成影像分类之后，对于一些错分、漏分部分需要进行归类操作。以及一些零碎点也需要优化。

##### 碎斑处理

`Majority/Minority Analysis(多数/少数分析)、Clump Classes(类别聚类)和Sleve Classes(类别过滤)。`

> 本次使用`Majority/Minority Analysis`，在toolbox-->Post Classification-->Majority/Minority Analysis

<img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240928_1741.png" style="zoom:70%;" />

选中算法后，选择分类结果影像，选择默认参数即可
<p align="center">   <img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240928_1742.png" alt="Image Description 1" style="display:inline-block; zoom:60%; margin:10px;">   <img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240928_1740.png" alt="Image Description 2" style="display:inline-block; zoom:60%; margin:10px;">
<div align="center">
  <p style="display:inline-block; text-align:center; margin:10px;">
    <img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240928_1723.png" alt="Image Description 1" style="zoom:40%;">
    <br>
    <strong><em>使用算法之前</em></strong>
  </p>
  <p style="display:inline-block; text-align:center; margin:10px;">
    <img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240928_1743.png" alt="Image Description 2" style="zoom:40%;">
    <br>
    <strong><em>使用算法之后</em></strong>
  </p>
</div>




##### **处理错分、漏分部分**

> 在toolbox-->Post Classification-->Edit Classification Image

打开Edit Classification Image后，选择已处理碎斑的图像。将船，路改为水系湿地。

如果无法判断河流中的船或者岛屿，可以用浏览器搜索Google Earth，精度在5m，能够判别。可以通过勾选，方便查看需要修改的内容。

<p align="center">   <img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240928_1747.png" alt="Image Description 1" style="display:inline-block; zoom:67%; margin:10px;">   <img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240928_1809.png" alt="Image Description 2" style="display:inline-block; zoom:50%; margin:10px;"> 
</p>


<div align="center">
  <p style="display:inline-block; text-align:center; margin:10px;">
    <img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240928_1753.png" alt="Image Description 1" style="zoom:40%;">
    <br>
    <strong><em>处理之前</em></strong>
  </p>
  <p style="display:inline-block; text-align:center; margin:10px;">
    <img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240928_1755.png" alt="Image Description 2" style="zoom:40%;">
    <br>
    <strong><em>处理之后</em></strong>
  </p>
</div>
修改完成之后记得保存。

##### 精度评价

最后进行`精度评价`，由于没有更高空间分辨率的影像，所以暂时使用原数据进行。不能使用原来的训练样本进行评价。要重新选择新的验证样本。`为了降低各类地物数量不平衡对总体精度的影响，用于验证的各类地物ROI像元数也应尽可能相近。`

在重新选取了验证样本之后，在toolbox-->Post Classification-->Confusion Matrix Using Gound Truth ROIs，点击需要验证的分类图
<p align="center">   <img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240928_1812.png" alt="Image Description 1" style="display:inline-block; zoom:60%; margin:10px;">   <img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240928_1820.png" alt="Image Description 2" style="display:inline-block; zoom:60%; margin:10px;">

如果有些未能匹配的地类，需要手动进行匹配，最后点击Add Combination即可。



<img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240928_1821.png" style="zoom:67%;" />

点击ok后，会获得混淆矩阵。主要看总体精度OA（Overall Accuracy）和kappa。最后把混淆矩阵数据导出，后续需要使用。

<img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240928_1827.png" style="zoom:50%;" />

#### 提高类别间的可分离性

**光谱特征指数和DEM数据可以提高类别间的**

>
>$NDWI_{G/NIR}=(\Rho_{Green}-\Rho_{NIR})/(\Rho_{Green}+\Rho_{NIR})$	(1)
>
>$NDVI_{NIR/R}=(\Rho_{NIR}-\Rho_{Red})/(\Rho_{NIR}+\Rho_{Red})$	       (2)
>
>(1)$NDWI_{G/NIR}$减少植被误读,最大限度区分建筑物和土壤等干扰。已被证明能够很好地提取水体,计算NDWI并采用标准逻辑阈值(W≥0[^①],W为水体)
>
>[^①]: 还是要根据实际影像更改阈值
>
>(2)$NDVI_{NIR/R}$对于 哨兵数据，东洞庭湖在平水期，0.05左右适用。

`操作使用`

点击`toolbox-->Band Algebra-->Band Math`

<img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240929_2239.png" style="zoom:67%;" />

> 输入函数$(float(b1)-float(b2))/(float(b1)+float(b2))$
>
> 点击OK后，并对$b1$, $b2$赋相应的波段

<p align="center">   <img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240929_2244.png" alt="Image Description 1" style="display:inline-block; zoom:60%; margin:10px;">   <img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240929_2249.png" alt="Image Description 2" style="display:inline-block; zoom:60%; margin:10px;">




输出结果：

<img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240929_2250.png" style="zoom:50%;" />

> 选中输出图层，右键选择`New Raster Color Slice`，点击Band Math波段，弹出颜色层后，点击${\underset{xx}{xx}}$删除所有颜色层，然后点击**+**添加
>
> 最后调整参数即可。

<p align="center">   <img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240929_2251.png" alt="Image Description 1" style="display:inline-block; zoom:50%; margin:10px;">   <img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240929_2259.png" alt="Image Description 2" style="display:inline-block; zoom:50%; margin:10px;">
<p align="center">   <img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240929_2303.png" alt="Image Description 1" style="display:inline-block; zoom:40%; margin:10px;">   <img src="https://cdn.jsdelivr.net/gh/Rpower666/pic@main/20240929_2310.png" alt="Image Description 2" style="display:inline-block; zoom:40%; margin:10px;">



