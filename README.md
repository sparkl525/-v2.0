# 简译 v2.0 素材仓库

简译（离线优先的英语学习 App）的阅读与听力素材仓库。App 只从这个仓库**下载**，不上传任何数据。

## 下载通道

App 实际走的是 jsDelivr CDN（国内访问比 GitHub 原生通道稳定）：

```
https://cdn.jsdelivr.net/gh/sparkl525/-v2.0@main/manifest.json
https://cdn.jsdelivr.net/gh/sparkl525/-v2.0@main/articles/r-002.txt
https://cdn.jsdelivr.net/gh/sparkl525/-v2.0@main/audio/l-002.mp3
```

> 注意：jsDelivr 对单个文件有 20MB 上限。VOA 单篇音频 2～4MB，远低于上限。
> 清单里的 `baseUrl` 字段就是上面这个前缀，App 用它拼相对路径下载。

## 目录结构

```
articles/r-00N.txt        英文正文
articles/r-00N.zh.txt     每篇一句中文梗概（不是全文对照）
articles/l-00N.lrc        听力字幕（LRC 格式，带逐句时间轴）
audio/l-00N.mp3           听力音频
manifest.json             素材索引（本仓库的说明书，App 不依赖它）
```

> App 用的清单（含 builtin 标记和相对路径）是**内置在 APK 里**的，启动时不联网拉清单，
> 只按内置清单去 CDN 下载缺失的素材文件。所以这里只需要保证**文件路径和文件名不变**。

## 内置与在线

APK 里只内置了 `r-001` 和 `l-001` 两篇，保证装完就能看到效果；
其余条目的 `builtin` 为 `false`，用户在设置里打开「素材包」开关后才会下载到手机，关闭则删除。

## manifest.json 字段说明

| 字段 | 说明 |
|---|---|
| id | 篇目唯一标识，下载后存本地的文件名 |
| title / titleZh | 英文标题 / 中文标题 |
| topic | 栏目，如「伊索寓言」「VOA 慢速英语」 |
| level | 难度：easy / normal / hard |
| words | 正文词数，用于显示篇幅和预估阅读时间 |
| builtin | true = 已打进 APK，不需要下载 |
| bytes / audioBytes | 文件字节数，App 用它显示下载大小 |
| text / translation / audio | 文件在仓库里的相对路径 |
| durationSec / sentences | 听力时长与句数（听力清单用） |
| source | 素材出处 |
| license | 授权类型 |

> 听力条目在同一个清单里，额外带 `durationSec`（时长秒数）和 `sentences`（句数）。

## 素材授权

- 本仓库只收录**公有领域**或**明确允许再分发**的内容
- 伊索寓言：古登堡计划 #21，public domain
- VOA 慢速英语：美国联邦政府作品（17 U.S.C. §105），属公有领域；
  音频与字幕抓自 21voa.com 的存量内容，该站已停更，仅作学习用途
- 不收录：受版权保护的新闻期刊、考试真题、商业播客

## 更新方式

由维护者在电脑上生成后提交（见 `tools/build_reading.py` / `tools/build_listening.py`），
App 拉清单后按 `id` 增量下载缺失的文件。
