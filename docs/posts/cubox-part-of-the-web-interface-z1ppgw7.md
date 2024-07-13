---
title: Cubox 部分网页接口
short_title: ''
date: 2022-12-20 10:13:20
tag:
  - 工作流
  - 网页抓包
article: true
timeline: false
isOriginal: true
---


<!-- more -->


本文分享通过抓包获得的 Cubox 网页接口，涵盖 Cubox 网页端可能进行的大部分操作。为避免歧义 Cubox 登录后以卡片形式展示的内容在下文均以“卡片”指代。



**请求类型**：POST 请求

**请求链接**：https://cubox.pro/c/api/login

**参数说明**：

* **userName**：用户名
* **password**：用户密码，需要进行 MD5 加密
* **autoLogin**：是否自动登录

**请求头**：

添加`content-type`​​​为`application/x-www-form-urlencoded`​​​

**请求体**：

​`userName=用户名&password=用户密码&autoLogin=自动登录`​​

**返回值**：

```js
{
  "message": "login success",
  "code": 200,
  "data": null,
  "token": "用于后续鉴权",
  "userId": "用户ID"
}
```

# 卡片操作

## 获取卡片列表

**请求类型**：GET 请求

**请求链接**：`URL`​​ + `?asc=false&page=1&filters=&archiving=false`​​

**参数说明**：

* **asc**：按创建时间日期，从新到旧
* **page**：页码（一页最多 49 个）
* **filters**：0: 文章、网页, 1: 片段, 2: 速记, 3: 图片, 4: 语音, 5: 视频, 6: 文件
* **archiving**：是否在归档卡片中搜索，是的话将会返回归档卡片的列表，不含未归档的卡片
* **starTarget**：星标卡片（默认不含该参数）
* **tagId**：使用指定标签卡片（默认不含该参数），未指定 id 会返回所有无标签卡片
* **groupId**：指定收藏夹卡片（默认不含该参数）

**URL 说明**

* 收集箱 URL：https://cubox.pro/c/api/v2/search_engine/inbox
* 所有 URL：https://cubox.pro/c/api/v2/search_engine/my
* 今日 URL：https://cubox.pro/c/api/search_engine/today
* 星标 URL：https://cubox.pro/c/api/v2/search_engine/my?starTarget=true
* 标签 URL：https://cubox.pro/c/api/v2/search_engine/my?tagId=标签ID
* 收藏夹 URL：https://cubox.pro/c/api/v2/search_engine/my?groupId=收藏夹ID

## 获取卡片信息

**请求类型**：POST 请求

**请求链接**：

* https://cubox.pro/c/api/search_engine/visit/卡片ID
* https://cubox.pro/c/api/v2/bookmark/detail?bookmarkId=卡片ID

**请求体**：无请求体

**返回值**：

```js
{
  "message": "",
  "code": 200,
  "data": {
    "userSearchEngineID": "ff80808184793cdd01847b3e6be1422e",
    "title": "标题",
    "description": "简述",
    "targetURL": "原文链接",
    "resourceURL": null,
    "homeURL": "mp.weixin.qq.com",
    "archiveName": "archive/1668515023709/243525.html",
    "content": "剪藏内容 HTML",
    "articleName": "unAYy3",
    "articleWordCount": 2587,
    "byline": "原文作者",
    "cover": "surface/2022111520231896973/70906.jpg",
    "articleURL": null,
    "littleIcon": "http://mp.weixin.qq.com/favicon.ico",
    "archiving": false,
    "starTarget": null,
    "hasMark": false,
    "isRead": true,
    "markCount": 0,
    "tags": [
      {
        "tagID": "ff808081847930d401847b52dcaf5bc1",
        "name": "标签名",
        "rank": 3,
        "updateTime": "2022-11-15T21:07:59:033+08:00",
        "parentId": null
      }
    ],
    "allTags": [],
    "marks": [],
    "groupId": "ff8080817e05ac27017e06c64fed0def",
    "groupName": "",
    "createTime": "2022-11-15T20:23:18:937+08:00",
    "updateTime": "2022-11-15T21:07:59:033+08:00",
    "status": "Updated",
    "finished": true,
    "inBlackOrWhiteList": false,
    "type": 0
  }
}
```

