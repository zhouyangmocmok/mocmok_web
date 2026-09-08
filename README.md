# mocmok.com 静态官网 · 部署说明

这个目录可以直接作为 `mocmok.com` 的静态网站发布，无需 npm、React 或构建步骤。

## 当前版本包含

- `index.html` — MocMok 正式产品首页：AI-native social discovery、Agent Match、Social Games、Safety、About
- `terms.html` — 服务协议 / Terms of Service
- `privacy.html` — 隐私政策 / Privacy Policy
- `guidelines.html` — 社区规范 / Community Guidelines
- `support.html` — 帮助与支持 / Help & Support

所有页面均为中英文双语：

- **首次访问默认显示 English**
- 右上角使用**地球图标语言菜单**切换 `English / 中文`
- 用户主动选择的语言会保存在浏览器 `localStorage` 中，之后继续使用该选择

## App Store 常用 URL

- Privacy Policy: `https://mocmok.com/privacy.html`
- Support: `https://mocmok.com/support.html`
- Terms of Service: `https://mocmok.com/terms.html`
- Community Guidelines: `https://mocmok.com/guidelines.html`

这些 URL 上线后尽量保持不变，后续只更新页面内容。

## 推荐部署方式

### Vercel（推荐）

1. 把本 `website/` 目录放到 GitHub 仓库。
2. 在 Vercel 新建项目并连接该仓库。
3. 如果仓库根目录就是这些 HTML，Framework Preset 选择 `Other`，不需要 Build Command。
4. 如果仓库中本目录仍叫 `website/`，把 Root Directory 指向 `website`。
5. 在 Vercel 添加自定义域名 `mocmok.com` 和可选的 `www.mocmok.com`。
6. 按 Vercel 给出的记录，在 GoDaddy → DNS 中修改 `@` / `www`。
7. 等 HTTPS 生效后检查下面 URL 均可直接打开并返回 200。

```bash
curl -I https://mocmok.com/
curl -I https://mocmok.com/privacy.html
curl -I https://mocmok.com/support.html
curl -I https://mocmok.com/terms.html
```

## GoDaddy 的角色

GoDaddy 继续负责管理 `mocmok.com` 域名与 DNS；网站文件可以部署在 Vercel。你的 App 后端仍可继续放在 AWS，两者互不冲突。

例如：

```text
mocmok.com       -> Vercel 静态官网
www.mocmok.com   -> Vercel 静态官网
api.mocmok.com   -> AWS / Elastic Beanstalk（如你这样配置）
```

## 关于 App 内法律文案同步

如果你的 App 工程仍使用：

`frontend/i18n/locales/{zh,en}/legal.json`

以及：

`node scripts/build-legal-pages.js`

来生成网站法律页面，请把本版本中对 Terms / Privacy 等页面的相应文案同步回 `legal.json`，再让生成脚本保持一致。否则未来重新运行生成脚本时，可能会覆盖本目录中的修改。
