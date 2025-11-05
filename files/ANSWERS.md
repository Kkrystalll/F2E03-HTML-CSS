# CSS 選取器練習題 - 完整解答

## 題目 01：群組宣告

### 錯誤
```css
.news-list .info-list {
    color: red;
}
```

### 問題分析
- 中間有空格，變成「層疊選取器」
- 意思是：選取 `.news-list` 底下的 `.info-list`
- 但 HTML 中兩者是平行關係，不是上下層關係

### 正確答案
```css
.news-list, .info-list {
    color: red;
}
```

### 重點
- **群組選取器**用逗號 `,` 分隔
- 表示「或」的關係：選取 `.news-list` **或** `.info-list`

---

## 題目 02：組合式宣告

### 錯誤
```css
.btn .link-btn {
    color: blue;
}
```

### 問題分析
- 中間有空格，變成「層疊選取器」
- 意思是：選取 `.btn` 底下的 `.link-btn`
- 但題目要選「同時擁有兩個 class」的元素

### 正確答案
```css
a.btn.link-btn {
    color: blue;
}
```

或

```css
.btn.link-btn {
    color: blue;
}
```

### 重點
- **組合式選取器**中間沒有空格
- 表示「且」的關係：同時符合所有條件
- 可以組合 tag + class，或多個 class

---

## 題目 03：層疊式選取器

### 錯誤
```css
.news-list, li {
    color: red;
}
```

### 問題分析
- 用了逗號，變成「群組選取器」
- 會選到所有的 `.news-list` 和所有的 `li`
- 導致 `.info-list` 裡的 `li` 也變紅色

### 正確答案
```css
.news-list li {
    color: red;
}
```

### 重點
- **層疊選取器**用空格分隔
- 表示「後代關係」：選取 `.news-list` 底下所有的 `li`

---

## 題目 04：親代選取器 +

### 錯誤
```css
h1 ~ p {
    color: green;
}
```

### 問題分析
- `~` 會選取所有後續的兄弟元素
- 導致 h1 後面所有的 p 都變綠色

### 正確答案
```css
h1 + p {
    color: green;
}
```

### 重點
- `+`：選取**緊接著**的下一個兄弟元素
- `~`：選取**所有後續**的兄弟元素

---

## 題目 05：子代選取器 >

### 錯誤
```css
.first-item div {
    border: 2px solid orange;
}
```

### 問題分析
- 空格表示「所有後代」
- 會選到所有層級的 div，包括 `.second-item` 裡的

### 正確答案
```css
.first-item > div {
    border: 2px solid orange;
}
```

### 重點
- `>`：只選取**直接子元素**
- 空格：選取**所有後代**（包括子、孫、曾孫...）

---

## 題目 06：:first-child vs :first-of-type

### 錯誤
```css
.box p:first-child {
    color: purple;
}
```

### 問題分析
- `:first-child` 要求 `p` 必須是父元素的**第一個元素**
- 第一個 .box 中，第一個元素是 `div`，所以 `p` 不會被選到

### 正確答案
```css
.box p:first-of-type {
    color: purple;
}
```

### 重點
- `:first-child`：必須是第一個**元素**（考慮順序）
- `:first-of-type`：該類型的第一個（不考慮順序）

---

## 題目 07：:last-child vs :last-of-type

### 錯誤
```css
.container p:last-child {
    color: brown;
}
```

### 問題分析
- `:last-child` 要求 `p` 必須是父元素的**最後一個元素**
- 第一個 .container 中，最後一個元素是 `div`，所以 `p` 不會被選到

### 正確答案
```css
.container p:last-of-type {
    color: brown;
}
```

### 重點
- `:last-child`：必須是最後一個**元素**（考慮順序）
- `:last-of-type`：該類型的最後一個（不考慮順序）

---

## 題目 08：:nth-of-type() 語法

### 錯誤
```css
.list li:nth-of-type-odd {
    background-color: #f0f0f0;
}
```

### 問題分析
- 語法錯誤：用破折號連接
- 正確語法應該用括號

### 正確答案
```css
.list li:nth-of-type(odd) {
    background-color: #f0f0f0;
}
```

### 重點
- `:nth-of-type()` 需要**括號**
- 可以用 `odd`（奇數）、`even`（偶數）、或公式 `an+b`

---

## 題目 09：:nth-child() 公式

### 錯誤
```css
.wrapper p:nth-child(3n+1) {
    background-color: lightblue;
}
```