## 获取卡片原文及标注

**请求类型**：GET 请求

**请求链接**：https://cubox.pro/c/api/bookmark/content?bookmarkId=卡片ID

**返回值**：

```js
{
    "message": "",
    "code": 200,
    "data": {
        "marks": [
            {
                "markID": "ff80808184acf0460184bb88db773f16",
                "startParentTagName": "SPAN",
                "startTextOffset": 8,
                "startParentIndex": 63,
                "endParentTagName": "SPAN",
                "endTextOffset": 28,
                "endParentIndex": 68,
                "index": 0,
                "text": "标注文本",
                "createTime": "2022-11-28T08:00:19:319+08:00",
                "updateTime": "2022-11-28T08:00:38:401+08:00",
                "engineID": "ff80808184a8c17f0184aa51f7137637",
                "noteText": "标注笔记",
                "links": null,
                "type": 0,
                "ratio": null,
                "url": null,
                "cover": null,
                "isPrivate": false,
                "status": null
            },
            {
                "markID": "ff80808184acf6880184bb8bbf01426c",
                "startParentTagName": "IMG",
                "startTextOffset": 0,
                "startParentIndex": 5,
                "endParentTagName": "IMG",
                "endTextOffset": 0,
                "endParentIndex": 5,
                "index": 0,
                "text": "",
                "createTime": "2022-11-28T08:03:28:641+08:00",
                "updateTime": "2022-11-28T08:03:57:016+08:00",
                "engineID": "ff80808184a8c17f0184aa51f7137637",
                "noteText": "",
                "links": null,
                "type": 0,
                "ratio": null,
                "url": "图片 URL",
                "cover": null,
                "isPrivate": false,
                "status": null
            },
        ],
        "content": "卡片 HTML 内容"
    }
}
```

# 标签操作

## 更新文档标签

**注意**：

这个请求发送的标签会覆盖原有标签，可以使用未创建的标签

**请求类型**：POST 请求

**请求链接**：https://cubox.pro/c/api/v3/search_engine/update

**请求头**：

添加`content-type`​​​为`application/x-www-form-urlencoded`​​​

**请求体**：

​`userSearchEngineID=卡片的ID&linkedTagNames=[{"name":"标签的名字"}]`​​​

**返回值**：

```
{
  "message": "",
  "code": 200,
  "data": {
    "userSearchEngineID": "ff808081842cc4c1018454d193d735d1",
    "title": "标题",
    "description": "简述",
    "targetURL": "原文链接",
    "resourceURL": null,
    "homeURL": "mp.weixin.qq.com",
    "archiveName": "archive/1667870336862/595265.html",
    "content": "剪藏内容 HTML",
    "articleName": "3repjS",
    "articleWordCount": 2151,
    "byline": "文章作者",
    "cover": "surface/2022110809185127032/14815.jpg",
    "articleURL": null,
    "littleIcon": "http://mp.weixin.qq.com/favicon.ico",
    "archiving": false,
    "starTarget": null,
    "hasMark": false,
    "isRead": false,
    "markCount": 0,
    "tags": [
      {
        "tagID": "ff8080818479358001847b60518921b1",
        "name": "标签名",
        "rank": 5,
        "updateTime": "2022-11-15T21:03:56:023+08:00",
        "parentId": null
      }
    ],
    "allTags": [
      {
        "tagID": "ff8080818479358001847b60518921b1",
        "name": "标签名",
        "rank": 5,
        "createTime": "2022-11-15T21:00:20:740+08:00",
        "updateTime": "2022-11-15T21:00:20:740+08:00",
        "state": 1,
        "bookmarkCount": null,
        "parentId": null
      }
    ],
    "marks": [],
    "groupId": "ff8080817e05ac27017e06c64fed0def",
    "groupName": "",
    "createTime": "2022-11-08T09:18:51:470+08:00",
    "updateTime": "2022-11-15T21:03:56:023+08:00",
    "status": "Updated",
    "finished": true,
    "inBlackOrWhiteList": false,
    "type": 0
  }
}
```

