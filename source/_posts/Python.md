---
title: 'Python实例:实现bing壁纸自动更新'
date: 2018-10-21 16:48:27
tags: python,壁纸
src: 
comments: true
---
 > Bing搜索每天都会有一张图片更新，而这些图片的质量都很高，很多人就想把他设置为电脑壁纸，但是一天换一张也是比较麻烦的，因此，今天我们使用Python来实现**每日自动更新Bing壁纸**
<!-- more -->
 * 准备:
 - Python 3.7 [download]
 [download]: python.org
 - requests模块(后续有安装教程)
 - 自动更换壁纸脚本

---
# 下载python并安装requests
## 下载python并安装
在上文链接中找到适合自己电脑版本的python程序，安装即可。

##安装requests
python3.6及以上自带pip，我们只需要打开cmd，输入以下命令即可。
``` 
  pip install requests

```
# 建立python及bat脚本
## 新建文本文件，命名为SetBingImageAsWallpaper.py，并输入下列内容。
``` python
import urllib.request
import requests         
import os.path
import ctypes

def save_img(img_url,dirname):
    #保存图片到磁盘文件夹dirname中
    try:
        if not os.path.exists(dirname):
            print ('文件夹',dirname,'不存在，重新建立')
            #os.mkdir(dirname)
            os.makedirs(dirname)
        #获得图片文件名，包括后缀
        basename = os.path.basename(img_url)
        #拼接目录与文件名，得到图片路径
        filepath = os.path.join(dirname, basename)
        #下载图片，并保存到文件夹中
        urllib.request.urlretrieve(img_url,filepath)
    except IOError as e:
        print ('文件操作失败',e)
    except Exception as e:
        print ('错误 ：',e)
    print("Save", filepath, "successfully!")

    return filepath

# 请求网页，跳转到最终 img 地址
def get_img_url(raw_img_url = "https://area.sinaapp.com/bingImg/"):
    r = requests.get(raw_img_url)       
    img_url = r.url # 得到图片文件的网址
    print('img_url:', img_url)
    return img_url

# 设置图片绝对路径 filepath 所指向的图片为壁纸
def set_img_as_wallpaper(filepath):
    ctypes.windll.user32.SystemParametersInfoW(20, 0, filepath, 0)

def main():
    dirname = "g:\\bingImg"       # 图片要被保存在的位置
    img_url = get_img_url()
    filepath = save_img(img_url, dirname)   # 图片文件的的路径
    set_img_as_wallpaper(filepath)

main()

```
其中你只需要更改倒数第五行的内容。（python中，路径的"\"必须改为"\\\")

## 新建一个名为Py_BingImg.bat的批处理文件，输入
```
@echo off
del g:\bingImg\*.jpg
python SetBingImgAsWallpaper.py
```
# 实现开机自动更改
## 复制上文中的bat文件，转至```C:\User\yourname\AppData\Roaming\Microsoft\Windows\开始菜单\程序\启动``` 右击选择粘贴快捷方式，这样，每次开机后就会自动运行批处理文件，删除昨天的壁纸文件并获取新壁纸。

