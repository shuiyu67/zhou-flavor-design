# ETeam Official Site · eteam.yhdet.top

易腾科技（ETeam）官网。设计语言 1:1 对齐明日方舟官网（ak.hypergryph.com）实证代码：

- 页面基色 `#181a1b`，块面板 `#1d1f20` / `#242424` / `#272727`（官网 CSS 逐 token 提取）
- 品牌青 `#18d1ff` 五种官方用法：hover 变色 / 青底黑字选中态 / 直角青滚动条 / 4px 强调左边框 / 三角角标
- 分类 chip：绿 `#8fc31f` / 蓝 `#3387fb`（仅 chip 级）
- 巨型 Oswald 基线裁切字（`height:.95em` + `flex-end` + `overflow:hidden`）
- 签名记号：`//`、`://`、日期 `2026 // 10 / 01`
- 细线斜切 `skewX(45deg)` 仅限 2px 笔画；过渡统一 `.3s`；`clip-path` `.2s linear`
- 直角化（`border-radius:0`），无玻璃拟态、无发光、无等宽常驻

内容聚焦 Lix 产品线：自研中文大语言模型 **Lix**（xiaoli-v2）+ 命令行 AI 助手 **Lix CLI**。

## 部署

单文件静态站：`index.html` 上传到 nginx 站点根目录即可（同源需 `lenis.min.js` / `gsap.min.js` / `gsap-scrolltrigger.min.js`）。

## License

MIT
