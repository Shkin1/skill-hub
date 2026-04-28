# 设计令牌（Design Tokens）

完整的设计系统变量定义，所有组件样式都基于这些令牌构建。

---

## 颜色系统

### 背景层级（Surface）

深色主题的背景色从深到浅，形成视觉层次。

| 令牌名 | 值 | 用途 |
|--------|-----|------|
| `--surface-900` | `#0d1117` | 主背景，页面底色 |
| `--surface-800` | `#161b22` | 卡片背景，浮层背景 |
| `--surface-700` | `#21262d` | 边框，分割线 |
| `--surface-600` | `#30363d` | 次级边框，禁用边框 |
| `--surface-500` | `#484f58` | 禁用文字，占位符 |
| `--surface-400` | `#6e7681` | 描述文字，图标 |
| `--surface-300` | `#8b949e` | 次级文字 |
| `--surface-200` | `#b1bac4` | 强调文字 |
| `--surface-100` | `#c9d1d9` | 主要文字 |
| `--surface-50` | `#f0f6fc` | 最高对比文字 |

### 品牌色（Brand）

Amber 橙色系，温暖且在深色背景上突出。

| 令牌名 | 值 | 用途 |
|--------|-----|------|
| `--brand-600` | `#d97706` | 品牌深色，按下态 |
| `--brand-500` | `#f59e0b` | 品牌主色 |
| `--brand-400` | `#fbbf24` | 品牌高亮，悬停态 |
| `--brand-300` | `#fcd34d` | 渐变端点 |

### 语义色

| 令牌名 | 值 | 用途 |
|--------|-----|------|
| `--success-500` | `#22c55e` | 成功状态 |
| `--warning-500` | `#eab308` | 警告状态 |
| `--error-500` | `#ef4444` | 错误状态 |
| `--info-500` | `#3b82f6` | 信息状态 |

### 分类标签色

| 令牌名 | 值 | 用途 |
|--------|-----|------|
| `--tag-quant-bg` | `rgba(59, 130, 246, 0.12)` | 量化标签背景 |
| `--tag-quant-text` | `#60a5fa` | 量化标签文字 |
| `--tag-data-bg` | `rgba(168, 85, 247, 0.12)` | 数据标签背景 |
| `--tag-data-text` | `#c084fc` | 数据标签文字 |
| `--tag-code-bg` | `rgba(34, 197, 94, 0.12)` | 代码标签背景 |
| `--tag-code-text` | `#4ade80` | 代码标签文字 |

---

## 阴影系统

| 令牌名 | 值 | 用途 |
|--------|-----|------|
| `--shadow-card` | `0 0 0 1px rgba(48, 54, 61, 0.6), 0 2px 8px rgba(0, 0, 0, 0.4)` | 卡片默认阴影 |
| `--shadow-card-hover` | `0 0 0 1px rgba(245, 158, 11, 0.35), 0 8px 32px rgba(0, 0, 0, 0.5), 0 0 24px rgba(245, 158, 11, 0.15)` | 卡片悬停阴影 |
| `--shadow-glow` | `0 0 20px rgba(245, 158, 11, 0.3), 0 0 40px rgba(245, 158, 11, 0.15)` | 发光效果 |
| `--shadow-focus` | `0 0 0 2px rgba(245, 158, 11, 0.5)` | 焦点环 |

---

## 圆角系统

| 令牌名 | 值 | 用途 |
|--------|-----|------|
| `--radius-sm` | `4px` | 小按钮，标签 |
| `--radius-md` | `8px` | 输入框，小卡片 |
| `--radius-lg` | `12px` | 卡片，弹窗 |
| `--radius-xl` | `16px` | 大卡片 |
| `--radius-2xl` | `20px` | 特殊容器 |
| `--radius-full` | `9999px` | 药丸形，圆形 |

---

## 字体系统

### 字体族

```css
--font-sans: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', 'PingFang SC', sans-serif;
--font-mono: 'JetBrains Mono', 'Fira Code', monospace;
```

### 字号

| 令牌 | 值 | 用途 |
|------|-----|------|
| `--text-xs` | `11px` | 辅助文字，标签 |
| `--text-sm` | `13px` | 次级文字 |
| `--text-base` | `15px` | 正文 |
| `--text-lg` | `17px` | 小标题 |
| `--text-xl` | `20px` | 标题 |
| `--text-2xl` | `26px` | 大标题 |
| `--text-3xl` | `32px` | 页面标题 |
| `--text-4xl` | `40px` | Hero标题 |

