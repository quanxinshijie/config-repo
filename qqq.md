# 和宝贝机器人服务端切换https方案
## 1. 统一切换时间



## 2. 需要配合的服务
* 云平台
* 和宝贝APP端
* 和宝贝APP SDK端（安卓和IOS）
* 和宝贝H5
* 和宝贝机器人端
* 和宝贝机器人服务端

## 3. 切换方案

为了使新老用户使用体验一致。切换方案如下：

* 强制和宝贝APP和和宝贝机器人升级到最新版。
* 和宝贝机器人服务端必须保证新老环境数据的一致性：
  * 将已绑定的用户数据迁到新环境。
  * 每天同步旧环境的新绑定数据和读书相关数据到新环境。
  * 新机器只在新环境添加。
* 旧环境在没有访问量后逐渐退出服务生产环境的机器。

## 4. 各端修改详细列表
**各端对照这个表来修改：**

| 服务名称 |      需要修改的调用服务地址      |
|:----------:|:--------------|
| 移动云平台 | 机器人服务端：https://robot.andedu.net:9010/everobo<br>听听：https://robot.andedu.net:9010/FindBook/listenBook.html<br/>收藏的音乐：https://robot.andedu.net:9010/FindBook/listenCollect.html<br/>查书：https://robot.andedu.net:9010/FindBook/bookSeek.html<br/>书架：https://robot.andedu.net:9010/FindBook/bookshelf.html<br/>自制书：https://robot.andedu.net:9010/FindBook/bookMake.html |
| 和宝贝APP SDK端 |   机器人服务端：https://robot.andedu.net:9010/everobo   |
| 机器人端 |机器人服务端：https://robot.andedu.net:9010/everobo |
| H5 | 机器人服务端：https://robot.andedu.net:9010/everobo |



**各端提供的服务列表**：

| 服务名称 |      提供的服务地址      |
|:----------:|:-------------:|
| 移动云平台 | https://robot.andedu.net:9003/robsso<br/>https://robot.andedu.net:9003/robmanager |
| 和宝贝APP SDK端 |   N/A   |
| 机器人服务端 | https://robot.andedu.net:9010/everobo |
| 机器人端 | N/A |
| H5 | https://robot.andedu.net:9010/FindBook/listenBook.html<br/>https://robot.andedu.net:9010/FindBook/bookSeek.html<br/>https://robot.andedu.net:9010/FindBook/bookshelf.html<br/>https://robot.andedu.net:9010/FindBook/listenCollect.html<br/>https://robot.andedu.net:9010/FindBook/bookMake.html |


# 有问题的专辑统计

|类别id|类别名|有问题专辑数|
|:-:|:-:|:-:|
|1001|国学经典||
|1002|绘本讲读||
|1003|儿童故事||
|1004|儿童歌谣||
|1005|英语启蒙||
|1006|英语进阶||
|1007|教材配套||
|1008|长篇连载||
|1009|历史人文||
|1010|乐器启蒙||
|1011|性格养成||
|1012|生活百科||

## 每个类别有问题的专辑名称


|类别id|类别名|故事总数|有问题专辑数|专辑总数|
|:-:|:-:|:-:|:-:|:-:|
|1001|国学经典|13804|94|329|
|1002|绘本讲读|12327|42|189|
|1003|儿童故事|84204|538|1778|
|1004|儿童歌谣|11122|99|283|
|1005|英语启蒙|21190|282|597|
|1006|英语进阶|8990|119|215|
|1007|教材配套|3229|55|123|
|1008|长篇连载|2032|11|58|
|1009|历史人文|5584|44|97|
|1010|乐器启蒙|1203|6|21|
|1011|性格养成|1321|17|51|
|1012|生活百科|2561|10|50|
