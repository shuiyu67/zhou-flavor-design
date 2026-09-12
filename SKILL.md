---
name: zhou-flavor-design
description: "Arknights-derived (zhou-flavor / 舟味) design system skill with a full AI teaching curriculum: evidence-based design constants (palette, typography, textures, components), six layout templates with SVG instances, copy-paste SVG component library, step-by-step tutorial, anti-AI-flavor self-check gates, and same-canvas motion specification. This skill should be used when the user asks for 舟味 / 明日方舟风格 / 方舟风 / Arknights style / 海猫风 / 罗德岛风 visuals — promo frames, KV posters, UI-style pages, covers, or storyboard frames — or when reproducing the Arknights official UI look. Produces static frames (SVG/HTML) and motion pieces (CSS/JS timelines rendered via headless browser plus ffmpeg)."
agent_created: true
---

# 舟味设计（zhou-flavor-design）

把明日方舟官方 UI/平面语言复刻为可复用设计系统，让没见过明日方舟的 AI 也能做出合格舟味图。

核心判断（先记住这一句）：**舟味 = 信息设计/界面思维，不是海报思维。** 每个元素必须承担信息或引导职能；亮色只做小面积点睛；底色默认浅色纸感，深色页需要命题理由。

## 教学路径（按序读，不许跳）

| 步 | 文件 | 读完你会 |
|---|---|---|
| 1 | `references/design-system.md` | 舟味五条判据、色板/字体/质感常量、六大布局模板、皮肤机制、反面清单 |
| 2 | `references/components.md` | 15+ 组可直接抄的 SVG/HTML 组件代码 |
| 3 | `references/tutorial.md` | 从零做一张舟味图的 9 步实操 |
| 4 | `references/self-check.md` | 交付前六条测试 + 十点清单 + 症状→处方诊断表 |
| 5 | `references/animation.md`（做视频时） | 同一画布原则、六种标准行为、机械感缓动、渲染管线 |

## 资源

- `assets/templates/`：六大布局模板 SVG 实例（V2_01 简历卡 ~ V2_06 专题页）
- `assets/examples/default_example.html`：默认示例，含逐区域组件标注表
- `assets/examples/demo_deck.html`：分页演示（类 PPT）——六模板、六动效行为逐页展示，←/→ 翻页
- `assets/examples/demo_animated.html`：连续版同一画布参考实现

## 工作流

1. 读 `references/design-system.md`（重点 §0 判据、§1 常量、§4 反面清单）。
2. 与用户确认皮肤三要素：主视觉、点缀色、主题符号。
3. 按 `references/tutorial.md` 的 Step 0 先列信息清单，再从 `assets/templates/` 选模板起稿；组件抄 `references/components.md`，不重新发明。
4. 静帧交付前过 `references/self-check.md` 全部条目。
5. 需要动效时读 `references/animation.md`，参考 `assets/examples/demo_deck.html` 的分页实现与 `demo_animated.html` 的连续实现；成片走 headless 渲染 + ffmpeg（先 ffmpeg 抽帧自查）。

## 硬规则（违反任何一条=返工）

- 先列信息清单再动手；无信息可说的装饰直接删。
- 中文大标题思源黑体 900 + 负字距；拉丁副标宽字距；装饰用宋体衬线。
- 青色元素 ≤4 处、红色 ≤3 处且 ≤32px；整面高饱和 = AI 味，直接毙。
- 记号按实证分级：六边形仅限地图节点/干员卡水印；四角 HUD 括号、扫描线、常驻等宽字禁止。
- 动效永远不换画布：只做局部位移，全局统一缓动 `cubic-bezier(.25,.1,.25,1)` 与四档时长。

## 溯源

规范从知乎《从ta的视角看UI#1——明日方舟美术设计分析》（纳兹）+ 腾讯游戏学堂《明日方舟 UI/UX 分析》（AJ）等四篇分析正文与 26 张官方截图实证提炼；v1 海报风、v2 科技 HUD 风、v2 动效幻灯片三次被否的教训均沉淀在反面清单与自检清单中。
