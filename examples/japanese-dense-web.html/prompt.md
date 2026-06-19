# SKILL: Japanese Portal Directory Design
# Brief: 価格.com–style information-dense category portal
# Mood word: Dense
# Do not use this skill for any other aesthetic register.

---

## 1. Design System

### Colors
--color-bg:           #FFFFFF    /* dominant background */
--color-red:          #CC0000    /* primary action, brand header, CTA buttons */
--color-red-hover:    #AA0000    /* button hover state */
--color-blue-link:    #0066CC    /* ALL hyperlinks, unvisited */
--color-link-visited: #551A8B    /* visited links (browser default, do not override) */
--color-nav-bg:       #F2F2F2    /* navigation rows, alternating row bg */
--color-border:       #CCCCCC    /* ALL 1px borders, grid dividers */
--color-text-body:    #333333    /* main body text */
--color-text-dark:    #000000    /* category header labels, bold text */
--color-text-small:   #666666    /* meta text, breadcrumbs, utility links */
--color-accent-yellow:#FFD900    /* promotional banners ONLY — use sparingly */
--color-accent-orange:#FF6600    /* secondary promo callouts ONLY */

### Typography
Font stack JP:    "Yu Gothic", "Meiryo", "MS Gothic", sans-serif
Font stack Latin: Arial, "Helvetica Neue", sans-serif
Font stack number:"Arial", "Courier New", monospace (for prices/counts)

Font sizes (px, fixed — do NOT use rem/em for this aesthetic):
  - Utility bar text:       10px, color: #666666
  - Body / sub-category:    11px, color: #0066CC (links) or #333333
  - Category header:        12–13px, font-weight: bold, color: #333333
  - Navigation label:       12px, font-weight: bold
  - Search placeholder:     12px
  - Section title bar:      13px, font-weight: bold, background: #CC0000, color: #FFF
  - Promotional headline:   18–24px, font-weight: bold (promotional banners only)

Line-height: 1.4 everywhere. Do NOT increase.
Letter-spacing: 0 (default). Do NOT add.

### Spacing Scale
Internal cell padding:    4px top/bottom, 6px left/right
Gap between grid cells:   0 (border handles separation)
Section margin:           6px vertical between major sections
Icon margin-right:        4px (icon always left of category name)
Link vertical gap:        2–3px between stacked links

### Structural Rules
- ALL borders: 1px solid #CCCCCC
- NO border-radius anywhere
- NO box-shadow anywhere
- NO gradient backgrounds (except promotional banners)
- NO images as design elements — images only in ad slots and product thumbnails
- Page width: 1000px fixed, centered, margin: 0 auto
- Layout: 3 columns, always fixed px widths, NO flexbox stretch behavior for columns

---

## 2. Section-by-Section Brief

### Section A: Utility Bar (top edge)
- Content: right-aligned utility links — ログイン, 新規登録, 閲覧履歴, ご利用ガイド
- Composition: single row, 1000px wide, white bg, text 10px #666666, links right-aligned
- Border-bottom: 1px #CCCCCC
- Height: ~22px
- No icons. Text only.

### Section B: Search Header
- Content: site logo (left), search input (center), 検索 button (red), ★人気キーワード button (outline)
- Composition: horizontal row. Logo occupies ~180px left. Input field takes flexible center. 
  Buttons right of input. RIGHT side has ad slot (~200px) for banner (e.g. Toshiba ad).
- Search input: border 1px #CC0000 (red border — signature detail), height 26px, 
  placeholder text 12px, padding-left 6px
- 検索 button: background #CC0000, color #FFFFFF, font-weight bold, 13px, no border-radius,
  padding: 4px 12px
- ★人気キーワード button: border 1px #999, background white, 12px, padding 4px 10px

