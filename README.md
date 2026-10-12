<div align="center">

# 🖥️ Bing Wallpaper UHD

**Bing 每日壁纸收藏系统的 UHD 高清图片镜像仓库**

[![Images](https://img.shields.io/badge/Assets-UHD_Images-5b8def)](https://github.com/chendada00/bing-uhd)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

🌐 **网站：** [bing.伴随.cn](https://bing.伴随.cn)  
🖥️ **UHD 图片服务：** [bing-uhd.伴随.cn](https://bing-uhd.伴随.cn)

</div>

------------------------------------------------------------------------

## 📌 仓库简介

`bing-uhd` 专门保存 Bing 每日壁纸的 UHD
高清图片镜像，为网站高清查看与下载提供独立的静态图片来源。

整个 Bing Wallpaper 系统由三个仓库组成：

| 仓库                                                             | 职责                                           |
|------------------------------------------------------------------|------------------------------------------------|
| [`bing-wallpaper`](https://github.com/chendada00/bing-wallpaper) | 前端页面、浏览、搜索、详情与下载               |
| [`bing-data`](https://github.com/chendada00/bing-data)           | JSON 数据、历史索引、预览图、Base64 与颜色分析 |
| **`bing-uhd`**                                                   | UHD 高清原图镜像                               |

## 🧱 仓库职责

本仓库主要保存：

- 🖼️ UHD 高清 JPEG 图片
- 🗓️ 按年份、月份与日期组织的历史图片

本仓库不负责保存：

- 月度 JSON 或 `data/index.json`
- `preview` 预览图
- Base64 占位数据
- 主色调与 HSV 颜色直方图

这些结构化数据和预览资源由
[`bing-data`](https://github.com/chendada00/bing-data) 维护。

## 📁 目录结构

``` text
bing-uhd/
├── images/
│   └── YYYY/
│       └── MM/
│           ├── YYYY-MM-DD.jpg
│           └── ...
└── README.md
```

例如：

``` text
images/
└── 2026/
    └── 10/
        ├── 2026-10-01.jpg
        ├── 2026-10-02.jpg
        └── ...
```

历史年份与月份会随着每日壁纸的积累继续增加。

## 📐 图片规格与命名

项目主要保存 Bing 官方提供的 UHD 壁纸。

- 常见尺寸：`3840 × 2160`
- 常见比例：`16:9`
- 文件格式：JPEG
- 文件命名：`YYYY-MM-DD.jpg`

图片尺寸以原始资源为准；如遇到特殊尺寸，应以实际文件信息为准，而不是假定每张图片都一定是相同分辨率。

## 🌐 图片访问地址

UHD 图片通过独立域名提供：

``` text
https://bing-uhd.伴随.cn
```

典型 URL：

``` text
https://bing-uhd.伴随.cn/images/YYYY/MM/YYYY-MM-DD.jpg
```

例如：

``` text
https://bing-uhd.伴随.cn/images/2026/10/2026-10-08.jpg
```

只有对应日期的文件实际存在时，URL 才能访问成功。

## 🔗 与 `bing-data` 的关系

`bing-data` 中的壁纸记录会引用不同用途的图片地址：

| 字段          | 含义                               |
|---------------|------------------------------------|
| `sourceImage` | Bing 官方原图地址                  |
| `image`       | 本仓库提供的 UHD 镜像地址          |
| `preview`     | `bing-data` 提供的网页预览图       |
| `base64`      | 用于占位和视觉效果的小尺寸图片数据 |

典型访问思路：

``` text
打开首页
   └─ preview / base64 占位

查看高清图片
   ├─ 尝试 sourceImage（Bing 官方原图）
   └─ 使用 image（本仓库镜像）作为备用来源

下载
   └─ 由前端按当前实现选择可用的高清来源
```

具体加载顺序和失败回退逻辑由 `bing-wallpaper`
前端决定；本仓库只负责提供图片文件，不负责前端逻辑。

## 🔄 图片更新与历史补齐

每日图片更新任务运行在
[`bing-data`](https://github.com/chendada00/bing-data) 仓库的 GitHub
Actions 中。工作流会检出本仓库，将新 UHD
图片写入对应目录，然后提交更新。

基本流程：

``` text
Bing 每日壁纸
      ↓
bing-data 的自动化工作流
      ↓
下载并检查 UHD 图片
      ↓
写入 images/YYYY/MM/YYYY-MM-DD.jpg
      ↓
提交并推送到 bing-uhd
```

历史图片的检查与修复同样由 `bing-data`
仓库中的维护脚本和工作流负责。本仓库本身不生成月度 JSON 或历史搜索索引。

### 自动更新所需权限

`bing-data` 的每日工作流使用 `BING_UHD_TOKEN` 检出并推送本仓库。该 Token
应配置在 `bing-data` 仓库的 Actions Secrets
中，并仅授予必要的仓库访问与写入权限。**不要将 Token 写入
README、源码或日志。**

## ⚡ 静态资源与缓存

本仓库以静态图片文件为主，适合由 GitHub Raw、CDN
或静态托管平台提供资源。若通过自定义域名 `bing-uhd.伴随.cn`
提供图片，建议在托管平台配置适合大图的缓存策略，并确认图片 URL 与
`bing-data` JSON 中的 `image` 字段保持一致。

图片更新频率相对较低，适合使用 CDN
缓存；若替换或修复了已存在的同路径文件，需要留意 CDN 缓存刷新策略。

## 🔗 相关链接

- 🌐 [在线网站](https://bing.伴随.cn)
- 🗂️ [bing-data 数据仓库](https://github.com/chendada00/bing-data)
- 🖼️ [bing-uhd 高清图片仓库](https://github.com/chendada00/bing-uhd)
- 💻 [bing-wallpaper
  前端仓库](https://github.com/chendada00/bing-wallpaper)

## 📄 License

本仓库使用 MIT License，详见仓库中的 `LICENSE` 文件。
