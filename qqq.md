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



