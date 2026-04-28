# JavaScript 交互逻辑

完整的交互逻辑实现，包含搜索、筛选、动画效果等。

---

## 初始化

```javascript
// DOM 元素
const header = document.getElementById('header');
const searchInput = document.getElementById('searchInput');
const filters = document.getElementById('filters');
const cardsGrid = document.getElementById('cardsGrid');
const countNum = document.getElementById('countNum');
const emptyState = document.getElementById('emptyState');

// 状态
let currentCategory = 'all';
let currentSearchTerm = '';
let cards = [];

// 数据
const cardsData = []; // 从 JSON 加载或直接定义
```

---

## 数据加载

```javascript
async function loadData() {
    try {
        const response = await fetch('data/items.json');
        const data = await response.json();
        cards = data;
        renderCards();
    } catch (error) {
        console.error('Failed to load data:', error);
    }
}

// 页面加载时执行
document.addEventListener('DOMContentLoaded', loadData);
```

---

## 卡片渲染

```javascript
function renderCards() {
    // 过滤数据
    const filtered = cards.filter(card => {
        const matchCategory = currentCategory === 'all' || card.category === currentCategory;
        const matchSearch = !currentSearchTerm || 
            card.name.toLowerCase().includes(currentSearchTerm) ||
            card.description.toLowerCase().includes(currentSearchTerm) ||
            (card.tags && card.tags.some(tag => tag.toLowerCase().includes(currentSearchTerm)));
        return matchCategory && matchSearch;
    });

    // 更新计数
    countNum.textContent = filtered.length;

    // 显示/隐藏空状态
    emptyState.style.display = filtered.length === 0 ? 'block' : 'none';

    // 渲染卡片
    cardsGrid.innerHTML = filtered.map((card, index) => createCardHTML(card, index)).join('');

    // 绑定卡片事件
    bindCardEvents();
}

function createCardHTML(card, index) {
    const tagsHTML = card.tags 
        ? card.tags.map(tag => `<span class="tag tag-${card.category}">${tag}</span>`).join('')
        : '';

    return `
        <article class="card" data-id="${card.id}" style="animation-delay: ${index * 50}ms">
            <div class="card-header">
                <div class="card-icon">
                    ${getIconSVG(card.icon)}
                </div>
                ${card.level ? `<span class="card-level">${card.level}</span>` : ''}
            </div>
            <div class="card-body">
                <h3 class="card-title">${highlightText(card.name)}</h3>
                <p class="card-desc">${highlightText(card.description)}</p>
            </div>
            ${tagsHTML ? `<div class="card-tags">${tagsHTML}</div>` : ''}
            <div class="card-footer">
                <div class="card-author">
                    ${card.author ? `<span class="author-name">${card.author.name}</span>` : ''}
                </div>
                ${card.stars !== undefined ? `
                    <div class="card-stats">
                        <svg class="star-icon" viewBox="0 0 24 24" fill="currentColor">
                            <path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/>
                        </svg>
                        <span class="star-count">${card.stars}</span>
                    </div>
                ` : ''}
            </div>
            <div class="card-ripple"></div>
        </article>
    `;
}

function highlightText(text) {
    if (!currentSearchTerm) return text;
    const regex = new RegExp(`(${escapeRegExp(currentSearchTerm)})`, 'gi');
    return text.replace(regex, '<span class="highlight">$1</span>');
}

function escapeRegExp(string) {
    return string.replace(/[.*+?^${}()|[\]\\]/g, '\\$&');
}

function getIconSVG(iconName) {
    const icons = {
        chart: '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M3 3v18h18"/><path d="m19 9-5 5-4-4-3 3"/></svg>',
        code: '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="16 18 22 12 16 6"/><polyline points="8 6 2 12 8 18"/></svg>',
        data: '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><ellipse cx="12" cy="5" rx="9" ry="3"/><path d="M21 12c0 1.66-4 3-9 3s-9-1.34-9-3"/><path d="M3 5v14c0 1.66 4 3 9 3s9-1.34 9-3V5"/></svg>',
        default: '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/></svg>'
    };
    return icons[iconName] || icons.default;
}
```

---

## 卡片事件绑定

