# CSS 组件样式

完整的组件样式定义，基于设计令牌构建。

---

## 基础重置与全局样式

```css
/* 基础重置 */
*, *::before, *::after {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

html {
    scroll-behavior: smooth;
}

body {
    font-family: var(--font-sans);
    font-size: 15px;
    line-height: 1.6;
    color: var(--surface-100);
    background-color: var(--surface-900);
    min-height: 100vh;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

a {
    color: inherit;
    text-decoration: none;
}

button {
    font-family: inherit;
    cursor: pointer;
    border: none;
    background: none;
}

/* 选中文本样式 */
::selection {
    background: rgba(245, 158, 11, 0.3);
    color: var(--surface-50);
}
```

---

## 背景装饰

```css
/* 网格背景 */
.grid-bg {
    position: fixed;
    inset: 0;
    background-image: 
        linear-gradient(rgba(48, 54, 61, 0.3) 1px, transparent 1px),
        linear-gradient(90deg, rgba(48, 54, 61, 0.3) 1px, transparent 1px);
    background-size: 60px 60px;
    pointer-events: none;
    z-index: 0;
}

/* Hero 光晕 */
.hero-glow {
    position: fixed;
    top: -200px;
    left: 50%;
    transform: translateX(-50%);
    width: 800px;
    height: 600px;
    background: radial-gradient(
        ellipse at center,
        rgba(245, 158, 11, 0.08) 0%,
        rgba(245, 158, 11, 0.03) 40%,
        transparent 70%
    );
    pointer-events: none;
    z-index: 0;
}
```

---

## 导航栏

```css
.header {
    position: sticky;
    top: 0;
    z-index: 100;
    padding: 16px 24px;
    transition: all var(--duration-normal) var(--ease-out);
}

.header.scrolled {
    background: rgba(13, 17, 23, 0.85);
    backdrop-filter: blur(16px);
    border-bottom: 1px solid var(--surface-800);
}

.header-inner {
    max-width: 1280px;
    margin: 0 auto;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

/* Logo */
.logo {
    display: flex;
    align-items: center;
    gap: 10px;
}

.logo-icon {
    width: 32px;
    height: 32px;
    background: linear-gradient(135deg, var(--brand-500), var(--brand-300));
    border-radius: var(--radius-md);
}

.logo-text {
    font-size: 17px;
    font-weight: 600;
    color: var(--surface-100);
}

.logo-text .accent {
    color: var(--brand-400);
}

/* 导航 */
.nav {
    display: flex;
    align-items: center;
    gap: 8px;
}

.nav-link {
    padding: 8px 16px;
    font-size: 14px;
    font-weight: 500;
    color: var(--surface-300);
    border-radius: var(--radius-md);
    transition: all var(--duration-fast) var(--ease-out);
}

.nav-link:hover {
    color: var(--surface-100);
    background: var(--surface-800);
}

.nav-link.active {
    color: var(--brand-400);
    background: rgba(245, 158, 11, 0.1);
}

/* 导航按钮 */
.nav-btn {
    display: flex;
    align-items: center;
    gap: 6px;
    padding: 8px 16px;
    font-size: 14px;
    font-weight: 600;
    color: var(--surface-900);
    background: linear-gradient(135deg, var(--brand-400), var(--brand-500));
    border-radius: var(--radius-md);
    transition: all var(--duration-fast) var(--ease-out);
}

.nav-btn:hover {
    transform: translateY(-1px);
    box-shadow: var(--shadow-glow);
}

.nav-btn .btn-icon {
    width: 14px;
    height: 14px;
}
```

---

## Hero 区域

```css
.hero {
    position: relative;
    z-index: 1;
    text-align: center;
    padding: 80px 24px 60px;
}

/* 徽章 */
.hero-badge {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 6px 14px;
    font-size: 13px;
    font-weight: 500;
    color: var(--brand-400);
    background: rgba(245, 158, 11, 0.1);
    border: 1px solid rgba(245, 158, 11, 0.2);
    border-radius: var(--radius-full);
    margin-bottom: 24px;
}

.hero-badge-dot {
    width: 6px;
    height: 6px;
    background: var(--brand-400);
    border-radius: 50%;
    animation: pulse 2s infinite;
}

@keyframes pulse {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.5; }
}

/* 标题 */
.hero-title {
    font-size: clamp(32px, 5vw, 48px);
    font-weight: 900;
    color: var(--surface-50);
    margin-bottom: 16px;
    letter-spacing: -0.02em;
}

.hero-title .gradient {
    background: linear-gradient(135deg, var(--brand-400), var(--brand-300));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
}

/* 副标题 */
.hero-sub {
    font-size: 17px;
    color: var(--surface-400);
    max-width: 600px;
    margin: 0 auto 32px;
}

/* 统计数据 */
.hero-stats {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 24px;
}

.stat-item {
    font-size: 14px;
    color: var(--surface-400);
}

.stat-value {
    font-size: 20px;
    font-weight: 700;
    color: var(--surface-100);
    margin-right: 4px;
}

.stat-divider {
    width: 1px;
    height: 24px;
    background: var(--surface-700);
}
```

