---
name: aab-html-single-file
description: 单文件 HTML 开发规范——零依赖、自包含、快速迭代。用于任何只需要一个 HTML 文件的项目：Demo 原型、比赛展示页、Dashboard、工具页面。也用于用户提到"单文件""一个 HTML""不用框架""纯 HTML""index.html"时。
---

# HTML Single File

## 核心原则

单文件 HTML 的核心优势：**零依赖、开箱即用、随便拷走就能跑**。

三个铁律：
1. **所有资源内联**——CSS 在 `<style>`、JS 在 `<script>`、图标用 SVG/Unicode
2. **不引入外部依赖**——无 CDN、无 npm、无 Google Fonts
3. **一个文件就是整个项目**——拷到任何电脑，双击就能跑

## AAB Single-file Priority（优先级排序）

对于 AAB 的比赛 Demo 和展示项目：

```
1. 稳定优先 —— Demo 翻车 > 功能不完善 > 视觉不完美
2. 一个 index.html 就是整个项目 —— 不拆文件
3. CSS 必须在 <style> 里 —— 不引入外部样式表
4. JS 必须在 <script> 里 —— 不引入外部脚本
5. 不用 CDN —— 除非用户明确允许（如需要特定图表库）
6. 视觉效果用内联 SVG / Canvas / CSS —— 不引入图片资源
7. 文件必须双击就能跑 —— 拷到任何电脑都能打开
8. 离线可用 —— 所有数据内置，不需要网络请求
```

一句话：**比赛 Demo 稳定压倒一切。** 视觉再好，翻车了就是零分。

## 文件结构

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>项目名</title>
<style>
  /* ===== CSS Variables ===== */
  /* ===== Reset ===== */
  /* ===== Layout ===== */
  /* ===== Components ===== */
  /* ===== Animations ===== */
  /* ===== Responsive ===== */
</style>
</head>
<body>
  <!-- ===== HTML ===== -->
<script>
  // ===== Data =====
  // ===== State =====
  // ===== Functions =====
  // ===== Event Handlers =====
  // ===== Init =====
</script>
</body>
</html>
```

分区用注释隔开，注释用 `===== Section =====` 格式，方便快速定位。

## CSS 规范

### 变量

所有颜色/字号/间距用 CSS 变量，放在 `:root`：

```css
:root {
  --bg: #0a0e14; --bg-card: #12161e;
  --text: #e6e8ec; --text-secondary: #8b92a1;
  --accent: #3b8beb; --border: #1e2433;
  --radius: 8px; --gap: 16px;
}
```

### 不使用

- Tailwind（单文件不需要）
- CSS preprocessor（没有构建步骤）
- `@import`（产生外部依赖）
- `!important`（如果写了，说明选择器没设计好）

### 响应式

```css
/* 移动优先 */
.card { width: 100%; }

/* 平板 */
@media (min-width: 768px) {
  .card { width: calc(50% - var(--gap)); }
}

/* 桌面 */
@media (min-width: 1024px) {
  .card { width: calc(33.33% - var(--gap)); }
}
```

## JS 规范

### 零依赖原则

- 不用 jQuery（原生 DOM API 够用）
- 不用 React/Vue（单文件不需要框架）
- 不用 lodash/moment（自己写或用原生 API）
- 数据可视化：用 Canvas 手写，不引入 Chart.js（除非图表非常复杂）

### 原生 API 速查

```js
// DOM 选择
document.querySelector('.card')
document.querySelectorAll('.card')

// 事件
el.addEventListener('click', handler)

// AJAX（如果需要）
fetch('/api/data').then(r => r.json()).then(data => {})

// 模板
`<div class="card">${data.name}</div>`

// 类名操作
el.classList.add('active')
el.classList.toggle('dark')

// 数据属性
el.dataset.id  // <div data-id="123">
```

### 数据管理

简单数据用数组/对象，不用状态管理库：

```js
const state = {
  items: [],
  filter: 'all',
  page: 1
};

function updateState(changes) {
  Object.assign(state, changes);
  render();  // 统一渲染
}
```

## 字体策略

只用系统字体，不引入 Google Fonts / CDN 字体。

```css
--font-mono: 'JetBrains Mono', 'Cascadia Code', 'Consolas', monospace;
--font-sans: 'Inter', 'Noto Sans SC', -apple-system, 'Microsoft YaHei', sans-serif;
```

系统自带等宽字体优先级：JetBrains Mono > Cascadia Code > Consolas（Windows）

## 图标

优先级：
1. **Unicode 符号**：→ ✓ ✗ ⚡ ▲ ▼ ● ◆ ▶ ♥ ★ ☰ — 够用 80% 场景
2. **内联 SVG**：需要精确控制的图标
3. **CSS 绘制**：纯装饰性图形（圆形、三角形、箭头）

不引入 Font Awesome / Material Icons CDN。

## 数据嵌入

如果页面需要数据，直接嵌入 JS 对象或 JSON：

```js
const DATA = [
  { id: 1, name: '项目A', value: 89 },
  { id: 2, name: '项目B', value: 67 },
];
```

数据量大（>100 条）时，考虑分页或虚拟滚动。

## 文件体积意识

- 总文件 < 500KB（含数据）→ 正常
- 总文件 500KB - 1MB → 考虑压缩数据或减少不必要的样式
- 总文件 > 1MB → 考虑是否需要这么多内容

体积大 = 加载慢 = 展示翻车（比赛场合尤其致命）。

## 兼容性

最低目标：Chrome 90+ / Edge 90+ / Firefox 90+
不需要兼容 IE。

## 快速检查清单

每次交付前过一遍：

```
[ ] 双击 HTML 文件能直接在浏览器打开吗？
[ ] 所有 CSS 都在 <style> 里吗？
[ ] 所有 JS 都在 <script> 里吗？
[ ] 没有外部 CDN 链接吗？（检查 src/href）
[ ] 没有 Google Fonts 吗？
[ ] 颜色用了 CSS 变量吗？
[ ] 有基本的响应式吗？（手机上不崩）
[ ] 数据是硬编码的，需要联网的部分有 fallback 吗？
```

## 与其他 Skill 的关系

- `aab-frontend-ui` → 配色、动效、组件风格
- `aab-low-token` → 减少不必要的文件读取
- `aab-competition-demo` → 比赛场景的 Demo 约束
