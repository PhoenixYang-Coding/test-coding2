# Phase 2 — Navigation & Header Icon Replacement

## 前置分析

当前 `index.html` 中**不存在** Phase 2 提到的以下元素：
- `☰` 汉堡菜单 / `.menu-toggle`
- `▶` 播放按钮 / `.hero-play-button`
- `★` 星标图标

因此需要**新增**这些 UI 组件，全部使用 Lucide 图标库（已通过 CDN 引入）渲染为 SVG。

---

## #0 导航栏：新增移动端汉堡菜单

### HTML 变更（index.html ~L439）

在 `.navbar` 中新增 `<button class="menu-toggle">`：

```html
<button class="menu-toggle" aria-label="打开菜单" onclick="toggleMenu(this)">
  <i data-lucide="menu"></i>
</button>
```

- 放置于 `<div class="logo">` 之后、`<nav>` 之前
- 使用 Lucide `menu` 图标，`lucide.createIcons()` 会自动渲染为 SVG
- 添加 `aria-label` 满足无障碍要求

### CSS 变更（index.html `<style>` 区）

```css
/* 汉堡菜单按钮 - 默认隐藏 */
.menu-toggle {
  display: none;                          /* 桌面端隐藏 */
  background: none;                       /* 透明背景 */
  border: none;                           /* 无边框 */
  color: #e6c9b8;                         /* 暖米色图标 */
  cursor: pointer;                        /* 手型光标 */
  padding: 8px;                           /* 点击区域 */
}

/* 平板以下：显示汉堡、导航改为垂直 */
@media (max-width: 768px) {
  .menu-toggle {
    display: block;                       /* 显示汉堡按钮 */
  }
  .navbar nav {
    display: none;                        /* 默认隐藏导航 */
    flex-direction: column;               /* 垂直排列 */
    position: absolute;                   /* 脱离文档流 */
    top: 100%;                            /* 紧贴导航栏底部 */
    left: 0;                              /* 左对齐 */
    right: 0;                             /* 右对齐 */
    background-color: #1f140d;            /* 深暖黑背景 */
    border-bottom: 1px solid #3a2a1b;     /* 底部边框 */
    padding: 16px;                        /* 内边距 */
  }
  .navbar nav.nav-open {
    display: flex;                         /* 展开导航 */
  }
  .navbar nav a {
    margin-left: 0;                        /* 重置左侧间距 */
    padding: 8px 0;                        /* 上下间距 */
  }
}
```

### JS 变更（index.html `<script>` 区）

新增 `toggleMenu` 函数：

```js
function toggleMenu(btn) { /* 切换移动端导航菜单 */
  var nav = btn.parentElement.querySelector('nav'); /* 获取导航元素 */
  nav.classList.toggle('nav-open'); /* 切换展开状态 */
} /* 结束菜单切换函数 */
```

### 验证

- `index.html` 包含 `.menu-toggle` 元素，内部为 Lucide 图标（非 `☰` 文字）
- SVG 图标具有 `aria-label` 属性
- 768px 以上汉堡隐藏，以下显示且导航可展开/收起

---

## #1 Hero 区：新增播放按钮 + 统计星标

### HTML 变更

**播放按钮** — 在 hero `<p>` 与 `.stats` 之间插入：

```html
<button class="hero-play-button" aria-label="播放介绍视频">
  <i data-lucide="play-circle"></i>
</button>
```

**统计星标** — 在每个 `.stat-number` 前添加星标图标：

```html
<div class="stat-item">
  <span class="stat-number"><i data-lucide="star"></i> 9</span>
  <span class="stat-label">学习计划</span>
</div>
```

（3 个 stat-item 均做相同修改）

### CSS 变更

```css
/* 播放按钮 */
.hero-play-button {
  background: none;                       /* 透明背景 */
  border: 2px solid #ff6d00;             /* 暗橙边框 */
  border-radius: 50%;                     /* 圆形 */
  width: 64px;                            /* 宽度 */
  height: 64px;                           /* 高度 */
  display: flex;                          /* 弹性布局 */
  align-items: center;                    /* 垂直居中 */
  justify-content: center;                /* 水平居中 */
  margin: 0 auto 30px;                    /* 居中并添加底部间距 */
  cursor: pointer;                        /* 手型光标 */
  color: #ff6d00;                         /* 暗橙图标色 */
  transition: all 0.3s;                   /* 过渡动画 */
}

.hero-play-button:hover {
  background-color: #ff6d00;              /* 悬停填充背景 */
  color: #1a0f0a;                         /* 深色图标 */
}

.hero-play-button [data-lucide] {
  width: 32px;                            /* 图标宽度 */
  height: 32px;                           /* 图标高度 */
}

/* 统计星标 */
.stat-number [data-lucide] {
  width: 20px;                            /* 星标宽度 */
  height: 20px;                           /* 星标高度 */
  vertical-align: middle;                 /* 垂直居中 */
  margin-right: 4px;                      /* 右侧间距 */
  fill: #ffab40;                          /* 亮橙填充 */
  color: #ffab40;                         /* 亮橙描边 */
}
```

### 响应式补充

```css
@media (max-width: 480px) {
  .hero-play-button {
    width: 48px;                          /* 缩小按钮 */
    height: 48px;
  }
  .hero-play-button [data-lucide] {
    width: 24px;                          /* 缩小图标 */
    height: 24px;
  }
  .stat-number [data-lucide] {
    width: 16px;                          /* 缩小星标 */
    height: 16px;
  }
}
```

### 验证

- `index.html` 包含 `.hero-play-button` 元素，内部为 Lucide SVG 图标（非 `▶` 文字）
- `.stats` 区域包含 Lucide `star` SVG 图标（非 `★` 文字）
- 480px 断点下图标和按钮缩小正常

---

## 执行顺序

1. CSS：新增 `.menu-toggle`、`.hero-play-button`、`.stat-number [data-lucide]` 样式及响应式
2. HTML #0：在 navbar 中插入 `.menu-toggle` 按钮
3. HTML #1：在 hero 中插入播放按钮 + 3 个星标图标
4. JS：新增 `toggleMenu` 函数
5. 浏览器验证所有断点显示效果
