# Bright Data Google/Bing 搜索结果抓取器（Node.js）

本项目提供一个基于 Node.js 的简易样板，用于通过 Bright Data Web Scraper API 获取 Google 和 Bing 的首页搜索结果 HTML。

---

## 目录

- [概览](#概览)
- [功能](#功能)
- [先决条件](#先决条件)
- [安装](#安装)
- [使用方法](#使用方法)
- [配置](#配置)
- [示例](#示例)
- [输出](#输出)
- [支持](#支持)
- [许可证](#许可证)

---

## 概览

该仓库演示如何使用 Bright Data Scraper API 触发并下载 Google/Bing 搜索结果的 HTML。包含示例搜索配置与用于批量/自定义搜索的实用函数。

---

## 功能

- 通过 Bright Data Scraper 的 `/trigger` API 端点触发 Google/Bing 搜索请求
- 使用 `/status` 端点监控进度
- 下载并保存结果为 JSON
- 同时支持 Google 与 Bing 搜索引擎
- 支持站点过滤
- 可配置超时设置

---

## 先决条件

- Node.js v16 或更高版本
- 拥有带 API Key 的 Bright Data 账号

---

## 安装

```bash
git clone https://github.com/your-org/bright-data-scrape-first-page-search-results-html-nodejs-project.git
cd bright-data-scrape-first-page-search-results-html-nodejs-project
npm install
```

---

## 使用方法

1. 设置 Bright Data API Key  
   编辑 `index.js` 并设置你的 API Key：
   ```javascript
   const API_KEY = 'YOUR_API_KEY_HERE';
   ```

2. 运行抓取器  
   ```bash
   node index.js
   ```  
   结果将以带时间戳的 `.json` 文件保存在项目目录中。

---

## 配置

- API Key：  
  在 Bright Data 控制台的 Account Settings 获取你的 API Key。
- 数据集 ID：  
  Google/Bing 搜索结果的默认数据集 ID 已在 `index.js` 中设置。

---

## 示例

### 运行示例搜索

脚本默认运行三个示例搜索：

```javascript
const SAMPLE_SEARCHES = [
  {
    url: "https://google.com",
    with: "Google",
    where: "edition.cnn.com/business",
    find: "money",
    timeline: 5000
  },
  {
    url: "https://www.bing.com",
    with: "Bing",
    where: "www.bbc.com/business",
    find: "obama",
    timeline: 5000
  },
  {
    url: "https://google.com",
    with: "Google",
    find: "artificial intelligence trends 2024",
    timeline: 5000
  }
];
```

### 自定义搜索

在 `index.js` 中取消注释并编辑以下内容以运行你的自定义搜索：

```javascript
const customSearch = [createSearch("Best programming languages to learn in 2024", "Google")];
const customResults = await searchEngines(customSearch);
await saveResults(customResults, 'custom_search.json');
```

### 批量搜索

```javascript
const multipleSearches = [
  createSearch("Climate change solutions", "Google"),
  createSearch("AI ethics guidelines", "Bing"),
  createSearch("Sustainable business practices", "Google", "www.forbes.com")
];
const multiResults = await searchEngines(multipleSearches);
await saveResults(multiResults, 'multiple_searches.json');
```

### 搜索参数

每个搜索配置支持以下参数：

- `url`（字符串，必填）：搜索引擎 URL（"https://google.com" 或 "https://www.bing.com"）
- `with`（字符串，必填）：搜索引擎（"Google" 或 "Bing"）
- `where`（字符串，可选）：站点过滤，仅在指定域名下检索结果
- `find`（字符串，必填）：搜索关键词
- `timeline`（数字，可选）：每个并行请求的超时毫秒数（默认：5000）

---

## 输出

- 结果将保存为 JSON 文件（例如：`search_results_YYYY-MM-DDTHH-MM-SS.json`）。
- 每个文件包含来自 Bright Data 的原始 API 响应及搜索结果的 HTML。

---

## API 限制

- 请求数量无限制
- 平均每个输入的响应时间：11 秒
- 支持 Google 与 Bing 搜索引擎

---

## 支持

- Bright Data 帮助中心：https://www.bright.cn/help
- 联系支持：https://www.bright.cn/contact

---

## 许可证

本项目基于 MIT 许可证开源。详见 [LICENSE](LICENSE)。
