# 雅文的工作台 - 静态站点部署清单

> 本项目为纯静态 HTML/CSS/JS，无需打包、无需 Node 构建，直接部署即可。

---

## 一、部署前准备

1. 确认项目目录结构完整：
   ```
   private-domain-workbench/
   ├── pages/               # 所有页面 HTML
   ├── colors_and_type.css  # 品牌样式变量
   ├── private-domain-workbench.design  # 设计项目文件
   └── assets/              # 图片等静态资源
   ```
2. 首页入口：`pages/index.html`
3. 可选：把项目文件夹压缩成 `private-domain-workbench.zip`（Vercel/Netlify 拖拽部署用）

---

## 二、Vercel 部署

### 方式 A：网页拖拽（最快，无需命令行）

1. 打开 [vercel.com](https://vercel.com) 并登录 GitHub/GitLab/Bitbucket 账号
2. 点击右上角 **"Add New..." → "Project"**
3. 选择 **"Import Git Repository"** 导入仓库；如果没有仓库，选择 **"Upload"** 直接上传文件夹
4. 上传 `private-domain-workbench` 文件夹
5. Framework Preset 选择 **Other**
6. Build Command 留空，Output Directory 留空（默认根目录）
7. 点击 **Deploy**
8. 部署完成后获得链接：`https://xxx.vercel.app`
9. 访问首页：`https://xxx.vercel.app/pages/index.html`

### 方式 B：Vercel CLI

```bash
# 1. 安装 Vercel CLI
npm i -g vercel

# 2. 进入项目目录
cd private-domain-workbench

# 3. 登录并部署
vercel --prod

# 4. 按提示选择作用域、确认目录
# 5. 部署完成后自动返回访问链接
```

### 自定义域名（可选）

1. 在 Vercel 项目控制台选择 **Settings → Domains**
2. 添加你的域名并按提示配置 DNS
3. 等待证书自动签发

---

## 三、Netlify 部署

### 方式 A：网页拖拽

1. 打开 [app.netlify.com](https://app.netlify.com) 并登录
2. 在 Sites 页面找到 **"Add new site" → "Deploy manually"**
3. 把 `private-domain-workbench` 文件夹直接拖到上传区域
4. 等待上传完成，自动生成 `https://xxx.netlify.app`
5. 访问首页：`https://xxx.netlify.app/pages/index.html`

### 方式 B：Netlify CLI

```bash
# 1. 安装 Netlify CLI
npm i -g netlify-cli

# 2. 进入项目目录
cd private-domain-workbench

# 3. 登录
netlify login

# 4. 初始化站点（首次）
netlify init

# 5. 部署到生产环境
netlify deploy --prod --dir=.

# 6. 获得访问链接
```

### 自定义域名（可选）

1. 进入 Netlify 项目 **Domain management**
2. 点击 **Add custom domain**
3. 配置 DNS 解析到 Netlify 提供的地址
4. 等待 HTTPS 证书自动签发

---

## 四、部署后检查项

- [ ] 首页 `pages/index.html` 能正常打开
- [ ] 左侧导航点击可跳转到各个子页面
- [ ] 浅色/深色主题切换正常
- [ ] 实时时钟、天气组件显示正常
- [ ] 个人待办、设置中心等新增页面可访问
- [ ] 手机端访问无横向滚动、按钮可点击
- [ ] localStorage 数据在刷新后仍保留

---

## 五、常见问题

**Q：页面打开后是空白或 404？**  
A：确认访问路径包含 `/pages/index.html`，因为首页不在根目录。

**Q：样式没生效？**  
A：检查 `colors_and_type.css` 是否随项目一起上传，且 pages 目录中的 HTML 已内联该 CSS。

**Q：想设置根目录自动跳转到首页？**  
Vercel：在项目根目录添加 `vercel.json`：
```json
{
  "routes": [
    { "src": "^/$", "dest": "/pages/index.html" }
  ]
}
```

Netlify：在项目根目录添加 `_redirects`：
```
/  /pages/index.html  301
```

---

## 六、项目文件说明

| 文件/目录 | 说明 |
| --- | --- |
| `pages/index.html` | 工作台首页 |
| `pages/todo.html` | 个人待办 |
| `pages/settings.html` | 设置中心 |
| `pages/daily-opportunity.html` | 每日商机数据 |
| `pages/weekly-deals.html` | 社群唤醒成单 |
| `pages/opportunity-assign.html` | 商机分配 |
| `pages/advisor-ranking.html` | 顾问转化排名 |
| `pages/content-library.html` | 社群图文素材库 |
| `pages/content-calendar.html` | 社群日历 |
| `pages/community-activity.html` | 社群活动 |
| `pages/points.html` | 积分激励 |
| `pages/profile.html` | 我的 |
| `colors_and_type.css` | 品牌色、字体、动画等设计令牌 |

---

生成时间：2026-08-18