### Section C: Hot Keywords Bar (注目キーワード)
- Content: 注目キーワード label (bold, small, white text on #CC0000 bg, ~80px wide)
  followed by horizontal list of keyword links separated by spaces
- Composition: single row, full 1000px, bg #FFF8E0 (very light cream/yellow)
- Border-top and bottom: 1px #CCCCCC
- Keywords: 12px, color #0066CC, no underline at rest, underline on hover
- Height: ~24px, vertical-align: middle

### Section D: Info Ticker Row
- Content: "今が買い時の商品は？" + "花粉対策の商品は？" + "自己負担0円とは？" — editorial links
- Composition: single row, separator pipes | between items, 11px text
- Background: #FFFFFF, border-bottom: 1px #CCCCCC

### Section E: Main 3-Column Body
Layout: 
  Left column:   200px (category nav)
  Center column: 560px (featured content + main category grid)
  Right column:  220px (ad sidebar)
  Total:         980px + borders = ~1000px

#### E1: Left Column — Category Navigation
- Each category cell:
  - 200px wide
  - Icon (20×20px, colorful) + bold category name (13px #333) in one row
  - Below: sub-category links as 11px #0066CC, each on its own line OR comma-separated
  - Cell padding: 5px 6px
  - Border-bottom: 1px #CCCCCC
  - NO background color (white)
  - On hover over category name: color → #CC0000

Categories to implement (in order, with typical sub-categories):
  パソコン: ノート, タブレット, デスクトップ, PC/サーバ, 周辺機器
  プロバイダ: ADSL, 光, CATV, WIMAX
  自動車・バイク: 新車, 中古車, パーツ, 自転車, 用品
  ファッション: ブランド, バッグ, シューズ, スポーツ, ジュエリー
  スポーツ: ゴルフ, 野球, サッカー, 格闘技, マリン
  電気料金: 各地域比較リンク
  インテリア・家具: ベッド, マットレス, 照明, カーテン
  コンタクトレンズ: (sub items)
  家電: テレビ, 洗濯機, 冷蔵庫, 掃除機, エアコン
  モバイルデータ通信: スマートフォン, SIM, MVNO, Wi-Fi
  自動車保険: 各社比較
  クレジットカード: Visa, Master, AMEX, ETC
  靴・シューズ: スニーカー, パンプス, サンダル
  アウトドア: キャンプ, 登山, ランニング
  住宅設備・リフォーム: (sub items)
  キッチン用品: 包丁, 鍋, フライパン
  カメラ: デジタル一眼, ミラーレス, コンデジ
  スマートフォン・携帯電話: iPhone, Android, ガラケー
  ローン: 住宅, カーローン, 教育ローン
  投資・資産運用: FX, 株, NISA, 投資信託
  腕時計・アクセサリー: 腕時計, ネックレス
  本・CD・DVD: 書籍, CD, DVD, ブルーレイ
  DIY・工具: (sub items)
  生活雑貨: (sub items)
  ベビー・キッズ: (sub items)
  美容・ヘルス: (sub items)

#### E2: Center Column — Featured Content
- TOP: Full-width promotional banner within center column (560px wide, ~130px tall)
  Background: yellow #FFD900, contains bold Japanese promotional text + logo
  e.g. "まとめるのが断然お得！" + price callout "¥99,600/年 割引"
  Typography for promo: 20–28px bold Japanese, color #CC0000 or #333333

- BELOW BANNER: Two sub-feature rows (editorial links), each ~26px tall, 
  full 560px width, separated by 1px #CCCCCC
  e.g. "今が買い時の商品は？" | "花粉対策の商品は？"

- BELOW THAT: THE MAIN CATEGORY GRID
  Grid: 3 columns × N rows within the 560px center column
  Each cell: ~186px wide, identical structure to left column cells
  Same border treatment: 1px #CCCCCC on all sides
  Same padding: 5px 6px
  Categories duplicate the left nav but show MORE sub-category depth

#### E3: Right Column — Ad Sidebar (220px)
- Top: Large banner ad (220×200px approx) — product photo + specs text + brand logo
  Style matches editorial: no heavy drop shadows, integrate visually
- Below: News/article list
  Section header: 13px bold "新着・お知らせ一覧" on background #CC0000 white text
  Items: 11px #0066CC links, date prefix in #666666, one per line
  Border-bottom: 1px #CCCCCC between items
- Below: More product news items with small product thumbnail (60×45px left)
  + headline text 11px right of thumbnail + date 10px below

---

## 3. Signature Element Spec

The signature element is the **category grid with icon + bold header + indented sub-links**.

**At rest:** A rectangular cell ~200px wide, white background, 1px #CCCCCC border on all sides.
Top row: small colorful icon (20px) immediately followed by bold category name 13px #333.
Below that: 3–6 sub-category names as 11px #0066CC links, each on its own line, left-aligned
flush with icon (not indented further). No bullets. No separators. Just text rows.

**On hover:** The hovered link text changes color to #CC0000. No other change — 
no background shift, no border change, no elevation.

**What triggers it:** Purely static — renders on page load. The visual idea is 
a newspaper classified ad section turned into interactive navigation.

**The feeling it produces:** The viewer feels simultaneously overwhelmed and competent —
the density signals authority ("everything is here") while the consistent cell structure 
signals navigability ("but I can find what I want").

---

## 4. Functional Spec per Interactive Element

### Search Bar
─────────────────────────────────────────────
State:    queryText: string (value of text input, initially empty)
          filterMode: enum ["all"] — default; expands if filter tabs present

Trigger:  User types → queryText = event.target.value (live, no debounce needed)
          User clicks 検索 button → window.location = `/search?q=${queryText}`
          User presses Enter while focused on input → same as clicking 検索

Reaction: Input field → displays queryText as typed
          検索 button → no visual state change (no loading spinner — this is 
          a navigation action, not an async operation)

Pseudocode:
  searchInput = document.querySelector('#search-input')
  searchBtn   = document.querySelector('#search-btn')

  searchBtn.onclick = () => navigateTo('/search?q=' + searchInput.value)
  searchInput.onkeydown = (e) => if (e.key === 'Enter') navigateTo('/search?q=' + searchInput.value)

---

### Filter Toggle Tabs (メーカー / 製品カテゴリ / etc.)
─────────────────────────────────────────────
State:    activeTab: string, one of ["maker", "category", "product", "model"]
          initial value: "maker" (first tab)

Trigger:  User clicks any tab label → activeTab = that tab's key

Reaction: Clicked tab → background #CC0000, text #FFFFFF, border-bottom removed
          All other tabs → background #F2F2F2, text #333333, border 1px #CCCCCC

Pseudocode:
  tabs.forEach(tab => {
    tab.onclick = () => {
      activeTab = tab.dataset.key
      tabs.forEach(t => t.classList.remove('active'))
      tab.classList.add('active')
    }
  })
  // CSS: .active { background: #CC0000; color: #fff; border-bottom: none; }

---

## 5. Animation and Interaction Rules

**These things animate:** Nothing. Zero animation.

**Permitted states:**
- Link hover: color changes to #CC0000, text-decoration: underline — this is browser behavior, not designed animation
- Link visited: #551A8B (browser default) — do not suppress
- Active/pressed button: background darkens to #AA0000 — CSS :active only, instant, no transition

**Prohibited explicitly:**
- NO transition or animation CSS properties on any element
- NO transform on any element
- NO opacity change on any element
- NO JavaScript-driven visual state change except the search filter tab toggle
- NO scroll-triggered effects
- NO hover-reveal content (tooltips, dropdowns, sub-menus) unless implementing 
  a true megamenu that is architecturally required

**Everything else is static.**

---

## 6. Anti-Patterns for This Brief

1. **DO NOT add whitespace as a "breathing" or "premium" design decision.**
   Every pixel between elements that could be a text character is a missed opportunity
   in this design language. Padding is functional (4–6px), not expressive.

2. **DO NOT use border-radius on any element.**
   Rounded corners signal friendliness, modernity, and approachability — all three
   are the wrong register. Sharp 90° corners are non-negotiable.

3. **DO NOT use CSS drop-shadows or elevation.**
   No box-shadow, no text-shadow (except on promotional banner text if needed for contrast),
   no z-axis simulation of any kind. The design lives entirely in 2D.

4. **DO NOT use large images as layout elements.**
   Images appear only in: (a) ad slots with defined px dimensions, (b) product thumbnails
   in news lists (60×45px). A full-bleed hero image would destroy the information
   density that defines this aesthetic.

5. **DO NOT reduce the number of categories or sub-categories "for clarity."**
   Comprehensiveness IS the clarity. A user on this page expects to see everything.
   Hiding categories in "see more" interactions betrays the design contract.
   If it exists in the product catalog, it appears in the category grid.

---
END OF SKILL