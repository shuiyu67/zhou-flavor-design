# 组件代码库（直接抄，改参数别改结构）

> 全部为 SVG 片段。坐标系假设 1280x720。颜色变量见 design-system.md §1.1。
> 用法：复制 → 改文字/坐标 → 守自检清单。**不要重新发明组件**，官方组件 2020 年至今没变过。

## 0. 公共 defs（每个文件开头放一次）

```xml
<defs>
  <!-- 浮窗投影：白 panel 必带 -->
  <filter id="sh"><feDropShadow dx="0" dy="6" stdDeviation="10" flood-color="#000" flood-opacity="0.3"/></filter>
  <!-- 重投影：居中弹窗用 -->
  <filter id="shBig"><feDropShadow dx="0" dy="10" stdDeviation="18" flood-color="#000" flood-opacity="0.4"/></filter>
  <!-- 毛玻璃：背景强模糊 -->
  <filter id="blurBg" x="-20%" y="-20%" width="140%" height="140%"><feGaussianBlur stdDeviation="22"/></filter>
  <!-- 半调点网格（黄色，间距/半径可调 14~22 / 1.2~1.8） -->
  <pattern id="dots" width="16" height="16" patternUnits="userSpaceOnUse">
    <circle cx="4" cy="4" r="1.8" fill="#F2C14E"/>
  </pattern>
  <!-- 胶片颗粒（叠最上层，opacity 0.08~0.12） -->
  <filter id="grain"><feTurbulence type="fractalNoise" baseFrequency="0.9" numOctaves="2" stitchTiles="stitch"/>
    <feColorMatrix type="saturate" values="0"/></filter>
</defs>
```

## 1. 角饰线（深色页四角，界定的"仪表感"）

```xml
<g stroke="#39445C" stroke-width="1.5" fill="none">
  <path d="M20,70 L120,70 M20,70 L20,150"/>
  <path d="M1260,70 L1160,70 M1260,70 L1260,150"/>
  <line x1="30" y1="30" x2="90" y2="90"/>
</g>
```

## 2. 三种 chip

```xml
<!-- 黑 chip：节目标签/标题徽章 -->
<rect x="0" y="0" width="150" height="40" fill="#111318"/>
<text x="18" y="27" font-family="'Noto Sans SC','Microsoft YaHei',sans-serif"
      font-size="19" font-weight="700" fill="#FFFFFF">星火 X2.5</text>

<!-- 白 chip：当前选中项（列表里唯一的白底黑字） -->
<rect width="270" height="48" fill="#FFFFFF" filter="url(#sh)"/>
<text x="16" y="31" font-size="20" font-weight="800" fill="#141517"
      font-family="'Noto Sans SC','Microsoft YaHei',sans-serif">星火 X2.5</text>

<!-- 边框标签 chip：信息行标签 -->
<rect width="58" height="28" fill="none" stroke="#54607A" stroke-width="1"/>
<text x="12" y="20" font-size="17" fill="#AEB6C6"
      font-family="'Noto Sans SC','Microsoft YaHei',sans-serif">代号</text>
```

## 3. 信息行（标签 chip + 值 + 细下划线，简历卡核心）

```xml
<g font-family="'Noto Sans SC','Microsoft YaHei',sans-serif">
  <rect x="150" y="330" width="58" height="28" fill="none" stroke="#54607A"/>
  <text x="162" y="350" font-size="17" fill="#AEB6C6">定位</text>
  <text x="226" y="351" font-size="17" fill="#E8ECF2">新一代认知大模型</text>
  <line x1="226" y1="360" x2="420" y2="360" stroke="#3A4458" stroke-width="1"/>
</g>
```
规则：下划线右端对齐本列统一宽度；行距 42~44px。

## 4. 大数字 panel（主界面视觉锚点）

