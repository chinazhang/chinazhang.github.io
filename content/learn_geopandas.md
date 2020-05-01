Title: 学习geopandas
Date: 2020-05-01 22:19
Modified: 2020-05-01 22:20
Category: learn
Tags: geopandas
Slug: learn

# 一、geopandas install use pip

按https://geopandas.org/install.html网址安装依赖 numpy,pandas,shapely,fiona,pyproj,six,matplotlib,descartes

没有使用 Anaconda 是因为我使用它安装失败了，而且完整的 Anaconda 太大了，占了我3个G的空间

- 安装fiona时，使用了https://www.lfd.uci.edu/~gohlke/pythonlibs网址下的whl包，安装了GDAL和fiona。包名如下
GDAL-3.0.4-cp36-cp36m-win_amd64.whl，Fiona-1.8.13-cp36-cp36m-win_amd64.whl。36是指我电脑安装的python版本是python3.6。
安装命令为
```
pip install Fiona-1.8.13-cp36-cp36m-win_amd64.whl
```

备忘一下setup.py安装方法
```
python setup.py build
python setup.py install
```


- 后续进行数据可视化时，需要用到scheme参数，需要安装mapclassify，依赖包有scipy,scikit-learn


# 二、相关使用

- 依赖包导入
```
import geopandas as gp
import matplotlib.pyplot as plt
import pandas as pd
```

- IO
pandas 使用 read_excel 和 read_csv来读取 Excel和csv格式的文件。usecols筛选列。（后续需要学一下直接读压缩包内的数据）

geopandas 使用 read_file 读取地图文件。
http://datav.aliyun.com/tools/atlas/#&lat=31.840232667909365&lng=104.2822265625&zoom=4 上可以下载我国地图的json文件

```
sitesdata = pd.read_excel('E:\geopandas_try\sitedata.xlsx', sheet_name='Sheet1')
kpidata = pd.read_csv('E:\geopandas_try\omc7_lte_cell_kpi_day_20200408.csv', usecols = ['ECGI','下行流量MB','上行流量MB'])
shanghai = gp.read_file('E:\上海市.json')
```

- 撒点作图需要相同的CRS坐标系，merge可以连接两个表，loc表示了连接后的结果的列
```
gdf = gp.GeoDataFrame(sitesdata, geometry=gp.points_from_xy(sitesdata.经度, sitesdata.纬度), crs="EPSG:4326")
kpi_with_geometry = pd.merge(left=kpidata,right=gdf,left_on='ECGI',right_on='CGI',how='right').loc[:,['ECGI','下行流量MB','上行流量MB','geometry']]
kpi_with_geometry = gp.GeoDataFrame(kpi_with_geometry, crs="EPSG:4326")
```

- pandas的concat可以合并读入的多个表格
```
result = pd.concat([pd.read_csv('file_0.csv'),pd.read_csv('file_1.csv'), pd.read_csv('file_2.csv')], ignore_index = True)
```

- 撒点作图，scheme选择不同的数据分段算法
```
fig, ax = plt.subplots()
shanghai.plot(ax=ax, color = 'white' ,edgecolor = 'black')
kpi_with_geometry.plot(ax=ax, column='下行流量MB', cmap = 'Reds', legend = True, scheme='NaturalBreaks', k = 5)

plt.show()
```



参考链接：
https://geopandas.org
https://www.cnblogs.com/feffery/

python依赖包下载链接：
https://www.lfd.uci.edu/~gohlke/pythonlibs
https://pypi.org/
