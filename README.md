# 全球局势监测 (Situation Monitor)

# Just for fun
这是一个基于 SvelteKit 和 Vite 构建的现代化实时全球局势监控前端应用。该平台提供新闻追踪、市场分析和重要事件的可视化面板，且已完全汉化。

## ✨ 核心特性

- 🌍 **全球数据一览**：集成政治、科技、金融、政府政策、人工智能等多个维度的局势新闻流。
- 📊 **市场总览监控**：全面汇集大盘指数、行业板块、大宗商品、加密货币市场热力图。
- 🔍 **个性化配置**：根据优先级自定义需要的分析面板和图表展示。
- 🌐 **全面的国际化支持**：原生支持中文与英文之间的切换。

## 🚀 快速开始

### 前提条件

- 确保您的开发环境已安装了推荐版本的 **Node.js**
- 获取相关的 API 密钥（如 Finnhub API Key）以获取实时市场数据。

### 安装与运行

1. 克隆此项目：
   ```bash
   git clone git@github.com:Shin8543/situation-monitor.git
   cd situation-monitor
   ```

2. 安装依赖项：
   ```bash
   npm install
   ```

3. 配置环境变量：
   将 `.env.example` 复制为 `.env` 并填入您的 API Key：
   ```bash
   cp .env.example .env
   # 在 .env 中填入 VITE_FINNHUB_API_KEY
   ```

4. 启动本地开发服务器：
   ```bash
   npm run dev
   ```

项目启动后，可在浏览器中访问 `http://localhost:5173`。

## 📦 打包与生产环境部署

要在生产模式下构建和预览该应用：

```bash
# 生成生产打包文件
npm run build

# 在本地进行发布前的最终预览
npm run preview
```

## 🛠️ 技术栈

- 框架：[Svelte 5](https://svelte.dev/) / [SvelteKit](https://kit.svelte.dev/)
- 构建工具：[Vite](https://vitejs.dev/)
- 样式方案：[Tailwind CSS](https://tailwindcss.com/)
- 编程语言：[TypeScript](https://www.typescriptlang.org/)
- 数据可视化：[D3.js](https://d3js.org/)
- 国际化方案：svelte-i18n