## 批量更新文档标签

**请求类型**：POST 请求

**请求链接**：https://cubox.pro/c/api/v2/search_engines/updateTagsForName

**请求头**：

添加`content-type`​​​​为`application/x-www-form-urlencoded`​​​​

**请求体**：

​`searchEngineIds="卡片ID,卡片ID"&deleteTagIds="删除标签ID,删除标签"&addLinkedTagNames=[{"name":"标签的名字"}]`​​​

**返回值**：

```js
{
  "message": "",
  "code": 200,
  "data": {
    "tags": [
      {
        "tagID": "添加标签的ID",
        "name": "添加标签的标签名",
        "rank": 10,
        "createTime": "2022-11-25T20:57:27:134+08:00",
        "updateTime": "2022-11-25T21:40:53:854+08:00",
        "state": 1,
        "bookmarkCount": null,
        "parentId": null
      }
    ],
    "searchEngines": [
      {
        "userSearchEngineID": "文档一ID",
        "title": null,
        "description": null,
        "targetURL": null,
        "resourceURL": null,
        "homeURL": null,
        "archiveName": null,
        "content": null,
        "articleName": null,
        "articleWordCount": 0,
        "byline": "",
        "cover": null,
        "articleURL": null,
        "littleIcon": null,
        "archiving": null,
        "starTarget": null,
        "hasMark": null,
        "isRead": null,
        "markCount": null,
        "tags": [
          {
            "tagID": "添加标签的ID",
            "name": "添加标签的标签名",
            "rank": 10,
            "updateTime": null,
            "parentId": null
          }
        ],
        "allTags": [],
        "marks": [],
        "groupId": null,
        "groupName": null,
        "createTime": null,
        "updateTime": null,
        "status": null,
        "finished": null,
        "inBlackOrWhiteList": null,
        "type": 0
      }
    ]
  }
}
```

## 获取标签列表

**请求类型**：GET 请求

**请求链接**：https://cubox.pro/c/api/v2/tag/list

**返回值**：

```js
{
  "message": "",
  "code": 200,
  "data": {
    "hasNoTagEngineCount": 640,
    "tagList": [
      {
        "tagID": "标签ID",
        "name": "标签名",
        "rank": 0,	# 标签序号
        "createTime": null,
        "updateTime": null,
        "state": null,
        "bookmarkCount": 0,	# 标记数量
        "parentId": null
      },
      {
        "tagID": "标签ID",
        "name": "标签名",
        "rank": 1,	# 标签序号
        "createTime": null,
        "updateTime": null,
        "state": null,
        "bookmarkCount": 1,	# 标记数量
        "parentId": null
      }
    ]
  }
}
```

## 获取最近使用标签列表

**请求类型**：GET 请求

**请求链接**：https://cubox.pro/c/api/tag/use/recent

**返回值**：

```js
{
  "message": "",
  "code": 200,
  "data": [
    {
      "tagID": "ff8080818479358001847b60518921b1",
      "name": "标签1",
      "link": null
    },
    {
      "tagID": "ff80808184793cdd01847bcc40241841",
      "name": "标签2",
      "link": null
    },
    {
      "tagID": "ff808081847930d401847bcb946348a5",
      "name": "标签3",
      "link": null
    },
    {
      "tagID": "ff808081847930d401847b52dcaf5bc1",
      "name": "标签4",
      "link": null
    },
    {
      "tagID": "ff8080818479358001847b586eda192b",
      "name": "标签5",
      "link": null
    }
  ]
}
```

## 新建标签

**请求类型**：POST 请求

**请求链接**：https://cubox.pro/c/api/v2/tag/new

**请求头**：

添加`content-type`​​​为`application/x-www-form-urlencoded`​​​

**请求体**：

​`linkedName=标签名`​​

可选参数：`parentId=父标签ID`​​​

**返回值**：

