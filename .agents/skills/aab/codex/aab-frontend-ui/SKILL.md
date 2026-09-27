---
name: aab-frontend-ui
description: 暗色科技风 UI 规范——AAB 的默认前端风格。深色背景、科技感配色、利落排版、克制动效。用于任何需要 UI 的场景：HTML 页面、比赛 Demo、Dashboard、产品展示。也用于用户提到"暗色风""科技风""赛博""酷炫""高级感""Dark UI""Sci-fi style"时。
---

# Frontend UI — 暗色科技风

## 设计原则

三个关键词：**克制、科技感、可信**。

- 不要花哨。科技感来自精确，不来自装饰。
- 每个像素都有理由。去掉不能解释的视觉效果。
- 比赛场景 → 看起来成熟、可信、有技术深度。
- 个人项目 → 可以更酷，但不能乱。

## Avoid Generic AI UI（避免廉价 AI 感）

Agent 看到"科技风"容易乱加东西。以下行为**明确禁止**：

```
❌ 满屏粒子动画 / 星空背景（除非用户明确要）
❌ 到处毛玻璃效果（glassmorphism 泛滥 = 廉价）
❌ 无意义的扫描线/网格线装饰
❌ 随机渐变卡片（每张卡片不同颜色渐变 = 乱）
❌ 大段渐变色文字（可读性差）
❌ 纯装饰性 3D 旋转（性能杀手 + 投影仪翻车）
```

**AAB 偏好的科技感**：
```
✅ 克制的 neon glow（只在关键元素上，透明度 ≤ 0.15）
✅ 精确的间距和网格对齐
✅ 真实的 dashboard 卡片（顶部分割线强调色）
✅ 数据可视化优先于装饰
✅ 留白 > 填充
✅ 单强调色统领全局（最多加一个辅助色）
```

判断标准：**这个效果能向评委/老师解释为什么要这样做吗？** 不能 → 删掉。

## 配色系统

### 主色板

```
背景层：
  --bg-primary:    #0a0e14      主背景（最深）
  --bg-secondary:  #12161e      卡片/面板背景
  --bg-tertiary:   #1a1f2b      悬浮/hover 背景
  --bg-elevated:   #1e2433      最高层（modal/dropdown）

文字层：
  --text-primary:   #e6e8ec     主文字
  --text-secondary: #8b92a1     次要文字
  --text-tertiary:  #555b6b     辅助/禁用文字

强调色（选 1-2 个，不要全用）：
  --accent-blue:    #3b8beb     默认主强调色（冷静、专业）
  --accent-cyan:    #00d4cc     数据/科技感强调
  --accent-purple:  #7c5ce7     创意/高端强调
  --accent-green:   #2ecc71     成功/正向指标
  --accent-red:     #e74c3c     警告/危险（少用）
  --accent-amber:   #f0a030     中等警告/高亮

边框/分割：
  --border-default: #1e2433     默认边框
  --border-hover:   #2a3142     悬浮边框
  --border-active:  #3b8beb     激活边框（用主强调色）
```

### 渐变

```
科技感渐变（按钮/标题/重点区域）：
  gradient-tech: linear-gradient(135deg, #3b8beb, #7c5ce7)
  gradient-data:  linear-gradient(135deg, #00d4cc, #3b8beb)
  gradient-dark:   linear-gradient(180deg, #12161e, #0a0e14)

发光效果：
  glow-blue:   0 0 20px rgba(59, 139, 235, 0.15)
  glow-cyan:   0 0 20px rgba(0, 212, 204, 0.15)
  glow-purple: 0 0 20px rgba(124, 92, 231, 0.15)
```

## 排版

```
字体栈：
  --font-mono:  'JetBrains Mono', 'Fira Code', 'Cascadia Code', monospace
  --font-sans:  'Inter', 'Noto Sans SC', -apple-system, sans-serif
  --font-display: 'Inter', 'Noto Sans SC', sans-serif

层级：
  H1:  28px / 700 weight / --text-primary
  H2:  22px / 600 weight / --text-primary
  H3:  18px / 600 weight / --text-primary
  H4:  16px / 500 weight / --text-secondary
  Body: 14px / 400 weight / --text-primary
  Caption: 12px / 400 weight / --text-tertiary
  Code: 13px / 400 weight / --font-mono

行高：
  正文 1.6、标题 1.3、代码 1.5
```

