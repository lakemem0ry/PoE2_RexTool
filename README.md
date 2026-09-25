# PoE2_RexTool
<!-- Language switcher -->
**English** | [繁體中文](#繁體中文) | [简体中文](#简体中文)

---

<a id="english"></a>

# PoE 2 Regex Tool

A single-file, zero-dependency **search-regex generator for the Path of Exile 2 trade site**.

Tick affixes, enter numeric thresholds, and the tool assembles a regex you can paste straight into the trade-site search box. All data is bundled offline — just open the page. No network access, no installation.

> Data sources: **Poe2DB** (https://poe2db.tw/) and **炖了一锅鱼** (https://space.bilibili.com/27021867)

---

## Features

### Waystones

- **Tier filter**: T1–T16. Generates the correct word order for the selected language (`16 阶` in Simplified Chinese, `階級 16` in Traditional Chinese, `Tier 16` in English).
- **Revives**: 0 / 1 / 2 / 3 / 4 / 5, placed to the left of **Rarity**.
- **Rarity**: Normal / Magic / Rare, **multi-select** (pick several, or none). Waystones have no Unique rarity, so that option is omitted for waystones and kept for tablets.
- **Corrupted**: Any / Not corrupted / Corrupted.
- **Effect filters**: Item Rarity, Pack Size, Monster Effectiveness, Monster Rarity, Waystone Drop Chance — just enter a minimum value.

### Affix filters

- **34** waystone affixes (15 prefixes / 19 suffixes) covering every tier.
- **Different rolls of the same affix are merged into one entry**: the numeric range is the **union** of every tier, so you no longer have to tick each tier separately.
  For example, extra Fire Damage was previously four tiers — `(5—9)`, `(10—14)`, `(15—19)`, `(20—24)` — and is now a single entry spanning `(5—24)%`.
- **Composite affixes** (one affix whose effect spans several lines) render on multiple lines but count as **one affix sharing a single ± toggle**, positioned at the vertical middle of the lines. For example:
  - increased Ailment Threshold + increased Stun Threshold
  - increased Critical Hit Chance + Critical Damage Bonus
- **Composite affixes are never merged with single-line affixes**, which prevents unrelated affixes from being combined by mistake.
- Search, prefix/suffix toggles, include (`+`) / exclude (`−`), and value thresholds (at least / at most) are all supported.

### Tablets

- **92** tablet affixes with **8** type filters: Irradiated, Ritual, Delirium, Breach, Abyss, Temple, Overseer, Expedition.
- **High-value tablet affixes**: filter high-value combos by price; each row provides its own regex with one-click copy.

### Other

- **Favorites**: save the current set of conditions as a preset and re-apply it in one click.
- **Output language**: Simplified Chinese / Traditional Chinese / English. Both the UI text and the generated regex switch together.
- **Auto-save**: every setting is stored in your browser's `localStorage` and restored on your next visit.

---

## Usage

### Option 1: Open it directly

Download `POE2_Rex.html` and double-click it. The whole tool is that one file — no dependencies, no build step.

### Option 2: GitHub Pages

1. Upload `POE2_Rex.html` to your repository (renaming it to `index.html` is recommended).
2. Go to **Settings → Pages**, choose the branch and directory, then save.
3. After a moment, visit `https://<your-username>.github.io/<repo-name>/`.

### After generating a regex

1. Click **Copy regex**.
2. Open the Path of Exile 2 trade site search page.
3. Paste it into the search box (the box accepts this quoted regex syntax).

---

## Regex length limit

The PoE 2 trade-site search box caps input at **250 characters**. The tool budgets a safe **248 characters** and automatically degrades when needed — replacing specific numeric ranges with `[0-9]` so the regex stays usable — while showing the current length in the UI.

---

## Multi-language notes

Item text differs between clients, so the tool generates the regex for the language you select. For a "Tier 16 waystone", even the word order of the tier marker differs:

| Language | Generated fragment |
| --- | --- |
| English | `Tier\s*16` |
| 繁體中文 | `階級\s*16\s*` |
| 简体中文 | `\s*16\s*阶` |

Rarity works the same way, using the exact in-game values (`中` / `魔` / `稀`):

```
稀有度\s*[:：]\s*\+?.*(?:中)
```

---

## Data notes

- Waystone and tablet affix data comes from **Poe2DB**, scraped and cleaned, then merged across tiers and bundled offline.
- High-value tablet prices reference the *PoE 2 Memo* international listing of 9/19 and are for filtering reference only.
- Affixes may change with game updates; treat the build date in `POE2_DATA.meta.built` inside the file as authoritative.

Bundled data (current build):

| Item | Count |
| --- | --- |
| Waystone affixes | 34 (15 prefixes / 19 suffixes, including 2 composite affixes) |
| Tablet affixes | 92 |
| High-value tablet combos | 148 across 8 types |

---

## Free of charge

**This tool is completely free.**

- This tool is published free of charge by the author. Every feature is available directly, with no payment and no licence purchase required.
- The author has **not** authorised any individual or organisation to sell this tool, its source code or related files for a fee.
- If you paid to obtain this tool or related files, please note: that charge has nothing to do with the author. The author did not receive your payment and cannot issue you a refund.
- Please contact the seller or platform that charged you to request a refund. If they cannot be reached or you suspect fraud, consider filing a complaint through your payment provider, a consumer protection body or the relevant authority, and keep your payment receipts.
- This notice only states that the tool is free; it is not a guarantee or undertaking regarding any third party's conduct.

## Voluntary support

This tool is completely free. If you find it useful, you can reach **LMemory氿忆** on Bilibili (https://space.bilibili.com/7132721) to make a voluntary donation.

Donating is entirely optional: it is not a purchase or a paid service, it grants no extra features, services, licence or priority support, and it does not affect your normal use of this tool. The author has not authorised any third party to sell this tool for a fee; if you paid for it, that charge has nothing to do with the author, who cannot issue a refund — please contact the recipient of your payment. Thank you for your support.

---

## Credits

- **[Poe2DB](https://poe2db.tw/)** — source of affix and item data.
- **[炖了一锅鱼](https://space.bilibili.com/27021867)** — data source.
- Author: **LMemory氿忆**

---

## Technical notes

- **Single file**: HTML, CSS and vanilla JavaScript are all inlined in one `.html` — no framework, no build, no external requests.
- Regex is assembled on the fly by a built-in engine based on the current language and your selections, with no third-party library.
- Settings live in your browser's local storage; nothing is uploaded.

## License

This tool is provided free of charge. When using the source or data, please also observe the free-of-charge notice above and the terms of the data-source sites (Poe2DB, Bilibili).

---

**[↑ Back to top](#poe-2-regex-tool)** · **English** | [繁體中文](#繁體中文) | [简体中文](#简体中文)

---
---

<a id="繁體中文"></a>

# PoE 2 正則工具

一個單檔、零依賴的 **《流亡之路 2》交易站搜尋正則產生器**。

勾選詞綴、填入數值門檻，工具會即時拼出一段可直接貼進交易站搜尋框的正則表達式。全部資料離線內建，打開網頁即可使用，不需要連網、不需要安裝任何東西。

> 資料來源：**Poe2DB**（https://poe2db.tw/）與 **炖了一锅鱼**（https://space.bilibili.com/27021867）

---

## 主要功能

### 換界石（Waystone）

- **階級篩選**：T1–T16，會依目前語言自動產生對應語序的正則（簡中 `16 阶`、繁中 `階級 16`、英文 `Tier 16`）。
- **復活次數**：0 / 1 / 2 / 3 / 4 / 5 選項，位置在「稀有度」左側。
- **稀有度**：普通 / 魔法 / 稀有**可多選**（可多選，也可不選）。換界石沒有傳奇，故不提供該檔；碑牌（石板）則保留傳奇。
- **腐化狀態**：不限 / 未汙染 / 已汙染。
- **效果篩選**：物品稀有度、怪物群大小、怪物效用、怪物稀有度、換界石掉落機率，填入最低值即可。

### 詞綴篩選

- **34 條**換界石詞綴（15 前綴 / 19 後綴），涵蓋全部階級。
- **同一條詞綴的不同強度已合併**為一條：數值區間取全部階級的**聯集**，填門檻時不必再逐檔勾選。
  例如火焰額外傷害原本四檔 `(5—9)`、`(10—14)`、`(15—19)`、`(20—24)`，現合併為一條 `(5—24)%`。
- **複合詞綴**（同一條詞綴含多行效果）顯示為多行，但**算作一條詞綴、共用一個 ± 號**，± 號位於兩行效果中間的右側。例如：
  - 增加怪物異常狀態門檻 + 增加怪物的暈眩門檻
  - 增加怪物的暴擊率 + 怪物暴擊傷害加成
- **複合詞綴不與單一詞綴合併**，避免把不同的詞綴錯併成一條。
- 支援搜尋、前綴/後綴開關、包含（`+`）/ 排除（`−`），以及數值門檻（至少 / 至多）。

### 碑牌（石板 / Tablet）

- **92 條**碑牌詞綴，支援 **8 種類型**篩選：輻照、祭祀、譫妄、裂痕、深淵、神廟、總督、探險。
- **高價值碑牌詞綴**：依價格篩選高價值組合，每條給出獨立正則，可一鍵複製。

### 其它

- **最愛**：把目前條件組存成預設，隨時一鍵套用。
- **輸出語言**：簡體中文 / 繁體中文 / English 三檔切換，介面文案與產生的正則**同步切換**。
- **設定自動儲存**：所有設定存在瀏覽器本機（`localStorage`），下次打開自動還原。

---

## 使用方法

### 方式一：直接打開

下載 `POE2_Rex.html`，點兩下用瀏覽器打開即可。整個工具就是這一個檔案，沒有任何依賴或建置步驟。

### 方式二：GitHub Pages

1. 把 `POE2_Rex.html` 上傳到倉庫（建議同時改名為 `index.html`）。
2. 倉庫 **Settings → Pages**，Source 選擇分支與目錄後儲存。
3. 稍等片刻，前往 `https://<你的使用者名稱>.github.io/<倉庫名稱>/`。

### 產生正則之後

1. 按下「複製正則」。
2. 打開《流亡之路 2》交易站搜尋頁面。
3. 貼進搜尋框（搜尋框支援這種帶引號的正則語法）。

---

## 關於正則長度

PoE 2 交易站搜尋框有 **250 字元**上限。工具內建 **248 字元**的安全預算，超出時會自動降級（把具體的數值區間替換為 `[0-9]`）以確保正則可用，同時會在介面上顯示目前長度。

---

## 多語言說明

不同語言客戶端的物品文本不同，工具會依你選擇的語言產生對應正則。以「階級 16 換界石」為例，連階級標記的語序都不相同：

| 語言 | 產生的片段 |
| --- | --- |
| English | `Tier\s*16` |
| 繁體中文 | `階級\s*16\s*` |
| 简体中文 | `\s*16\s*阶` |

稀有度同理，依遊戲內實際取值產生（`中` / `魔` / `稀`）：

```
稀有度\s*[:：]\s*\+?.*(?:中)
```

---

## 資料說明

- 換界石與碑牌的詞綴資料來自 **Poe2DB**，經抓取、清洗後離線內建，並做了跨階級合併。
- 高價值碑牌詞綴的價格參考《流放2 備忘錄》國際服 9/19 報價，僅供篩選參考。
- 遊戲版本更新後詞綴可能變動，資料以檔案內 `POE2_DATA.meta.built` 標註的建置日期為準。

內建資料規模（目前建置）：

| 項目 | 數量 |
| --- | --- |
| 換界石詞綴 | 34（15 前綴 / 19 後綴，含 2 條複合詞綴） |
| 碑牌詞綴 | 92 |
| 高價值碑牌組合 | 148 條，分屬 8 個類型 |

---

## 免費聲明

**本工具完全免費。**

- 本工具由作者免費公開提供，所有功能均可直接使用，無需付費、無需購買授權。
- 作者**未授權**任何個人或組織以收費方式銷售本工具、原始碼或相關檔案。
- 如果您是透過付費方式獲得本工具或相關檔案，請注意：該收費行為與作者無關，作者未收到您的款項，也無法為您辦理退款。
- 請直接聯繫向您收費的商家／平台協商退款；如遇無法聯繫或涉嫌詐欺，建議透過支付平台投訴、向消費者保護機構或相關主管機關反映，並保留付款憑證。
- 本聲明僅為說明免費性質，不構成對任何第三方行為的擔保或承諾。

## 自願贊助

本工具完全免費。如果您覺得好用，可以透過 Bilibili 聯繫 **LMemory氿忆**（https://space.bilibili.com/7132721）自願贊助。

贊助完全自願，不構成購買或付費服務，也不會獲得額外功能、服務、授權或優先支援，不影響您正常使用本工具。作者未授權任何第三方收費銷售本工具；如您是付費獲得，該收費與作者無關，作者無法辦理退款，請聯繫收款方處理。感謝支持。

---

## 致謝

- **[Poe2DB](https://poe2db.tw/)** —— 詞綴與物品資料來源。
- **[炖了一锅鱼](https://space.bilibili.com/27021867)** —— 資料來源。
- 作者：**LMemory氿忆**

---

## 技術說明

- **單一檔案**：HTML + CSS + 原生 JavaScript 全部內嵌在一個 `.html` 裡，無框架、無建置、無外部請求。
- 正則由內建引擎依目前語言與選取項目即時組裝，不依賴任何第三方函式庫。
- 設定儲存於瀏覽器本機，不上傳任何資料。

## License

本工具免費公開提供。原始碼與資料的使用請一併遵守上述免費聲明，以及資料來源網站（Poe2DB、Bilibili）的相關條款。

---

**[↑ 回到頂端](#poe-2-正則工具)** · [English](#english) | **繁體中文** | [简体中文](#简体中文)

---
---

<a id="简体中文"></a>

# PoE 2 正则工具

一个单文件、零依赖的 **《流放之路 2》交易站搜索正则生成器**。

勾选词缀、填写数值门槛，工具会实时拼出一段可直接粘贴进交易站搜索框的正则表达式。全部数据离线内置，打开网页即可使用，不需要联网、不需要安装任何东西。

> 数据来源：**Poe2DB**（https://poe2db.tw/）与 **炖了一锅鱼**（https://space.bilibili.com/27021867）

---

## 主要功能

### 引路石（Waystone）

- **阶级筛选**：T1–T16，自动按当前语言生成对应语序的正则（简中 `16 阶`、繁中 `階級 16`、英文 `Tier 16`）。
- **复活次数**：0 / 1 / 2 / 3 / 4 / 5 选项，位置在「稀有度」左侧。
- **稀有度**：普通 / 魔法 / 稀有**多选**（可多选，也可不选）。引路石没有传奇，故不提供该档；碑牌（石板）则保留传奇。
- **腐化状态**：不限 / 未腐化 / 已腐化。
- **效果筛选**：物品稀有度、怪物群规模、怪物效能、怪物稀有度、引路石掉落几率，填最低值即可。

### 词缀筛选

- **34 条**引路石词缀（15 前缀 / 19 后缀），覆盖全部阶级。
- **同一词缀的不同强度已合并**为一条：数值区间取全部阶级的**并集**，填写门槛时不必再逐档勾选。
  例如火焰额外伤害原先四档 `(5—9)`、`(10—14)`、`(15—19)`、`(20—24)`，现合并为一条 `(5—24)%`。
- **复合词缀**（同一条词缀含多行效果）显示为多行，但**算作一条词缀、共用一个 ± 号**，± 号位于两行效果中间的右侧。例如：
  - 怪物的异常状态阈值提高 + 怪物的晕眩阈值提高
  - 怪物暴击率提高 + 怪物暴击伤害加成
- **复合词缀不与单一词缀合并**，避免把不同的词缀错并成一条。
- 支持搜索、前缀/后缀开关、包含（`+`）/ 排除（`−`）、以及数值门槛（至少 / 至多）。

### 碑牌（石板 / Tablet）

- **92 条**碑牌词缀，支持 **8 种类型**筛选：辐照、仪式、迷雾、裂隙、深渊、神庙、霸主、探险。
- **高价值碑牌词缀**：按价格筛选高价值组合，每条给出独立正则，可一键复制。

### 其它

- **最爱**：把当前条件组合存成预设，随时一键套用。
- **输出语言**：简体中文 / 繁體中文 / English 三档切换，界面文案与生成的正则**同步切换**。
- **设置自动保存**：所有设置保存在浏览器本地（`localStorage`），下次打开自动恢复。

---

## 使用方法

### 方式一：直接打开

下载 `POE2_Rex.html`，双击用浏览器打开即可。整个工具就是这一个文件，没有任何依赖或构建步骤。

### 方式二：GitHub Pages

1. 把 `POE2_Rex.html` 上传到仓库（建议同时改名为 `index.html`）。
2. 仓库 **Settings → Pages**，Source 选择分支与目录后保存。
3. 稍等片刻，访问 `https://<你的用户名>.github.io/<仓库名>/`。

### 生成正则后

1. 点「复制正则」。
2. 打开《流放之路 2》交易站搜索页面。
3. 粘贴进搜索框（搜索框支持这种带引号的正则语法）。

---

## 关于正则长度

PoE 2 交易站搜索框有 **250 字符**上限。工具内置 **248 字符**的安全预算，超出时会自动降级（把具体的数值区间替换为 `[0-9]`）以保证正则可用，同时会在界面上提示当前长度。

---

## 多语言说明

不同语言客户端的物品文本不同，工具会按你选择的语言生成对应正则。例如「16 阶引路石」的阶级标记语序并不相同：

| 语言 | 生成的片段 |
| --- | --- |
| English | `Tier\s*16` |
| 繁體中文 | `階級\s*16\s*` |
| 简体中文 | `\s*16\s*阶` |

稀有度同理，按游戏内实际取值生成（`中` / `魔` / `稀`）：

```
稀有度\s*[:：]\s*\+?.*(?:中)
```

---

## 数据说明

- 引路石与碑牌的词缀数据来自 **Poe2DB**，经抓取、清洗后离线内置，并做了跨阶级合并。
- 高价值碑牌词缀的价格参考《流放2 备忘录》国际服 9/19 报价，仅供筛选参考。
- 游戏版本更新后词缀可能变动，数据以文件内 `POE2_DATA.meta.built` 标注的构建日期为准。

内置数据规模（当前构建）：

| 项目 | 数量 |
| --- | --- |
| 引路石词缀 | 34（15 前缀 / 19 后缀，含 2 条复合词缀） |
| 碑牌词缀 | 92 |
| 高价值碑牌组合 | 148 条，分属 8 个类型 |

---

## 免费声明

**本工具完全免费。**

- 本工具由作者免费公开提供，所有功能均可直接使用，无需付费、无需购买授权。
- 作者**未授权**任何个人或组织以收费方式销售本工具、源码或相关文件。
- 如果您是通过付费方式获得本工具或相关文件，请注意：该收费行为与作者无关，作者未收到您的款项，也无法为您办理退款。
- 请直接联系向您收费的商家/平台协商退款；如遇无法联系或涉嫌欺诈，建议通过支付平台投诉、向消费者协会或相关监管部门反映，并保留付款凭证。
- 本声明仅为说明免费性质，不构成对任何第三方行为的担保或承诺。

## 自愿赞助

本工具完全免费。如果您觉得好用，可以通过 Bilibili 联系 **LMemory氿忆**（https://space.bilibili.com/7132721）自愿赞助。

赞助完全自愿，不构成购买或付费服务，也不会获得额外功能、服务、授权或优先支持，不影响您正常使用本工具。作者未授权任何第三方收费销售本工具；如您是付费获得，该收费与作者无关，作者无法办理退款，请联系收款方处理。感谢支持。

---

## 致谢

- **[Poe2DB](https://poe2db.tw/)** —— 词缀与物品数据来源。
- **[炖了一锅鱼](https://space.bilibili.com/27021867)** —— 数据来源。
- 作者：**LMemory氿忆**

---

## 技术说明

- **单文件**：HTML + CSS + 原生 JavaScript 全部内联在一个 `.html` 里，无框架、无构建、无外部请求。
- 正则由内置引擎按当前语言与选中项实时拼装，不依赖任何第三方库。
- 设置存储于浏览器本地，不上传任何数据。

## License

本工具免费公开提供。源码与数据的使用请一并遵守上述免费声明，以及数据来源网站（Poe2DB、Bilibili）的相关条款。

---

**[↑ 回到顶部](#poe-2-正则工具)** · [English](#english) | [繁體中文](#繁體中文) | **简体中文**
