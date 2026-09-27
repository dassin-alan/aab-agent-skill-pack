---
name: "aab-playwright-qa"
description: "AAB 专用的自动验收流程——HTML 页面和比赛 Demo 的质量检查。基于 Playwright 做截图对比、功能验证、翻车预防"
---

# Playwright QA — AAB 专用验收

## 触发时机

- 完成一个 HTML 页面后
- 比赛 Demo 答辩前
- 用户说"检查一下能不能跑"
- 改完代码想确认没改坏

## QA Levels（三档验收）

每次触发时根据场景选择对应档位。默认从 Quick QA 开始。
### Level 1: Quick QA（日常开发，每次改完就跑）
```
[ ] 页面能打开（HTTP 200 / 直接双击能加载）
[ ] 控制台无报错（JS error / 404 / CORS）
[ ] 主要按钮能点击（不报错即可，不要求每个都有功能）
[ ] 无明显的文字溢出/重叠
耗时： 30 秒
```

### Level 2: Demo QA（给老师/老板看之前）

```
[ ] Quick QA 全部通过
[ ] 1920x1080 截图正常
[ ] 1366x768 截图正常
[ ] 375x812（手机）截图正常
[ ] 文字无溢出/重叠（仔细检查）
[ ] 暗色主题对比度正常（文字清晰可读）
[ ] 无明显的布局断裂
耗时： 3 分钟
```

### Level 3: Competition QA（答辩前必须跑）

```
[ ] Demo QA 全部通过
[ ] 投影仪分辨率（1024x768 + 1920x1080）都正常
[ ] 暗色主题在投影仪上可读（对比度 ≥ 4.5:1）
[ ] 完全离线可用（断网测试）
[ ] 关键数据逐项核对（数字、图表、表格）
[ ] 所有按钮功能走一遍
[ ] 截图备份已生成（翻车时备用）
[ ] 加载时间 < 3 秒
耗时： 10 分钟
```

## 快速验收脚本
```js
// save as qa-check.js
const { chromium } = require('playwright');

(async () => {
  const browser = await chromium.launch();
  const page = await browser.newPage();

  // 收集控制台错误
  const errors = [];
  page.on('console', msg => {
    if (msg.type() === 'error') errors.push(msg.text());
  });

  await page.goto('http://localhost:3000'); // 或 file:// 路径

  // 截图
  await page.screenshot({ path: 'qa-desktop.png', fullPage: true });

  // 检查关键元素存在
  const checks = ['h1', '.hero', '.card', 'button'];
  for (const sel of checks) {
    const el = await page.$(sel);
    console.log(el ? `OK: ${sel}` : `MISSING: ${sel}`);
  }

  console.log(`Errors: ${errors.length}`);
  if (errors.length) console.log(errors);

  await browser.close();
})();
```

## 验收标准

| 场景 | 通过条件 |
|------|----------|
| 日常开发 | 无报错、关键元素存在 |
| 给老板/老师看 | 以上 + 3 种分辨率正常 |
| 比赛答辩 | 以上 + 离线可用 + 截图备份 + 投影仪检查 |

## 翻车预防清单

```
[ ] 页面加载时间 < 3 秒（比赛现场网络可能很差）
[ ] 字体不依赖外部 CDN（现场可能被墙/限速）
[ ] 数据有 fallback（API 挂了页面不能白屏）
[ ] 所有外部链接目标正确（别点到不该点的）
[ ] 页面标题正确（浏览器标签页显示的名字）
[ ] favicon 存在或不会 404
```

## 与现有 playwright-skill 的关系
本 Skill 定义**AAB 专属的验收标准**，不重复 Playwright 的 API 文档。具体测试代码的编写参考 `playwright-skill`，但检查什么、检查到什么程度由本 Skill 决定。