```js
{
  "message": "",
  "code": 200,
  "data": [
    {
      "tagID": "ff8080818479358001847b60518921b1",
      "name": "标签6",
      "rank": 5,	# 第六个标签
      "createTime": "2022-11-15T21:00:20:740+08:00",
      "updateTime": "2022-11-15T21:00:20:740+08:00",
      "state": 1,
      "bookmarkCount": null,
      "parentId": null
    }
  ]
}
```

## 删除标签

**注意**：该操作会删除标签及标签下的子标签

**请求类型**：POST 请求

**请求链接**：https://cubox.pro/c/api/tags/delete

**请求体**：

​`ids=标签ID`​​​或

```js
{
    "ids": 标签ID	# List，或使用","分隔的 String
}
```

**返回值**：

```js
{
  "message": "",
  "code": 200,
  "data": null
}
```

## 重命名标签

**请求类型**：POST 请求

**请求链接**：https://cubox.pro/c/api/tag/update

**请求体**：

​`id=标签ID&name=新标签名`​​​或

```js
{
    "id": 标签ID,
    "name": 标签名
}
```

**返回值**：

```js
{
  "message": "",
  "code": 200,
  "data": {
    "tagID": "标签ID",
    "name": "标签名",
    "rank": 0,
    "createTime": "2022-11-25T20:39:29:271+08:00",
    "updateTime": "2022-11-25T20:42:18:017+08:00",
    "state": 1,
    "bookmarkCount": null,
    "parentId": "父标签ID"
  }
}
```

## 合并标签

**注意**：该操作会将被合并标签的子标签也一并合并

**请求类型**：POST 请求

**请求链接**：https://cubox.pro/c/api/tag/merge

**请求体**：

​`mergedTagId="目标标签ID"&mergeTagIds="标签一ID,标签二ID"`​​​或

```js
{
    "mergedTagId": merged_tag_id,
    # 单标签：String
    # 多标签：List，或使用","分隔的 String
    "mergeTagIds": merge_tag_ids
}
```

**返回值**：

```js
{
  "message": "",
  "code": 200,
  "data": [
    {
      "tagID": "目标标签ID",
      "name": "目标标签名",
      "rank": 8,
      "createTime": "2022-11-25T20:39:18:622+08:00",
      "updateTime": "2022-11-25T20:39:18:622+08:00",
      "state": 1,
      "bookmarkCount": null,
      "parentId": null
    }
  ]
}
```

## 移动标签

**请求类型**：POST 请求

**请求链接**：https://cubox.pro/c/api/tag/move

**请求体**：

​`movedTagId="目标标签ID"&moveTagIds="标签一ID,标签二ID"`​​​或

```js
{
    "movedTagId": 目标标签ID,
    "moveTagIds": [
        "标签一ID"
    ]
}
```

**返回值**：

```js
{
  "message": "",
  "code": 200,
  "data": [
    {
      "tagID": "被移动标签ID",
      "name": "标签名",
      "rank": 0,
      "createTime": "2022-11-25T20:39:18:622+08:00",
      "updateTime": "2022-11-25T20:54:49:899+08:00",
      "state": 1,
      "bookmarkCount": null,
      "parentId": "目标标签ID"
    }
  ]
}
```

## 标签归类

**请求类型**：POST 请求

**请求链接**：https://cubox.pro/c/api/tag/sort

**请求体**：

​`targetPriorBrotherId`​​​和`targetParentId`​​​选填一个，都为空会将标签移到标签树顶端

​`sourceTagId="被移动的标签ID"&targetPriorBrotherId="移动到该标签后"`​​​或

​`sourceTagId="被移动的标签ID"&targetParentId="移动到该标签下"`​​​或

```js
{
    "sourceTagId": "被移动的标签ID",
    "targetPriorBrotherId": "移动到该标签后",
    "targetParentId": "移动到该标签下"
}
```

**返回值**：

该方法返回被移动标签及该标签后的所有同级标签

