# The_Headmaster_CN_translate_pack
P站游戏 The Headmaster(Altos and Herdone) 的翻译工具包.

## 汉化交流群

971809199

### 如果出现错误应该如何提交，或者自定debug
[https://github.com/RedmondLee/TheHeadmaster_CN_translate_pack/blob/main/misc/readme.md#提交bug与修正错误的方法](https://github.com/RedmondLee/TheHeadmaster_CN_translate_pack/blob/main/misc/readme.md#提交bug与修正错误的方法)

### 如果您完全没有使用过Github，应该如何下载最新的汉化补丁
[https://github.com/RedmondLee/TheHeadmaster_CN_translate_pack/tree/main/misc#玩家如何下载最新汉化补丁](https://github.com/RedmondLee/TheHeadmaster_CN_translate_pack/tree/main/misc#玩家如何下载最新汉化补丁)

### 当前更新版本号
0.11.1

### 正确的目录配置
在开始工作前，你需要将游戏解包，并将本文件夹内的所有内容，替换`游戏目录/game/tl`文件夹下的所有内容。

### 正确的翻译脚本使用流程
```
0. pip install -r requirements.txt
安装依赖，需要python版本大于3.7

1. python note_translate_1_generate.py
提取行内文本

2. 备份
提取文本后，可以选择上传至github仓库，在面临版本更新时，可以使用git工具查看新增文档与原有文档的差异。

3. python note_translate_2_baiduapi.py
运行百度翻译api，将提取出的文本进行自动机翻。运行前需要先注册并填写自己的百度翻译权限key

4. 润色
改正看起来不像人类说出的话。

5. python note_translate_3_reduction.py
将翻译后的文本贴回脚本。
```

### 版本更新后检查图片差异的方法

由于部分文字被直接编入图片中，且本作图片数量庞大，这个脚本是为了方便版本更新后检查新增了哪些图片（有哪些图片在上一版本已经检查过，无需再次进行检查）

具体使用方法为，首先修改`image_translatino_helper.py`的头两行，第一行为当前更新后的版本，第二行为对比之前的版本（由于本次汉化不存在更早先版本，第二行可以填None）

之后执行`python image_translatino_helper.py`
该脚本会首先扫描当前目录下存在哪些文件，之后将这些文件与之前记录下的文件的哈希值进行对比，如果新版本新增/修改了某些图片，则会将这些图片复制到`tl/images_副本`目录下，由于每次更新新增图片不会很多，在该目录下可以比较方便地对比有哪些图片需要ps修图。将修正好的文件放入`tl/images`文件夹下即可。

应用举例 
```
1、由于本次为初次汉化，将py文件前两行改为'0.11.1'和None，脚本记录下当前所有图片哈希值即会结束。
2、若之后更新版本，比如更新为'0.12'，则将tl文件夹复制到新游戏文件夹中，修改前两行为'0.12'和'0.11.1'
  之后脚本会在储存0.12所有图片哈希的同时，对比这些哈希与0.11.1的差异，将差异部分复制到 tl/images_副本 文件夹中
```

### 有关图片上传至github

由于政策原因，汉化文件中暴露图片不宜直接在github中储存和预览，故上传时会执行`reverse_img.exe`对图片进行简单处理，将所有图片的二进制字节码反转（以字节为单位），使其不被github识别为一张图片。需要使用图片时双击执行`reverse_img.exe`将图片转回来即可。

如果执行`update.cmd`进行快速提交，会自动执行`.\reverse_img.exe --enc`进行加密。加密时会自动读文件头，如果已经翻转则不会翻转第二次。
