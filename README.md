# 舟味设计（zhou-flavor-design）

明日方舟实证风格的"舟味"设计系统 + 完整 AI 教学体系。把官方 UI/平面语言拆成**可抄的常量、组件、教程与自检清单**，让没见过明日方舟的 AI 也能做出合格舟味图。

> 触发词：舟味 / 明日方舟风格 / 方舟风 / Arknights style / 海猫风 / 罗德岛风

## 这是什么

- **不是**抽象的"风格描述"，而是一套可执行规范：色板/字体/质感常量、15 组可复制组件代码、6 大布局模板（含 SVG 实例）、从零实操教程、防 AI 味自检清单、动效规范与参考实现。
- 核心判断：**舟味 = 信息设计/界面思维，不是海报思维**。每个元素必须承担信息或引导职能。
- 所有结论从官方截图逐张实证提炼，v1/v2 两版被否的教训都沉淀在反面清单里。

## 文件结构（官方 Skill 规范：SKILL.md + references/ + assets/）

```
SKILL.md            # 入口：教学路径（按序读，不许跳）· 已通过官方打包校验
references/         # 按需加载的规范文档
  design-system.md    # 权威规范：五条判据 / 色板字体质感常量 / 六模板 / 皮肤机制 / 反面清单
  components.md       # 15+ 组可直接抄的 SVG 组件代码
  tutorial.md         # 从零做一张舟味图：9 步实操
  self-check.md       # 六条测试 + 十点清单 + 症状→处方诊断表
  animation.md        # 动效规范：同一画布 / 六种标准行为 / 机械感缓动
assets/
  templates/          # 六大布局模板 SVG 实例（T1 简历卡 ~ T6 专题页）
  examples/           # 全套示例：6 风格静帧 + demo_deck.html（类 PPT 分页演示）+ demo_animated.html（连续版）
dist/
  zhou-flavor-design.zip  # 官方脚本打包产物（可直接导入）
```

## 快速上手

1. 读 `references/design-system.md` §0 五条判断标准。
2. 从 `assets/templates/` 选模板起稿，组件抄 `references/components.md`。
3. 交付前过 `references/self-check.md`。
4. 要动效：读 `references/animation.md`，打开 `assets/examples/demo_deck.html`（分页演示）看参考实现。

安装：解压 `dist/zhou-flavor-design.zip` 到 `~/.workbuddy/skills/` 即可作为 WorkBuddy 技能使用。

## 三条硬规则

1. 亮色只做小面积点睛（青 ≤4 处、红 ≤3 处且 ≤32px）；整面高饱和 = AI 味。
2. 中文大标题思源黑体 900 + 负字距；装饰用宋体衬线；等宽/外语字点缀。
3. 动效永远不换画布：只做局部位移（横移淡入/毛玻璃覆盖/数值展开…），全局统一缓动与时长。

## 演示

打开 `example/demo_animated.html`（同一画布动效参考实现），`example/default_example.html`（组件逐区域标注）。

## 溯源与致谢

规范从知乎《[从ta的视角看UI#1——明日方舟美术设计分析](https://zhuanlan.zhihu.com/p/570566718)》（作者 纳兹）正文 + 26 张官方截图实证提炼；动效部分参考鹰角系动效解析（终末地 UI 动效简析）。本项目为风格学习方法论整理，明日方舟及相关权利归上海鹰角网络所有。

## License

MIT