---

## 工具栏

```css
.toolbar {
    position: relative;
    z-index: 1;
    max-width: 1280px;
    margin: 0 auto;
    padding: 0 24px 24px;
    display: flex;
    align-items: center;
    gap: 16px;
    flex-wrap: wrap;
}

/* 搜索框 */
.search {
    position: relative;
    flex: 1;
    min-width: 200px;
    max-width: 400px;
}

.search-input {
    width: 100%;
    padding: 10px 16px 10px 42px;
    font-size: 14px;
    color: var(--surface-100);
    background: var(--surface-800);
    border: 1px solid var(--surface-700);
    border-radius: var(--radius-md);
    outline: none;
    transition: all var(--duration-fast) var(--ease-out);
}

.search-input::placeholder {
    color: var(--surface-500);
}

.search-input:focus {
    border-color: rgba(245, 158, 11, 0.5);
    background: var(--surface-700);
}

.search-input:focus + .search-icon {
    color: var(--brand-400);
}

.search-icon {
    position: absolute;
    left: 14px;
    top: 50%;
    transform: translateY(-50%);
    width: 18px;
    height: 18px;
    color: var(--surface-500);
    pointer-events: none;
    transition: color var(--duration-fast) var(--ease-out);
}

/* 筛选按钮组 */
.filters {
    display: flex;
    align-items: center;
    gap: 8px;
    flex-wrap: wrap;
}

.filter-btn {
    padding: 8px 16px;
    font-size: 13px;
    font-weight: 500;
    color: var(--surface-300);
    background: transparent;
    border: 1px solid var(--surface-700);
    border-radius: var(--radius-md);
    transition: all var(--duration-fast) var(--ease-out);
}

.filter-btn:hover {
    color: var(--surface-100);
    border-color: var(--surface-600);
}

.filter-btn.active {
    color: var(--brand-400);
    background: rgba(245, 158, 11, 0.12);
    border-color: rgba(245, 158, 11, 0.35);
    box-shadow: 0 0 12px rgba(245, 158, 11, 0.1);
}

/* 结果信息 */
.results-info {
    position: relative;
    z-index: 1;
    max-width: 1280px;
    margin: 0 auto;
    padding: 0 24px 16px;
    font-size: 13px;
    color: var(--surface-500);
}

.results-num {
    color: var(--surface-300);
    font-weight: 600;
}
```

---

## 卡片网格

```css
.grid {
    position: relative;
    z-index: 1;
    max-width: 1280px;
    margin: 0 auto;
    padding: 0 24px;
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(340px, 1fr));
    gap: 24px;
}
```

---

## 卡片组件

