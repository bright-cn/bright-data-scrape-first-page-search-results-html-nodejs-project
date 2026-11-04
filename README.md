# Bright Data Google/Bing 搜索结果抓取工具（Node.js）

本项目提供了一个简单的 Node.js 样板，用于通过 Bright Data 网页爬虫工具 API 获取 Google 和 Bing 第一页搜索结果的 HTML。

---

## 目录

* [概述](#概述)
* [功能](#功能)
* [前提条件](#前提条件)
* [安装](#安装)
* [使用方法](#使用方法)
* [配置](#配置)
* [示例](#示例)
* [输出](#输出)
* [支持](#支持)
* [许可证](#许可证)

---

## 概述

本仓库演示了如何使用 Bright Data 爬虫工具 API 触发并下载 Google/Bing 搜索结果的 HTML。其中包含搜索配置示例，以及用于批量搜索和自定义搜索的实用函数。

---

## 功能

* 通过 Bright Data 爬虫工具的 `/trigger` API 端点触发 Google/Bing 搜索请求
* 使用 `/status` 端点监控进度
* 以 JSON 格式下载并保存结果
* 同时支持 Google 和 Bing 搜索引擎
* 支持网站筛选
* 可配置超时设置

---

## 前提条件

* Node.js v16 或更高版本
* 具有 API 密钥的 Bright Data 账户

---

## 安装

```bash
git clone https://github.com/your-org/bright-data-scrape-first-page-search-results-html-nodejs-project.git
cd bright-data-scrape-first-page-search-results-html-nodejs-project
npm install
```

---

## 使用方法

1. **设置你的 Bright Data API 密钥**  
   编辑 `index.js` 并设置你的 API 密钥：  
   ```javascript
   const API_KEY = 'YOUR_API_KEY_HERE';
   ```

2. **运行抓取工具**  
   ```bash
   node index.js
   ```  
   结果将以带时间戳的 `.json` 文件形式保存在项目目录中。

---

## 配置

* **API 密钥：**  
  在 Bright Data 控制面板的账户设置中获取你的 API 密钥。
* **数据集 ID：**  
  Google/Bing 搜索结果的默认数据集 ID 已在 `index.js` 中设置。

---

## 示例

### 运行搜索示例

默认情况下，该脚本会运行三个搜索示例：

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

取消注释并编辑 `index.js` 中的以下内容，以运行你自己的搜索：

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

每项搜索配置都支持以下参数：

* `url`（字符串，必填）：搜索引擎 URL（“https://google.com”或“https://www.bing.com”）
* `with`（字符串，必填）：搜索引擎（“Google”或“Bing”）
* `where`（字符串，可选）：用于将结果限制为特定域名的网站筛选条件
* `find`（字符串，必填）：搜索关键词/搜索词
* `timeline`（数字，可选）：每个并行请求的超时时间，以毫秒为单位（默认值：5000）

---

## 输出

* 结果将保存为 JSON 文件（例如 `search_results_YYYY-MM-DDTHH-MM-SS.json`）。
* 每个文件都包含 Bright Data API 返回的原始响应及 HTML 搜索结果。

---

## API 限制

* 请求数量不受限制
* 每项输入的平均响应时间：11 秒
* 同时支持 Google 和 Bing 搜索引擎

---

## 支持

* [Bright Data 帮助中心](https://brightdata.com/help)
* [联系支持团队](https://www.bright.cn/contact)

---

## 许可证

本项目采用 MIT 许可证授权。有关详细信息，请参阅 [LICENSE](LICENSE)。