```xml
<g filter="url(#sh)">
  <rect x="700" y="90" width="300" height="150" fill="#FFFFFF"/>
  <!-- 数字：900 字重 + 负字距，是全图最大元素 -->
  <text x="720" y="200" font-size="110" font-weight="900" fill="#111318"
        letter-spacing="-6" font-family="'Noto Sans SC','Microsoft YaHei',sans-serif">2.5</text>
  <text x="920" y="140" font-size="22" font-weight="700" fill="#111318">认知模型</text>
  <text x="920" y="168" font-size="13" fill="#8A8F98">SPARK · 当前版本</text>
</g>
```

## 5. 青色操作条（全页唯一大面积亮色）

```xml
<g filter="url(#sh)">
  <rect x="700" y="398" width="480" height="86" fill="#2FA6DE"/>
  <text x="724" y="448" font-size="20" font-weight="700" fill="#FFF"
        font-family="'Noto Sans SC','Microsoft YaHei',sans-serif">多模态引擎</text>
  <line x1="856" y1="414" x2="856" y2="468" stroke="#FFF" stroke-width="1" opacity="0.6"/>
  <!-- 白色细分隔线 + 并列项，项数 2~3 -->
</g>
```

## 6. 警戒色任务卡（红/黄小徽标 + 进度条）

```xml
<g filter="url(#sh)">
  <rect x="700" y="508" width="480" height="52" fill="#FFFFFF"/>
  <rect x="712" y="518" width="32" height="32" fill="#E14A4A"/>          <!-- 徽标≤32px -->
  <path d="M722,540 L728,526 L734,540 Z" fill="#FFFFFF"/>
  <text x="760" y="540" font-size="16" font-weight="700" fill="#111318">128K 上下文</text>
  <rect x="980" y="596" width="160" height="6" fill="#E3E5E8"/>          <!-- 进度槽 -->
  <rect x="980" y="596" width="104" height="6" fill="#F2A93B"/>          <!-- 进度 -->
  <polygon points="1084,592 1092,599 1084,606 1076,599" fill="#111318"/> <!-- 菱形游标 -->
</g>
```

## 7. 六边形节点 + OPERATION 地图 chip + 双描边路线

```xml
<!-- 节点：青填充白描边；特殊关换 #E14A4A -->
<polygon points="0,20 14,10 14,30 0,40" fill="#2FA6DE" stroke="#FFFFFF" stroke-width="2"/>
<!-- 关卡 chip -->
<g transform="translate(90,395)">
  <rect x="26" width="130" height="52" fill="#FFF" stroke="#1A1A1A" stroke-width="2"/>
  <rect x="26" width="130" height="17" fill="#1A1A1A"/>
  <text x="36" y="13" font-size="9" fill="#FFF" letter-spacing="2">OPERATION</text>
  <text x="38" y="42" font-size="19" font-weight="800" fill="#1A1A1A">X2.5-1</text>
</g>
<!-- 路线：黑底白面双描边 -->
<polyline points="150,430 400,360" fill="none" stroke="#1A1A1A" stroke-width="6"/>
<polyline points="150,430 400,360" fill="none" stroke="#FFFFFF" stroke-width="3.5"/>
```

## 8. chevron 横幅（右端箭头切角）

```xml
<polygon points="700,648 1060,648 1084,674 1060,700 700,700" fill="#FFFFFF" filter="url(#sh)"/>
<text x="722" y="680" font-size="15" font-weight="700" fill="#111318">前往能力白皮书</text>
<path d="M860,660 L872,674 L860,688" stroke="#111318" stroke-width="2.5" fill="none"/>
```

## 9. 底部图标导航（细竖线分隔）

```xml
<g stroke="#C9CCD1" stroke-width="1">
  <line x1="1120" y1="660" x2="1120" y2="688"/><line x1="1160" y1="660" x2="1160" y2="688"/>
</g>
<g fill="#8A8F98"><!-- 简单几何 icon：方块/圆环/三角，≤20px --></g>
```

## 10. 标题组（装饰符 + Heavy 负字距 + 拉丁副标）

