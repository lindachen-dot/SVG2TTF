# SVG2TTF

解析 SVG 向量字符，依 Unicode 對照批次轉換為 TTF 字型檔的單頁網頁工具。

---

## 使用方式

### 1. 準備 SVG 檔案

在 Illustrator 中製作字符，匯出為 SVG 時請注意：

- **每個 `<path>` = 一個字符**
- **複合字符**（如 `i`、`j`、`%`）須先在 Illustrator 以 `<g>` 群組包覆，再匯出
- 若需保留字符相對垂直位置，可在畫布上畫水平 `<line>` 作為 baseline 參考，工具會自動偵測每條線段並為每個字符找最近的 baseline 對齊

### 2. 上傳 SVG

上傳後右側預覽區會即時顯示所有偵測到的字符，依左到右、上到下的座標順序排列編號。

### 3. 輸入 Unicode 對照

支援兩種格式，擇一使用：

**純文字模式**
直接輸入字符，工具逐字拆解，依序對應 SVG 內字符：
```
!"#$%&'()*+,-./0123456789
```

**uni 格式**（每行一個）
```
uni0021
uni0022
uni0023
```

Unicode 數量須與 SVG 字符數量一致，不符時工具會提示錯誤。

### 4. 設定參數

| 參數 | 說明 |
|------|------|
| EM 大小 | EM 1000 或 EM 2048，影響縮放精度與相容性 |
| 檔名 | 輸出的字型家族名稱，例如輸入 `HFFont` 會產生 `HFFont-Regular.ttf` |

### 5. 下載 TTF

確認預覽無誤後按「下載 TTF」。

---

## 輸出規格

### 字符尺寸
- 以所有字符中最高者為基準縮放，其餘等比處理
- EM 1000：目標高度 880u，LSB = RSB = 50
- EM 2048：目標高度 1800u，LSB = RSB = 100

### Font Dimensions

| 欄位 | EM 1000 | EM 2048 |
|------|---------|---------|
| sTypoAscender | 760 | 1556 |
| sTypoDescender | −214 | −438 |
| sxHeight | 517 | 1059 |
| sCapHeight | 730 | 1495 |
| usWinAscent | 1069 | 2189 |
| usWinDescent | 293 | 600 |
| hhea Ascender | 1069 | 2189 |
| hhea Descender | −293 | −600 |

### 字型資訊
- **Vendor**：Kika
- **Manufacturer**：Beijing Xinmeihutong Technology Co., LTD.
- **Copyright**：依下載年份自動更新
- **Creation date**：下載當下時間
- **Unicode Ranges / Codepages**：依實際字符自動偵測寫入

---

## 注意事項

- SVG 內的 `<line>` 元素會被自動識別為 baseline 參考線，請確保畫布中不含其他非 baseline 用途的線段
- 不含 baseline 線的 SVG 仍可正常使用，字符底部統一對齊 baseline (0)
- 建議輸出前在預覽區確認字符順序與 Unicode 對應是否一致
