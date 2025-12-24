# `_card`と`_item`の使い分け（完全版）

---

## 結論

| 親要素 | 子要素の背景色・枠線 | 子要素のflex | 使う接尾語 |
|--------|---------------------|-------------|-----------|
| **flex使う** | **あり** | 使う・使わない関係なし | `_card` |
| **flex使う** | **なし** | 使う・使わない関係なし | `_item` |
| flex使わない | - | - | `_container` / `_inner` |

**判断基準は2つだけ：**
1. 親がflexを使ってるか？
2. 子に背景色・枠線があるか？

**子自身がflexを使うかどうかは関係ない**

---

## パターン1: 親flex + 子flex + 背景色あり → `_card`

### 1-1. 構造図

```
recipe_list ← ①親がflex
 │
 ├─ recipe_card ← ②子もflex + 背景色あり → _card
 │   ├─ recipe_card_image
 │   ├─ recipe_card_title
 │   └─ recipe_card_description
 │
 └─ recipe_card ← ②子もflex + 背景色あり → _card
     ├─ recipe_card_image
     ├─ recipe_card_title
     └─ recipe_card_description
```

---

### 1-2. HTML

```html
<div class="recipe_list">
  <div class="recipe_card">
    <img class="recipe_card_image" src="food1.jpg">
    <h3 class="recipe_card_title">レシピ1</h3>
    <p class="recipe_card_description">説明文</p>
  </div>
  
  <div class="recipe_card">
    <img class="recipe_card_image" src="food2.jpg">
    <h3 class="recipe_card_title">レシピ2</h3>
    <p class="recipe_card_description">説明文</p>
  </div>
</div>
```

---

### 1-3. CSS

```css
/* ①親：flexでカードを横並び */
.recipe_list {
  display: flex;
  gap: 20px;
}

/* ②子：flexで中身を縦並び + 背景色あり */
.recipe_card {
  display: flex;          /* ← flexを使う */
  flex-direction: column;
  background-color: #fff; /* ← 背景色あり */
  border: 1px solid #ddd; /* ← 枠線あり */
  padding: 20px;
}
```

---

### 1-4. なぜ`_card`？

- ✅ 親がflex
- ✅ 背景色・枠線あり
- ✅ 子もflexを使ってる（でもこれは関係ない）

**→ 背景色があるから`_card`**

---

## パターン2: 親flex + 子flex + 背景色なし → `_item`

### 2-1. 構造図

```
header_row ← ①親がflex
 │
 ├─ site_logo ← ②子もflex + 背景色なし → _item
 │   └─ ロゴ画像
 │
 └─ global_nav ← ②子もflex + 背景色なし → _item
     └─ global_nav_list
         ├─ リンク1
         ├─ リンク2
         └─ リンク3
```

---

### 2-2. HTML

```html
<div class="header_row">
  <div class="site_logo">
    <img src="logo.svg">
  </div>
  
  <nav class="global_nav">
    <ul class="global_nav_list">
      <li><a href="#">HOME</a></li>
      <li><a href="#">ABOUT</a></li>
    </ul>
  </nav>
</div>
```

---

### 2-3. CSS

```css
/* ①親：flexでロゴとナビを横並び */
.header_row {
  display: flex;
  justify-content: space-between;
}

/* ②子：それぞれflexを使うけど、背景色なし */
.site_logo {
  display: flex;    /* ← flexを使う */
  /* 背景色なし */
}

.global_nav_list {
  display: flex;    /* ← flexを使う */
  gap: 20px;
  /* 背景色なし */
}
```

---

### 2-4. なぜ`_item`？（または固有名）

- ✅ 親がflex
- ❌ 背景色・枠線なし
- ✅ 子もflexを使ってる（でもこれは関係ない）

**→ 背景色がないから`_item`**

ただし、この例では`site_logo`と`global_nav`という固有名を使ってる。  
これは「ロゴ」「ナビ」という明確な役割があるから。

---

## パターン3: 親flex + 子flexなし + 背景色なし → `_item`

### 3-1. 構造図