### 問題分析
- `3n+1` 會選到：1, 4, 7, 10...
- 題目要求選：2, 5, 8...

### 正確答案
```css
.wrapper p:nth-child(3n+2) {
    background-color: lightblue;
}
```

### 重點
- 公式：`an+b`
  - `a`：週期（每幾個）
  - `b`：起始位置
- `3n+2`：從第 2 個開始，每 3 個選一個

---

## 題目 10：:not() 語法

### 錯誤
```css
.menu li:not-special {
    color: gray;
}
```

### 問題分析
- 語法錯誤：沒有括號
- class 前面缺少點號

### 正確答案
```css
.menu li:not(.special) {
    color: gray;
}
```

### 重點
- `:not()` 需要**括號**
- 括號內要寫完整的選取器（包括 `.` 或 `#`）

---

## 題目 11：偽類前不能有空格

### 錯誤
```css
.action-btn :hover {
    background-color: darkblue;
}

.action-btn :focus {
    border-color: yellow;
}
```

### 問題分析
- 偽類前面有空格，變成「後代選取器」
- 意思是：選取 `.action-btn` 底下處於 hover 狀態的元素

### 正確答案
```css
.action-btn:hover {
    background-color: darkblue;
    color: white;
}

.action-btn:focus {
    border-color: yellow;
    outline: none;
}
```

### 重點
- 偽類選取器前面**不能有空格**
- 緊接在元素或 class 後面

---

## 題目 12：偽類順序

### 錯誤
```css
.nav-link:active {
    color: red;
}

.nav-link:visited {
    color: purple;
}

.nav-link {
    color: blue;
}
```

### 問題分析
- CSS 優先權相同時，後面的會覆蓋前面的
- `:active` 放太前面，會被後面的覆蓋

### 正確答案
```css
.nav-link {
    color: blue;
    text-decoration: none;
}

.nav-link:visited {
    color: purple;
}

.nav-link:hover {
    color: orange;
}

.nav-link:active {
    color: red;
}
```

### 重點
- 正確順序：**visited → focus → hover → active**
- 記憶口訣：**LVFHA** (Link, Visited, Focus, Hover, Active)
- 或記：**visited > focus > hover > active**

---

## 題目 13：CSS 優先權

### 錯誤
```css
h1 {
    color: red;
}

.main-title {
    color: blue;
}
```

### 問題分析
- tag 選取器優先權：1
- class 選取器優先權：10
- class 優先權較高，所以標題是藍色

### 正確答案（方法一：使用 ID）
```css
#title {
    color: red;
}

.main-title {
    color: blue;
}
```

### 正確答案（方法二：提高優先權）
```css
h1.main-title {
    color: red;
}

.main-title {
    color: blue;
}
```

### 重點
- 優先權順序：`!important` > `inline style` > `ID` (100) > `class` (10) > `tag` (1) > `*` (0)
- 優先權相同時，後面的覆蓋前面的

---

## 題目 14：屬性選取器 *=

### 錯誤
```css
img[alt="可愛"] {
    border: 3px solid red;
}
```

### 問題分析
- `=` 表示「完全相等」
- 只會選到 `alt="可愛"` 的圖片
- 不會選到 `alt="可愛貓咪"` 或 `alt="超級可愛兔子"`

### 正確答案
```css
img[alt*="可愛"] {
    border: 3px solid red;
}
```

### 重點
- `[attr="value"]`：完全相等
- `[attr*="value"]`：包含
- `[attr^="value"]`：開頭等於
- `[attr$="value"]`：結尾等於
- `[attr~="value"]`：包含完整單字（空格分隔）

---

## 題目 15：屬性選取器 $=

### 錯誤
```css
a[href^=".jpg"] {
    color: green;
}
```

### 問題分析
- `^=` 表示「開頭等於」
- 但檔名不會以 `.jpg` 開頭
- 應該用 `$=`（結尾等於）

### 正確答案
```css
a[href$=".jpg"] {
    color: green;
}
```

### 重點
- `^=`：開頭匹配（如：選取 `https://` 開頭的連結）
- `$=`：結尾匹配（如：選取 `.jpg` 結尾的連結）

---

## 題目 16：綜合應用

### 錯誤
```css
article p:first-child {
    font-weight: bold;
}

article p:not:first-of-type {
    color: gray;
}
```

### 問題分析
1. `p` 不是 article 的第一個子元素（第一個是 `h2`）
2. `:not` 語法錯誤，沒有括號