### 字重

| 令牌 | 值 | 用途 |
|------|-----|------|
| `--font-normal` | `400` | 正文 |
| `--font-medium` | `500` | 强调文字 |
| `--font-semibold` | `600` | 小标题 |
| `--font-bold` | `700` | 标题 |
| `--font-black` | `900` | Hero标题 |

---

## 动画系统

### 缓动曲线

```css
--ease-out: cubic-bezier(0.16, 1, 0.3, 1);
--ease-in-out: cubic-bezier(0.65, 0, 0.35, 1);
--ease-spring: cubic-bezier(0.34, 1.56, 0.64, 1);
```

### 持续时间

| 令牌 | 值 | 用途 |
|------|-----|------|
| `--duration-fast` | `120ms` | 微交互，状态切换 |
| `--duration-normal` | `200ms` | 常规过渡 |
| `--duration-slow` | `300ms` | 入场动画 |
| `--duration-slower` | `500ms` | 复杂动画 |

---

## 间距系统

基于 4px 基础单位：

| 令牌 | 值 | 用途 |
|------|-----|------|
| `--space-1` | `4px` | 最小间距 |
| `--space-2` | `8px` | 紧凑间距 |
| `--space-3` | `12px` | 组件内部间距 |
| `--space-4` | `16px` | 标准间距 |
| `--space-5` | `20px` | 组件间距 |
| `--space-6` | `24px` | 区块间距 |
| `--space-8` | `32px` | 大区块间距 |
| `--space-10` | `40px` | 页面区块间距 |
| `--space-12` | `48px` | 大间距 |
| `--space-16` | `64px` | 页面级间距 |

---

## 完整 CSS 变量定义

```css
:root {
  /* 背景层级 */
  --surface-900: #0d1117;
  --surface-800: #161b22;
  --surface-700: #21262d;
  --surface-600: #30363d;
  --surface-500: #484f58;
  --surface-400: #6e7681;
  --surface-300: #8b949e;
  --surface-200: #b1bac4;
  --surface-100: #c9d1d9;
  --surface-50: #f0f6fc;

  /* 品牌色 */
  --brand-600: #d97706;
  --brand-500: #f59e0b;
  --brand-400: #fbbf24;
  --brand-300: #fcd34d;

  /* 语义色 */
  --success-500: #22c55e;
  --warning-500: #eab308;
  --error-500: #ef4444;
  --info-500: #3b82f6;

  /* 标签色 */
  --tag-quant-bg: rgba(59, 130, 246, 0.12);
  --tag-quant-text: #60a5fa;
  --tag-data-bg: rgba(168, 85, 247, 0.12);
  --tag-data-text: #c084fc;
  --tag-code-bg: rgba(34, 197, 94, 0.12);
  --tag-code-text: #4ade80;

  /* 阴影 */
  --shadow-card: 0 0 0 1px rgba(48, 54, 61, 0.6), 0 2px 8px rgba(0, 0, 0, 0.4);
  --shadow-card-hover: 0 0 0 1px rgba(245, 158, 11, 0.35), 0 8px 32px rgba(0, 0, 0, 0.5), 0 0 24px rgba(245, 158, 11, 0.15);
  --shadow-glow: 0 0 20px rgba(245, 158, 11, 0.3), 0 0 40px rgba(245, 158, 11, 0.15);
  --shadow-focus: 0 0 0 2px rgba(245, 158, 11, 0.5);

  /* 圆角 */
  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 12px;
  --radius-xl: 16px;
  --radius-2xl: 20px;
  --radius-full: 9999px;

  /* 字体 */
  --font-sans: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', 'PingFang SC', sans-serif;
  --font-mono: 'JetBrains Mono', 'Fira Code', monospace;

  /* 动画 */
  --ease-out: cubic-bezier(0.16, 1, 0.3, 1);
  --ease-in-out: cubic-bezier(0.65, 0, 0.35, 1);
  --ease-spring: cubic-bezier(0.34, 1.56, 0.64, 1);
  --duration-fast: 120ms;
  --duration-normal: 200ms;
  --duration-slow: 300ms;
  --duration-slower: 500ms;

  /* 间距 */
  --space-1: 4px;
  --space-2: 8px;
  --space-3: 12px;
  --space-4: 16px;
  --space-5: 20px;
  --space-6: 24px;
  --space-8: 32px;
  --space-10: 40px;
  --space-12: 48px;
  --space-16: 64px;
}
```