```
sns_list ← ①親がflex
 │
 ├─ sns_item ← ②子はflexなし + 背景色なし → _item
 │   └─ Instagram画像
 │
 ├─ sns_item ← ②子はflexなし + 背景色なし → _item
 │   └─ Twitter画像
 │
 └─ sns_item ← ②子はflexなし + 背景色なし → _item
     └─ Facebook画像
```

---

### 3-2. HTML

```html
<div class="sns_list">
  <a class="sns_item" href="#">
    <img src="instagram.svg">
  </a>
  <a class="sns_item" href="#">
    <img src="twitter.svg">
  </a>
  <a class="sns_item" href="#">
    <img src="facebook.svg">
  </a>
</div>
```

---

### 3-3. CSS

```css
/* ①親：flexでアイコンを横並び */
.sns_list {
  display: flex;
  gap: 10px;
}

/* ②子：flexを使わない + 背景色なし */
.sns_item {
  /* flexは使わない */
  /* 背景色なし */
}
```

---

### 3-4. なぜ`_item`？

- ✅ 親がflex
- ❌ 背景色・枠線なし
- ❌ 子はflexを使わない

**→ 背景色がないから`_item`**

---

## パターン4: 親flex + 子flexなし + 背景色あり → `_card`

### 4-1. 構造図

```
product_list ← ①親がflex
 │
 ├─ product_card ← ②子はflexなし + 背景色あり → _card
 │   ├─ 商品画像
 │   └─ 商品名（テキストだけ、縦並びは自然な流れ）
 │
 └─ product_card ← ②子はflexなし + 背景色あり → _card
     ├─ 商品画像
     └─ 商品名
```

---

### 4-2. HTML

```html
<div class="product_list">
  <div class="product_card">
    <img src="product1.jpg">
    <p>商品名1</p>
  </div>
  
  <div class="product_card">
    <img src="product2.jpg">
    <p>商品名2</p>
  </div>
</div>
```

---

### 4-3. CSS

```css
/* ①親：flexでカードを横並び */
.product_list {
  display: flex;
  gap: 20px;
}

/* ②子：flexは使わない + 背景色あり */
.product_card {
  /* flexは使わない（imgとpは自然に縦並びになる） */
  background-color: #fff; /* ← 背景色あり */
  border: 1px solid #ddd; /* ← 枠線あり */
  padding: 20px;
}
```

---

### 4-4. なぜ`_card`？

- ✅ 親がflex
- ✅ 背景色・枠線あり
- ❌ 子はflexを使わない（でもこれは関係ない）

**→ 背景色があるから`_card`**

---

## まとめ

### 判断フローチャート

```
親要素がflexを使ってる？
 │
 ├─ NO → _container または _inner
 │
 └─ YES → 子要素に背景色・枠線がある？
     │
     ├─ YES → _card
     │
     └─ NO → _item（または固有名）
```

### 重要ポイント

1. **子要素自身がflexを使うかどうかは関係ない**
2. **判断基準は「背景色・枠線があるか」だけ**
3. **flexが2重でも、背景色がなければ`_item`**
4. **flexが1回でも、背景色があれば`_card`**

---

## よくある間違い

### ❌ 間違い1: 「flexが2回使われてるから`_card`」

```html
<div class="header_row">  <!-- flex -->
  <nav class="global_nav">  <!-- flex -->
    <!-- ナビの中身 -->
  </nav>
</div>
```

**正しい判断：**
- 親がflex ✅
- 背景色なし ❌
- **→ `_item`または固有名（この場合は`global_nav`）**

---

### ❌ 間違い2: 「子がflexを使ってないから`_item`」

```html
<div class="blog_list">  <!-- flex -->
  <div class="blog_card">  <!-- flexなし + 背景色あり -->
    <img src="blog.jpg">
    <h3>ブログタイトル</h3>
  </div>
</div>
```

**正しい判断：**
- 親がflex ✅
- 背景色あり ✅
- **→ `_card`**（子がflexを使ってなくても関係ない）

---

## ドキュメント情報

- **作成日**: 2024年12月18日
- **最終更新**: 2024年12月18日
- **バージョン**: 1.0
- **ステータス**: 補足資料
