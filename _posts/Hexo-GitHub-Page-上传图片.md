---
title: Hexo GitHub Page 上传图片
date: 2020-03-29 11:27:07
tags: ['Hexo', 'GitHub Pages', 'Hexo 上传图片']
categories: ['Hexo 上传图片']
---

### 图片需要在文章和首页中 同时出现

{% asset_img big_image.jpg alert content %}

## 上传本地图片

### 使用相对路径

需要 配置 **/\_config.yml**
`post_asset_folder: true`
然后 执行命令 `hexo n post_name`
会在 **source/\_posts** 下面 出现一个 **post_name** 文件夹和 **post_name.md** 的文件
将图片存放在 **post_name** 文件夹 下面即可

使用

```
![](big_image.jpg)
```

![](big_image.jpg)

### 使用绝对路径

```
图片存储位置
source/images/2020-03-29/big_image.jpg
```

使用

```
![](/images/2020-03-29/big_image.jpg)
```

![](/images/2020-03-29/big_image.jpg)

## 添加网络图片

使用图床将图片上传至 图片服务器 [七牛云]()、[又拍云]() 、[阿里云]() 或其他的，获取到图片下载链接

使用

```
![](https://gb-imgs.oss-cn-beijing.aliyuncs.com/big_image.jpg)
```

![](https://gb-imgs.oss-cn-beijing.aliyuncs.com/big_image.jpg)