```css
.card {
    position: relative;
    padding: 20px;
    background: var(--surface-800);
    border: 1px solid var(--surface-700);
    border-radius: var(--radius-lg);
    box-shadow: var(--shadow-card);
    transition: all var(--duration-normal) var(--ease-out);
    overflow: hidden;
}

.card:hover {
    transform: translateY(-3px);
    border-color: rgba(245, 158, 11, 0.3);
    box-shadow: var(--shadow-card-hover);
}

/* 卡片涟漪效果 */
.card-ripple {
    position: absolute;
    inset: 0;
    background: radial-gradient(
        circle at var(--ripple-x, 50%) var(--ripple-y, 50%),
        rgba(245, 158, 11, 0.08) 0%,
        transparent 50%
    );
    opacity: 0;
    transition: opacity var(--duration-normal) var(--ease-out);
    pointer-events: none;
}

.card:hover .card-ripple {
    opacity: 1;
}

/* 卡片头部 */
.card-header {
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    margin-bottom: 16px;
}

.card-icon {
    width: 40px;
    height: 40px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: var(--surface-700);
    border-radius: var(--radius-md);
}

.card-icon svg {
    width: 20px;
    height: 20px;
    color: var(--brand-400);
}

.card-meta {
    display: flex;
    align-items: center;
    gap: 8px;
}

.card-level {
    padding: 4px 10px;
    font-size: 11px;
    font-weight: 600;
    color: var(--surface-400);
    background: var(--surface-700);
    border-radius: var(--radius-full);
}

/* 卡片内容 */
.card-body {
    margin-bottom: 16px;
}

.card-title {
    font-size: 17px;
    font-weight: 600;
    color: var(--surface-100);
    margin-bottom: 8px;
    transition: color var(--duration-fast) var(--ease-out);
}

.card:hover .card-title {
    color: var(--brand-400);
}

.card-desc {
    font-size: 13px;
    color: var(--surface-400);
    line-height: 1.6;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
}

/* 卡片标签 */
.card-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-bottom: 16px;
}

.tag {
    padding: 4px 10px;
    font-size: 11px;
    font-weight: 500;
    border-radius: var(--radius-full);
}

.tag-quant {
    background: var(--tag-quant-bg);
    color: var(--tag-quant-text);
}

.tag-data {
    background: var(--tag-data-bg);
    color: var(--tag-data-text);
}

.tag-code {
    background: var(--tag-code-bg);
    color: var(--tag-code-text);
}

/* 卡片底部 */
.card-footer {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding-top: 16px;
    border-top: 1px solid var(--surface-700);
}

.card-author {
    font-size: 12px;
    color: var(--surface-500);
}

.author-name {
    color: var(--surface-300);
}

.card-stats {
    display: flex;
    align-items: center;
    gap: 4px;
    font-size: 12px;
    color: var(--surface-500);
}

.star-icon {
    width: 14px;
    height: 14px;
    color: var(--brand-400);
}

.star-count {
    font-weight: 500;
}
```

---

## 空状态

```css
.empty {
    position: relative;
    z-index: 1;
    max-width: 1280px;
    margin: 0 auto;
    padding: 80px 24px;
    text-align: center;
}

.empty-icon {
    width: 64px;
    height: 64px;
    color: var(--surface-600);
    margin-bottom: 16px;
}

.empty-title {
    font-size: 17px;
    font-weight: 600;
    color: var(--surface-300);
    margin-bottom: 8px;
}

.empty-desc {
    font-size: 14px;
    color: var(--surface-500);
}
```

---

## 页脚

```css
.footer {
    position: relative;
    z-index: 1;
    text-align: center;
    padding: 40px 24px;
    margin-top: 60px;
    font-size: 13px;
    color: var(--surface-500);
    border-top: 1px solid var(--surface-800);
}
```

---

## 动画

```css
/* 入场动画 */
@keyframes fadeInUp {
    from {
        opacity: 0;
        transform: translateY(20px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

.card {
    animation: fadeInUp var(--duration-slow) var(--ease-out) backwards;
}

/* 交错入场 */
.card:nth-child(1) { animation-delay: 0ms; }
.card:nth-child(2) { animation-delay: 50ms; }
.card:nth-child(3) { animation-delay: 100ms; }
.card:nth-child(4) { animation-delay: 150ms; }
.card:nth-child(5) { animation-delay: 200ms; }
.card:nth-child(6) { animation-delay: 250ms; }

/* 高亮匹配文本 */
.highlight {
    background: rgba(245, 158, 11, 0.3);
    color: var(--brand-400);
    padding: 0 2px;
    border-radius: 2px;
}
```

---

## 响应式

```css
/* 平板 */
@media (max-width: 768px) {
    .hero {
        padding: 60px 20px 40px;
    }
    
    .hero-title {
        font-size: 28px;
    }
    
    .hero-stats {
        flex-wrap: wrap;
        gap: 16px;
    }
    
    .toolbar {
        flex-direction: column;
        align-items: stretch;
    }
    
    .search {
        max-width: none;
    }
    
    .grid {
        grid-template-columns: 1fr;
    }
}

/* 移动端 */
@media (max-width: 480px) {
    .header {
        padding: 12px 16px;
    }
    
    .nav-link {
        display: none;
    }
    
    .hero-title {
        font-size: 24px;
    }
    
    .hero-sub {
        font-size: 15px;
    }
    
    .grid {
        padding: 0 16px;
        gap: 16px;
    }
    
    .card {
        padding: 16px;
    }
}
```