```xml
<g fill="#35A7CF">
  <rect x="128" y="196" width="46" height="3"/>
  <polygon points="188,197 196,189 204,197 196,205"/>  <!-- 横线+菱形 -->
</g>
<text x="220" y="238" font-size="104" font-weight="900" fill="#F4F6F8"
      letter-spacing="-4" font-family="'Noto Sans SC','Microsoft YaHei',sans-serif">星火</text>
<text x="222" y="292" font-size="28" fill="#35A7CF" letter-spacing="12">SPARK X2.5</text>
```
注意：中文主标题负字距，拉丁副标**正字距宽排**，一负一正是官方对比手法。

## 11. 技能/能力条目（图标方块 + 标题 + 高亮 tspan）

```xml
<g font-family="'Noto Sans SC','Microsoft YaHei',sans-serif">
  <rect x="150" y="590" width="34" height="34" fill="none" stroke="#E14A4A" stroke-width="2"/>
  <path d="M158,598 L176,616 M176,598 L158,616" stroke="#E14A4A" stroke-width="2"/>
  <text x="200" y="606" font-size="17" font-weight="700" fill="#E8ECF2">多模态理解</text>
  <text x="200" y="630" font-size="13" fill="#8A93A6">图文音跨模态推理，<tspan fill="#35A7CF">一体化对齐</tspan></text>
</g>
```
规则：每条描述**只允许一个青色高亮词组**，多则失焦。

## 12. 毛玻璃弹窗场景（背景彩 + 暗化 + 中央白卡）

```xml
<g filter="url(#blurBg)"><!-- 任意彩色内容：色块/网格/插画 --></g>
<rect width="1280" height="720" fill="#1A1A1A" opacity="0.18"/>
<g filter="url(#shBig)"><rect x="360" y="160" width="560" height="400" fill="#FFFFFF"/></g>
<!-- 卡内：左上黑chip标题 + 右上灰chip + 内容 + 分隔线 + 红下划线链接 -->
```

## 13. 宋体装饰行 / 引言 / 白框画卡

```xml
<text font-family="'Noto Serif SC','SimSun',serif" font-style="italic"
      font-size="19" fill="#7C8699">「以认知为燃料，回答每一个问题。」</text>

<!-- 白框画卡（专辑/封面） -->
<g filter="url(#sh)">
  <rect x="470" y="200" width="250" height="250" fill="#FFFFFF"/>
  <rect x="482" y="212" width="226" height="226" fill="#1E2023"/>
</g>
<!-- 卡内标题用宋体/衬线 + 宽字距 -->
```

## 14. 质感层（⚠️ 按场合选用，通常 0~1 种，不是全页必叠——详见 design-system §1.3）

```xml
<rect x="60" y="480" width="120" height="60" fill="url(#dots)" opacity="0.5"/> <!-- 半调块 -->
<g fill="none" stroke="#C2C4BD" stroke-width="1.4">                            <!-- 等高线×4~6 -->
  <path d="M-20,120 C200,60 380,180 620,120 C860,60 1060,170 1300,110"/>
  <path d="M-20,150 C210,90 390,210 630,150 C870,90 1070,200 1300,140"/>
</g>
<rect width="1280" height="720" filter="url(#grain)" opacity="0.10"
      style="mix-blend-mode:overlay"/>                                          <!-- 颗粒最上层 -->
```

## 15. 印刷/摄影隐喻组件（design-system §1.3b，AJ 分析实证）

```html
<!-- Vignette 暗角：盖最上层，突出中心（章节选择页实证） -->
<div style="position:absolute;inset:0;pointer-events:none;box-shadow:inset 0 0 130px rgba(31,33,36,.16)"></div>

<!-- 相片白边卡：图片元素加粗白边+微倾，"夹在细绳上的打印照片" -->
<figure style="background:#fff;padding:10px 10px 14px;box-shadow:0 4px 14px rgba(0,0,0,.18);transform:rotate(-1.2deg)">
  <img src="kv.png" style="display:block">
</figure>

<!-- 尘埃粒子：呼吸感来源，响应鼠标拂开（animation.md §3c，canvas 实现） -->
<!-- 参考实现：example/demo_animated.html 的 motes 循环：26 颗、r 0.8~2.6、
     上飘 v 0.0001~0.0004、鼠标 95px 半径内拂开、透明度 0.1~0.26 呼吸闪烁 -->
```

