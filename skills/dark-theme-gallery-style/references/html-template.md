# HTML 结构模板

完整的页面结构模板，包含所有核心组件。

---

## 基础页面结构

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Your Gallery</title>
    
    <!-- 字体 -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;900&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
    
    <!-- 样式 -->
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <!-- 背景装饰 -->
    <div class="grid-bg"></div>
    <div class="hero-glow"></div>

    <!-- 导航栏 -->
    <header class="header" id="header">
        <div class="header-inner">
            <a href="#" class="logo">
                <div class="logo-icon"></div>
                <span class="logo-text"><span class="accent">your</span>-gallery</span>
            </a>
            <nav class="nav">
                <a href="#" class="nav-link active">首页</a>
                <a href="#" class="nav-link">Gallery</a>
                <a href="#" class="nav-btn">Star</a>
            </nav>
        </div>
    </header>

    <!-- Hero 区域 -->
    <section class="hero">
        <div class="hero-badge">
            <span class="hero-badge-dot"></span>
            Your Badge Text
        </div>
        <h1 class="hero-title">探索 <span class="gradient">Gallery</span></h1>
        <p class="hero-sub">你的描述文字</p>
        <div class="hero-stats">
            <div class="stat-item">
                <span class="stat-value">10+</span> Items
            </div>
        </div>
    </section>

    <!-- 工具栏 -->
    <div class="toolbar">
        <div class="search">
            <input type="text" id="searchInput" class="search-input" placeholder="搜索...">
            <svg class="search-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <circle cx="11" cy="11" r="8"/>
                <path d="m21 21-4.35-4.35"/>
            </svg>
        </div>
        <div class="filters" id="filters">
            <button class="filter-btn active" data-category="all">全部</button>
            <button class="filter-btn" data-category="cat1">分类1</button>
            <button class="filter-btn" data-category="cat2">分类2</button>
        </div>
    </div>

    <!-- 结果信息 -->
    <p class="results-info">共 <span class="results-num" id="countNum">0</span> 项</p>

    <!-- 卡片网格 -->
    <main>
        <div class="grid" id="cardsGrid"></div>
        <div class="empty" id="emptyState" style="display: none;">
            <p class="empty-title">未找到匹配项</p>
        </div>
    </main>

    <!-- 页脚 -->
    <footer class="footer">Your Footer</footer>

    <!-- 脚本 -->
    <script src="js/main.js"></script>
</body>
</html>
```

---

## 卡片组件结构

```html
<article class="card" data-category="cat1" data-id="1">
    <!-- 卡片头部 -->
    <div class="card-header">
        <div class="card-icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <!-- 图标路径 -->
            </svg>
        </div>
        <div class="card-meta">
            <span class="card-level">级别</span>
        </div>
    </div>

    <!-- 卡片内容 -->
    <div class="card-body">
        <h3 class="card-title">项目名称</h3>
        <p class="card-desc">项目描述文字</p>
    </div>

    <!-- 卡片标签 -->
    <div class="card-tags">
        <span class="tag tag-quant">标签1</span>
        <span class="tag tag-data">标签2</span>
    </div>

    <!-- 卡片底部 -->
    <div class="card-footer">
        <div class="card-author">
            <span class="author-name">作者</span>
        </div>
        <div class="card-stats">
            <svg class="star-icon" viewBox="0 0 24 24" fill="currentColor">
                <path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/>
            </svg>
            <span class="star-count">100</span>
        </div>
    </div>

    <!-- 涟漪效果层 -->
    <div class="card-ripple"></div>
</article>
```

---

## 导航栏组件

```html
<header class="header" id="header">
    <div class="header-inner">
        <!-- Logo -->
        <a href="#" class="logo">
            <div class="logo-icon"></div>
            <span class="logo-text"><span class="accent">your</span>-gallery</span>
        </a>
        
        <!-- 导航链接 -->
        <nav class="nav">
            <a href="#" class="nav-link active">首页</a>
            <a href="#" class="nav-link">Gallery</a>
            <a href="#" class="nav-link">About</a>
            <a href="#" class="nav-btn">
                <svg class="btn-icon" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/>
                </svg>
                Star
            </a>
        </nav>
    </div>
</header>
```

---

## Hero 区域组件

```html
<section class="hero">
    <!-- 徽章 -->
    <div class="hero-badge">
        <span class="hero-badge-dot"></span>
        New Release
    </div>
    
    <!-- 标题 -->
    <h1 class="hero-title">
        探索 <span class="gradient">Gallery</span>
    </h1>
    
    <!-- 副标题 -->
    <p class="hero-sub">
        一套完整的现代化深色主题卡片画廊样式系统
    </p>
    
    <!-- 统计数据 -->
    <div class="hero-stats">
        <div class="stat-item">
            <span class="stat-value">10+</span> Items
        </div>
        <div class="stat-divider"></div>
        <div class="stat-item">
            <span class="stat-value">5</span> Categories
        </div>
        <div class="stat-divider"></div>
        <div class="stat-item">
            <span class="stat-value">100%</span> Responsive
        </div>
    </div>
</section>
```

---

## 搜索筛选组件

```html
<div class="toolbar">
    <!-- 搜索框 -->
    <div class="search">
        <input 
            type="text" 
            id="searchInput" 
            class="search-input" 
            placeholder="搜索项目..."
            autocomplete="off"
        >
        <svg class="search-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <circle cx="11" cy="11" r="8"/>
            <path d="m21 21-4.35-4.35"/>
        </svg>
    </div>
    
    <!-- 筛选按钮组 -->
    <div class="filters" id="filters">
        <button class="filter-btn active" data-category="all">全部</button>
        <button class="filter-btn" data-category="quant">量化</button>
        <button class="filter-btn" data-category="data">数据</button>
        <button class="filter-btn" data-category="code">代码</button>
    </div>
</div>
```

---

## 空状态组件

```html
<div class="empty" id="emptyState">
    <svg class="empty-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
        <circle cx="11" cy="11" r="8"/>
        <path d="m21 21-4.35-4.35"/>
        <path d="M8 11h6"/>
    </svg>
    <p class="empty-title">未找到匹配项</p>
    <p class="empty-desc">尝试调整搜索条件或筛选分类</p>
</div>
```

---

## 数据格式

```json
[
    {
        "id": 1,
        "name": "项目名称",
        "description": "项目描述文字，建议不超过100字",
        "category": "quant",
        "tags": ["量化", "策略"],
        "level": "高级",
        "icon": "chart",
        "author": {
            "name": "作者名",
            "github": "username"
        },
        "stars": 100,
        "created_at": "2024-01-01",
        "pinned": true
    }
]
```

### 字段说明

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `id` | number | 是 | 唯一标识 |
| `name` | string | 是 | 项目名称 |
| `description` | string | 是 | 项目描述 |
| `category` | string | 是 | 分类标识 |
| `tags` | string[] | 否 | 标签数组 |
| `level` | string | 否 | 难度级别 |
| `icon` | string | 否 | 图标名称 |
| `author` | object | 否 | 作者信息 |
| `stars` | number | 否 | 星标数 |
| `created_at` | string | 否 | 创建日期 |
| `pinned` | boolean | 否 | 是否置顶 |