```javascript
function bindCardEvents() {
    const cards = document.querySelectorAll('.card');
    
    cards.forEach(card => {
        // 涟漪效果
        card.addEventListener('mousemove', handleCardMouseMove);
        card.addEventListener('mouseleave', handleCardMouseLeave);
        
        // 点击事件
        card.addEventListener('click', handleCardClick);
    });
}

function handleCardMouseMove(e) {
    const rect = e.currentTarget.getBoundingClientRect();
    const x = ((e.clientX - rect.left) / rect.width) * 100;
    const y = ((e.clientY - rect.top) / rect.height) * 100;
    
    e.currentTarget.style.setProperty('--ripple-x', `${x}%`);
    e.currentTarget.style.setProperty('--ripple-y', `${y}%`);
}

function handleCardMouseLeave(e) {
    e.currentTarget.style.setProperty('--ripple-x', '50%');
    e.currentTarget.style.setProperty('--ripple-y', '50%');
}

function handleCardClick(e) {
    const cardId = e.currentTarget.dataset.id;
    const cardData = cards.find(c => c.id == cardId);
    
    // 触发自定义事件或导航
    console.log('Card clicked:', cardData);
    
    // 示例：跳转到详情页
    // window.location.href = `/detail/${cardId}`;
    
    // 示例：打开模态框
    // openModal(cardData);
}
```

---

## 搜索功能

```javascript
let searchTimer;

function initSearch() {
    searchInput.addEventListener('input', (e) => {
        clearTimeout(searchTimer);
        searchTimer = setTimeout(() => {
            currentSearchTerm = e.target.value.trim().toLowerCase();
            renderCards();
        }, 150);
    });

    // 清除搜索（ESC键）
    searchInput.addEventListener('keydown', (e) => {
        if (e.key === 'Escape') {
            searchInput.value = '';
            currentSearchTerm = '';
            renderCards();
        }
    });
}

// 初始化时调用
initSearch();
```

---

## 筛选功能

```javascript
function initFilters() {
    const filterBtns = filters.querySelectorAll('.filter-btn');
    
    filterBtns.forEach(btn => {
        btn.addEventListener('click', () => {
            // 更新激活状态
            filterBtns.forEach(b => b.classList.remove('active'));
            btn.classList.add('active');
            
            // 更新筛选条件
            currentCategory = btn.dataset.category;
            renderCards();
        });
    });
}

// 初始化时调用
initFilters();
```

---

## 滚动效果

```css
/* 头部滚动效果 */
function initScrollEffect() {
    let lastScrollY = 0;
    let ticking = false;

    window.addEventListener('scroll', () => {
        lastScrollY = window.scrollY;
        
        if (!ticking) {
            requestAnimationFrame(() => {
                handleScroll(lastScrollY);
                ticking = false;
            });
            ticking = true;
        }
    });
}

function handleScroll(scrollY) {
    // 头部毛玻璃效果
    if (scrollY > 16) {
        header.classList.add('scrolled');
    } else {
        header.classList.remove('scrolled');
    }
}

// 初始化时调用
initScrollEffect();
```

---

## 入场动画

```javascript
function initEntryAnimations() {
    // 使用 Intersection Observer 实现滚动入场
    const observer = new IntersectionObserver(
        (entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('visible');
                    observer.unobserve(entry.target);
                }
            });
        },
        {
            threshold: 0.1,
            rootMargin: '0px 0px -50px 0px'
        }
    );

    // 观察所有卡片
    document.querySelectorAll('.card').forEach(card => {
        observer.observe(card);
    });
}

// 在 renderCards 后调用
function renderCards() {
    // ... 渲染逻辑
    
    // 初始化入场动画
    requestAnimationFrame(() => {
        initEntryAnimations();
    });
}
```

---

## 键盘导航

```javascript
function initKeyboardNavigation() {
    document.addEventListener('keydown', (e) => {
        // Ctrl/Cmd + K 聚焦搜索框
        if ((e.ctrlKey || e.metaKey) && e.key === 'k') {
            e.preventDefault();
            searchInput.focus();
        }
        
        // Ctrl/Cmd + / 切换筛选
        if ((e.ctrlKey || e.metaKey) && e.key === '/') {
            e.preventDefault();
            const filterBtns = filters.querySelectorAll('.filter-btn');
            const activeIndex = Array.from(filterBtns).findIndex(btn => btn.classList.contains('active'));
            const nextIndex = (activeIndex + 1) % filterBtns.length;
            filterBtns[nextIndex].click();
        }
    });
}

// 初始化时调用
initKeyboardNavigation();
```

---

## 完整代码