```js
{
  "message": "",
  "code": 200,
  "data": [
    {
      "tagID": "被移动标签的ID",
      "name": "被移动标签名",
      "rank": 0,
      "createTime": "2022-11-26T00:00:00:470+08:00",
      "updateTime": "2022-11-26T00:15:52:189+08:00",
      "state": 1,
      "bookmarkCount": null,
      "parentId": "被移动标签的父标签ID"
    },
    {
      "tagID": "被移动标签的同级标签ID",
      "name": "被移动标签的同级标签名",
      "rank": 1,
      "createTime": "2022-11-25T23:50:09:670+08:00",
      "updateTime": "2022-11-26T00:15:40:569+08:00",
      "state": 1,
      "bookmarkCount": null,
      "parentId": "ff80808184acf2d60184af85297107fe"
    }
  ]
}
```

# 标注操作

## 获取最近标注文档

**请求类型**：GET 请求

**请求链接**：https://cubox.pro/c/api/mark/search_engine/latest

**返回值**：

**注意**：该方法仅返回最后高亮的九篇文章

```js
{
  "message": "Get SearchEngine successfully",
  "code": 200,
  "data": [
    {
      "userSearchEngineID": "ff8080818484e31b018485f7e80d273e",
      "title": "文章标题",
      "description": "文章摘要",
      "targetURL": "文章链接",
      "resourceURL": null,
      "homeURL": "mp.weixin.qq.com",
      "archiveName": null,
      "content": "",
      "articleName": null,
      "articleWordCount": 0,
      "byline": "",
      "cover": "surface/2022111722220619093/98525.jpg",
      "articleURL": null,
      "littleIcon": "http://mp.weixin.qq.com/favicon.ico",
      "archiving": false,
      "starTarget": false,
      "hasMark": true,
      "isRead": null,
      "markCount": 2,
      "tags": [],
      "allTags": [],
      "marks": [],
      "groupId": "ff8080817e05ac27017e06c64fed0def",
      "groupName": "",
      "createTime": "2022-11-17T22:22:06:944+08:00",
      "updateTime": "2022-11-18T23:30:40:924+08:00",
      "status": "normal",
      "finished": null,
      "inBlackOrWhiteList": false,
      "type": 0
    }
  ]
}
```

## 获取标注列表

**请求类型**：GET 请求

**请求链接**：https://cubox.pro/c/api/v2/mark

**请求参数**：`?asc=false&filters=`​​​

* **asc**：按创建时间日期，从新到旧
* **lastTimestamp**：最后标注时间（上一个请求最后一个的创建时间，初次请求时不需要这个参数）
* **filters**：0: 文章、网页, 1: 片段, 2: 速记, 3: 图片, 4: 语音, 5: 视频, 6: 文件

**返回值**：

```js
{
  "message": "",
  "code": 200,
  "data": [
    {
      "markID": "ff808081848a0ab901848b5d089c45de",
      "startParentTagName": "IMG",
      "startTextOffset": 0,
      "startParentIndex": 5,
      "endParentTagName": "IMG",
      "endTextOffset": 0,
      "endParentIndex": 5,
      "index": 0,
      "text": "",
      "createTime": "2022-11-18T23:30:40:924+08:00",
      "updateTime": "2022-11-18T23:30:40:924+08:00",
      "engineID": "ff8080818484e31b018485f7e80d273e",
      "noteText": "",
      "links": null,
      "type": 1,
      "ratio": 1.3274216,
      "url": "封面图链接",
      "cover": "",
      "isPrivate": false,
      "searchEngine": {
        "userSearchEngineID": "ff8080818484e31b018485f7e80d273e",
        "title": "文章标题",
        "description": "文章摘要",
        "targetURL": "文章链接",
        "resourceURL": null,
        "homeURL": "mp.weixin.qq.com",
        "archiveName": null,
        "content": null,
        "articleName": "yhgeOp",
        "articleWordCount": 0,
        "byline": "",
        "cover": "surface/2022111722220619093/98525.jpg",
        "articleURL": null,
        "littleIcon": "http://mp.weixin.qq.com/favicon.ico",
        "archiving": false,
        "starTarget": false,
        "hasMark": true,
        "isRead": null,
        "markCount": null,
        "tags": [],
        "allTags": [],
        "marks": [],
        "groupId": "ff8080817e05ac27017e06c64fed0def",
        "groupName": "",
        "createTime": "2022-11-17T22:22:06:944+08:00",
        "updateTime": "2022-11-18T23:30:40:924+08:00",
        "status": "normal",
        "finished": null,
        "inBlackOrWhiteList": null,
        "type": 0	# 卡片类型，0 为文章
      }
    }
  ],
  "pageCount": 3,	# 总共几页
  "totalCounts": 135	# 总共有几条高亮
}
```

