# matplotlib图例中文乱码问题

## 下载中文字体

下载SimHei.ttf字体

## 添加字体到matplotlib字体文件夹

base环境目录为

/anaconda3/lib/python3.7/site-packages/matplotlib/mpl-data/fonts

其他环境目录为

/anaconda3/envs/env-name/lib/python3.7/site-packages/matplotlib/mpl-data/fonts

## 修改配置文件matplotlibrc

位置为matplotlib/mpl-data

取消注释

`font.family         : sans-serif`

取消注释，并添加SimHei

`font.sans-serif     : SimHei, DejaVu Sans, Bitstream Vera Sans, Computer Modern Sans Serif, Lucida Grande, Verdana, Geneva, Lucid, Arial, Helvetica, Avant Garde, sans-serif`

如果负号'-'显示为方块，则取消注释下面这行并修改为False

`axes.unicode_minus  : False`

## 重新加载字体

执行

`from matplotlib.font_manager import _rebuild`

`_rebuild()` 

也可以删除.matplotlib目录下的fontList.json和tex.cache