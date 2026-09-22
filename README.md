# 简译 v2.0 素材仓库

简译（离线优先的英语学习 App）的阅读/听力素材仓库。App 只从这个仓库**下载**，不上传任何数据。

## 下载通道

App 实际走的是 jsDelivr CDN（国内访问比 GitHub 原生通道稳定）：

```
https://cdn.jsdelivr.net/gh/sparkl525/-v2.0@main/manifest.json
https://cdn.jsdelivr.net/gh/sparkl525/-v2.0@main/articles/sample-001.txt
```

> 注意：jsDelivr 对单个文件有 20MB 上限，音频文件需要控制在这个体积以内
> （VOA 单篇压到 64kbps 单声道约 1.5～2.5MB，远低于上限）。

## 目录结构

```
manifest.json        篇目总清单，App 启动时拉取
articles/            英文正文（.txt）与中文译文（.zh.txt），同名配对
audio/               音频 mp3，按需下载
```

## manifest.json 字段说明

| 字段 | 说明 |
|---|---|
| id | 篇目唯一标识，下载后存本地的文件名 |
| title / titleZh | 英文标题 / 中文标题 |
| topic | 栏目，如「科技报道」 |
| level | 难度：easy / normal / hard |
| words | 正文词数，用于显示篇幅和预估阅读时间 |
| hasAudio / audioBytes | 是否有音频、音频字节数（App 用它显示下载大小） |
| text / translation / audio | 三个文件在仓库里的相对路径 |
| license | 授权类型 |

## 素材授权

- 本仓库只收录**公有领域**或**明确允许再分发**的内容
- 目前收录：古登堡计划的伊索寓言（public domain）
- 计划收录：VOA Learning English（美国政府作品，属公有领域）
- 不收录：受版权保护的新闻期刊、考试真题、商业播客

## 更新方式

由维护者在电脑上生成后提交，App 每次启动比对 `updated` 字段决定是否重新拉清单。