# 导出操作

## 导出文件

**请求类型**：POST 请求

**请求链接**：https://cubox.pro/c/api/search_engines/export/text

**请求体**：

​`engineIds=卡片的ID&type=导出类型&snap=false`​

* **engineIds**：卡片的 ID
* **type**：导出的类型

  * 纯文本：text
  * HTML：html
  * MarkDown：md

**返回值**：

```js
{
  "message": "",
  "code": 200,
  "data": "导出内容"
}
```

# 网页操作

## 添加网页

**请求类型**：POST

**请求链接**：https://cubox.pro/c/api/v2/search_engine/new

**参数说明**：

```go
type: 0
title: article title
description: article desc
targetURL: article url
```

**返回值**：

```go
{
    "message": "",
    "data": {
        "userSearchEngineID": "7096217623314039634",
        "title": "为什么要避免在 Go 中使用 ioutil.ReadAll？",
        "description": "据说是一颗定时炸弹？",
        "targetURL": "https://mp.weixin.qq.com/s/e2A3ME4vhOK2S3hLEJtPsw",
        "resourceURL": "",
        "homeURL": "mp.weixin.qq.com",
        "archiveName": "archive/fail.html",
        "content": null,
        "articleName": null,
        "articleWordCount": 0,
        "byline": "",
        "cover": "",
        "articleURL": null,
        "littleIcon": "https://res.wx.qq.com/a/wx_fed/assets/res/NTI4MWU5.ico",
        "archiving": false,
        "starTarget": false,
        "hasMark": false,
        "isRead": false,
        "markCount": 0,
        "tags": [],
        "marks": null,
        "groupId": "7095099423725718692",
        "groupName": "收集箱",
        "createTime": "2023-08-29T23:08:20:346+08:00",
        "updateTime": "2023-08-29T23:08:20:346+08:00",
        "status": null,
        "finished": false,
        "inBlackOrWhiteList": false,
        "type": 0
    },
    "code": 200,
    "token": null,
    "userId": null,
    "pageCount": 0,
    "totalCounts": 0
}
```

## 获取网页信息

**请求类型**：POST

**请求链接**：https://cubox.pro/c/api/v2/search_engine/webInfo

**参数说明**：

```go
url=you_url
```

**返回值**：

```go
{
    "message": "",
    "data": {
        "url": "https://zhuanlan.zhihu.com/p/453999587",
        "title": "为什么要避免在 Go 中使用 ioutil.ReadAll？ - 知乎",
        "description": "原文链接： 为什么要避免在 Go 中使用 ioutil.ReadAll？ ioutil.ReadAll 主要的作用是从一个 io.Reader 中读取所有数据，直到结尾。 在 GitHub 上搜索 ioutil.ReadAll，类型选择 Code，语言选择 Go，一共得到了 63…",
        "covers": [],
        "tags": [
            "数据",
            "类型",
            "搜索",
            "读取",
            "结尾"
        ]
    },
    "code": 200,
    "token": null,
    "userId": null,
    "pageCount": 0,
    "totalCounts": 0
}
```

## 判断是否存在

**请求类型**：GET

**请求链接**：https://cubox.pro/c/api/bookmark/exist

**参数说明**：

```go
targetURL=you_url
```

**返回值**：

```go
{
    "message": "",
    "data": {
        "exist": true,
        "bookmarkId": "7096215861354038991"
    },
    "code": 200,
    "token": null,
    "userId": null,
    "pageCount": 0,
    "totalCounts": 0
}
```