```javascript
(function() {
    'use strict';

    // DOM 元素
    const header = document.getElementById('header');
    const searchInput = document.getElementById('searchInput');
    const filters = document.getElementById('filters');
    const cardsGrid = document.getElementById('cardsGrid');
    const countNum = document.getElementById('countNum');
    const emptyState = document.getElementById('emptyState');

    // 状态
    let currentCategory = 'all';
    let currentSearchTerm = '';
    let cards = [];
    let searchTimer;

    // 初始化
    document.addEventListener('DOMContentLoaded', () => {
        loadData();
        initSearch();
        initFilters();
        initScrollEffect();
        initKeyboardNavigation();
    });

    // 数据加载
    async function loadData() {
        try {
            const response = await fetch('data/items.json');
            cards = await response.json();
            renderCards();
        } catch (error) {
            console.error('Failed to load data:', error);
        }
    }

    // 渲染卡片
    function renderCards() {
        const filtered = cards.filter(card => {
            const matchCategory = currentCategory === 'all' || card.category === currentCategory;
            const matchSearch = !currentSearchTerm || 
                card.name.toLowerCase().includes(currentSearchTerm) ||
                card.description.toLowerCase().includes(currentSearchTerm);
            return matchCategory && matchSearch;
        });

        countNum.textContent = filtered.length;
        emptyState.style.display = filtered.length === 0 ? 'block' : 'none';
        cardsGrid.innerHTML = filtered.map((card, i) => createCardHTML(card, i)).join('');
        bindCardEvents();
    }

    // 创建卡片 HTML
    function createCardHTML(card, index) {
        return `
            <article class="card" data-id="${card.id}" style="animation-delay: ${index * 50}ms">
                <div class="card-header">
                    <div class="card-icon">${getIconSVG(card.icon)}</div>
                    ${card.level ? `<span class="card-level">${card.level}</span>` : ''}
                </div>
                <div class="card-body">
                    <h3 class="card-title">${highlightText(card.name)}</h3>
                    <p class="card-desc">${highlightText(card.description)}</p>
                </div>
                <div class="card-footer">
                    <div class="card-author">
                        ${card.author ? `<span class="author-name">${card.author.name}</span>` : ''}
                    </div>
                    ${card.stars !== undefined ? `
                        <div class="card-stats">
                            <svg class="star-icon" viewBox="0 0 24 24" fill="currentColor">
                                <path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/>
                            </svg>
                            <span class="star-count">${card.stars}</span>
                        </div>
                    ` : ''}
                </div>
                <div class="card-ripple"></div>
            </article>
        `;
    }

    // 高亮搜索文本
    function highlightText(text) {
        if (!currentSearchTerm) return text;
        const regex = new RegExp(`(${escapeRegExp(currentSearchTerm)})`, 'gi');
        return text.replace(regex, '<span class="highlight">$1</span>');
    }

    function escapeRegExp(string) {
        return string.replace(/[.*+?^${}()|[\]\\]/g, '\\$&');
    }

    // 图标 SVG
    function getIconSVG(name) {
        const icons = {
            chart: '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M3 3v18h18"/><path d="m19 9-5 5-4-4-3 3"/></svg>',
            code: '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="16 18 22 12 16 6"/><polyline points="8 6 2 12 8 18"/></svg>',
            data: '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><ellipse cx="12" cy="5" rx="9" ry="3"/><path d="M21 12c0 1.66-4 3-9 3s-9-1.34-9-3"/><path d="M3 5v14c0 1.66 4 3 9 3s9-1.34 9-3V5"/></svg>'
        };
        return icons[name] || icons.chart;
    }

    // 卡片事件
    function bindCardEvents() {
        document.querySelectorAll('.card').forEach(card => {
            card.addEventListener('mousemove', (e) => {
                const rect = card.getBoundingClientRect();
                card.style.setProperty('--ripple-x', `${((e.clientX - rect.left) / rect.width) * 100}%`);
                card.style.setProperty('--ripple-y', `${((e.clientY - rect.top) / rect.height) * 100}%`);
            });
        });
    }

    // 搜索
    function initSearch() {
        searchInput.addEventListener('input', (e) => {
            clearTimeout(searchTimer);
            searchTimer = setTimeout(() => {
                currentSearchTerm = e.target.value.trim().toLowerCase();
                renderCards();
            }, 150);
        });
    }

    // 筛选
    function initFilters() {
        filters.addEventListener('click', (e) => {
            if (e.target.classList.contains('filter-btn')) {
                filters.querySelectorAll('.filter-btn').forEach(btn => btn.classList.remove('active'));
                e.target.classList.add('active');
                currentCategory = e.target.dataset.category;
                renderCards();
            }
        });
    }

    // 滚动效果
    function initScrollEffect() {
        window.addEventListener('scroll', () => {
            requestAnimationFrame(() => {
                header.classList.toggle('scrolled', window.scrollY > 16);
            });
        });
    }

    // 键盘导航
    function initKeyboardNavigation() {
        document.addEventListener('keydown', (e) => {
            if ((e.ctrlKey || e.metaKey) && e.key === 'k') {
                e.preventDefault();
                searchInput.focus();
            }
        });
    }
})();
```

---

## 性能优化建议

1. **防抖搜索**：使用 150ms 防抖避免频繁渲染
2. **虚拟滚动**：卡片数量超过 100 时考虑虚拟滚动
3. **图片懒加载**：卡片图片使用 `loading="lazy"`
4. **CSS 动画**：优先使用 `transform` 和 `opacity`
5. **事件委托**：筛选按钮使用事件委托
6. **requestAnimationFrame**：滚动事件使用 RAF 优化