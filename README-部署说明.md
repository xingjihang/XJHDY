# 独立站部署说明（麻城星际航 · XINGJIHANG）

这套代码是一个**完整可上线的轻量独立站**：5 个页面 + 4 张产品示意图，纯静态、无框架、无外部依赖，任意主机上传即可运行。

---

## 一、文件清单

| 文件 | 作用 |
|---|---|
| `index.html` | 首页（同时是总落地页）：三条产品线入口 + 询盘表单 + FAQ |
| `voltage-stabilizer.html` | 稳压器落地页（关键词：voltage stabilizer / AVR / servo stabilizer） |
| `dry-type-transformer.html` | 干式变压器落地页（关键词：dry type transformer / cast resin / SCB10） |
| `switchgear.html` | 低压开关柜落地页（关键词：GGD switchgear / LV panel / distribution board） |
| `privacy.html` | 隐私政策（**Google Ads 审核必需**，不能少） |
| `thank-you.html` | 表单提交成功页（广告转化跟踪用） |
| `assets/style.css` | 全站样式（一处修改全站生效） |
| `assets/*.svg` | 产品示意图（线稿风格，后续可换实拍图） |
| `assets/favicon.svg` | 网站图标 |
| `robots.txt` / `sitemap.xml` | 搜索引擎收录 |

三条产品线的选择逻辑：**稳压器**（搜索量最大、非洲/中东刚需、金保最熟）+ **干式变压器**（客单价 $3,900–34,520，一单顶百台小稳压器）+ **开关柜**（项目入口，客户买柜必然带变压器）。油浸变压器和环网柜暂不上，原因见页面内说明。

---

## 二、上线三步（合计约 1 小时）

### 第 1 步：买域名（约 ¥80/年）
- 在 **Namecheap、Cloudflare 或阿里云国际版** 注册一个 `.com`。
- 建议候选：`xingjihang.com` / `machengpower.com` / `xjpower.cn 的 .com 版`。
- **不要用国内需备案的服务商托管**，选境外托管，免备案、海外访问快。

### 第 2 步：免费托管（推荐 Cloudflare Pages）
1. 注册 [pages.cloudflare.com](https://pages.cloudflare.com)（免费）。
2. 「Direct Upload」→ 把 `website` 文件夹整个拖进去 → 部署完成。
3. 绑定你的域名，Cloudflare 自动给 **HTTPS**（Google Ads 硬性要求）。
- 备选：Vercel、Netlify，操作相同。

### 第 3 步：接通询盘表单（10 分钟）
表单目前指向占位地址，需要换成你自己的：
1. 注册 [formspree.io](https://formspree.io)（免费档每月 50 条）。
2. 新建 Form → 得到一个地址如 `https://formspree.io/f/abcd1234`。
3. 在 **4 个 html 文件**里搜索 `REPLACE_WITH_YOUR_FORM_ID`，全部替换。
4. 在 Formspree 后台把通知邮箱设为你的企业邮箱（sales@…），询盘自动进邮箱 + WhatsApp。

> 询盘量起来后（每月 >50 条）再考虑升级付费档或换成自建接口，初期免费档够用。

---

## 三、上线前必须替换的 6 处占位

全部用「查找替换」处理，每处搜哪个词、换成什么：

| # | 搜索 | 替换为 |
|---|---|---|
| 1 | `https://www.example.com` | 你的正式域名（含 sitemap.xml、robots.txt 里也要改） |
| 2 | `sales@example.com` | 你的企业邮箱 |
| 3 | `+86 138 0000 0000` | 你的 WhatsApp 展示号码 |
| 4 | `861380000000`（在每页底部 script 里 `WHATSAPP_NUMBER`） | 真实 WhatsApp 号码，**纯数字、含国家码 86** |
| 5 | `REPLACE_WITH_YOUR_FORM_ID` | 你的 Formspree 表单 ID |
| 6 | Macheng Economic Development Zone…地址 | 工厂/公司实际注册地址 |

**注意**：WhatsApp 号码出现在每个页面的 `<script>` 里，共 5 处； Formspree ID 出现在 4 处。用 VS Code「全局查找替换」一次完成，不要一页一页改。

---

## 四、上线后的广告接入（配合已交付的 Google Ads 方案）

1. **Google Ads 转化跟踪**：在 `thank-you.html` 的 `</body>` 前粘贴 Google Ads 发给你的转化代码即可——只有填完表单跳到这页的人才会被计为「一次转化」，天然防误计。
2. **广告最终到达网址**：
   - 搜 "voltage stabilizer" 系列词 → `voltage-stabilizer.html`
   - 搜 "dry type transformer" 系列词 → `dry-type-transformer.html`
   - 搜 "switchgear / panel" 系列词 → `switchgear.html`
   - 品牌词、通用词 → 首页
3. **质量分**：每个落地页都已有标题、描述、产品表、FAQ 和隐私政策链接，符合 Google 对工业品落地页的审核要求；上线后跑「Ad Preview」确认无「destination not working」报错。

---

## 五、产品图与价格

- **图**：现在是技术线稿风格的 SVG，风格统一、体积小（几 KB）、全球加载快。等金保提供实拍图后，替换 `assets/` 下同名文件即可，无需改代码。建议每条线配 2–3 张真实照片（正面 + 铭牌特写 + 装柜现场），铭牌特写对工业买家信任度提升最大。
- **价格**：页面上的价格为「Indicative FOB price」，取自《金保产品线出口定价表》的基准价（S 级市场中位价 ×1.05–1.15）。改动位置：各产品页「MODELS & INDICATIVE PRICING」表格内。**拿到金保含税价目表后**，按测算表重算一遍再更新，并保持「页面价 ≥ 底线价 ×1.08」。
- 如担心价格透明引来竞品盯价，可在拿到第一批真实询盘后把表格价格改为「from US$xxx」区间价。

---

## 六、上线检查清单

- [ ] 6 处占位全部替换，页面里搜不到 `example.com` / `REPLACE` / `0000`
- [ ] HTTPS 打开无锁角警告（Cloudflare 自动处理）
- [ ] 用手机流量（不连 WiFi）打开首页，3 秒内出内容
- [ ] 填一次表单，确认 Formspree 收到、邮箱收到、跳转到 thank-you 页
- [ ] 点 WhatsApp 按钮，跳出的聊天窗口预填文本正确
- [ ] 三个产品页各点一遍导航、面包屑、页脚链接，无死链
- [ ] Google Search Console 提交 sitemap.xml
- [ ] 把网址发给一个朋友在海外（或用免费代理 IP）测试打开速度

---

## 七、下一步（按优先级）

1. **本周**：买域名 → Cloudflare Pages 部署 → 替换占位 → 表单连通。
2. **下周**：向金保索取含税价目表，用《退税与报价测算表》验算后更新价格页；拍 3–5 张实拍图替换 SVG。
3. **再下周**：开 Google Ads 账户，按《Google 搜索广告投放方案》建 3 个广告组，每组指向对应落地页，转化代码装在 thank-you 页。