### 中文排版注意

- 中文字体不加斜体（italic fallback 难看）
- 中英文混排时字体栈先写英文再写中文
- 比赛材料优先系统自带字体，不引入 Google Fonts（加载慢、展示翻车风险）

## 组件规范

### 卡片

```
标准卡片：
  background: --bg-secondary
  border: 1px solid --border-default
  border-radius: 8px
  padding: 20px 24px
  hover: border-color → --border-hover, 轻微 glow

数据卡片（Dashboard 风格）：
  同上 + 顶部 2px accent 色条
  适合：指标展示、状态面板
```

### 按钮

```
主按钮：
  background: gradient-tech
  color: white
  border: none
  border-radius: 6px
  padding: 10px 20px
  hover: 亮度 +10%, glow-blue

次按钮：
  background: transparent
  border: 1px solid --border-default
  color: --text-secondary
  hover: border-color → --accent-blue, color → --text-primary

Ghost 按钮：
  background: transparent
  border: none
  color: --accent-blue
  hover: background → rgba(59, 139, 235, 0.08)
```

### 数据展示

```
数字指标：
  数值用 --font-mono，大字号，强调色
  标签用 --text-tertiary，12px

表格：
  表头深色 bg，行间 1px 分割线
  hover 行 bg → --bg-tertiary
  对齐：文字左对齐，数字右对齐，状态居中

图表配色（从强调色派生）：
  系列色序：blue → cyan → purple → green → amber
```

### 状态标签

```
Badge：
  border-radius: 4px
  padding: 2px 8px
  font-size: 11px
  font-weight: 500

  成功：bg green 10%透明度, color green
  警告：bg amber 10%透明度, color amber
  错误：bg red 10%透明度, color red
  信息：bg blue 10%透明度, color blue
```

## 动效

### 原则

- 动效服务于"科技感"，不服务于"炫"
- 持续时间：150-300ms，不超 400ms
- Easing：`cubic-bezier(0.4, 0, 0.2, 1)`（标准缓出）
- 比赛场景 → 减少动效（评委不关心，可能卡顿）

### 常用动效

```
Fade in：       opacity 0→1, 200ms
Slide up：      translateY(8px)→0, opacity 0→1, 250ms
Scale reveal：  scale(0.95)→1, opacity 0→1, 200ms
Hover lift：    translateY(-2px), box-shadow 增强, 200ms
数据更新：      数值变化用 countUp 效果，背景短暂高亮
```

### 不需要动效的地方

- 大列表渲染
- 路由切换（单文件 HTML 不存在路由）
- 表格排序/筛选
- 任何比赛 PPT 中嵌入的页面

## 单文件 HTML 特殊约束

在单文件 HTML 中实现时：

```
CSS 放在 <style> 标签内，不引入外部样式
字体：只用系统字体（不加载 Google Fonts / CDN）
图标：用 Unicode 符号或内联 SVG，不引入 icon font
动效：只用 CSS transition/animation，不引入 JS 动画库
背景：CSS gradient 或纯色，不用背景图片（体积大）
```

## 快速启动模板

当用户需要暗色科技风页面时，直接使用这个骨架：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Project</title>
<style>
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
:root {
  --bg-primary: #0a0e14; --bg-secondary: #12161e; --bg-tertiary: #1a1f2b;
  --text-primary: #e6e8ec; --text-secondary: #8b92a1; --text-tertiary: #555b6b;
  --accent: #3b8beb; --border: #1e2433;
  --font-mono: 'JetBrains Mono', 'Cascadia Code', monospace;
  --font-sans: 'Inter', 'Noto Sans SC', -apple-system, sans-serif;
}
body {
  background: var(--bg-primary); color: var(--text-primary);
  font-family: var(--font-sans); line-height: 1.6;
  min-height: 100vh;
}
/* 从这里开始写 */
</style>
</head>
<body>
<!-- 内容 -->
</body>
</html>
```

## 不与现有 Skill 冲突

- 当用户同时需要 frontend-design 或 frontend-ui-engineering 时，以本 Skill 的风格约束为准，但实现细节可以参考那两个 Skill 的技术方案。
- 本 Skill 定义"长什么样"，其他 Skill 定义"怎么做"。