### 正確答案
```css
article p:first-of-type {
    font-weight: bold;
}

article p:not(:first-of-type) {
    color: gray;
}
```

### 重點
- 結合使用 `:first-of-type` 和 `:not()`
- `:not()` 內要用括號包住選取器

---

## 題目 17：群組選取多個

### 錯誤
```css
.gallery > div:nth-child(2) {
    background-color: lightblue;
}
```

### 問題分析
- 只選了第 2 個，沒有選第 3 個

### 正確答案
```css
.gallery > div:nth-child(2),
.gallery > div:nth-child(3) {
    background-color: lightblue;
    padding: 10px;
}
```

### 重點
- 需要選多個時，用**群組選取器**（逗號分隔）
- 每個選取器都要寫完整

---

## 題目 18：CSS 順序

### 錯誤
```css
.btn:hover { ... }
.btn.primary:hover { ... }
.btn.primary { ... }
.btn { ... }
```

### 問題分析
- 基本樣式應該放前面
- 狀態樣式應該放後面
- 否則會被覆蓋

### 正確答案
```css
.btn {
    padding: 10px 20px;
    border: none;
    background-color: lightgray;
    cursor: pointer;
}

.btn.primary {
    background-color: blue;
    color: white;
}

.btn:hover {
    box-shadow: 0 2px 5px rgba(0,0,0,0.2);
}

.btn.primary:hover {
    background-color: darkblue;
}
```

### 重點
- CSS 順序：**基本樣式 → 變化樣式 → 狀態樣式**
- 越特定的樣式放越後面

---

## 題目 19：表格樣式

### 錯誤
```css
tr:nth-child(even) { ... }
tr:hover { ... }
tr:first-child { ... }
```

### 問題分析
1. `tr:nth-child(even)` 會選到第 2, 4 行（包括可能是資料行）
2. `tr:hover` 會影響表頭

### 正確答案
```css
table {
    border-collapse: collapse;
    width: 100%;
}

th, td {
    padding: 10px;
    text-align: left;
    border: 1px solid #ddd;
}

tr:first-child {
    background-color: #333;
    color: white;
}

tr:not(:first-child):nth-child(even) {
    background-color: #f2f2f2;
}

tr:not(:first-child):hover {
    background-color: lightyellow;
}
```

### 重點
- 使用 `:not(:first-child)` 排除表頭
- 可以串連多個偽類選取器

---

## 題目 20：最終挑戰

### 錯誤
```css
input textarea { ... }
input :focus { ... }
input[type=email]:focus { ... }
a[href*="http"]::after { ... }
```

### 問題分析
1. `input textarea` 缺少逗號（應該是群組）
2. `input :focus` 有空格（應該無空格）
3. `type=email` 缺少引號
4. `href*="http"` 應該用 `^=`（開頭）而非 `*=`（包含）

### 正確答案
```css
input, textarea {
    border: 1px solid #ccc;
    padding: 8px;
    border-radius: 4px;
}

input:focus,
textarea:focus {
    border-color: blue;
    outline: none;
}

input[type="email"]:focus {
    border-color: green;
}

a[href^="http"]::after {
    content: " ↗";
    font-size: 0.8em;
}
```

### 重點
- 群組選取器用逗號
- 偽類前不能有空格
- 屬性值要加引號
- 外部連結通常以 `http` 開頭，用 `^=`

---

## 總結重點

### 1. 選取器符號
| 符號 | 意義 | 範例 |
|------|------|------|
| `,` | 群組（或） | `.a, .b` |
| 空格 | 後代（層疊） | `.a .b` |
| 無空格 | 組合（且） | `.a.b` |
| `>` | 直接子元素 | `.a > .b` |
| `+` | 緊接的下一個 | `.a + .b` |
| `~` | 所有後續兄弟 | `.a ~ .b` |

### 2. 偽類選取器
- `:first-child` vs `:first-of-type`（考慮順序 vs 不考慮）
- `:nth-child()` vs `:nth-of-type()`（所有元素 vs 同類型）
- `:not()` 要用括號
- 偽類前**不能有空格**

### 3. 偽類順序
**visited → focus → hover → active**

### 4. 優先權
`!important` > `inline` > `#id` (100) > `.class` (10) > `tag` (1) > `*` (0)

### 5. 屬性選取器
- `=`：完全相等
- `*=`：包含
- `^=`：開頭
- `$=`：結尾
- 值要加**引號**