## 16. 基线裁切巨型标题（官网首页标准式，§1.6 实证）

官网 10+ 处复用：7rem Oswald + -.05em + .95em 基线裁切。HTML 原式：

```html
<div style="display:flex;align-items:flex-end;height:.95em;overflow:hidden;
     font-family:'Oswald',sans-serif;font-weight:500;font-size:7rem;
     letter-spacing:-.05em;color:#242424;line-height:1">
  RHODES ISLAND
</div>
```

SVG 等效（clipPath 裁掉下缘 5%）：

```xml
<clipPath id="crop"><rect x="0" y="0" width="700" height="95"/></clipPath>
<text x="0" y="88" font-family="Oswald,sans-serif" font-weight="500" font-size="96"
      letter-spacing="-4" fill="#242424" clip-path="url(#crop)">RHODES ISLAND</text>
```

## 17. 记号文本行（`//` 日期 / 进度 / 归属声明，§1.6 实证）

```xml
<g font-family="'Oswald','Noto Sans SC',sans-serif">
  <!-- 日期：年 // 月 / 日 -->
  <text x="0" y="0" font-size="15" fill="#585858" letter-spacing="2">2026 // 09 / 15</text>
  <!-- 进度：页码 // 序号 / 总数 -->
  <text x="0" y="0" font-size="13" fill="#ABABAB" letter-spacing="3">00 // 03 / 05</text>
  <!-- 归属声明（页脚/旁注） -->
  <text x="0" y="0" font-size="12" fill="#ABABAB" letter-spacing="1">RHODES ISLAND :// PROFILE</text>
</g>
```

## 18. 斜切细线分隔符（官网唯一合法的 skew 用法，§1.6）

```xml
<!-- 2px 竖线 skewX(45deg)：官网实证 transform:skewX(45deg) -->
<rect x="640" y="0" width="2" height="72" fill="#242424" transform="skewX(-30)"/>
<!-- HTML 原式：width:2px;height:75%;background:currentColor;transform:skewX(45deg) -->
```

**纪律**：只许细笔画（≤3px）斜切。整块面板斜切 = 返工。

## 19. 青色状态组（`#18D1FF` 五种官方用法，§1.6）

```xml
<!-- ① 选中态：青底黑字（官方 color:#000; background:#18d1ff） -->
<rect x="0" y="0" width="120" height="34" fill="#18D1FF"/>
<text x="14" y="23" font-size="16" font-weight="700" fill="#000"
      font-family="'Noto Sans SC',sans-serif">当前项</text>

<!-- ② 强调左边框：4px 青线 + 左内边距（引用/重点块） -->
<g>
  <rect x="0" y="0" width="4" height="52" fill="#18D1FF"/>
  <text x="14" y="21" font-size="15" fill="#242424">重点条目正文……</text>
  <text x="14" y="42" font-size="13" fill="#585858">注释小字……</text>
</g>

<!-- ③ 进度/滚动条 drag 块：直角（官方 border-radius:0） -->
<rect x="0" y="0" width="64" height="4" fill="#18D1FF"/>

<!-- ④ 边框三角角标：贴角 1px 青三角 -->
<path d="M300,0 L312,0 L300,12 Z" fill="none" stroke="#18D1FF" stroke-width="1"/>

<!-- ⑤ 分类标签底色（绿/蓝，仅小 chip） -->
<rect x="0" y="0" width="70" height="24" fill="#8FC31F"/>
<text x="10" y="17" font-size="14" font-weight="700" fill="#000">活动</text>
```
