# CSS枠生成の具体例サンプル

このファイルは、インストラクションに基づいた生成例を示します。

---

## サンプル1：SAKURA Cafeのメニューページ

### 入力：HTMLコード

```html
<!-- メインコンテンツ -->
<main class="all_container">
  
  <!-- メニューテキスト表示セクション -->
  <section class="menu_area">
    <div class="menu_title">MENU</div>
    <div class="menu_description">こだわりのコーヒーとスイーツをご用意しています</div>
  </section>
  
  <!-- おすすめセクション -->
  <section class="recommendation_area">
    <div class="recommendation_title">おすすめメニュー</div>
    <div class="recommendation-row">
      
      <!-- カード1 -->
      <div class="recommendation_menu_item">
        <img src="image1.jpg" alt="コーヒー">
        <div class="recommendation_goods_name">ブレンドコーヒー</div>
        <div class="recommendation_goods_description">毎朝焙煎した新鮮な豆を使用。</div>
        <div class="recommendation_goods_price">¥480</div>
      </div>
      
      <!-- カード2 -->
      <div class="recommendation_menu_item">
        <img src="image2.jpg" alt="ドーナツ">
        <div class="recommendation_goods_name">手作りドーナツ</div>
        <div class="recommendation_goods_description">毎日店内で手作り。</div>
        <div class="recommendation_goods_price">¥320</div>
      </div>
      
      <!-- カード3 -->
      <div class="recommendation_menu_item">
        <img src="image3.jpg" alt="カフェラテ">
        <div class="recommendation_goods_name">カフェラテ</div>
        <div class="recommendation_goods_description">エスプレッソとミルクの絶妙なバランス。</div>
        <div class="recommendation_goods_price">¥520</div>
      </div>
      
    </div>
  </section>
  
</main>
```

### 入力：スクリーンショット
（ブラウザ表示：3枚のカードが横並びになっている様子）

---

### 出力：CSS枠

```css
/* ===============================================
  メインコンテンツ
 =============================================== */

/* ┌─────────────────────────────────────────┐
   │ メニューエリア（MENUタイトル・説明文）    │
   └─────────────────────────────────────────┘ */
.menu_area {
    
}

/*   └ 子要素 */
.menu_title {
    
}

/*   └ 子要素 */
.menu_description {
    
}


/* ┌─────────────────────────────────────────┐
   │ おすすめメニューエリア                    │
   └─────────────────────────────────────────┘ */
.recommendation_area {
    
}

/*   └ 子要素 */
.recommendation_title {
    
}

/*   ▼ Flex親（3枚のカードを横並びにする） */
.recommendation-row {
    
}

/*     └ Flex子要素（カード1枚分） */
.recommendation_menu_item {
    
}

/*       └ 子要素 */
.recommendation_menu_item img {
    
}

/*       └ 子要素 */
.recommendation_goods_name {
    
}

/*       └ 子要素 */
.recommendation_goods_description {
    
}

/*       └ 子要素 */
.recommendation_goods_price {
    
}
```

---

### 構造の説明

#### 1. menu_area
- **役割**: メニュータイトルと説明文を包むコンテナ
- **Flex**: 不要（縦並びのみ）
- **子要素**:
  - `.menu_title` - タイトル
  - `.menu_description` - 説明文

#### 2. recommendation_area
- **役割**: おすすめメニュー全体のコンテナ
- **Flex**: 不要（縦並びのみ）
- **子要素**:
  - `.recommendation_title` - セクションタイトル
  - `.recommendation-row` - **Flex親（重要！）**

#### 3. recommendation-row
- **役割**: 3枚のカードを横並びにする
- **Flex**: 必要（`display: flex`）
- **理由**: 横並び配置のため
- **子要素**:
  - `.recommendation_menu_item` × 3 - **Flex子要素**

#### 4. recommendation_menu_item
- **役割**: カード1枚分
- **Flex**: カード内部は縦並び（Flex不要）
- **子要素**:
  - `img` - 商品画像
  - `.recommendation_goods_name` - 商品名
  - `.recommendation_goods_description` - 説明
  - `.recommendation_goods_price` - 価格

---

## サンプル2：ヘッダーナビゲーション

### 入力：HTMLコード

```html
<header class="header">
  <div class="header_list">
    <div class="header_logo">SAKURA Cafe</div>
    <nav class="header_navi">
      <ul class="header_navi_list">
        <li><a class="header_menu_item" href="#">ホーム</a></li>
        <li><a class="header_menu_item" href="#">メニュー</a></li>
        <li><a class="header_menu_item" href="#">アクセス</a></li>
        <li><a class="header_menu_item" href="#">お問い合わせ</a></li>
      </ul>
    </nav>
  </div>
</header>
```

### 出力：CSS枠

```css
/* ===============================================
  ヘッダー
 =============================================== */

/* ┌─────────────────────────────────────────┐
   │ ヘッダー全体                             │
   └─────────────────────────────────────────┘ */
.header {
    
}

/*   ▼ Flex親（ロゴとナビを左右に配置） */
.header_list {
    
}

/*     └ Flex子要素（左側） */
.header_logo {
    
}

/*     └ Flex子要素（右側） */
.header_navi {
    
}

/*       ▼ Flex親（メニュー項目を横並び） */
.header_navi_list {
    
}

/*         └ Flex子要素 */
.header_menu_item {
    
}
```

### 構造の説明

#### 入れ子のFlex構造
1. **第1階層**: `.header_list`（Flex親）
   - ロゴとナビを左右に分ける
   
2. **第2階層**: `.header_navi_list`（Flex親）
   - ナビの中で、メニュー項目を横並び

このように、**Flexの中にFlexがある**構造も対応できる。

---

## パターン別の判断例

### パターン1：縦並びのみ → Flexなし
```html
<div class="container">
  <h1>タイトル</h1>
  <p>説明文</p>
</div>
```

```css
.container {
    
}
  .container h1 {  /* └ 子要素 */
      
  }
  .container p {  /* └ 子要素 */
      
  }
```

### パターン2：横並び → Flexあり
```html
<div class="card-row">
  <div class="card">カード1</div>
  <div class="card">カード2</div>
  <div class="card">カード3</div>
</div>
```

```css
.card-row {  /* ▼ Flex親 */
    
}
  .card {  /* └ Flex子要素 */
      
  }
```

### パターン3：左右配置 → Flexあり
```html
<div class="split">
  <div class="left">左側</div>
  <div class="right">右側</div>
</div>
```

```css
.split {  /* ▼ Flex親 */
    
}
  .left {  /* └ Flex子要素 */
      
  }
  .right {  /* └ Flex子要素 */
      
  }
```

---

## このサンプルの使い方

1. **インストラクション本文**（`css-framework-instruction.md`）をプロジェクトに設定
2. このサンプルを参考に、生成イメージを把握
3. 実際のHTMLとスクショをClaudeに渡す
4. Claudeが同じ形式でCSS枠を生成

---

## 更新履歴
- 2024-12-18: 初版作成
