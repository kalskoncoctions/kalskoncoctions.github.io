<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Kal's Koncoctions Katalog</title>
  <link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Serif+Display:ital@0;1&family=Inconsolata:wght@400;600&display=swap" rel="stylesheet"/>
  <style>
    :root {
      --ember:    #FF3B00;
      --lava:     #FF6B1A;
      --gold:     #FFB347;
      --smoke:    #1A1108;
      --char:     #0D0A06;
      --ash:      #2E2016;
      --cream:    #F5ECD7;
      --muted:    #8A7560;
      --glow:     rgba(255,59,0,0.18);
    }

    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    html { scroll-behavior: smooth; }

    body {
      background-color: var(--char);
      color: var(--cream);
      font-family: 'Inconsolata', monospace;
      min-height: 100vh;
      overflow-x: hidden;
    }

    /* ── GRAIN OVERLAY ── */
    body::before {
      content: '';
      position: fixed; inset: 0;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='1'/%3E%3C/svg%3E");
      opacity: 0.04;
      pointer-events: none;
      z-index: 999;
    }

    /* ── HEADER ── */
    header {
      position: relative;
      padding: 80px 40px 60px;
      text-align: center;
      overflow: hidden;
    }

    header::before {
      content: '';
      position: absolute;
      bottom: -60px; left: 50%;
      transform: translateX(-50%);
      width: 600px; height: 300px;
      background: radial-gradient(ellipse at center, var(--glow) 0%, transparent 70%);
      pointer-events: none;
    }

    .header-eyebrow {
      font-family: 'Inconsolata', monospace;
      font-size: 0.75rem;
      letter-spacing: 0.35em;
      text-transform: uppercase;
      color: var(--ember);
      margin-bottom: 16px;
      animation: fadeUp 0.6s ease both;
    }

    h1 {
      font-family: 'Bebas Neue', sans-serif;
      font-size: clamp(5rem, 14vw, 11rem);
      line-height: 0.88;
      letter-spacing: 0.02em;
      background: linear-gradient(160deg, var(--gold) 0%, var(--ember) 55%, #8B1A00 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      animation: fadeUp 0.6s 0.1s ease both;
    }

    .header-sub {
      font-family: 'DM Serif Display', serif;
      font-style: italic;
      font-size: 1.15rem;
      color: var(--muted);
      margin-top: 18px;
      animation: fadeUp 0.6s 0.2s ease both;
    }

    .header-divider {
      width: 80px; height: 2px;
      background: linear-gradient(90deg, transparent, var(--ember), transparent);
      margin: 32px auto 0;
      animation: fadeUp 0.6s 0.3s ease both;
    }

    /* ── SECTION LABELS ── */
    .section-label {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 0.65rem;
      letter-spacing: 0.4em;
      text-transform: uppercase;
      color: var(--ember);
      padding: 60px 40px 20px;
      max-width: 1100px;
      margin: 0 auto;
      opacity: 0.7;
    }

    /* ── SPICE BLEND CARD ── */
    .blend-card {
      max-width: 1100px;
      margin: 0 auto 60px;
      padding: 0 40px;
      animation: fadeUp 0.5s 0.4s ease both;
    }

    .blend-inner {
      border: 1px solid var(--ash);
      border-left: 3px solid var(--lava);
      padding: 28px 36px;
      background: rgba(255,107,26,0.04);
      position: relative;
    }

    .blend-inner::after {
      content: 'BLEND';
      position: absolute;
      top: -10px; right: 24px;
      font-family: 'Bebas Neue', sans-serif;
      font-size: 0.6rem;
      letter-spacing: 0.3em;
      background: var(--char);
      color: var(--lava);
      padding: 0 8px;
    }

    .blend-name {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 2rem;
      letter-spacing: 0.08em;
      color: var(--gold);
      margin-bottom: 12px;
    }

    /* ── CATALOG GRID ── */
    .catalog {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
      gap: 1px;
      max-width: 1100px;
      margin: 0 auto;
      padding: 0 40px 80px;
      background: var(--ash);
    }

    /* ── SAUCE CARD ── */
    .sauce-card {
      background: var(--smoke);
      padding: 32px 28px 28px;
      position: relative;
      transition: background 0.25s ease;
      cursor: default;
      animation: fadeUp 0.4s ease both;
    }

    .sauce-card:hover {
      background: var(--ash);
      z-index: 2;
    }

    .sauce-card:hover .card-glow {
      opacity: 1;
    }

    .card-glow {
      position: absolute;
      inset: 0;
      background: radial-gradient(ellipse at 30% 0%, rgba(255,59,0,0.07) 0%, transparent 65%);
      opacity: 0;
      transition: opacity 0.3s ease;
      pointer-events: none;
    }

    .card-number {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 0.65rem;
      letter-spacing: 0.3em;
      color: var(--muted);
      margin-bottom: 10px;
    }

    .card-name {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 1.85rem;
      line-height: 1;
      letter-spacing: 0.05em;
      color: var(--cream);
      margin-bottom: 16px;
      transition: color 0.2s;
    }

    .sauce-card:hover .card-name {
      color: var(--gold);
    }

    /* heat badge */
    .heat-badge {
      display: inline-flex;
      align-items: center;
      gap: 3px;
      margin-bottom: 18px;
    }

    .flame {
      font-size: 0.75rem;
      filter: grayscale(1);
      opacity: 0.3;
      transition: all 0.2s;
    }

    .flame.lit {
      filter: none;
      opacity: 1;
    }

    .heat-label {
      font-size: 0.6rem;
      letter-spacing: 0.25em;
      color: var(--muted);
      margin-left: 6px;
      text-transform: uppercase;
    }

    /* ingredient tags */
    .ingredients {
      display: flex;
      flex-wrap: wrap;
      gap: 5px;
    }

    .tag {
      font-size: 0.65rem;
      letter-spacing: 0.06em;
      padding: 3px 8px;
      border: 1px solid var(--ash);
      color: var(--muted);
      transition: border-color 0.2s, color 0.2s;
      border-radius: 1px;
    }

    .tag.highlight {
      border-color: rgba(255,59,0,0.4);
      color: var(--lava);
    }

    .sauce-card:hover .tag {
      border-color: rgba(255,107,26,0.2);
      color: #9A8570;
    }

    .sauce-card:hover .tag.highlight {
      border-color: var(--ember);
      color: var(--gold);
    }

    /* ── FOOTER ── */
    footer {
      text-align: center;
      padding: 40px;
      font-size: 0.65rem;
      letter-spacing: 0.25em;
      color: var(--muted);
      border-top: 1px solid var(--ash);
      opacity: 0.5;
    }

    /* ── ANIMATIONS ── */
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(18px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    /* stagger cards */
    .sauce-card:nth-child(1)  { animation-delay: 0.05s }
    .sauce-card:nth-child(2)  { animation-delay: 0.10s }
    .sauce-card:nth-child(3)  { animation-delay: 0.15s }
    .sauce-card:nth-child(4)  { animation-delay: 0.20s }
    .sauce-card:nth-child(5)  { animation-delay: 0.25s }
    .sauce-card:nth-child(6)  { animation-delay: 0.30s }
    .sauce-card:nth-child(7)  { animation-delay: 0.35s }
    .sauce-card:nth-child(8)  { animation-delay: 0.40s }
    .sauce-card:nth-child(9)  { animation-delay: 0.45s }
    .sauce-card:nth-child(10) { animation-delay: 0.50s }
    .sauce-card:nth-child(11) { animation-delay: 0.55s }
    .sauce-card:nth-child(12) { animation-delay: 0.60s }
    .sauce-card:nth-child(13) { animation-delay: 0.65s }

    @media (max-width: 600px) {
      header { padding: 60px 24px 40px; }
      .section-label, .blend-card, .catalog { padding-left: 24px; padding-right: 24px; }
    }
  </style>
</head>
<body>

  <!-- HEADER -->
  <header>
    <p class="header-eyebrow">Handcrafted · Small Batch · No Compromise</p>
    <h1>Kal's<br>Koncoctions<br>Katalog</h1>
    <p class="header-sub">Flavor With A Fever</p>
    <div class="header-divider"></div>
  </header>

  <!-- PEPPER POTPURRI -->
  <p class="section-label">— Spice Blend</p>
  <div class="blend-card">
    <div class="blend-inner">
      <div class="blend-name">Pepper Potpurri</div>
      <div class="ingredients">
        <span class="tag highlight">Crushed Red Pepper</span>
        <span class="tag highlight">Jordanian Thyme</span>
        <span class="tag">Oregano</span>
        <span class="tag highlight">Paprika</span>
        <span class="tag highlight">Garlic</span>
        <span class="tag">Onion</span>
        <span class="tag">Sugar</span>
        <span class="tag highlight">Red Bell Pepper</span>
        <span class="tag">Black Pepper</span>
        <span class="tag">Lemon Pepper</span>
        <span class="tag">Tomato</span>
        <span class="tag highlight">Chili</span>
        <span class="tag">Lemon Peel</span>
        <span class="tag">Rosemary</span>
        <span class="tag">Chives</span>
        <span class="tag">Smoked Flavor</span>
      </div>
    </div>
  </div>

  <!-- HOT SAUCES -->
  <p class="section-label">— Hot Sauce Catalog · 13 Expressions</p>

  <div class="catalog">

    <!-- 1. Humungous Hog -->
    <div class="sauce-card">
      <div class="card-glow"></div>
      <div class="card-number">No. 01</div>
      <div class="card-name">Humungous Hog</div>
      <div class="heat-badge">
        <span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame lit">🔥</span>
        <span class="heat-label">Extreme</span>
      </div>
      <div class="ingredients">
        <span class="tag highlight">Carolina Reaper</span>
        <span class="tag highlight">Moruga Scorpion</span>
        <span class="tag highlight">Ghost Pepper</span>
        <span class="tag highlight">Chile de Arbol</span>
        <span class="tag highlight">Thai Chili</span>
        <span class="tag">Chicken Broth</span>
        <span class="tag">Cilantro</span>
        <span class="tag">Saffron</span>
        <span class="tag">Smoked Paprika</span>
        <span class="tag">Baharat</span>
        <span class="tag">Turmeric</span>
        <span class="tag">Tomato Paste</span>
        <span class="tag highlight">Vulcan's Fire Salt</span>
        <span class="tag">Sumac</span>
        <span class="tag">Lemon Juice</span>
        <span class="tag">Aged Balsamic Vinegar</span>
        <span class="tag">Apple Cider Vinegar</span>
      </div>
    </div>

    <!-- 2. Ghoulish Garlic -->
    <div class="sauce-card">
      <div class="card-glow"></div>
      <div class="card-number">No. 02</div>
      <div class="card-name">Ghoulish Garlic</div>
      <div class="heat-badge">
        <span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame">🔥</span><span class="flame">🔥</span>
        <span class="heat-label">Hot</span>
      </div>
      <div class="ingredients">
        <span class="tag highlight">Orange Habanero</span>
        <span class="tag">Orange Bell Pepper</span>
        <span class="tag highlight">Garlic</span>
        <span class="tag">Lime</span>
        <span class="tag">Shredded Carrots</span>
        <span class="tag">Cucumber</span>
        <span class="tag">Jordanian Thyme</span>
        <span class="tag">White Pepper</span>
        <span class="tag">Black Pepper</span>
        <span class="tag">Ground Mustard</span>
        <span class="tag">Ground Cumin</span>
        <span class="tag">Tomato Paste</span>
        <span class="tag highlight">Pomegranate Molasses</span>
        <span class="tag">Celtic Sea Salt</span>
        <span class="tag">Pink Himalayan Salt</span>
        <span class="tag">Apple Cider Vinegar</span>
      </div>
    </div>

    <!-- 3. Cucumber Coolant -->
    <div class="sauce-card">
      <div class="card-glow"></div>
      <div class="card-number">No. 03</div>
      <div class="card-name">Cucumber Coolant</div>
      <div class="heat-badge">
        <span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame">🔥</span><span class="flame">🔥</span><span class="flame">🔥</span>
        <span class="heat-label">Medium</span>
      </div>
      <div class="ingredients">
        <span class="tag highlight">Orange Habanero</span>
        <span class="tag">Orange Bell Pepper</span>
        <span class="tag">Lime</span>
        <span class="tag highlight">Cucumber</span>
        <span class="tag">Shredded Carrots</span>
        <span class="tag">Jordanian Thyme</span>
        <span class="tag">White Pepper</span>
        <span class="tag">Ground Mustard</span>
        <span class="tag">Ground Cumin</span>
        <span class="tag">Tomato Paste</span>
        <span class="tag highlight">Pomegranate Molasses</span>
        <span class="tag highlight">Date Molasses</span>
        <span class="tag">Celtic Sea Salt</span>
        <span class="tag">Pink Himalayan Salt</span>
        <span class="tag">Apple Cider Vinegar</span>
      </div>
    </div>

    <!-- 4. Gorilla's Giard -->
    <div class="sauce-card">
      <div class="card-glow"></div>
      <div class="card-number">No. 04</div>
      <div class="card-name">Gorilla's Giard</div>
      <div class="heat-badge">
        <span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame">🔥</span><span class="flame">🔥</span><span class="flame">🔥</span>
        <span class="heat-label">Medium</span>
      </div>
      <div class="ingredients">
        <span class="tag highlight">Giardiniera Peppers</span>
        <span class="tag highlight">Serrano Pepper</span>
        <span class="tag">Red Bell Pepper</span>
        <span class="tag">Tomato Paste</span>
        <span class="tag highlight">Organic Juniper Berries</span>
        <span class="tag">Whole Grain Mustard</span>
        <span class="tag">Dill</span>
        <span class="tag">Shredded Carrots</span>
        <span class="tag">Citric Acid</span>
        <span class="tag">Sugar</span>
        <span class="tag">Onion</span>
        <span class="tag">Parsley</span>
        <span class="tag">Lemon Peel</span>
        <span class="tag">Lime</span>
        <span class="tag">Celery Seed</span>
        <span class="tag">Fennel Seed</span>
        <span class="tag">Coriander</span>
        <span class="tag">Oregano</span>
        <span class="tag">Black Pepper</span>
        <span class="tag">White Wine Vinegar</span>
      </div>
    </div>

    <!-- 5. Summertime Sunshine -->
    <div class="sauce-card">
      <div class="card-glow"></div>
      <div class="card-number">No. 05</div>
      <div class="card-name">Summertime Sunshine</div>
      <div class="heat-badge">
        <span class="flame lit">🔥</span><span class="flame">🔥</span><span class="flame">🔥</span><span class="flame">🔥</span><span class="flame">🔥</span>
        <span class="heat-label">Mild</span>
      </div>
      <div class="ingredients">
        <span class="tag highlight">Serrano Pepper</span>
        <span class="tag">Green Bell Pepper</span>
        <span class="tag highlight">Honeydew</span>
        <span class="tag highlight">Cantaloupe</span>
        <span class="tag highlight">Dragonfruit</span>
        <span class="tag highlight">Papaya</span>
        <span class="tag">Peach</span>
        <span class="tag highlight">Pineapple</span>
        <span class="tag">Organic Dates</span>
        <span class="tag">Black Plum</span>
        <span class="tag">Kiwi</span>
        <span class="tag">Lime</span>
        <span class="tag">Organic Celery</span>
        <span class="tag">Cilantro</span>
        <span class="tag">Pitted Dried Apricots</span>
        <span class="tag">Pomegranate Molasses</span>
        <span class="tag">Ground Cumin</span>
        <span class="tag">White Wine Vinegar</span>
      </div>
    </div>

    <!-- 6. Heated Honey -->
    <div class="sauce-card">
      <div class="card-glow"></div>
      <div class="card-number">No. 06</div>
      <div class="card-name">Heated Honey</div>
      <div class="heat-badge">
        <span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame">🔥</span><span class="flame">🔥</span>
        <span class="heat-label">Hot</span>
      </div>
      <div class="ingredients">
        <span class="tag highlight">Habanero Pepper</span>
        <span class="tag highlight">Serrano Pepper</span>
        <span class="tag">Mini Sweet Pepper</span>
        <span class="tag highlight">Infinity Hero IPA</span>
        <span class="tag highlight">Manuka Honey</span>
        <span class="tag">Minneolas</span>
        <span class="tag">Minneola Zest</span>
        <span class="tag">Malt Vinegar</span>
        <span class="tag">Aged Red Wine Vinegar</span>
        <span class="tag">Xanthan Gum</span>
      </div>
    </div>

    <!-- 7. Diabolical Distillery -->
    <div class="sauce-card">
      <div class="card-glow"></div>
      <div class="card-number">No. 07</div>
      <div class="card-name">Diabolical Distillery</div>
      <div class="heat-badge">
        <span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame">🔥</span>
        <span class="heat-label">Very Hot</span>
      </div>
      <div class="ingredients">
        <span class="tag highlight">Carolina Reaper</span>
        <span class="tag highlight">Chile de Arbol</span>
        <span class="tag">Sweet Mini Pepper</span>
        <span class="tag highlight">Torshi (Pickled Cabbage)</span>
        <span class="tag highlight">Pomegranate Juice</span>
        <span class="tag">Mandarin Oranges</span>
        <span class="tag">Whole Grain Mustard</span>
        <span class="tag">Sweet Spanish Paprika</span>
        <span class="tag">Onion</span>
        <span class="tag">Sea Salt</span>
        <span class="tag">Celery Salt</span>
        <span class="tag">Distilled White Vinegar</span>
        <span class="tag">Xanthan Gum</span>
      </div>
    </div>

    <!-- 8. Molten Magma -->
    <div class="sauce-card">
      <div class="card-glow"></div>
      <div class="card-number">No. 08</div>
      <div class="card-name">Molten Magma</div>
      <div class="heat-badge">
        <span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame">🔥</span><span class="flame">🔥</span>
        <span class="heat-label">Hot</span>
      </div>
      <div class="ingredients">
        <span class="tag highlight">Red Hot Jamaican Pepper</span>
        <span class="tag">Green Pepper</span>
        <span class="tag highlight">Guava Nectar Juice</span>
        <span class="tag">Shredded Carrots</span>
        <span class="tag">White Pepper</span>
        <span class="tag">Sweet Spanish Paprika</span>
        <span class="tag">Onion</span>
        <span class="tag">Sugar</span>
        <span class="tag">Celtic Sea Salt</span>
        <span class="tag">Aged Red Wine Vinegar</span>
        <span class="tag">Spring Water</span>
      </div>
    </div>

    <!-- 9. Coco Cataclysm -->
    <div class="sauce-card">
      <div class="card-glow"></div>
      <div class="card-number">No. 09</div>
      <div class="card-name">Coco Cataclysm</div>
      <div class="heat-badge">
        <span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame">🔥</span>
        <span class="heat-label">Very Hot</span>
      </div>
      <div class="ingredients">
        <span class="tag highlight">Scorpion Pepper</span>
        <span class="tag highlight">Serrano Pepper</span>
        <span class="tag highlight">Organic Coconut Water</span>
        <span class="tag">Orange/Peach/Mango Juice</span>
        <span class="tag">Honeydew Melon</span>
        <span class="tag">Cantaloupe</span>
        <span class="tag">Tomato Paste</span>
        <span class="tag">Onion</span>
        <span class="tag">White Pepper</span>
        <span class="tag">Black Pepper</span>
        <span class="tag">Citric Acid</span>
        <span class="tag">Lime</span>
        <span class="tag">Celery Salt</span>
        <span class="tag">Pink Himalayan Salt</span>
        <span class="tag">Aged Red Wine Vinegar</span>
      </div>
    </div>

    <!-- 10. Serrano Scientist -->
    <div class="sauce-card">
      <div class="card-glow"></div>
      <div class="card-number">No. 10</div>
      <div class="card-name">Serrano Scientist</div>
      <div class="heat-badge">
        <span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame">🔥</span>
        <span class="heat-label">Very Hot</span>
      </div>
      <div class="ingredients">
        <span class="tag highlight">Scorpion Pepper</span>
        <span class="tag highlight">Scotch Bonnet</span>
        <span class="tag highlight">Jalapeño</span>
        <span class="tag highlight">Serrano</span>
        <span class="tag">Garden Salsa</span>
        <span class="tag highlight">Thai Chili</span>
        <span class="tag">Pomegranate Juice</span>
        <span class="tag">Orange Juice</span>
        <span class="tag">Dill Pickle Juice</span>
        <span class="tag">Organic Dates</span>
        <span class="tag">Turkish Black Currant</span>
        <span class="tag">Tomato Paste</span>
        <span class="tag">Garlic</span>
        <span class="tag">Cilantro</span>
        <span class="tag">Sumac</span>
        <span class="tag">Sweet Spanish Paprika</span>
        <span class="tag highlight">Vulcan's Fire Salt</span>
        <span class="tag">Violet Salt</span>
        <span class="tag">Pink Himalayan Salt</span>
        <span class="tag">Celtic Sea Salt</span>
        <span class="tag">Aged Red Wine Vinegar</span>
      </div>
    </div>

    <!-- 11. Volcanic Vulture -->
    <div class="sauce-card">
      <div class="card-glow"></div>
      <div class="card-number">No. 11</div>
      <div class="card-name">Volcanic Vulture</div>
      <div class="heat-badge">
        <span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame">🔥</span><span class="flame">🔥</span><span class="flame">🔥</span>
        <span class="heat-label">Medium</span>
      </div>
      <div class="ingredients">
        <span class="tag highlight">Cayenne Pepper</span>
        <span class="tag highlight">Super Chili Pepper</span>
        <span class="tag highlight">Serrano Pepper</span>
        <span class="tag">Onion</span>
        <span class="tag">Garlic</span>
        <span class="tag">Tomato Paste</span>
        <span class="tag">Chicken Bone Broth</span>
        <span class="tag highlight">Organic MCT Oil</span>
        <span class="tag">White Mushrooms</span>
        <span class="tag">Shredded Carrots</span>
        <span class="tag">Lemon</span>
        <span class="tag">White Pepper</span>
        <span class="tag">Baharat</span>
        <span class="tag">Sumac</span>
        <span class="tag">Turmeric</span>
        <span class="tag">Jordanian Thyme</span>
        <span class="tag">Oregano</span>
        <span class="tag">Rosemary</span>
        <span class="tag">Celery Salt</span>
        <span class="tag">Distilled White Vinegar</span>
      </div>
    </div>

    <!-- 12. Naga Nectarine -->
    <div class="sauce-card">
      <div class="card-glow"></div>
      <div class="card-number">No. 12</div>
      <div class="card-name">Naga Nectarine</div>
      <div class="heat-badge">
        <span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame lit">🔥</span>
        <span class="heat-label">Extreme</span>
      </div>
      <div class="ingredients">
        <span class="tag highlight">Carolina Reaper</span>
        <span class="tag highlight">Scorpion Pepper</span>
        <span class="tag highlight">Ghost Pepper</span>
        <span class="tag highlight">Red Jamaican Pepper</span>
        <span class="tag">Sweet Mini Pepper</span>
        <span class="tag highlight">Toasted Chile de Arbol</span>
        <span class="tag highlight">Chile Pullas</span>
        <span class="tag highlight">Mango</span>
        <span class="tag highlight">Nectarine</span>
        <span class="tag">Lemon</span>
        <span class="tag">Onion</span>
        <span class="tag">Sweet Spanish Paprika</span>
        <span class="tag">Ginger</span>
        <span class="tag">Pink Himalayan Salt</span>
        <span class="tag">Aged Red Wine Vinegar</span>
        <span class="tag">Spring Water</span>
      </div>
    </div>

    <!-- 13. Molten Material -->
    <div class="sauce-card">
      <div class="card-glow"></div>
      <div class="card-number">No. 13</div>
      <div class="card-name">Molten Material</div>
      <div class="heat-badge">
        <span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame lit">🔥</span><span class="flame">🔥</span><span class="flame">🔥</span>
        <span class="heat-label">Hot</span>
      </div>
      <div class="ingredients">
        <span class="tag highlight">Orange Habanero</span>
        <span class="tag">Sweet Mini Pepper</span>
        <span class="tag">Onion</span>
        <span class="tag">Shredded Carrots</span>
        <span class="tag highlight">Pomegranate Molasses</span>
        <span class="tag">Sugar</span>
        <span class="tag">Paprika</span>
        <span class="tag">White Pepper</span>
        <span class="tag">Pink Himalayan Salt</span>
        <span class="tag">Red Wine Vinegar</span>
      </div>
    </div>

  </div>

  <footer>
    KAL'S KONCOCTIONS KATALOG &nbsp;·&nbsp; 13 EXPRESSIONS &nbsp;·&nbsp; SMALL BATCH ALWAYS
  </footer>

</body>
</html>
