# Cinnamon — 红云irch的肉桂卷

个人学习笔记在线浏览网站，基于 GitHub Pages 免费部署。

🌐 在线访问：<https://redcloud2696.github.io/Cinnamon/>

---

## 快速上手

### 1. 添加笔记

把 `.pdf` 和 `.one` 文件放入 `notes/` 对应文件夹：

```
notes/
└── 普通化学实验（乙）/
    ├── 实验一 基本操作.pdf
    └── 实验一 基本操作.one
```

- 同名 PDF + `.one`（或 `.pptx`）自动配对为一份笔记
- 支持无限层级文件夹

### 2. 配置别名（可选）

编辑 `subjects.json`，给文件夹加搜索别名：

```json
{
  "普通化学实验（乙）": ["普化实验", "普化实验乙"]
}
```

### 3. 生成索引并上传

```bash
node scripts/build-index.js   # 重新生成 notes-index.json
git add -A
git commit -m "添加笔记"
git push
```

推送后 GitHub Actions 会自动更新索引，约 1 分钟后网页更新。

---

## 本地预览（可选）

```bash
node scripts/build-index.js   # 生成索引
npx serve .                   # 启动本地服务器
```

---

## 文件说明

| 文件 | 用途 |
|------|------|
| `index.html` | 首页（单页应用，含序言与笔记浏览） |
| `comments.html` | 留言区页面（giscus） |
| `style.css` | 样式 |
| `app.js` | 前端逻辑 |
| `subjects.json` | 科目搜索别名 |
| `notes-index.json` | 自动生成，勿手动编辑 |
| `scripts/build-index.js` | 扫描 `notes/` 生成索引 |
| `summary/项目总览.md` | 项目结构、维护流程与注意事项 |

---

## 注意事项

- `notes/` 下的文件由 GitHub Pages 直接托管，**不要启用 Git LFS**——Pages 无法读取 LFS 指针文件，会导致下载按钮失效。
- 单个文件不得超过 GitHub 的 100 MB 硬限制（目前最大的是 `notes/普通化学实验（乙）/讲义/汇总.one`，约 83 MB）。
- 每次推送后 Actions 会重写 `notes-index.json`；本地推送被拒时先 `git pull --rebase` 再推。
