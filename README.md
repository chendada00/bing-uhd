# Bing Wallpaper UHD

Bing Wallpaper 收藏系统的 UHD 高清原图仓库。

在线网站：

**https://bing.伴随.cn**

UHD 图片服务：

**https://bing-uhd.伴随.cn**

---

## 项目组成

整个 Bing Wallpaper 收藏系统由三个仓库组成：

### bing-wallpaper

前端网站：

```text
https://bing.伴随.cn
```

负责：

- 壁纸浏览
- 历史搜索
- 颜色搜索
- 详情页
- 高清查看
- 原图下载

### bing-data

数据仓库：

```text
https://bing-data.伴随.cn
```

负责：

- 壁纸 JSON
- 历史索引
- preview
- Base64
- 主色调
- HSV 颜色直方图

### bing-uhd

本仓库。

负责保存 UHD 高清原图。

---

## 仓库职责

本仓库只负责保存高清图片。

不保存：

- 月度 JSON
- 历史搜索索引
- preview
- Base64
- 颜色分析数据

这些内容由：

```text
chendada00/bing-data
```

负责。

---

## 目录结构

```text
bing-uhd/
│
├── images/
│   └── YYYY/
│       └── MM/
│           └── YYYY-MM-DD.jpg
│
└── README.md
```

例如：

```text
images/
└── 2026/
    └── 10/
        ├── 2026-10-01.jpg
        ├── 2026-10-02.jpg
        ├── 2026-10-03.jpg
        └── ...
```

---

## 图片规格

项目主要保存 Bing 官方 UHD 壁纸。

标准尺寸：

```text
3840 × 2160
```

即：

```text
16 : 9
```

每张图片使用日期作为文件名：

```text
YYYY-MM-DD.jpg
```

---

## 图片地址

图片通过独立域名提供：

```text
https://bing-uhd.伴随.cn
```

例如：

```text
https://bing-uhd.伴随.cn/images/2026/10/2026-10-08.jpg
```

---

## 数据中的图片关系

`bing-data` 中的壁纸记录包含三个主要图片地址：

```text
sourceImage
image
preview
```

其中：

### sourceImage

Bing 官方 UHD 原图地址。

```text
Bing 官方
```

### image

本仓库提供的稳定 UHD 镜像。

```text
bing-uhd.伴随.cn
```

### preview

网站浏览使用的预览图。

```text
bing-data.伴随.cn
```

因此：

```text
用户打开网站
    ↓
preview

用户查看高清
    ↓
sourceImage
    ↓
image 作为备用

用户下载
    ↓
image
    ↓
sourceImage 作为备用
```

---

## 图片更新

每日 Bing Wallpaper 更新任务运行于：

```text
chendada00/bing-data
```

GitHub Actions 获取当天壁纸后，将 UHD 原图写入本仓库：

```text
images/YYYY/MM/YYYY-MM-DD.jpg
```

然后提交到 `main` 分支。

本仓库本身不负责生成 JSON 数据。

---

## 历史图片

历史 UHD 图片通过历史数据修复任务补齐。

修复任务运行于：

```text
chendada00/bing-data
```

主要流程：

```text
历史资料
 ↓
获取官方 UHD 地址
 ↓
下载 UHD
 ↓
检查图片尺寸
 ↓
写入 bing-uhd
 ↓
更新 bing-data JSON
```

---

## 三个仓库之间的关系

```text
                  Bing
                   │
                   │
                   ▼
          ┌─────────────────┐
          │   bing-data     │
          │                 │
          │ JSON            │
          │ preview         │
          │ color           │
          │ histogram       │
          └───────┬─────────┘
                  │
          ┌───────┴─────────┐
          │                 │
          ▼                 ▼
 ┌─────────────────┐ ┌─────────────────┐
 │   bing-uhd      │ │ bing-wallpaper  │
 │                 │ │                 │
 │ UHD 原图        │ │ Vue 前端        │
 │                 │ │                 │
 └─────────────────┘ └─────────────────┘
```

在线服务：

```text
网站：
https://bing.伴随.cn

数据：
https://bing-data.伴随.cn

UHD：
https://bing-uhd.伴随.cn
```

---

## License

MIT
