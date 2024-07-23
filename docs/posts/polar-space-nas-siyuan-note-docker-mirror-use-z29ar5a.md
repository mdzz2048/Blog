---
title: 【极空间 NAS】思源笔记 Docker 镜像使用
short_title: ''
date: 2023-10-23 07:08:50
tag:
  - Docker
  - NAS
article: true
timeline: false
isOriginal: true
---


<!-- more -->




截止至 2023 年 10 月 23 日，极空间的 Docker 还是只能使用以 root 用户运行的镜像，思源笔记官方镜像使用 siyuan 用户运行，因此不能直接使用。

目前极空间有[zsource/siyuan](https://hub.docker.com/r/zsource/siyuan)和[ylsislove/siyuan](https://hub.docker.com/r/ylsislove/siyuan)两个镜像可以用，但是前者很久没有更新了，后者最新镜像的只有 amd64 架构，arm 架构的停留在 2.9.9 版本，可能不能满足一些 Z2 和 Q2 用户的需求。

为了方便持有极空间 NAS 的思源用户使用，我重新构建了一份和官方镜像支持架构一致的镜像。项目地址在这里：[mdzz2048/siyuan at zspace](https://github.com/mdzz2048/siyuan/tree/zspace)，Docker 镜像在这里：[mdzz2048/siyuan](https://hub.docker.com/r/mdzz2048/siyuan)

## 使用说明

1. 在极空间 Docker 中搜索`mdzz2048/siyuan`​，下载对应的镜像

​![image](https://raw.githubusercontent.com/mdzz2048/blog/master/images/image-20231023151146-18fruvi.png)​

2. 点击创建容器，创建容器之后的 GUI 界面如果没有说明就是可以使用默认配置

​![image](https://raw.githubusercontent.com/mdzz2048/blog/master/images/image-20231023225134-opfgqli.png)​

3. 配置文件夹路径（这里直接使用了默认路径）

​![image](https://raw.githubusercontent.com/mdzz2048/blog/master/images/image-20231023221445-v4vjqpw.png)​

4. 设置端口（随便设置一个空闲的端口即可）

​![image](https://raw.githubusercontent.com/mdzz2048/blog/master/images/image-20231023223727-15e6nku.png)​

5. 设置鉴权码，这里是随便设置的（--accessAuthCode=123456）

​![image](https://raw.githubusercontent.com/mdzz2048/blog/master/images/image-20231023224731-85wl5xf.png)​

以上设置完成后就可以愉快的使用思源笔记了。
