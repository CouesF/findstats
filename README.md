# Find Your Stats · 统计检验检索表

一个单文件的静态网页：回答几个问题找到该用的统计检验，每种方法附前提、效应量、报告格式和 Python / R 代码，另有基础知识页。

整个网站就是 `index.html` 一个文件，不需要构建、不需要服务器，双击就能在本地打开。

## 用 GitHub Pages 部署（网页操作，约 5 分钟）

1. 登录 GitHub，右上角 **+ → New repository**。
   - Repository name 填 `findyourstats`（随意）
   - 选 **Public**（免费账号的 Pages 只支持公开仓库）
   - 点 **Create repository**
2. 在新仓库页面点 **uploading an existing file**，把 `index.html` 和 `README.md` 拖进去，点 **Commit changes**。
3. 进入仓库的 **Settings → Pages**：
   - Build and deployment → Source 选 **Deploy from a branch**
   - Branch 选 **main**，目录选 **/ (root)**，点 **Save**
4. 等 1–2 分钟，页面顶部会出现网址：`https://<你的用户名>.github.io/findyourstats/`

以后改内容：在仓库里点开 `index.html` → 右上角铅笔图标编辑 → Commit，1 分钟左右网站自动更新。

## 用命令行部署

```bash
git init
git add index.html README.md .nojekyll
git commit -m "Find Your Stats"
git branch -M main
git remote add origin https://github.com/<你的用户名>/findyourstats.git
git push -u origin main
```

然后按上面第 3 步打开 Pages。

## 绑定自己的域名（例如 findyourstats.com）

1. 在域名注册商买好域名。
2. 仓库 **Settings → Pages → Custom domain** 填 `findyourstats.com`，点 Save（GitHub 会在仓库里自动生成一个 `CNAME` 文件）。
3. 到域名的 DNS 设置里添加记录：

   | 类型 | 主机记录 | 值 |
   |---|---|---|
   | A | @ | 185.199.108.153 |
   | A | @ | 185.199.109.153 |
   | A | @ | 185.199.110.153 |
   | A | @ | 185.199.111.153 |
   | CNAME | www | `<你的用户名>.github.io` |

4. DNS 生效后（几分钟到几小时），回到 Pages 设置勾选 **Enforce HTTPS**。
5. 建议在 GitHub 个人 **Settings → Pages** 里验证这个域名，防止别人抢先把它绑到自己的仓库。

用二级域名（如 `stats.example.com`）时，只需要一条 CNAME：`stats` → `<你的用户名>.github.io`。

## 国内访问

`github.io` 在国内有时较慢。同一个仓库可以再接到 Cloudflare Pages（免费）：登录 Cloudflare → Workers & Pages → Create → Pages → 连接 GitHub 仓库，构建命令留空、输出目录填 `/`，即可得到 `*.pages.dev` 网址并绑定域名。

页面字体来自 Google Fonts；如果加载不到，会自动使用系统自带的中文字体，功能不受影响。

## 怎么改内容

全部内容都在 `index.html` 底部的 `<script>` 里：

- `TESTS`：每种检验的说明、前提、效应量、报告示例、Python / R 代码
- `TREE`：检索表的问题和选项。选项格式是 `["选项文字", "补充说明", "下一步"]`；下一步写另一个节点名，或写 `"R:检验id"` 表示落到某个检验
- `QUICK`：左侧"常见场景"快捷路径
- `CHEAT`：方法卡片上方的速查表

基础知识页是普通 HTML，在 `<section id="basics">` 里直接改文字。

## 链接到某个方法

每个方法卡片都有锚点，例如：

- `https://<你的网址>/#welch`：Welch t 检验
- `https://<你的网址>/#mixed`：线性混合模型
- `https://<你的网址>/#basics`：基础知识

## 说明

内容用于学习和快速查阅；方法选择最终取决于实验设计，重要研究请咨询统计专业人员。报告示例中的数字都是示意。
