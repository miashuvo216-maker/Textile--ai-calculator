
# TEXTILE AI CALCULATOR (MVP v1.0)

A client-side web application engineered specifically for textile engineers, textile students, wet processing specialists, stenter finishing operators, production managers, quality assurance teams, and garment merchandisers.

Built strictly with **HTML5**, **CSS3**, and **Vanilla JavaScript** without Python, Java, or backend server dependencies. The application is completely offline-capable, responsive across mobile, tablet, and desktop, and executes deterministic textile mathematics.

---

### Key Features Implemented

1. **10 Core Fully Functional Textile Calculators:**
   - **GSM Calculator:** Calculates sample area, GSM ($\text{g/m}^2$), and imperial conversion ($\text{oz/yd}^2$) with multiple unit options (cm, mm, inch, m, g, mg).
   - **Fabric Weight Calculator:** Calculates total batch or roll weight in Kilograms (kg) and Pounds (lbs) from length, cuttable width, and GSM.
   - **Fabric Shrinkage Calculator:** Calculates warp/length or weft/width dimensional stability percentage based on standard AATCC 135 / ISO 6330 principles (handles both shrinkage and elongation/growth).
   - **Stenter Overfeed Calculator:** Computes pin-chain overfeed percentage from inlet and delivery speeds, complete with factory warning notices.
   - **Yarn Count Converter:** Universal converter between English Cotton Count ($\text{Ne}$), Metric Count ($\text{Nm}$), $\text{Tex}$, and $\text{Denier}$ with direct/indirect count formulas.
   - **Dye & Chemical Percentage Calculator:** Dual-mode calculation supporting both Percentage on Weight of Fabric ($\% \text{ o.w.f.}$) and Liquor Concentration ($\text{g/L}$).
   - **Liquor Ratio ($\text{M:L}$) Calculator:** Computes total process bath volume in liters based on fabric dry batch weight, liquor ratio ($1:X$), and optional machine piping dead volume.
   - **Machine Production Calculator:** Calculates continuous fabric production rates ($\text{m/hr}$, $\text{kg/hr}$, shift output, and daily output) with realistic efficiency factors and assumptions.
   - **Production Efficiency Calculator:** Evaluates actual vs. target production outputs, calculating efficiency percentages, production variance, and performance ratings.
   - **Fabric Consumption & Booking:** Merchandising calculator for apparel orders calculating net fabric, cutting/process wastage allowances, and gross mill bookings.

2. **Full UI & Industrial Features:**
   - **Real-Time Search Filter:** Instant keyword filtering (e.g., typing *"GSM"*, *"Stenter"*, *"Dyeing"*, *"Yarn"*, *"Shrinkage"*).
   - **Category Menu & Roadmap:** Filter tabs for Fabric, Yarn, Dyeing, Finishing, Production, Quality, Garments, and Favorites, plus an interactive index of all 63 textile calculators.
   - **One-Click Pre-fill Sample Values:** Each calculator includes a sample test button to fill factory benchmark numbers instantly.
   - **Step-by-Step Breakdown:** Detailed mathematical derivations with values substituted into the formulas.
   - **Bilingual Support ($\text{English}$ | $\text{বাংলা}$):** Complete toggle for titles, field labels, units, explanations, error messages, and industrial terminology.
   - **Calculation History:** Browser `localStorage` storage of calculations with timestamps, input summaries, reload capabilities, and single or bulk deletion.
   - **Favorites System:** One-tap bookmarking persisted in `localStorage`.
   - **Dark / Light Mode:** Adaptive theme with persistent user preference.
   - **Defensive Error Handling:** Validates empty fields, rejects invalid negative values, and prevents division-by-zero errors without producing `NaN` or `Infinity`.

---

## Source Code

### 1. `index.html`

```html
<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=5.0, user-scalable=yes">
  <meta name="description" content="Textile AI Calculator - Professional engineering calculators for textile engineers, students, dyeing, finishing, production, quality and garment professionals.">
  <meta name="theme-color" content="#0b0f19">
  <title>Textile AI Calculator | টেক্সটাইল এআই ক্যালকুলেটর</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <!-- Top Navigation Bar -->
  <header class="navbar" id="navbar">
    <div class="nav-container">
      <div class="brand-group" id="brandLogo" role="button" tabindex="0" title="Go to Home">
        <div class="brand-icon">
          <!-- Textile Fabric Weave SVG Icon -->
          <svg viewBox="0 0 24 24" width="28" height="28" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <rect x="2" y="2" width="20" height="20" rx="3" stroke="currentColor" opacity="0.3" fill="none" />
            <path d="M7 2v20M12 2v20M17 2v20" stroke="var(--primary)" />
            <path d="M2 7h20M2 12h20M2 17h20" stroke="var(--accent)" />
            <circle cx="12" cy="12" r="3" fill="var(--primary)" />
          </svg>
        </div>
        <div class="brand-text">
          <div class="brand-title">
            <span class="highlight">TEXTILE</span> AI <span class="badge-mini">PRO</span>
          </div>
          <div class="brand-subtitle" data-i18n="tagline">Engineering & Apparel Suite</div>
        </div>
      </div>

      <div class="nav-actions">
        <!-- Language Switcher -->
        <button id="langToggleBtn" class="nav-btn lang-btn" aria-label="Switch Language" title="English / বাংলা পরিবর্তন করুন">
          <span class="lang-globe">🌐</span>
          <span id="langLabel" class="lang-text">বাংলা</span>
        </button>

        <!-- Dark / Light Theme Toggle -->
        <button id="themeToggleBtn" class="nav-btn" aria-label="Toggle Dark/Light Mode" title="Toggle Theme">
          <span class="theme-icon sun-icon">☀️</span>
          <span class="theme-icon moon-icon">🌙</span>
        </button>

        <!-- Favorites Button -->
        <button id="favoritesNavBtn" class="nav-btn" aria-label="View Favorites" title="Favorites">
          <span class="nav-icon">⭐</span>
          <span id="favCountBadge" class="badge-count">0</span>
        </button>

        <!-- History Drawer Button -->
        <button id="historyNavBtn" class="nav-btn" aria-label="View History" title="Calculation History">
          <span class="nav-icon">⏱️</span>
          <span id="historyCountBadge" class="badge-count">0</span>
        </button>
      </div>
    </div>
  </header>

  <!-- Main Container -->
  <main class="main-content" id="mainContent">

    <!-- Hero / Quick Search Section -->
    <section class="hero-section">
      <div class="hero-content">
        <h1 class="hero-title" data-i18n="heroTitle">Textile AI Calculator</h1>
        <p class="hero-desc" data-i18n="heroDesc">
          Accurate, deterministic calculations for fabric parameters, yarn counts, dyeing chemicals, stenter finishing, machine production, efficiency, and garment costing.
        </p>
        
        <!-- Search Input Bar -->
        <div class="search-wrapper">
          <div class="search-icon">🔍</div>
          <input 
            type="text" 
            id="searchInput" 
            class="search-input" 
            placeholder="Search calculators (e.g. GSM, Stenter, Dyeing, Yarn, Shrinkage)..." 
            data-i18n-placeholder="searchPlaceholder"
            autocomplete="off"
            spellcheck="false"
          >
          <button id="clearSearchBtn" class="search-clear-btn" aria-label="Clear Search" style="display:none;">✕</button>
        </div>
      </div>
    </section>

    <!-- Category Pills Navigation -->
    <section class="category-nav-section">
      <div class="category-scroll" id="categoryTabs" role="tablist">
        <button class="cat-pill active" data-category="all" role="tab" aria-selected="true">
          <span class="cat-icon">🎛️</span>
          <span data-i18n="catAll">All</span>
          <span class="pill-count" id="countAll">10</span>
        </button>
        <button class="cat-pill" data-category="fabric" role="tab" aria-selected="false">
          <span class="cat-icon">🧵</span>
          <span data-i18n="catFabric">Fabric</span>
          <span class="pill-count" id="countFabric">0</span>
        </button>
        <button class="cat-pill" data-category="yarn" role="tab" aria-selected="false">
          <span class="cat-icon">🧶</span>
          <span data-i18n="catYarn">Yarn</span>
          <span class="pill-count" id="countYarn">0</span>
        </button>
        <button class="cat-pill" data-category="dyeing" role="tab" aria-selected="false">
          <span class="cat-icon">🧪</span>
          <span data-i18n="catDyeing">Dyeing</span>
          <span class="pill-count" id="countDyeing">0</span>
        </button>
        <button class="cat-pill" data-category="finishing" role="tab" aria-selected="false">
          <span class="cat-icon">⚙️</span>
          <span data-i18n="catFinishing">Finishing</span>
          <span class="pill-count" id="countFinishing">0</span>
        </button>
        <button class="cat-pill" data-category="production" role="tab" aria-selected="false">
          <span class="cat-icon">🏭</span>
          <span data-i18n="catProduction">Production</span>
          <span class="pill-count" id="countProduction">0</span>
        </button>
        <button class="cat-pill" data-category="quality" role="tab" aria-selected="false">
          <span class="cat-icon">🔍</span>
          <span data-i18n="catQuality">Quality</span>
          <span class="pill-count" id="countQuality">0</span>
        </button>
        <button class="cat-pill" data-category="garment" role="tab" aria-selected="false">
          <span class="cat-icon">👔</span>
          <span data-i18n="catGarment">Garments</span>
          <span class="pill-count" id="countGarment">0</span>
        </button>
        <button class="cat-pill" data-category="favorites" role="tab" aria-selected="false">
          <span class="cat-icon">⭐</span>
          <span data-i18n="catFavorites">Favorites</span>
          <span class="pill-count" id="countFavorites">0</span>
        </button>
      </div>
    </section>

    <!-- Content Views: Directory View vs Calculator Detail View -->
    <div class="view-container">

      <!-- View 1: Calculator Cards Grid (Directory View) -->
      <section id="directoryView" class="view-panel active">
        <div class="directory-header">
          <div class="directory-info">
            <h2 id="currentCategoryTitle" class="section-heading" data-i18n="featuredCalculators">Calculators Directory</h2>
            <span id="resultsCount" class="results-badge">10 available</span>
          </div>
          <div class="directory-actions">
            <button id="viewRoadmapBtn" class="btn-secondary-sm" title="View full 63 calculator scope">
              <span data-i18n="btnFullSuite">📋 Complete 63 Calculator Index</span>
            </button>
          </div>
        </div>

        <!-- Dynamic Calculator Cards Grid -->
        <div class="calculators-grid" id="calculatorsGrid">
          <!-- Injected via JavaScript -->
        </div>

        <!-- Empty Search / Filter State -->
        <div id="noResultsState" class="empty-state" style="display:none;">
          <div class="empty-icon">🔎</div>
          <h3 data-i18n="noResultsTitle">No Calculators Found</h3>
          <p data-i18n="noResultsDesc">Try searching for keywords like "GSM", "Stenter", "Dyeing", "Yarn", "Shrinkage", or clear the filter.</p>
          <button id="resetSearchBtn" class="btn btn-primary" data-i18n="btnResetSearch">Reset Search</button>
        </div>
      </section>

      <!-- View 2: Active Calculator Workspace (Dedicated Interactive View) -->
      <section id="calculatorView" class="view-panel" style="display:none;">
        <div class="calc-workspace">
          
          <!-- Calculator Header Bar -->
          <div class="calc-top-bar">
            <button id="backToDirectoryBtn" class="btn-back" aria-label="Back to Directory">
              <span class="back-arrow">←</span>
              <span data-i18n="btnBack">Back to Calculators</span>
            </button>
            <div class="calc-top-actions">
              <button id="calcFavToggleBtn" class="btn-icon" aria-label="Toggle Favorite" title="Bookmark Calculator">
                <span class="fav-icon">☆</span>
              </button>
              <button id="copyShareBtn" class="btn-icon" aria-label="Copy Link" title="Copy Direct Link">
                <span>🔗</span>
              </button>
            </div>
          </div>

          <!-- Active Calculator Container -->
          <div class="calc-card-main" id="activeCalcContainer">
            <!-- Dynamically populated by JS: Inputs, Calculate / Clear buttons, Results, Steps, Formulas, Notes -->
          </div>

        </div>
      </section>

      <!-- View 3: Complete 63 Calculators Roadmap Modal / Drawer -->
      <div id="roadmapModal" class="modal-overlay" style="display:none;">
        <div class="modal-card">
          <div class="modal-header">
            <div class="modal-title-group">
              <h3 data-i18n="roadmapTitle">Textile Engineering 63 Calculator Suite</h3>
              <span class="badge-accent" data-i18n="roadmapSubtitle">Industry Architecture Standard</span>
            </div>
            <button id="closeRoadmapBtn" class="modal-close" aria-label="Close modal">✕</button>
          </div>
          <div class="modal-body" id="roadmapContent">
            <!-- Full 63 category list injected via JS -->
          </div>
        </div>
      </div>

    </div>
  </main>

  <!-- History Drawer (Slide-Over Panel) -->
  <aside id="historyDrawer" class="drawer" aria-hidden="true">
    <div class="drawer-header">
      <div class="drawer-title-group">
        <span class="drawer-icon">⏱️</span>
        <h3 data-i18n="historyTitle">Calculation History</h3>
        <span id="drawerHistoryBadge" class="badge-mini">0</span>
      </div>
      <div class="drawer-actions">
        <button id="clearAllHistoryBtn" class="btn-text-danger" data-i18n="btnClearHistory" title="Clear all history">Clear All</button>
        <button id="closeHistoryBtn" class="drawer-close" aria-label="Close history">✕</button>
      </div>
    </div>
    <div class="drawer-body" id="historyList">
      <!-- Injected via JavaScript -->
    </div>
  </aside>

  <!-- Drawer Backdrop Overlay -->
  <div id="drawerBackdrop" class="drawer-backdrop" style="display:none;"></div>

  <!-- Global Toast Notification Container -->
  <div id="toastContainer" class="toast-container" aria-live="polite"></div>

  <!-- Professional Textile Footer -->
  <footer class="site-footer">
    <div class="footer-container">
      <div class="footer-brand">
        <div class="footer-logo">
          <span class="highlight">TEXTILE AI</span> CALCULATOR
        </div>
        <p class="footer-tagline" data-i18n="footerTagline">
          Built for Textile Engineers, Students, Wet Processing Specialists, Apparel Merchandisers & Production Managers.
        </p>
      </div>
      <div class="footer-standards">
        <div class="standard-pill">ISO 3801 / ASTM D3776 (GSM)</div>
        <div class="standard-pill">AATCC 135 / ISO 6330 (Shrinkage)</div>
        <div class="standard-pill">Direct & Indirect Yarn Counts</div>
        <div class="standard-pill">Standard Liquor Ratios (M:L)</div>
      </div>
      <div class="footer-bottom">
        <div class="footer-copy">
          © 2026 Textile AI Calculator • Client-Side Deterministic Textile Mathematics
        </div>
        <div class="footer-privacy">
          <span data-i18n="offlineReady">100% Offline Capable & Private</span>
        </div>
      </div>
    </div>
  </footer>

  <script src="script.js"></script>
</body>
</html>
```

---

### 2. `style.css`

```css
/* ==========================================================================
   TEXTILE AI CALCULATOR - CORE STYLESHEET
   Mobile-First, Professional Textile Engineering Design
   ========================================================================== */

/* --------------------------------------------------------------------------
   1. CSS Custom Properties / Design Tokens
   -------------------------------------------------------------------------- */
:root {
  /* Color Palette - Dark Theme (Default) */
  --bg-primary: #0b0f19;
  --bg-secondary: #111827;
  --bg-card: #151e32;
  --bg-card-hover: #1c2742;
  --bg-card-active: #223052;
  --bg-input: #0e1626;
  --bg-glass: rgba(17, 24, 39, 0.85);

  --border-color: #1f2d47;
  --border-light: #28395a;
  --border-focus: #0ea5e9;

  --text-primary: #f8fafc;
  --text-secondary: #94a3b8;
  --text-muted: #64748b;
  --text-inverse: #0b0f19;

  --primary: #0ea5e9;
  --primary-glow: rgba(14, 165, 233, 0.25);
  --primary-hover: #38bdf8;
  --primary-dark: #0284c7;

  --accent: #06b6d4;
  --accent-glow: rgba(6, 182, 212, 0.2);

  --success: #10b981;
  --success-bg: rgba(16, 185, 129, 0.12);
  --success-border: #059669;

  --warning: #f59e0b;
  --warning-bg: rgba(245, 158, 11, 0.12);
  --warning-border: #d97706;

  --danger: #ef4444;
  --danger-bg: rgba(239, 68, 68, 0.12);
  --danger-border: #dc2626;

  --radius-sm: 6px;
  --radius-md: 10px;
  --radius-lg: 16px;
  --radius-xl: 22px;
  --radius-full: 9999px;

  --shadow-sm: 0 1px 2px 0 rgba(0, 0, 0, 0.25);
  --shadow-md: 0 4px 12px 0 rgba(0, 0, 0, 0.35);
  --shadow-lg: 0 10px 25px -3px rgba(0, 0, 0, 0.45);
  --shadow-glow: 0 0 20px rgba(14, 165, 233, 0.25);

  --font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Noto Sans Bengali', Oxygen, Ubuntu, Cantarell, sans-serif;
  --font-mono: 'SFMono-Regular', Consolas, 'Liberation Mono', Menlo, Courier, monospace;

  --transition-fast: 0.15s ease;
  --transition-normal: 0.25s ease;
  --transition-slow: 0.4s ease;

  --header-height: 64px;
}

/* Light Theme Overrides */
[data-theme="light"] {
  --bg-primary: #f8fafc;
  --bg-secondary: #f1f5f9;
  --bg-card: #ffffff;
  --bg-card-hover: #f1f5f9;
  --bg-card-active: #e2e8f0;
  --bg-input: #ffffff;
  --bg-glass: rgba(255, 255, 255, 0.88);

  --border-color: #e2e8f0;
  --border-light: #cbd5e1;
  --border-focus: #0284c7;

  --text-primary: #0f172a;
  --text-secondary: #475569;
  --text-muted: #64748b;
  --text-inverse: #f8fafc;

  --primary: #0284c7;
  --primary-glow: rgba(2, 132, 199, 0.2);
  --primary-hover: #0369a1;
  --primary-dark: #075985;

  --accent: #0891b2;
  --accent-glow: rgba(8, 145, 178, 0.15);

  --success: #059669;
  --success-bg: rgba(5, 150, 105, 0.1);
  --success-border: #10b981;

  --warning: #d97706;
  --warning-bg: rgba(217, 119, 6, 0.1);
  --warning-border: #f59e0b;

  --danger: #dc2626;
  --danger-bg: rgba(220, 38, 38, 0.1);
  --danger-border: #ef4444;

  --shadow-sm: 0 1px 3px rgba(15, 23, 42, 0.08);
  --shadow-md: 0 4px 14px rgba(15, 23, 42, 0.08);
  --shadow-lg: 0 10px 25px rgba(15, 23, 42, 0.1);
  --shadow-glow: 0 0 18px rgba(2, 132, 199, 0.15);
}

/* --------------------------------------------------------------------------
   2. Reset and Base Styles
   -------------------------------------------------------------------------- */
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html {
  font-size: 16px;
  scroll-behavior: smooth;
  -webkit-text-size-adjust: 100%;
}

body {
  font-family: var(--font-family);
  background-color: var(--bg-primary);
  color: var(--text-primary);
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  line-height: 1.5;
  overflow-x: hidden;
  transition: background-color var(--transition-normal), color var(--transition-normal);
}

button, input, select, textarea {
  font-family: inherit;
  font-size: 1rem;
  color: inherit;
}

button {
  cursor: pointer;
  border: none;
  background: none;
  touch-action: manipulation;
}

a {
  color: var(--primary);
  text-decoration: none;
}

/* --------------------------------------------------------------------------
   3. Navigation Bar
   -------------------------------------------------------------------------- */
.navbar {
  position: sticky;
  top: 0;
  z-index: 100;
  height: var(--header-height);
  background: var(--bg-glass);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border-bottom: 1px solid var(--border-color);
  transition: background-color var(--transition-normal), border-color var(--transition-normal);
}

.nav-container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 16px;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.brand-group {
  display: flex;
  align-items: center;
  gap: 10px;
  cursor: pointer;
  user-select: none;
}

.brand-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--primary);
  filter: drop-shadow(0 0 8px var(--primary-glow));
}

.brand-title {
  font-size: 1.15rem;
  font-weight: 800;
  letter-spacing: -0.02em;
  display: flex;
  align-items: center;
  gap: 6px;
}

.brand-title .highlight {
  color: var(--primary);
}

.badge-mini {
  font-size: 0.65rem;
  font-weight: 700;
  padding: 2px 6px;
  border-radius: var(--radius-sm);
  background: var(--primary-glow);
  color: var(--primary);
  border: 1px solid var(--primary);
  letter-spacing: 0.05em;
  text-transform: uppercase;
}

.brand-subtitle {
  font-size: 0.72rem;
  color: var(--text-muted);
  font-weight: 500;
  line-height: 1;
}

.nav-actions {
  display: flex;
  align-items: center;
  gap: 8px;
}

.nav-btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-height: 40px;
  padding: 6px 10px;
  border-radius: var(--radius-md);
  background: var(--bg-card);
  border: 1px solid var(--border-color);
  color: var(--text-primary);
  font-size: 0.88rem;
  font-weight: 600;
  transition: all var(--transition-fast);
  position: relative;
}

.nav-btn:hover {
  background: var(--bg-card-hover);
  border-color: var(--border-light);
  transform: translateY(-1px);
}

.nav-btn:active {
  transform: translateY(0);
}

.lang-btn {
  gap: 5px;
  padding: 6px 12px;
  border-color: var(--border-light);
}

.lang-globe {
  font-size: 1rem;
}

.lang-text {
  font-weight: 700;
  color: var(--primary);
}

.badge-count {
  position: absolute;
  top: -4px;
  right: -4px;
  min-width: 18px;
  height: 18px;
  border-radius: 9px;
  background: var(--primary);
  color: #ffffff;
  font-size: 0.68rem;
  font-weight: 700;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0 4px;
  box-shadow: var(--shadow-sm);
}

/* Theme icon toggling */
[data-theme="dark"] .sun-icon {
  display: block;
}
[data-theme="dark"] .moon-icon {
  display: none;
}
[data-theme="light"] .sun-icon {
  display: none;
}
[data-theme="light"] .moon-icon {
  display: block;
}

/* --------------------------------------------------------------------------
   4. Hero & Quick Search
   -------------------------------------------------------------------------- */
.main-content {
  flex: 1;
  max-width: 1280px;
  width: 100%;
  margin: 0 auto;
  padding: 16px;
}

.hero-section {
  padding: 20px 0 16px;
  text-align: center;
}

.hero-content {
  max-width: 760px;
  margin: 0 auto;
}

.hero-title {
  font-size: 1.85rem;
  font-weight: 800;
  letter-spacing: -0.03em;
  margin-bottom: 8px;
  background: linear-gradient(135deg, var(--text-primary) 30%, var(--primary) 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.hero-desc {
  font-size: 0.92rem;
  color: var(--text-secondary);
  margin-bottom: 18px;
  line-height: 1.5;
}

.search-wrapper {
  position: relative;
  width: 100%;
  max-width: 600px;
  margin: 0 auto;
}

.search-icon {
  position: absolute;
  left: 16px;
  top: 50%;
  transform: translateY(-50%);
  color: var(--text-muted);
  font-size: 1.1rem;
  pointer-events: none;
}

.search-input {
  width: 100%;
  height: 50px;
  padding: 0 44px 0 48px;
  border-radius: var(--radius-full);
  background: var(--bg-card);
  border: 2px solid var(--border-color);
  color: var(--text-primary);
  font-size: 0.96rem;
  transition: all var(--transition-fast);
  box-shadow: var(--shadow-sm);
}

.search-input:focus {
  outline: none;
  border-color: var(--primary);
  box-shadow: 0 0 0 4px var(--primary-glow);
}

.search-clear-btn {
  position: absolute;
  right: 14px;
  top: 50%;
  transform: translateY(-50%);
  width: 26px;
  height: 26px;
  border-radius: 50%;
  background: var(--bg-card-hover);
  color: var(--text-muted);
  font-size: 0.8rem;
  display: flex;
  align-items: center;
  justify-content: center;
}

.search-clear-btn:hover {
  background: var(--border-light);
  color: var(--text-primary);
}

/* --------------------------------------------------------------------------
   5. Category Navigation Bar (Pills)
   -------------------------------------------------------------------------- */
.category-nav-section {
  margin-bottom: 24px;
  position: relative;
}

.category-scroll {
  display: flex;
  gap: 8px;
  overflow-x: auto;
  padding: 6px 2px 10px;
  scrollbar-width: thin;
  scrollbar-color: var(--border-color) transparent;
  -webkit-overflow-scrolling: touch;
}

.category-scroll::-webkit-scrollbar {
  height: 4px;
}

.category-scroll::-webkit-scrollbar-thumb {
  background: var(--border-color);
  border-radius: 4px;
}

.cat-pill {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 8px 14px;
  border-radius: var(--radius-full);
  background: var(--bg-card);
  border: 1px solid var(--border-color);
  color: var(--text-secondary);
  font-size: 0.85rem;
  font-weight: 600;
  white-space: nowrap;
  transition: all var(--transition-fast);
  user-select: none;
}

.cat-pill:hover {
  background: var(--bg-card-hover);
  color: var(--text-primary);
  border-color: var(--border-light);
}

.cat-pill.active {
  background: var(--primary);
  color: #ffffff;
  border-color: var(--primary);
  box-shadow: 0 2px 8px var(--primary-glow);
}

.pill-count {
  font-size: 0.72rem;
  padding: 1px 6px;
  border-radius: var(--radius-full);
  background: rgba(0, 0, 0, 0.2);
  color: inherit;
  font-weight: 700;
}

[data-theme="light"] .cat-pill:not(.active) .pill-count {
  background: rgba(0, 0, 0, 0.08);
}

/* --------------------------------------------------------------------------
   6. Directory Header & Calculator Grid
   -------------------------------------------------------------------------- */
.directory-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 18px;
  flex-wrap: wrap;
  gap: 12px;
}

.directory-info {
  display: flex;
  align-items: center;
  gap: 10px;
}

.section-heading {
  font-size: 1.25rem;
  font-weight: 700;
  color: var(--text-primary);
}

.results-badge {
  font-size: 0.78rem;
  font-weight: 600;
  padding: 3px 10px;
  border-radius: var(--radius-full);
  background: var(--bg-card-active);
  color: var(--primary);
  border: 1px solid var(--border-color);
}

.btn-secondary-sm {
  font-size: 0.82rem;
  font-weight: 600;
  padding: 6px 12px;
  border-radius: var(--radius-md);
  background: var(--bg-card);
  border: 1px solid var(--border-color);
  color: var(--text-secondary);
  transition: all var(--transition-fast);
}

.btn-secondary-sm:hover {
  background: var(--bg-card-hover);
  color: var(--text-primary);
  border-color: var(--border-light);
}

/* Calculators Cards Grid */
.calculators-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 16px;
}

@media (min-width: 640px) {
  .calculators-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1024px) {
  .calculators-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

/* Calculator Card */
.calc-card {
  background: var(--bg-card);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-lg);
  padding: 20px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  transition: transform var(--transition-fast), border-color var(--transition-fast), box-shadow var(--transition-fast);
  position: relative;
  overflow: hidden;
}

.calc-card:hover {
  transform: translateY(-3px);
  border-color: var(--border-light);
  box-shadow: var(--shadow-md);
}

.calc-card-top {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  margin-bottom: 12px;
}

.card-cat-badge {
  font-size: 0.72rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  padding: 3px 8px;
  border-radius: var(--radius-sm);
  background: var(--bg-input);
  color: var(--primary);
  border: 1px solid var(--border-color);
}

.card-fav-btn {
  font-size: 1.25rem;
  color: var(--text-muted);
  transition: color var(--transition-fast), transform var(--transition-fast);
  padding: 2px 6px;
}

.card-fav-btn:hover {
  color: var(--warning);
  transform: scale(1.15);
}

.card-fav-btn.active {
  color: var(--warning);
}

.calc-card-body {
  margin-bottom: 18px;
}

.calc-card-title {
  font-size: 1.12rem;
  font-weight: 700;
  margin-bottom: 6px;
  color: var(--text-primary);
  display: flex;
  align-items: center;
  gap: 8px;
}

.card-title-icon {
  font-size: 1.25rem;
}

.calc-card-desc {
  font-size: 0.86rem;
  color: var(--text-secondary);
  line-height: 1.45;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.calc-card-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-top: 1px solid var(--border-color);
  padding-top: 14px;
}

.card-tags {
  display: flex;
  gap: 6px;
  flex-wrap: wrap;
}

.tag-mini {
  font-size: 0.7rem;
  color: var(--text-muted);
  background: var(--bg-input);
  padding: 2px 6px;
  border-radius: 4px;
}

.btn-card-launch {
  font-size: 0.85rem;
  font-weight: 700;
  color: var(--primary);
  display: inline-flex;
  align-items: center;
  gap: 4px;
  transition: gap var(--transition-fast);
}

.calc-card:hover .btn-card-launch {
  gap: 8px;
  color: var(--primary-hover);
}

/* Empty State */
.empty-state {
  text-align: center;
  padding: 60px 20px;
  background: var(--bg-card);
  border-radius: var(--radius-lg);
  border: 1px dashed var(--border-color);
  margin-top: 20px;
}

.empty-icon {
  font-size: 3rem;
  margin-bottom: 12px;
  opacity: 0.7;
}

.empty-state h3 {
  font-size: 1.25rem;
  font-weight: 700;
  margin-bottom: 8px;
}

.empty-state p {
  color: var(--text-secondary);
  font-size: 0.9rem;
  max-width: 480px;
  margin: 0 auto 20px;
}

/* --------------------------------------------------------------------------
   7. Dedicated Calculator Workspace
   -------------------------------------------------------------------------- */
.calc-workspace {
  max-width: 880px;
  margin: 0 auto;
}

.calc-top-bar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 16px;
}

.btn-back {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  font-size: 0.9rem;
  font-weight: 600;
  color: var(--text-secondary);
  padding: 8px 14px;
  border-radius: var(--radius-md);
  background: var(--bg-card);
  border: 1px solid var(--border-color);
  transition: all var(--transition-fast);
}

.btn-back:hover {
  background: var(--bg-card-hover);
  color: var(--text-primary);
  border-color: var(--border-light);
}

.calc-top-actions {
  display: flex;
  align-items: center;
  gap: 8px;
}

.btn-icon {
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: var(--radius-md);
  background: var(--bg-card);
  border: 1px solid var(--border-color);
  color: var(--text-secondary);
  font-size: 1.1rem;
  transition: all var(--transition-fast);
}

.btn-icon:hover {
  background: var(--bg-card-hover);
  color: var(--text-primary);
  border-color: var(--border-light);
}

.btn-icon.active .fav-icon {
  color: var(--warning);
}

/* Main Calculator Card */
.calc-card-main {
  background: var(--bg-card);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-xl);
  padding: 24px;
  box-shadow: var(--shadow-md);
}

@media (min-width: 640px) {
  .calc-card-main {
    padding: 32px;
  }
}

.calc-header-block {
  margin-bottom: 24px;
  border-bottom: 1px solid var(--border-color);
  padding-bottom: 20px;
}

.calc-header-meta {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 8px;
}

.calc-title-main {
  font-size: 1.6rem;
  font-weight: 800;
  letter-spacing: -0.02em;
  display: flex;
  align-items: center;
  gap: 10px;
  color: var(--text-primary);
}

.calc-desc-main {
  color: var(--text-secondary);
  font-size: 0.94rem;
  margin-top: 6px;
  line-height: 1.55;
}

/* Form Fields */
.calc-form {
  margin-bottom: 24px;
}

.form-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 18px;
}

@media (min-width: 640px) {
  .form-grid.cols-2 {
    grid-template-columns: repeat(2, 1fr);
  }
  .form-grid.cols-3 {
    grid-template-columns: repeat(3, 1fr);
  }
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.form-label {
  font-size: 0.88rem;
  font-weight: 600;
  color: var(--text-primary);
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.field-required {
  color: var(--danger);
  margin-left: 3px;
}

.input-unit-group {
  display: flex;
  align-items: stretch;
  background: var(--bg-input);
  border: 1.5px solid var(--border-color);
  border-radius: var(--radius-md);
  overflow: hidden;
  transition: border-color var(--transition-fast), box-shadow var(--transition-fast);
}

.input-unit-group:focus-within {
  border-color: var(--primary);
  box-shadow: 0 0 0 3px var(--primary-glow);
}

.form-input {
  flex: 1;
  min-width: 0;
  height: 48px;
  padding: 0 14px;
  background: transparent;
  border: none;
  color: var(--text-primary);
  font-size: 1.05rem;
  font-weight: 600;
  font-variant-numeric: tabular-nums;
}

.form-input:focus {
  outline: none;
}

.form-input::placeholder {
  color: var(--text-muted);
  font-weight: 400;
  font-size: 0.92rem;
}

.unit-select {
  background: var(--bg-card-hover);
  border: none;
  border-left: 1px solid var(--border-color);
  color: var(--text-primary);
  font-size: 0.88rem;
  font-weight: 600;
  padding: 0 12px;
  cursor: pointer;
}

.unit-select:focus {
  outline: none;
}

.unit-addon {
  background: var(--bg-card-hover);
  border-left: 1px solid var(--border-color);
  color: var(--text-secondary);
  font-size: 0.86rem;
  font-weight: 600;
  display: flex;
  align-items: center;
  padding: 0 14px;
  user-select: none;
}

.field-helper {
  font-size: 0.76rem;
  color: var(--text-muted);
  line-height: 1.3;
}

.field-error-msg {
  font-size: 0.78rem;
  color: var(--danger);
  font-weight: 600;
  margin-top: 2px;
  display: none;
}

.form-group.has-error .input-unit-group {
  border-color: var(--danger);
}

.form-group.has-error .field-error-msg {
  display: block;
}

/* Action Buttons */
.form-actions {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-top: 24px;
  flex-wrap: wrap;
}

.btn {
  min-height: 48px;
  padding: 0 20px;
  border-radius: var(--radius-md);
  font-size: 0.94rem;
  font-weight: 700;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  transition: all var(--transition-fast);
  user-select: none;
}

.btn-primary {
  background: linear-gradient(135deg, var(--primary) 0%, var(--primary-dark) 100%);
  color: #ffffff;
  border: none;
  box-shadow: 0 4px 12px var(--primary-glow);
  flex: 1;
}

.btn-primary:hover {
  background: linear-gradient(135deg, var(--primary-hover) 0%, var(--primary) 100%);
  transform: translateY(-1px);
  box-shadow: 0 6px 16px var(--primary-glow);
}

.btn-primary:active {
  transform: translateY(0);
}

.btn-secondary {
  background: var(--bg-input);
  border: 1px solid var(--border-color);
  color: var(--text-secondary);
}

.btn-secondary:hover {
  background: var(--bg-card-hover);
  color: var(--text-primary);
  border-color: var(--border-light);
}

.btn-example {
  background: var(--bg-card-hover);
  border: 1px solid var(--primary);
  color: var(--primary);
}

.btn-example:hover {
  background: var(--primary-glow);
  color: var(--primary-hover);
}

/* Error Banner */
.calc-error-banner {
  background: var(--danger-bg);
  border: 1px solid var(--danger-border);
  color: #fca5a5;
  border-radius: var(--radius-md);
  padding: 14px 18px;
  margin-bottom: 20px;
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 0.92rem;
  font-weight: 600;
}

[data-theme="light"] .calc-error-banner {
  color: var(--danger);
}

/* Results Display Card */
.results-section {
  margin-top: 30px;
  animation: fadeIn 0.3s ease;
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(10px); }
  to { opacity: 1; transform: translateY(0); }
}

.result-hero-box {
  background: linear-gradient(145deg, var(--bg-card-active) 0%, var(--bg-card) 100%);
  border: 2px solid var(--border-light);
  border-radius: var(--radius-lg);
  padding: 24px;
  text-align: center;
  position: relative;
  box-shadow: var(--shadow-md);
  margin-bottom: 20px;
}

.result-hero-label {
  font-size: 0.84rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: var(--text-secondary);
  margin-bottom: 6px;
}

.result-hero-value-wrap {
  display: flex;
  align-items: baseline;
  justify-content: center;
  gap: 8px;
  flex-wrap: wrap;
}

.result-hero-value {
  font-size: 2.8rem;
  font-weight: 900;
  letter-spacing: -0.03em;
  color: var(--primary);
  font-variant-numeric: tabular-nums;
  line-height: 1.1;
}

.result-hero-unit {
  font-size: 1.3rem;
  font-weight: 700;
  color: var(--text-secondary);
}

.result-hero-status {
  margin-top: 10px;
  display: inline-block;
  font-size: 0.82rem;
  font-weight: 700;
  padding: 4px 12px;
  border-radius: var(--radius-full);
}

.status-excellent {
  background: var(--success-bg);
  color: var(--success);
  border: 1px solid var(--success-border);
}

.status-warning {
  background: var(--warning-bg);
  color: var(--warning);
  border: 1px solid var(--warning-border);
}

.status-danger {
  background: var(--danger-bg);
  color: var(--danger);
  border: 1px solid var(--danger-border);
}

.result-actions {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-top: 14px;
}

.btn-result-action {
  font-size: 0.84rem;
  font-weight: 600;
  padding: 6px 14px;
  border-radius: var(--radius-md);
  background: var(--bg-card);
  border: 1px solid var(--border-color);
  color: var(--text-secondary);
  display: inline-flex;
  align-items: center;
  gap: 6px;
  transition: all var(--transition-fast);
}

.btn-result-action:hover {
  background: var(--bg-card-hover);
  color: var(--text-primary);
  border-color: var(--border-light);
}

/* Secondary Metrics Grid */
.secondary-metrics-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(170px, 1fr));
  gap: 12px;
  margin-bottom: 24px;
}

.metric-card {
  background: var(--bg-card-hover);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-md);
  padding: 12px 16px;
  display: flex;
  flex-direction: column;
}

.metric-label {
  font-size: 0.76rem;
  color: var(--text-muted);
  font-weight: 600;
  text-transform: uppercase;
}

.metric-value {
  font-size: 1.25rem;
  font-weight: 800;
  color: var(--text-primary);
  margin-top: 4px;
  font-variant-numeric: tabular-nums;
}

/* Warning & Disclaimer Banners */
.factory-warning-box {
  background: var(--warning-bg);
  border: 1.5px solid var(--warning-border);
  border-radius: var(--radius-lg);
  padding: 16px 20px;
  margin-bottom: 24px;
  display: flex;
  gap: 14px;
  align-items: flex-start;
}

.warning-icon {
  font-size: 1.4rem;
  line-height: 1;
  color: var(--warning);
}

.warning-content h4 {
  font-size: 0.92rem;
  font-weight: 800;
  color: var(--warning);
  margin-bottom: 4px;
}

.warning-content p {
  font-size: 0.86rem;
  color: var(--text-primary);
  line-height: 1.45;
}

/* Technical Details Cards */
.tech-details-container {
  display: flex;
  flex-direction: column;
  gap: 18px;
}

.detail-card {
  background: var(--bg-input);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-lg);
  padding: 18px 22px;
}

.detail-header {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 12px;
}

.detail-title {
  font-size: 0.96rem;
  font-weight: 700;
  color: var(--text-primary);
}

/* Formula Box */
.formula-display {
  background: var(--bg-card);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-md);
  padding: 14px 18px;
  font-family: var(--font-mono);
  font-size: 0.92rem;
  color: var(--primary-hover);
  overflow-x: auto;
  line-height: 1.6;
}

/* Steps List */
.steps-list {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.step-item {
  display: flex;
  gap: 12px;
  align-items: flex-start;
}

.step-number {
  min-width: 24px;
  height: 24px;
  border-radius: 50%;
  background: var(--primary-glow);
  border: 1px solid var(--primary);
  color: var(--primary);
  font-size: 0.75rem;
  font-weight: 800;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  margin-top: 2px;
}

.step-content {
  flex: 1;
}

.step-heading {
  font-size: 0.88rem;
  font-weight: 700;
  color: var(--text-primary);
  margin-bottom: 2px;
}

.step-calc {
  font-size: 0.84rem;
  font-family: var(--font-mono);
  color: var(--text-secondary);
  background: var(--bg-card);
  padding: 4px 8px;
  border-radius: 4px;
  display: inline-block;
  margin-top: 4px;
}

/* Bilingual Explanations Tabs */
.explanation-box {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.lang-tab-pill {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-size: 0.82rem;
  font-weight: 700;
  color: var(--primary);
  text-transform: uppercase;
  letter-spacing: 0.05em;
  margin-bottom: 4px;
}

.explanation-text {
  font-size: 0.88rem;
  color: var(--text-secondary);
  line-height: 1.6;
}

.explanation-divider {
  height: 1px;
  background: var(--border-color);
  margin: 8px 0;
}

/* --------------------------------------------------------------------------
   8. History Drawer (Slide-Over)
   -------------------------------------------------------------------------- */
.drawer {
  position: fixed;
  top: 0;
  right: -420px;
  width: 100%;
  max-width: 400px;
  height: 100vh;
  background: var(--bg-card);
  border-left: 1px solid var(--border-color);
  box-shadow: var(--shadow-lg);
  z-index: 200;
  display: flex;
  flex-direction: column;
  transition: transform var(--transition-normal);
}

.drawer.open {
  transform: translateX(-420px);
}

@media (max-width: 480px) {
  .drawer {
    max-width: 100%;
    right: -100%;
  }
  .drawer.open {
    transform: translateX(-100%);
  }
}

.drawer-header {
  padding: 18px 20px;
  border-bottom: 1px solid var(--border-color);
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.drawer-title-group {
  display: flex;
  align-items: center;
  gap: 8px;
}

.drawer-title-group h3 {
  font-size: 1.1rem;
  font-weight: 700;
}

.drawer-actions {
  display: flex;
  align-items: center;
  gap: 12px;
}

.btn-text-danger {
  font-size: 0.8rem;
  font-weight: 700;
  color: var(--danger);
  padding: 4px 8px;
}

.btn-text-danger:hover {
  text-decoration: underline;
}

.drawer-close {
  font-size: 1.25rem;
  color: var(--text-muted);
  width: 32px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  background: var(--bg-card-hover);
}

.drawer-close:hover {
  color: var(--text-primary);
}

.drawer-body {
  flex: 1;
  overflow-y: auto;
  padding: 16px;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.history-card {
  background: var(--bg-input);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-md);
  padding: 14px;
  transition: all var(--transition-fast);
}

.history-card:hover {
  border-color: var(--border-light);
}

.history-card-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 8px;
}

.history-calc-title {
  font-size: 0.92rem;
  font-weight: 700;
  color: var(--text-primary);
}

.history-time {
  font-size: 0.72rem;
  color: var(--text-muted);
}

.history-summary {
  font-size: 0.82rem;
  color: var(--text-secondary);
  margin-bottom: 8px;
  line-height: 1.4;
}

.history-result-badge {
  font-size: 0.95rem;
  font-weight: 800;
  color: var(--primary);
  font-variant-numeric: tabular-nums;
  margin-bottom: 10px;
}

.history-card-actions {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  gap: 8px;
  border-top: 1px solid var(--border-color);
  padding-top: 8px;
}

.btn-hist-load {
  font-size: 0.78rem;
  font-weight: 700;
  color: var(--primary);
  padding: 4px 8px;
  border-radius: 4px;
  background: var(--bg-card-hover);
}

.btn-hist-del {
  font-size: 0.78rem;
  color: var(--danger);
  padding: 4px 8px;
}

.drawer-backdrop {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.6);
  backdrop-filter: blur(4px);
  z-index: 150;
  animation: fadeIn 0.2s ease;
}

/* --------------------------------------------------------------------------
   9. Full 63 Suite Roadmap Modal
   -------------------------------------------------------------------------- */
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.75);
  backdrop-filter: blur(5px);
  z-index: 210;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
  animation: fadeIn 0.2s ease;
}

.modal-card {
  background: var(--bg-card);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-xl);
  width: 100%;
  max-width: 900px;
  max-height: 90vh;
  display: flex;
  flex-direction: column;
  box-shadow: var(--shadow-lg);
  overflow: hidden;
}

.modal-header {
  padding: 20px 24px;
  border-bottom: 1px solid var(--border-color);
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.modal-title-group h3 {
  font-size: 1.25rem;
  font-weight: 800;
}

.badge-accent {
  font-size: 0.74rem;
  font-weight: 700;
  color: var(--accent);
}

.modal-close {
  font-size: 1.3rem;
  width: 36px;
  height: 36px;
  border-radius: 50%;
  background: var(--bg-card-hover);
  color: var(--text-muted);
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal-close:hover {
  color: var(--text-primary);
}

.modal-body {
  flex: 1;
  overflow-y: auto;
  padding: 24px;
}

.roadmap-cat-section {
  margin-bottom: 24px;
}

.roadmap-cat-title {
  font-size: 1.05rem;
  font-weight: 800;
  color: var(--primary);
  margin-bottom: 12px;
  display: flex;
  align-items: center;
  gap: 8px;
}

.roadmap-items-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
  gap: 10px;
}

.roadmap-item {
  padding: 10px 14px;
  background: var(--bg-input);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-md);
  font-size: 0.85rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.roadmap-item.active-item {
  border-color: var(--primary);
  background: var(--bg-card-hover);
  cursor: pointer;
}

.roadmap-item.active-item:hover {
  border-color: var(--primary-hover);
}

.roadmap-status-badge {
  font-size: 0.68rem;
  font-weight: 700;
  padding: 2px 6px;
  border-radius: var(--radius-full);
}

.status-live {
  background: var(--success-bg);
  color: var(--success);
  border: 1px solid var(--success-border);
}

.status-ready {
  background: var(--bg-card-active);
  color: var(--text-muted);
}

/* --------------------------------------------------------------------------
   10. Toast Notification
   -------------------------------------------------------------------------- */
.toast-container {
  position: fixed;
  bottom: 24px;
  right: 24px;
  z-index: 300;
  display: flex;
  flex-direction: column;
  gap: 8px;
  pointer-events: none;
}

@media (max-width: 640px) {
  .toast-container {
    left: 20px;
    right: 20px;
    bottom: 20px;
  }
}

.toast {
  background: var(--bg-card);
  border: 1px solid var(--border-light);
  color: var(--text-primary);
  padding: 12px 18px;
  border-radius: var(--radius-md);
  font-size: 0.9rem;
  font-weight: 600;
  box-shadow: var(--shadow-lg);
  display: flex;
  align-items: center;
  gap: 10px;
  pointer-events: auto;
  animation: slideToast 0.25s ease forwards;
}

@keyframes slideToast {
  from { opacity: 0; transform: translateY(16px); }
  to { opacity: 1; transform: translateY(0); }
}

.toast.toast-success {
  border-color: var(--success);
}

.toast.toast-error {
  border-color: var(--danger);
}

/* --------------------------------------------------------------------------
   11. Footer
   -------------------------------------------------------------------------- */
.site-footer {
  margin-top: 40px;
  border-top: 1px solid var(--border-color);
  background: var(--bg-secondary);
  padding: 36px 16px 24px;
}

.footer-container {
  max-width: 1280px;
  margin: 0 auto;
}

.footer-brand {
  margin-bottom: 20px;
}

.footer-logo {
  font-size: 1.15rem;
  font-weight: 800;
  letter-spacing: -0.02em;
}

.footer-logo .highlight {
  color: var(--primary);
}

.footer-tagline {
  font-size: 0.86rem;
  color: var(--text-muted);
  max-width: 600px;
  margin-top: 6px;
}

.footer-standards {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
  margin-bottom: 24px;
}

.standard-pill {
  font-size: 0.74rem;
  font-weight: 600;
  color: var(--text-secondary);
  background: var(--bg-card);
  border: 1px solid var(--border-color);
  padding: 4px 10px;
  border-radius: var(--radius-full);
}

.footer-bottom {
  border-top: 1px solid var(--border-color);
  padding-top: 16px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 12px;
  font-size: 0.8rem;
  color: var(--text-muted);
}

/* --------------------------------------------------------------------------
   12. Print Optimization
   -------------------------------------------------------------------------- */
@media print {
  body {
    background: #ffffff !important;
    color: #000000 !important;
  }
  .navbar, .hero-section, .category-nav-section, .form-actions, .calc-top-bar, .site-footer, .drawer, .modal-overlay {
    display: none !important;
  }
  .calc-card-main {
    border: none !important;
    box-shadow: none !important;
    padding: 0 !important;
  }
  .result-hero-box {
    border: 2px solid #000 !important;
    background: none !important;
  }
  .result-hero-value {
    color: #000000 !important;
  }
}
```

---

### 3. `script.js`

```javascript
/**
 * ==============================================================================
 * TEXTILE AI CALCULATOR - CORE APPLICATION SCRIPT
 * Full-Stack Client-Side Textile Engineering Calculator
 * ==============================================================================
 */

'use strict';

// ------------------------------------------------------------------------------
// 1. INTERNATIONALIZATION & LOCALIZATION DICTIONARY (English & বাংলা)
// ------------------------------------------------------------------------------
const I18N = {
  en: {
    appTitle: "Textile AI Calculator",
    tagline: "Engineering & Apparel Suite",
    heroTitle: "Textile AI Calculator",
    heroDesc: "Professional deterministic calculations for fabric engineering, yarn counts, dyeing chemistry, finishing, machine production, efficiency, and apparel merchandising.",
    searchPlaceholder: "Search calculators (e.g. GSM, Stenter, Dyeing, Yarn, Shrinkage)...",
    catAll: "All",
    catFabric: "Fabric",
    catYarn: "Yarn",
    catDyeing: "Dyeing",
    catFinishing: "Finishing",
    catProduction: "Production",
    catQuality: "Quality",
    catGarment: "Garments",
    catFavorites: "Favorites",
    featuredCalculators: "Calculators Directory",
    availableBadge: "active calculators",
    btnFullSuite: "📋 Complete 63 Calculator Index",
    roadmapTitle: "Textile Engineering 63 Calculator Suite",
    roadmapSubtitle: "Standard Textile & Apparel Industry Architecture",
    btnBack: "Back to Calculators",
    calculateBtn: "Calculate",
    clearBtn: "Clear",
    useExampleBtn: "Fill Sample Values",
    copyResultBtn: "Copy Result",
    copiedToast: "Result copied to clipboard!",
    historyTitle: "Calculation History",
    historyEmpty: "No calculations in history yet.",
    btnClearHistory: "Clear All",
    btnLoadHist: "Reload",
    btnDelHist: "Delete",
    historySavedToast: "Calculation saved to history",
    historyClearedToast: "History cleared successfully",
    formulaHeading: "Formula Used",
    stepsHeading: "Step-by-Step Calculation",
    technicalNotes: "Engineering Notes & Assumptions",
    explanationEn: "English Explanation",
    explanationBn: "বাংলা ব্যাখ্যা (Bengali Explanation)",
    noResultsTitle: "No Calculators Found",
    noResultsDesc: "Try searching for keywords like GSM, Stenter, Dyeing, Yarn, Shrinkage, or reset your search.",
    btnResetSearch: "Reset Search",
    offlineReady: "100% Offline Capable & Private",
    footerTagline: "Built for Textile Engineers, Students, Wet Processing Specialists, Apparel Merchandisers & Production Managers.",
    errors: {
      required: "Please enter a value.",
      positive: "Please enter a valid positive value.",
      nonZero: "Division by zero is not allowed.",
      invalid: "Please provide valid numeric inputs."
    },
    stenterWarning: "Actual factory settings may vary depending on machine, fabric construction, process and factory standard.",
    liquorRatioWarning: "Actual liquor requirement depends on machine type (soft-flow, winch, package), pump circulation, and piping dead volume.",
    productionWarning: "Calculation assumes continuous processing. For weaving looms or circular knitting, production depends on picks/min or machine RPM and number of feeders."
  },
  bn: {
    appTitle: "টেক্সটাইল এআই ক্যালকুলেটর",
    tagline: "ইঞ্জিনিয়ারিং ও অ্যাপারেল স্যুট",
    heroTitle: "টেক্সটাইল এআই ক্যালকুলেটর",
    heroDesc: "টেক্সটাইল ইঞ্জিনিয়ার, শিক্ষার্থী, ডাইং, ফিনিশিং, উৎপাদন, কোয়ালিটি এবং গার্মেন্টস পেশাদারদের জন্য নির্ভুল ও প্রমাণসিদ্ধ গাণিতিক হিসাব।",
    searchPlaceholder: "ক্যালকুলেটর খুঁজুন (যেমন: জিএসএম, স্টেনটার, ডাইং, সুতা, সংকোচন)...",
    catAll: "সবগুলো",
    catFabric: "ফেব্রিক",
    catYarn: "সুতা",
    catDyeing: "ডাইং",
    catFinishing: "ফিনিশিং",
    catProduction: "উৎপাদন",
    catQuality: "কোয়ালিটি",
    catGarment: "গার্মেন্টস",
    catFavorites: "প্রিয়",
    featuredCalculators: "ক্যালকুলেটর ডিরেক্টরি",
    availableBadge: "টি সক্রিয় ক্যালকুলেটর",
    btnFullSuite: "📋 সম্পূর্ণ ৬৩টি ক্যালকুলেটরের সূচি",
    roadmapTitle: "টেক্সটাইল ইঞ্জিনিয়ারিং ৬৩টি ক্যালকুলেটরের সম্পূর্ণ রূপরেখা",
    roadmapSubtitle: "আন্তর্জাতিক টেক্সটাইল ও পোশাক শিল্প মানদণ্ড",
    btnBack: "ক্যালকুলেটর তালিকায় ফিরুন",
    calculateBtn: "হিসাব করুন",
    clearBtn: "মুছে ফেলুন",
    useExampleBtn: "নমুনা মান দিন",
    copyResultBtn: "ফলাফল কপি করুন",
    copiedToast: "ফলাফল ক্লিপবোর্ডে কপি করা হয়েছে!",
    historyTitle: "হিসাবের ইতিহাস",
    historyEmpty: "এখনও কোনো হিসাবের ইতিহাস সংরক্ষিত নেই।",
    btnClearHistory: "সব মুছুন",
    btnLoadHist: "পুনরায় লোড",
    btnDelHist: "মুছুন",
    historySavedToast: "হিসাব ইতিহাসে সংরক্ষিত হয়েছে",
    historyClearedToast: "ইতিহাস সফলভাবে মুছে ফেলা হয়েছে",
    formulaHeading: "ব্যবহৃত সূত্র",
    stepsHeading: "ধাপে ধাপে হিসাব বিবরণী",
    technicalNotes: "ইঞ্জিনিয়ারিং নোট ও বিবেচ্য বিষয়",
    explanationEn: "English Explanation (ইংরেজি ব্যাখ্যা)",
    explanationBn: "বাংলা ব্যাখ্যা",
    noResultsTitle: "কোনো ক্যালকুলেটর পাওয়া যায়নি",
    noResultsDesc: "জিএসএম, স্টেনটার, ডাইং, সুতা, বা সংকোচন লিখে খুঁজুন অথবা সার্চ রিসেট করুন।",
    btnResetSearch: "সার্চ রিসেট করুন",
    offlineReady: "১০০% অফলাইনে সক্ষম এবং সম্পূর্ণ নিরাপদ",
    footerTagline: "টেক্সটাইল ইঞ্জিনিয়ার, শিক্ষার্থী, ওয়েট প্রসেসিং বিশেষজ্ঞ, মার্চেন্ডাইজার ও প্রোডাকশন অফিসারদের জন্য তৈরি।",
    errors: {
      required: "অনুগ্রহ করে একটি মান লিখুন।",
      positive: "অনুগ্রহ করে একটি বৈধ ধনাত্মক মান দিন।",
      nonZero: "শূন্য দিয়ে ভাগ করা অনুমোদিত নয়।",
      invalid: "অনুগ্রহ করে সঠিক সংখ্যাসূচক মান প্রবেশ করান।"
    },
    stenterWarning: "মেশিন, কাপড়ের বুনন/কনস্ট্রাকশন, প্রক্রিয়া এবং কারখানার মানদণ্ডের উপর ভিত্তি করে বাস্তব সেটিংস পরিবর্তিত হতে পারে।",
    liquorRatioWarning: "প্রকৃত লিকারের প্রয়োজনীয়তা মেশিনের ধরন (সফট-ফ্লো, উইঞ্চ, প্যাকেজ), পাম্পের সঞ্চালন এবং পাইপের ডেড ভলিউমের ওপর নির্ভর করে।",
    productionWarning: "এই গণনাটি কন্টিনিউয়াস প্রসেসিং ধরে করা হয়েছে। উইভিং বা সার্কুলার নিটিংয়ের ক্ষেত্রে উৎপাদন নির্ভর করে পিক্স/মিনিট বা মেশিন আরপিএম এবং ফিডারের সংখ্যার ওপর।"
  }
};

// ------------------------------------------------------------------------------
// 2. CORE CALCULATORS SPECIFICATION & IMPLEMENTATIONS
// ------------------------------------------------------------------------------
const CALCULATORS = [
  // --------------------------------------------------------------------------
  // 1. GSM CALCULATOR
  // --------------------------------------------------------------------------
  {
    id: "gsm",
    category: "fabric",
    icon: "⚖️",
    title: {
      en: "GSM Calculator",
      bn: "জিএসএম (GSM) ক্যালকুলেটর"
    },
    description: {
      en: "Calculate fabric Grams per Square Meter (GSM) and ounces per square yard (oz/yd²) from sample dimensions and weight.",
      bn: "নমুনার দৈর্ঘ্য, প্রস্থ এবং ওজন (গ্রাম) থেকে প্রতি বর্গমিটারে কাপড়ের ওজন (জিএসএম) ও oz/yd² হিসাব করুন।"
    },
    tags: ["gsm", "gram", "weight", "fabric", "area", "swatch", "oz/yd2", "জিএসএম", "ফেব্রিক", "ওজন"],
    inputs: [
      {
        id: "weight",
        label: { en: "Sample Weight", bn: "নমুনার ওজন" },
        type: "number",
        default: "1.85",
        min: 0.0001,
        step: "0.01",
        unitOptions: [
          { value: "g", label: "Grams (g)" },
          { value: "mg", label: "Milligrams (mg)" }
        ],
        defaultUnit: "g",
        helper: { en: "Weight measured on a precision balance", bn: "প্রিসিশন ব্যালেন্স দিয়ে মাপা ওজন" }
      },
      {
        id: "length",
        label: { en: "Sample Length", bn: "নমুনার দৈর্ঘ্য" },
        type: "number",
        default: "10",
        min: 0.001,
        step: "0.1",
        unitOptions: [
          { value: "cm", label: "Centimeters (cm)" },
          { value: "mm", label: "Millimeters (mm)" },
          { value: "inch", label: "Inches (in)" },
          { value: "m", label: "Meters (m)" }
        ],
        defaultUnit: "cm",
        helper: { en: "Standard GSM round cutter diameter is 11.28 cm (100 cm²)", bn: "জিএসএম রাউন্ড কাটারের সাধারণ ক্ষেত্রফল ১০০ বর্গসেমি" }
      },
      {
        id: "width",
        label: { en: "Sample Width", bn: "নমুনার প্রস্থ" },
        type: "number",
        default: "10",
        min: 0.001,
        step: "0.1",
        unitOptions: [
          { value: "cm", label: "Centimeters (cm)" },
          { value: "mm", label: "Millimeters (mm)" },
          { value: "inch", label: "Inches (in)" },
          { value: "m", label: "Meters (m)" }
        ],
        defaultUnit: "cm",
        helper: { en: "Width of swatch (use same as length for square swatches)", bn: "নমুনার প্রস্থ (বর্গাকার নমুনার জন্য দৈর্ঘ্যের সমান)" }
      }
    ],
    example: {
      weight: "1.80",
      weight_unit: "g",
      length: "10",
      length_unit: "cm",
      width: "10",
      width_unit: "cm"
    },
    calculate: function (inputs, lang) {
      const wRaw = parseFloat(inputs.weight);
      const lRaw = parseFloat(inputs.length);
      const wdRaw = parseFloat(inputs.width);

      if (isNaN(wRaw) || isNaN(lRaw) || isNaN(wdRaw)) {
        return { error: I18N[lang].errors.required };
      }
      if (wRaw <= 0 || lRaw <= 0 || wdRaw <= 0) {
        return { error: I18N[lang].errors.positive };
      }

      // Convert weight to grams
      const wGrams = inputs.weight_unit === "mg" ? wRaw / 1000 : wRaw;

      // Convert length to meters
      let lMeters = lRaw;
      if (inputs.length_unit === "cm") lMeters = lRaw / 100;
      else if (inputs.length_unit === "mm") lMeters = lRaw / 1000;
      else if (inputs.length_unit === "inch") lMeters = lRaw * 0.0254;

      // Convert width to meters
      let wdMeters = wdRaw;
      if (inputs.width_unit === "cm") wdMeters = wdRaw / 100;
      else if (inputs.width_unit === "mm") wdMeters = wdRaw / 1000;
      else if (inputs.width_unit === "inch") wdMeters = wdRaw * 0.0254;

      const areaSqM = lMeters * wdMeters;
      if (areaSqM <= 0) {
        return { error: I18N[lang].errors.nonZero };
      }

      const gsm = wGrams / areaSqM;
      const ozSqYd = gsm / 33.906; // Standard ASTM conversion: 1 oz/yd² = 33.906 g/m²

      return {
        primary: {
          label: lang === "bn" ? "গণনাকৃত জিএসএম" : "Calculated GSM",
          value: gsm.toFixed(2),
          unit: "g/m²"
        },
        secondary: [
          {
            label: lang === "bn" ? "ওজন (oz/yd²)" : "Weight (oz/yd²)",
            value: ozSqYd.toFixed(2),
            unit: "oz/yd²"
          },
          {
            label: lang === "bn" ? "নমুনার ক্ষেত্রফল" : "Sample Area",
            value: areaSqM.toFixed(5),
            unit: "m²"
          },
          {
            label: lang === "bn" ? "নমুনার ক্ষেত্রফল (বর্গসেমি)" : "Sample Area (cm²)",
            value: (areaSqM * 10000).toFixed(2),
            unit: "cm²"
          }
        ],
        formula: {
          en: "GSM (g/m²) = Sample Weight (grams) / Sample Area (m²)\nSample Area (m²) = Length (m) × Width (m)\noz/yd² = GSM / 33.906",
          bn: "জিএসএম (g/m²) = নমুনার ওজন (গ্রাম) ÷ নমুনার ক্ষেত্রফল (বর্গমিটার)\nক্ষেত্রফল (বর্গমিটার) = দৈর্ঘ্য (মিটার) × প্রস্থ (মিটার)\noz/yd² = জিএসএম ÷ ৩৩.৯০৬"
        },
        steps: [
          {
            title: { en: "Step 1: Convert dimensions to meters", bn: "ধাপ ১: মাত্রাগুলোকে মিটারে রূপান্তর" },
            calc: `Length = ${lMeters.toFixed(4)} m, Width = ${wdMeters.toFixed(4)} m`
          },
          {
            title: { en: "Step 2: Calculate Sample Area in square meters", bn: "ধাপ ২: বর্গমিটারে নমুনার ক্ষেত্রফল নির্ণয়" },
            calc: `Area = ${lMeters.toFixed(4)} m × ${wdMeters.toFixed(4)} m = ${areaSqM.toFixed(6)} m²`
          },
          {
            title: { en: "Step 3: Divide weight by sample area", bn: "ধাপ ৩: নমুনার ওজনকে ক্ষেত্রফল দিয়ে ভাগ" },
            calc: `GSM = ${wGrams.toFixed(4)} g / ${areaSqM.toFixed(6)} m² = ${gsm.toFixed(2)} g/m²`
          },
          {
            title: { en: "Step 4: Convert GSM to imperial oz/yd²", bn: "ধাপ ৪: জিএসএমকে oz/yd²-এ রূপান্তর" },
            calc: `oz/yd² = ${gsm.toFixed(2)} / 33.906 = ${ozSqYd.toFixed(2)} oz/yd²`
          }
        ],
        explanation: {
          en: "GSM (Grams per Square Meter) is the universal metric standard defined under ISO 3801 and ASTM D3776 for evaluating fabric weight and substance. It determines fabric density, handfeel, drape, and cost.",
          bn: "জিএসএম (গ্রাম প্রতি বর্গমিটার) হলো আন্তর্জাতিক মানদণ্ড (ISO 3801 / ASTM D3776) অনুসারে কাপড়ের ঘনত্ব ও ওজন নির্ধারণের একক। পোশাকের মান, থিকনেস এবং খরচে এটি সরাসরি ভূমিকা রাখে।"
        }
      };
    }
  },

  // --------------------------------------------------------------------------
  // 2. FABRIC WEIGHT CALCULATOR
  // --------------------------------------------------------------------------
  {
    id: "fabric-weight",
    category: "fabric",
    icon: "📦",
    title: {
      en: "Fabric Weight Calculator",
      bn: "কাপড়ের মোট ওজন ক্যালকুলেটর"
    },
    description: {
      en: "Compute total fabric roll or order weight in Kilograms and Pounds from length, width, and GSM.",
      bn: "কাপড়ের মোট দৈর্ঘ্য, প্রস্থ ও জিএসএম থেকে মোট ওজন কিলোগ্রাম এবং পাউন্ডে নির্ণয় করুন।"
    },
    tags: ["fabric", "weight", "roll", "kg", "lbs", "length", "width", "gsm", "রোল", "ওজন"],
    inputs: [
      {
        id: "length",
        label: { en: "Fabric Length", bn: "কাপড়ের দৈর্ঘ্য" },
        type: "number",
        default: "1000",
        min: 0.1,
        step: "1",
        unitOptions: [
          { value: "m", label: "Meters (m)" },
          { value: "yd", label: "Yards (yd)" }
        ],
        defaultUnit: "m",
        helper: { en: "Total roll or batch length", bn: "রোল বা ব্যাচের মোট দৈর্ঘ্য" }
      },
      {
        id: "width",
        label: { en: "Fabric Width", bn: "কাপড়ের প্রস্থ" },
        type: "number",
        default: "60",
        min: 1,
        step: "0.5",
        unitOptions: [
          { value: "inch", label: "Inches (in)" },
          { value: "cm", label: "Centimeters (cm)" },
          { value: "m", label: "Meters (m)" }
        ],
        defaultUnit: "inch",
        helper: { en: "Usable cuttable width", bn: "কাটেবল প্রস্থ" }
      },
      {
        id: "gsm",
        label: { en: "Fabric GSM", bn: "কাপড়ের জিএসএম (GSM)" },
        type: "number",
        default: "200",
        min: 1,
        step: "1",
        unitAddon: "g/m²",
        helper: { en: "Grams per square meter", bn: "প্রতি বর্গমিটারে গ্রাম" }
      }
    ],
    example: {
      length: "1000",
      length_unit: "m",
      width: "60",
      width_unit: "inch",
      gsm: "200"
    },
    calculate: function (inputs, lang) {
      const lenRaw = parseFloat(inputs.length);
      const widRaw = parseFloat(inputs.width);
      const gsmRaw = parseFloat(inputs.gsm);

      if (isNaN(lenRaw) || isNaN(widRaw) || isNaN(gsmRaw)) {
        return { error: I18N[lang].errors.required };
      }
      if (lenRaw <= 0 || widRaw <= 0 || gsmRaw <= 0) {
        return { error: I18N[lang].errors.positive };
      }

      // Convert length to meters (1 yd = 0.9144 m)
      const lenM = inputs.length_unit === "yd" ? lenRaw * 0.9144 : lenRaw;

      // Convert width to meters (1 inch = 0.0254 m, 1 cm = 0.01 m)
      let widM = widRaw;
      if (inputs.width_unit === "inch") widM = widRaw * 0.0254;
      else if (inputs.width_unit === "cm") widM = widRaw * 0.01;

      const totalArea = lenM * widM;
      const weightKg = (totalArea * gsmRaw) / 1000;
      const weightLbs = weightKg * 2.20462;
      const linearWeightGpm = widM * gsmRaw; // Grams per linear meter

      return {
        primary: {
          label: lang === "bn" ? "মোট কাপড়ের ওজন" : "Total Fabric Weight",
          value: weightKg.toFixed(2),
          unit: "kg"
        },
        secondary: [
          {
            label: lang === "bn" ? "ওজন (পাউন্ড)" : "Weight (Pounds)",
            value: weightLbs.toFixed(2),
            unit: "lbs"
          },
          {
            label: lang === "bn" ? "মোট ক্ষেত্রফল" : "Total Fabric Area",
            value: totalArea.toFixed(2),
            unit: "m²"
          },
          {
            label: lang === "bn" ? "লিনিয়ার ওজন" : "Linear Weight",
            value: linearWeightGpm.toFixed(2),
            unit: "g/linear m"
          }
        ],
        formula: {
          en: "Weight (kg) = [Length (m) × Width (m) × GSM] / 1000\nWeight (lbs) = Weight (kg) × 2.20462",
          bn: "ওজন (কেজি) = [দৈর্ঘ্য (মিটার) × প্রস্থ (মিটার) × জিএসএম] ÷ ১০০০\nওজন (পাউন্ড) = ওজন (কেজি) × ২.২০৪৬২"
        },
        steps: [
          {
            title: { en: "Step 1: Convert dimensions to meters", bn: "ধাপ ১: মাত্রাগুলোকে মিটারে রূপান্তর" },
            calc: `Length = ${lenM.toFixed(3)} m, Width = ${widM.toFixed(4)} m`
          },
          {
            title: { en: "Step 2: Calculate total fabric area", bn: "ধাপ ২: মোট ক্ষেত্রফল হিসাব" },
            calc: `Total Area = ${lenM.toFixed(3)} m × ${widM.toFixed(4)} m = ${totalArea.toFixed(2)} m²`
          },
          {
            title: { en: "Step 3: Multiply area by GSM and convert to kg", bn: "ধাপ ৩: ক্ষেত্রফলকে জিএসএম দিয়ে গুণ করে কেজিতে রূপান্তর" },
            calc: `Weight (kg) = (${totalArea.toFixed(2)} m² × ${gsmRaw} g/m²) / 1000 = ${weightKg.toFixed(2)} kg`
          },
          {
            title: { en: "Step 4: Convert to pounds (lbs)", bn: "ধাপ ৪: পাউন্ডে (lbs) রূপান্তর" },
            calc: `Weight (lbs) = ${weightKg.toFixed(2)} kg × 2.20462 = ${weightLbs.toFixed(2)} lbs`
          }
        ],
        explanation: {
          en: "Calculating total batch weight is essential for dyeing liquor preparation, dye recipe dosing, shipping weight calculation, container stuffing, and commercial invoice verification.",
          bn: "কাপড়ের মোট ওজন গণনা ডাইং লিকার তৈরি, কেমিক্যালের ডোজ নির্ধারণ, শিপিং কনটেইনারের ধারণক্ষমতা ও কমার্শিয়াল ইনভয়েসের জন্য অত্যন্ত প্রয়োজনীয়।"
        }
      };
    }
  },

  // --------------------------------------------------------------------------
  // 3. SHRINKAGE CALCULATOR
  // --------------------------------------------------------------------------
  {
    id: "shrinkage",
    category: "fabric",
    icon: "📐",
    title: {
      en: "Fabric Shrinkage Calculator",
      bn: "কাপড়ের সংকোচন (Shrinkage) ক্যালকুলেটর"
    },
    description: {
      en: "Calculate warp/length and weft/width dimensional stability percentage after washing or heat setting.",
      bn: "ওয়াশ বা হিট সেটিংয়ের পর দৈর্ঘ্য (টানা) এবং প্রস্থ (পড়েন) বরাবর কাপড়ের সংকোচন বা প্রসারণ শতকরা হারে হিসাব করুন।"
    },
    tags: ["shrinkage", "wash", "dimensional", "stability", "length", "width", "সংকোচন", "শ্রিনকেজ"],
    inputs: [
      {
        id: "orig_dim",
        label: { en: "Original Dimension (Before Wash)", bn: "মূল পরিমাপ (ওয়াশের পূর্বে)" },
        type: "number",
        default: "50",
        min: 0.1,
        step: "0.1",
        unitOptions: [
          { value: "cm", label: "Centimeters (cm)" },
          { value: "inch", label: "Inches (in)" },
          { value: "mm", label: "Millimeters (mm)" }
        ],
        defaultUnit: "cm",
        helper: { en: "Benchmark mark distance (typically 50 cm or 35 cm bench marks)", bn: "স্ট্যান্ডার্ড বেঞ্চমার্ক দূরত্ব (সাধারণত ৫০ সেমি বা ৩৫ সেমি)" }
      },
      {
        id: "fin_dim",
        label: { en: "Finished Dimension (After Wash/Test)", bn: "ওয়াশের পরের পরিমাপ" },
        type: "number",
        default: "47.5",
        min: 0.1,
        step: "0.1",
        unitOptions: [
          { value: "cm", label: "Centimeters (cm)" },
          { value: "inch", label: "Inches (in)" },
          { value: "mm", label: "Millimeters (mm)" }
        ],
        defaultUnit: "cm",
        helper: { en: "Dimension measured after conditioned relaxation", bn: "কন্ডিশনিংয়ের পর প্রাপ্ত পরিমাপ" }
      }
    ],
    example: {
      orig_dim: "50",
      orig_dim_unit: "cm",
      fin_dim: "47.5",
      fin_dim_unit: "cm"
    },
    calculate: function (inputs, lang) {
      const orig = parseFloat(inputs.orig_dim);
      const fin = parseFloat(inputs.fin_dim);

      if (isNaN(orig) || isNaN(fin)) {
        return { error: I18N[lang].errors.required };
      }
      if (orig <= 0 || fin <= 0) {
        return { error: I18N[lang].errors.positive };
      }

      // Convert to same base unit (cm)
      let origCm = orig;
      if (inputs.orig_dim_unit === "inch") origCm = orig * 2.54;
      else if (inputs.orig_dim_unit === "mm") origCm = orig / 10;

      let finCm = fin;
      if (inputs.fin_dim_unit === "inch") finCm = fin * 2.54;
      else if (inputs.fin_dim_unit === "mm") finCm = fin / 10;

      if (origCm === 0) {
        return { error: I18N[lang].errors.nonZero };
      }

      // Standard AATCC 135 / ISO 6330 formula:
      // Shrinkage % = ((Original - Finished) / Original) * 100
      const diff = origCm - finCm;
      const shrinkagePct = (diff / origCm) * 100;
      const isElongation = shrinkagePct < 0;

      let statusClass = "status-excellent";
      let statusText = lang === "bn" ? "সহনশীল মাত্রায় আছে (Within Tolerance)" : "Within Commercial Tolerance";
      if (Math.abs(shrinkagePct) > 5) {
        statusClass = "status-danger";
        statusText = lang === "bn" ? "উচ্চ সংকোচন - সমন্বয় প্রয়োজন" : "High Shrinkage - Attention Required";
      } else if (Math.abs(shrinkagePct) > 3) {
        statusClass = "status-warning";
        statusText = lang === "bn" ? "মধ্যম সংকোচন" : "Moderate Shrinkage";
      }

      return {
        primary: {
          label: isElongation
            ? (lang === "bn" ? "কাপড়ের প্রসারণ (Elongation / Growth)" : "Elongation / Growth")
            : (lang === "bn" ? "কাপড়ের সংকোচন (Shrinkage)" : "Fabric Shrinkage"),
          value: Math.abs(shrinkagePct).toFixed(2),
          unit: "%"
        },
        status: {
          class: statusClass,
          text: statusText
        },
        secondary: [
          {
            label: lang === "bn" ? "পার্থক্য" : "Dimension Delta",
            value: Math.abs(diff).toFixed(2),
            unit: inputs.orig_dim_unit
          },
          {
            label: lang === "bn" ? "পরিবর্তনের ধরন" : "Change Mode",
            value: isElongation
              ? (lang === "bn" ? "প্রসারণ (+ বৃদ্ধি)" : "Growth (+ Elongation)")
              : (lang === "bn" ? "সংকোচন (- হ্রাস)" : "Shrinkage (- Loss)"),
            unit: ""
          }
        ],
        formula: {
          en: "Shrinkage % = [(Original Dimension - Finished Dimension) / Original Dimension] × 100\n(Negative value indicates growth / elongation)",
          bn: "সংকোচন % = [(মূল পরিমাপ - ওয়াশ পরবর্তী পরিমাপ) ÷ মূল পরিমাপ] × ১০০\n(মান ঋণাত্মক হলে তা প্রসারণ বা ইলংগেশন নির্দেশ করে)"
        },
        steps: [
          {
            title: { en: "Step 1: Calculate dimensional difference", bn: "ধাপ ১: পরিমাপের পার্থক্য নির্ণয়" },
            calc: `Difference = ${origCm.toFixed(2)} cm - ${finCm.toFixed(2)} cm = ${diff.toFixed(2)} cm`
          },
          {
            title: { en: "Step 2: Divide by original dimension and multiply by 100", bn: "ধাপ ২: মূল পরিমাপ দিয়ে ভাগ করে ১০০ দিয়ে গুণ" },
            calc: `Shrinkage % = (${diff.toFixed(2)} cm / ${origCm.toFixed(2)} cm) × 100 = ${shrinkagePct.toFixed(2)}%`
          }
        ],
        explanation: {
          en: "Fabric dimensional stability testing (AATCC 135 / ISO 6330) ensures that garments retain their fit and dimensions after laundering. Knit fabrics generally have acceptable limits of -3% to -5%, while woven fabrics typically require -1% to -3%.",
          bn: "কাপড়ের ডাইমেনশনাল স্ট্যাবিলিটি টেস্টের (AATCC 135 / ISO 6330) মাধ্যমে নিশ্চিত করা হয় যে বারবার ধোয়ার পরও পোশাকের সাইজ সঠিক থাকবে। নিট কাপড়ে সাধারণত -৩% থেকে -৫% এবং ওভেন কাপড়ে -১% থেকে -৩% গ্রহণযোগ্য বিবেচনা করা হয়।"
        }
      };
    }
  },

  // --------------------------------------------------------------------------
  // 4. STENTER OVERFEED CALCULATOR
  // --------------------------------------------------------------------------
  {
    id: "stenter-overfeed",
    category: "finishing",
    icon: "🎛️",
    title: {
      en: "Stenter Overfeed Calculator",
      bn: "স্টেনটার ওভারফিড ক্যালকুলেটর"
    },
    description: {
      en: "Calculate Stenter machine overfeed or underfeed percentage based on inlet pin-chain speed and delivery speed.",
      bn: "ইনলেট স্পিড এবং ডেলিভারি স্পিডের ভিত্তিতে স্টেনটার ফিনিশিং মেশিনের ওভারফিড শতকরা হার নির্ণয় করুন।"
    },
    tags: ["stenter", "overfeed", "finishing", "speed", "inlet", "delivery", "স্টেনটার", "ওভারফিড", "ফিনিশিং"],
    inputs: [
      {
        id: "inlet_speed",
        label: { en: "Inlet Speed (Feeding Roller Speed)", bn: "ইনলেট স্পিড (ফিডিং রোলার স্পিড)" },
        type: "number",
        default: "46",
        min: 0.1,
        step: "0.5",
        unitAddon: "m/min",
        helper: { en: "Speed of fabric entering the stenter pin chain", bn: "স্টেনটার পিন চেইনে কাপড় প্রবেশের গতি" }
      },
      {
        id: "delivery_speed",
        label: { en: "Delivery Speed (Exit Chain Speed)", bn: "ডেলিভারি স্পিড (মেশিন এক্সিট স্পিড)" },
        type: "number",
        default: "40",
        min: 0.1,
        step: "0.5",
        unitAddon: "m/min",
        helper: { en: "Speed of fabric exiting the delivery end", bn: "মেশিন থেকে কাপড় বের হওয়ার গতি" }
      }
    ],
    example: {
      inlet_speed: "46",
      delivery_speed: "40"
    },
    calculate: function (inputs, lang) {
      const vIn = parseFloat(inputs.inlet_speed);
      const vOut = parseFloat(inputs.delivery_speed);

      if (isNaN(vIn) || isNaN(vOut)) {
        return { error: I18N[lang].errors.required };
      }
      if (vIn <= 0 || vOut <= 0) {
        return { error: I18N[lang].errors.positive };
      }
      if (vOut === 0) {
        return { error: I18N[lang].errors.nonZero };
      }

      // Formula: Overfeed % = ((Inlet Speed - Delivery Speed) / Delivery Speed) * 100
      const diff = vIn - vOut;
      const overfeedPct = (diff / vOut) * 100;
      const isUnderfeed = overfeedPct < 0;

      return {
        primary: {
          label: isUnderfeed
            ? (lang === "bn" ? "আন্ডারফিড শতাংশ" : "Underfeed Percentage")
            : (lang === "bn" ? "ওভারফিড শতাংশ" : "Overfeed Percentage"),
          value: (overfeedPct >= 0 ? "+" : "") + overfeedPct.toFixed(2),
          unit: "%"
        },
        secondary: [
          {
            label: lang === "bn" ? "গতির পার্থক্য" : "Speed Differential",
            value: (diff >= 0 ? "+" : "") + diff.toFixed(2),
            unit: "m/min"
          },
          {
            label: lang === "bn" ? "ফিড অনুপাত (Feed Ratio)" : "Feed Ratio",
            value: (vIn / vOut).toFixed(3),
            unit: ": 1"
          }
        ],
        warning: {
          en: "Actual factory settings may vary depending on machine, fabric construction, process and factory standard.",
          bn: "মেশিন, কাপড়ের বুনন/কনস্ট্রাকশন, প্রক্রিয়া এবং কারখানার মানদণ্ডের উপর ভিত্তি করে বাস্তব সেটিংস পরিবর্তিত হতে পারে।"
        },
        formula: {
          en: "Overfeed % = [(Inlet Speed - Delivery Speed) / Delivery Speed] × 100\nAlternative: Delivery Speed = Inlet Speed / (1 + Overfeed% / 100)",
          bn: "ওভারফিড % = [(ইনলেট স্পিড - ডেলিভারি স্পিড) ÷ ডেলিভারি স্পিড] × ১০০\nবিকল্প: ডেলিভারি স্পিড = ইনলেট স্পিড ÷ (১ + ওভারফিড% ÷ ১০০)"
        },
        steps: [
          {
            title: { en: "Step 1: Calculate speed differential between inlet and exit", bn: "ধাপ ১: ইনলেট ও এক্সিটের গতির পার্থক্য নির্ণয়" },
            calc: `Speed Delta = ${vIn} m/min - ${vOut} m/min = ${diff.toFixed(2)} m/min`
          },
          {
            title: { en: "Step 2: Divide difference by delivery speed and multiply by 100", bn: "ধাপ ২: ডেলিভারি গতি দিয়ে ভাগ করে ১০০ দিয়ে গুণ" },
            calc: `Overfeed % = (${diff.toFixed(2)} / ${vOut}) × 100 = ${overfeedPct.toFixed(2)}%`
          }
        ],
        explanation: {
          en: "Stenter overfeed is applied to control length shrinkage and compact fabric loops. By feeding more length into the pins than the machine pulls away, internal yarn tensions are relaxed during thermo-fixation and drying.",
          bn: "স্টেনটার মেশিনে কাপড়ের দৈর্ঘ্য সংকোচন (Length Shrinkage) নিয়ন্ত্রণ এবং জিএসএম বাড়াতে ওভারফিড দেওয়া হয়। ডেলিভারি স্পিডের চেয়ে ইনলেটে কাপড় বেশি ঢুকিয়ে গরম চেম্বারে হিট সেট করার ফলে সুতার অভ্যন্তরীণ টান শিথিল হয়।"
        }
      };
    }
  },

  // --------------------------------------------------------------------------
  // 5. YARN COUNT CONVERTER
  // --------------------------------------------------------------------------
  {
    id: "yarn-count",
    category: "yarn",
    icon: "🧶",
    title: {
      en: "Yarn Count Converter",
      bn: "সুতার কাউন্ট রূপান্তরকারী (Yarn Count)"
    },
    description: {
      en: "Universal bidirectional converter between English Cotton Count (Ne), Metric Count (Nm), Tex, and Denier.",
      bn: "ইংরেজি কটন কাউন্ট (Ne), মেট্রিক কাউন্ট (Nm), টেক্স (Tex) এবং ডেনিয়ার (Denier) এর মধ্যে সরাসরি নির্ভুল রূপান্তর।"
    },
    tags: ["yarn", "count", "ne", "tex", "denier", "nm", "converter", "সুতা", "কাউন্ট", "ডেনিয়ার", "টেক্স"],
    inputs: [
      {
        id: "count_val",
        label: { en: "Count Value", bn: "কাউন্টের মান" },
        type: "number",
        default: "30",
        min: 0.1,
        step: "0.1",
        unitOptions: [
          { value: "ne", label: "English Cotton (Ne / s)" },
          { value: "tex", label: "Tex (g/km)" },
          { value: "den", label: "Denier (g/9000m)" },
          { value: "nm", label: "Metric Count (Nm)" }
        ],
        defaultUnit: "ne",
        helper: { en: "Select your source yarn count system", bn: "আপনার মূল সুতার কাউন্ট সিস্টেম বেছে নিন" }
      }
    ],
    example: {
      count_val: "30",
      count_val_unit: "ne"
    },
    calculate: function (inputs, lang) {
      const val = parseFloat(inputs.count_val);
      const system = inputs.count_val_unit;

      if (isNaN(val)) {
        return { error: I18N[lang].errors.required };
      }
      if (val <= 0) {
        return { error: I18N[lang].errors.positive };
      }

      // Normalize all count systems through Tex (Direct System: grams per 1,000 meters)
      let texVal = 0;
      if (system === "ne") {
        texVal = 590.541 / val;
      } else if (system === "tex") {
        texVal = val;
      } else if (system === "den") {
        texVal = val / 9.0;
      } else if (system === "nm") {
        texVal = 1000.0 / val;
      }

      // Derive other systems from Tex
      const resNe = 590.541 / texVal;
      const resTex = texVal;
      const resDen = texVal * 9.0;
      const resNm = 1000.0 / texVal;

      return {
        primary: {
          label: `${lang === "bn" ? "রূপান্তরিত মান" : "Equivalent"} (${system.toUpperCase()})`,
          value: val.toFixed(2),
          unit: system.toUpperCase()
        },
        secondary: [
          {
            label: "English Count (Ne)",
            value: resNe.toFixed(2),
            unit: "Ne"
          },
          {
            label: "Tex Count",
            value: resTex.toFixed(2),
            unit: "Tex"
          },
          {
            label: "Denier (Filament)",
            value: resDen.toFixed(2),
            unit: "D"
          },
          {
            label: "Metric Count (Nm)",
            value: resNm.toFixed(2),
            unit: "Nm"
          }
        ],
        formula: {
          en: "• Tex = 590.54 / Ne = Denier / 9 = 1000 / Nm\n• Ne = 590.54 / Tex = 5314.9 / Denier\n• Denier = Tex × 9 = 5314.9 / Ne\n• Nm = 1000 / Tex = 1.6934 × Ne",
          bn: "• টেক্স = ৫৯০.৫৪ ÷ Ne = ডেনিয়ার ÷ ৯ = ১০০০ ÷ Nm\n• Ne = ৫৯০.৫৪ ÷ টেক্স = ৫৩১৪.৯ ÷ ডেনিয়ার\n• ডেনিয়ার = টেক্স × ৯ = ৫৩১৪.৯ ÷ Ne\n• Nm = ১০০০ ÷ টেক্স = ১.৬৯৩৪ × Ne"
        },
        steps: [
          {
            title: { en: "Step 1: Determine source system category", bn: "ধাপ ১: মূল কাউন্ট পদ্ধতির ধরন নির্ধারণ" },
            calc: system === "ne" || system === "nm"
              ? "Indirect System (Higher count = Finer yarn)"
              : "Direct System (Higher count = Coarser / Heavier yarn)"
          },
          {
            title: { en: "Step 2: Convert to fundamental Tex standard", bn: "ধাপ ২: মৌলিক টেক্স মানে রূপান্তর" },
            calc: `Tex = ${resTex.toFixed(3)} g/km`
          },
          {
            title: { en: "Step 3: Calculate corresponding yarn count equivalents", bn: "ধাপ ৩: অন্যান্য সমতুল্য কাউন্ট নির্ণয়" },
            calc: `Ne: ${resNe.toFixed(2)}, Denier: ${resDen.toFixed(2)}, Nm: ${resNm.toFixed(2)}`
          }
        ],
        explanation: {
          en: "Yarn numbering systems fall into Direct (weight per unit length: Tex, Denier) and Indirect (length per unit weight: Ne, Nm). Ne is dominant in cotton spinning, Denier in synthetics/filaments, and Tex is the universal ISO standard.",
          bn: "সুতার কাউন্ট পদ্ধতি মূলত দুই প্রকার: প্রত্যক্ষ (Direct - যেমন টেক্স, ডেনিয়ার যেখানে মান বাড়লে সুতা মোটা হয়) এবং পরোক্ষ (Indirect - যেমন Ne, Nm যেখানে মান বাড়লে সুতা চিকন হয়)। কটন শিল্পে Ne এবং সিন্থেটিক ফিলামেন্টে ডেনিয়ার বেশি ব্যবহৃত হয়।"
        }
      };
    }
  },

  // --------------------------------------------------------------------------
  // 6. DYE & CHEMICAL PERCENTAGE CALCULATOR
  // --------------------------------------------------------------------------
  {
    id: "dye-chem",
    category: "dyeing",
    icon: "🧪",
    title: {
      en: "Dye & Chemical Requirement",
      bn: "ডাইং ও কেমিক্যাল শতকরা হিসাব"
    },
    description: {
      en: "Calculate required dyestuffs or auxiliary chemicals based on fabric weight (% on weight of fabric - % o.w.f.) or bath liquor concentration (g/L).",
      bn: "কাপড়ের ওজনের শতকরা হার (% o.w.f.) বা লিকার ঘনমাত্রার (g/L) ভিত্তিতে প্রয়োজনীয় রঙ বা কেমিক্যালের পরিমাণ হিসাব করুন।"
    },
    tags: ["dye", "chemical", "percentage", "owf", "recipe", "dosage", "ডাইং", "কেমিক্যাল", "শতকরা"],
    inputs: [
      {
        id: "calc_mode",
        label: { en: "Dosing Method", bn: "ডোজের হিসাব পদ্ধতি" },
        type: "select",
        default: "owf",
        options: [
          { value: "owf", label: "% on Weight of Fabric (% o.w.f.)" },
          { value: "gl", label: "Concentration in Grams per Liter (g/L)" }
        ],
        helper: { en: "Choose % o.w.f. for dyes or g/L for salt/soda/auxiliaries", bn: "রঙের জন্য % o.w.f. এবং অক্সিলারির জন্য g/L নির্বাচন করুন" }
      },
      {
        id: "fabric_wt",
        label: { en: "Fabric Batch Weight", bn: "কাপড়ের ব্যাচ ওজন" },
        type: "number",
        default: "100",
        min: 0.1,
        step: "1",
        unitAddon: "kg",
        helper: { en: "Total dry batch weight in kilograms", bn: "কিলোগ্রামে কাপড়ের মোট শুকনা ওজন" }
      },
      {
        id: "dosage",
        label: { en: "Dosage (% or g/L)", bn: "ডোজ বা মাত্রা (% অথবা g/L)" },
        type: "number",
        default: "2",
        min: 0.001,
        step: "0.01",
        unitAddon: "% / g/L",
        helper: { en: "Percentage (e.g. 2%) or concentration (e.g. 30 g/L)", bn: "রেসিপি অনুযায়ী শতকরা হার বা ঘনমাত্রা" }
      },
      {
        id: "bath_vol",
        label: { en: "Total Bath Volume (for g/L mode only)", bn: "মোট লিকার আয়তন (শুধুমাত্র g/L পদ্ধতির জন্য)" },
        type: "number",
        default: "800",
        min: 1,
        step: "10",
        unitAddon: "Liters",
        helper: { en: "Total liquor volume in liters if using g/L mode", bn: "g/L পদ্ধতিতে লিকারের মোট লিটার" }
      }
    ],
    example: {
      calc_mode: "owf",
      fabric_wt: "100",
      dosage: "2",
      bath_vol: "800"
    },
    calculate: function (inputs, lang) {
      const mode = inputs.calc_mode;
      const fabKg = parseFloat(inputs.fabric_wt);
      const dose = parseFloat(inputs.dosage);
      const bathVol = parseFloat(inputs.bath_vol);

      if (isNaN(fabKg) || isNaN(dose)) {
        return { error: I18N[lang].errors.required };
      }
      if (fabKg <= 0 || dose <= 0) {
        return { error: I18N[lang].errors.positive };
      }

      let chemKg = 0;
      let chemG = 0;
      let formulaTextEn = "";
      let formulaTextBn = "";
      let stepsArray = [];

      if (mode === "owf") {
        // Chemical required (kg) = (Fabric Weight in kg * Dose %) / 100
        chemKg = (fabKg * dose) / 100.0;
        chemG = chemKg * 1000.0;

        formulaTextEn = "Chemical (kg) = [Fabric Weight (kg) × Chemical %] / 100\nChemical (g) = Chemical (kg) × 1000";
        formulaTextBn = "কেমিক্যাল (কেজি) = [কাপড়ের ওজন (কেজি) × কেমিক্যাল %] ÷ ১০০\nকেমিক্যাল (গ্রাম) = কেজি × ১০০০";

        stepsArray = [
          {
            title: { en: "Step 1: Multiply fabric weight by dosage percentage", bn: "ধাপ ১: কাপড়ের ওজনকে কেমিক্যাল % দিয়ে গুণ" },
            calc: `Subtotal = ${fabKg} kg × ${dose}% = ${fabKg * dose}`
          },
          {
            title: { en: "Step 2: Divide by 100 to get kg requirement", bn: "ধাপ ২: ১০০ দিয়ে ভাগ করে প্রয়োজনীয় কেজি নির্ণয়" },
            calc: `Chemical (kg) = (${fabKg} × ${dose}) / 100 = ${chemKg.toFixed(3)} kg`
          },
          {
            title: { en: "Step 3: Convert to grams for precise dispensing", bn: "ধাপ ৩: সুনির্দিষ্ট ওজনের জন্য গ্রামে রূপান্তর" },
            calc: `Chemical (g) = ${chemKg.toFixed(3)} kg × 1000 = ${chemG.toFixed(1)} grams`
          }
        ];
      } else {
        // g/L mode: Chemical (kg) = (Bath Volume in Liters * Dose in g/L) / 1000
        if (isNaN(bathVol) || bathVol <= 0) {
          return { error: lang === "bn" ? "অনুগ্রহ করে লিকারের সঠিক আয়তন লিখুন।" : "Please enter a valid liquor bath volume." };
        }

        chemG = bathVol * dose;
        chemKg = chemG / 1000.0;

        formulaTextEn = "Chemical (kg) = [Bath Volume (L) × Concentration (g/L)] / 1000";
        formulaTextBn = "কেমিক্যাল (কেজি) = [মোট লিকার (লিটার) × ঘনমাত্রা (g/L)] ÷ ১০০০";

        stepsArray = [
          {
            title: { en: "Step 1: Multiply bath volume by g/L concentration", bn: "ধাপ ১: লিকারের মোট আয়তনকে g/L দিয়ে গুণ" },
            calc: `Total Grams = ${bathVol} Liters × ${dose} g/L = ${chemG.toFixed(1)} grams`
          },
          {
            title: { en: "Step 2: Convert grams to kilograms", bn: "ধাপ ২: গ্রামকে কেজিতে রূপান্তর" },
            calc: `Chemical (kg) = ${chemG.toFixed(1)} g / 1000 = ${chemKg.toFixed(3)} kg`
          }
        ];
      }

      return {
        primary: {
          label: lang === "bn" ? "প্রয়োজনীয় কেমিক্যাল / রঙ" : "Chemical Required",
          value: chemKg.toFixed(3),
          unit: "kg"
        },
        secondary: [
          {
            label: lang === "bn" ? "পরিমাণ (গ্রামে)" : "Quantity in Grams",
            value: chemG.toFixed(1),
            unit: "g"
          },
          {
            label: lang === "bn" ? "হিসাব পদ্ধতি" : "Calculation Mode",
            value: mode === "owf" ? "% on Weight (o.w.f.)" : "Concentration (g/L)",
            unit: ""
          }
        ],
        formula: {
          en: formulaTextEn,
          bn: formulaTextBn
        },
        steps: stepsArray,
        explanation: {
          en: "In textile wet processing, dyestuffs are typically dosed on weight of fabric (% o.w.f.), whereas salts, leveling agents, and soda ash alkali buffers are frequently dosed in grams per liter (g/L) to maintain ionic strength and bath equilibrium.",
          bn: "টেক্সটাইল ডাইংয়ে সাধারণত রঙ কাপড়ের শুকনা ওজনের শতকরা হারে (% o.w.f.) এবং লবণ, ক্ষার ও অন্যান্য সহায়ক কেমিক্যালগুলো লিকার ঘনমাত্রায় (g/L) দেওয়া হয়।"
        }
      };
    }
  },

  // --------------------------------------------------------------------------
  // 7. LIQUOR RATIO (M:L) CALCULATOR
  // --------------------------------------------------------------------------
  {
    id: "liquor-ratio",
    category: "dyeing",
    icon: "💧",
    title: {
      en: "Liquor Ratio (M:L) Calculator",
      bn: "লিকার রেশিও (Liquor Ratio) ক্যালকুলেটর"
    },
    description: {
      en: "Calculate total dyeing bath volume required in liters from fabric batch weight, material-to-liquor ratio (M:L), and machine reserve volume.",
      bn: "কাপড়ের মোট ওজন, মেটেরিয়াল টু লিকার অনুপাত (১:X) এবং মেশিনের অতিরিক্ত রিজার্ভ থেকে মোট প্রয়োজনীয় পানির পরিমাণ হিসাব করুন।"
    },
    tags: ["liquor", "ratio", "dyeing", "volume", "water", "ml", "liters", "লিকার", "রেশিও", "পানি"],
    inputs: [
      {
        id: "fabric_weight",
        label: { en: "Fabric Batch Weight", bn: "কাপড়ের ব্যাচ ওজন" },
        type: "number",
        default: "100",
        min: 0.1,
        step: "1",
        unitAddon: "kg",
        helper: { en: "Total dry batch weight in machine", bn: "মেশিনে লোডকৃত কাপড়ের মোট ওজন" }
      },
      {
        id: "liquor_ratio",
        label: { en: "Liquor Ratio (1 : X)", bn: "লিকার অনুপাত (১ : X)" },
        type: "number",
        default: "8",
        min: 1,
        step: "0.5",
        unitAddon: "Ratio (1:X)",
        helper: { en: "Enter ratio number X (e.g. 6 for 1:6, 8 for 1:8)", bn: "অনুপাত X লিখুন (যেমন ১:৮ এর জন্য ৮)" }
      },
      {
        id: "dead_volume",
        label: { en: "Piping / Dead Volume Allowance", bn: "পাইপিং বা ডেড ভলিউম অতিরিক্ত পানি" },
        type: "number",
        default: "0",
        min: 0,
        step: "5",
        unitAddon: "Liters",
        helper: { en: "Optional machine circulation dead volume / reserve", bn: "মেশিন পাইপলাইনের অতিরিক্ত পানি (ঐচ্ছিক)" }
      }
    ],
    example: {
      fabric_weight: "100",
      liquor_ratio: "8",
      dead_volume: "0"
    },
    calculate: function (inputs, lang) {
      const fabKg = parseFloat(inputs.fabric_weight);
      const ratio = parseFloat(inputs.liquor_ratio);
      const deadVol = parseFloat(inputs.dead_volume) || 0;

      if (isNaN(fabKg) || isNaN(ratio)) {
        return { error: I18N[lang].errors.required };
      }
      if (fabKg <= 0 || ratio <= 0 || deadVol < 0) {
        return { error: I18N[lang].errors.positive };
      }

      // Liquor Volume (L) = (Fabric Weight kg * Liquor Ratio) + Dead Volume
      const netLiquor = fabKg * ratio;
      const totalLiquor = netLiquor + deadVol;

      return {
        primary: {
          label: lang === "bn" ? "মোট প্রয়োজনীয় লিকার" : "Total Liquor Volume",
          value: totalLiquor.toFixed(0),
          unit: "Liters"
        },
        secondary: [
          {
            label: lang === "bn" ? "নেট বাথ ভলিউম" : "Net Bath Liquor",
            value: netLiquor.toFixed(0),
            unit: "L"
          },
          {
            label: lang === "bn" ? "পাইপিং অতিরিক্ত রিজার্ভ" : "Dead Volume Allowance",
            value: deadVol.toFixed(0),
            unit: "L"
          },
          {
            label: lang === "bn" ? "কার্যকরী লিকার রেশিও" : "Effective Ratio",
            value: `1 : ${(totalLiquor / fabKg).toFixed(1)}`,
            unit: ""
          }
        ],
        warning: {
          en: "Actual liquor requirement depends on machine type (soft-flow, winch, package), pump circulation, and piping dead volume.",
          bn: "প্রকৃত লিকারের প্রয়োজনীয়তা মেশিনের ধরন (সফট-ফ্লো, উইঞ্চ, প্যাকেজ), পাম্পের সঞ্চালন এবং পাইপের ডেড ভলিউমের ওপর নির্ভর করে।"
        },
        formula: {
          en: "Total Liquor (Liters) = [Fabric Weight (kg) × Liquor Ratio] + Dead Volume (L)",
          bn: "মোট লিকার (লিটার) = [কাপড়ের ওজন (কেজি) × লিকার অনুপাত] + ডেড ভলিউম (লিটার)"
        },
        steps: [
          {
            title: { en: "Step 1: Multiply fabric weight by liquor ratio", bn: "ধাপ ১: কাপড়ের ওজনকে লিকার অনুপাত দিয়ে গুণ" },
            calc: `Net Liquor = ${fabKg} kg × ${ratio} = ${netLiquor.toFixed(1)} Liters`
          },
          {
            title: { en: "Step 2: Add piping / machine dead volume allowance", bn: "ধাপ ২: অতিরিক্ত ডেড ভলিউম যোগ" },
            calc: `Total Liquor = ${netLiquor.toFixed(1)} L + ${deadVol} L = ${totalLiquor.toFixed(1)} Liters`
          }
        ],
        explanation: {
          en: "The Material-to-Liquor ratio (M:L) represents the weight of the textile substrate relative to the volume of the process bath. Modern soft-flow and airflow dyeing machines operate at ultra-low ratios (1:4 to 1:6) to conserve water, steam energy, and chemical consumption.",
          bn: "মেটেরিয়াল-টু-লিকার রেশিও (M:L) বলতে কাপড়ের ওজনের অনুপাতে কত গুণ পানি ব্যবহার করা হবে তা বোঝায়। আধুনিক সফট-ফ্লো বা এয়ারফ্লো মেশিনে পানির অপচয় কমাতে অতি নিম্ন রেশিও (১:৪ থেকে ১:৬) ব্যবহৃত হয়।"
        }
      };
    }
  },

  // --------------------------------------------------------------------------
  // 8. MACHINE PRODUCTION CALCULATOR
  // --------------------------------------------------------------------------
  {
    id: "production",
    category: "production",
    icon: "🏭",
    title: {
      en: "Machine Production Calculator",
      bn: "মেশিন উৎপাদন (Production) ক্যালকুলেটর"
    },
    description: {
      en: "Calculate fabric continuous production output per hour, per shift (8 hrs), and per day in meters and kilograms based on speed, width, GSM, and efficiency.",
      bn: "মেশিনের গতি, কাপড়ের প্রস্থ, জিএসএম এবং দক্ষতার ভিত্তিতে ঘণ্টা, শিফট এবং দিনে মোট উৎপাদন (মিটার ও কেজি) হিসাব করুন।"
    },
    tags: ["machine", "production", "speed", "stenter", "output", "kg/hr", "meters", "উৎপাদন", "মেশিন"],
    inputs: [
      {
        id: "speed",
        label: { en: "Machine Speed", bn: "মেশিনের কাজের গতি" },
        type: "number",
        default: "45",
        min: 0.1,
        step: "1",
        unitOptions: [
          { value: "m_min", label: "Meters / min (m/min)" },
          { value: "yd_min", label: "Yards / min (yd/min)" }
        ],
        defaultUnit: "m_min",
        helper: { en: "Operating processing speed", bn: "মেশিনের চলমান গতি" }
      },
      {
        id: "width",
        label: { en: "Fabric Working Width", bn: "কাপড়ের কাজের প্রস্থ" },
        type: "number",
        default: "1.8",
        min: 0.1,
        step: "0.1",
        unitOptions: [
          { value: "m", label: "Meters (m)" },
          { value: "inch", label: "Inches (in)" },
          { value: "cm", label: "Centimeters (cm)" }
        ],
        defaultUnit: "m",
        helper: { en: "Average finished width across the chamber", bn: "কাপড়ের গড় প্রস্থ" }
      },
      {
        id: "gsm",
        label: { en: "Fabric GSM", bn: "কাপড়ের জিএসএম (GSM)" },
        type: "number",
        default: "180",
        min: 1,
        step: "1",
        unitAddon: "g/m²",
        helper: { en: "Finished Grams per Square Meter", bn: "ফিনিশড জিএসএম" }
      },
      {
        id: "efficiency",
        label: { en: "Process Efficiency (%)", bn: "কাজের দক্ষতা বা এফিশিয়েন্সি (%)" },
        type: "number",
        default: "85",
        min: 1,
        max: 100,
        step: "1",
        unitAddon: "%",
        helper: { en: "Effective running time percentage accounting for roll changes and downtime", bn: "ডাউনটাইম বাদে কার্যকর দক্ষতা" }
      },
      {
        id: "hours",
        label: { en: "Operating Shift Duration", bn: "কাজের সময়কাল" },
        type: "number",
        default: "8",
        min: 0.5,
        step: "0.5",
        unitAddon: "Hours",
        helper: { en: "Shift duration (e.g. 8 hours or 12 hours)", bn: "কাজের শিফট (সাধারণত ৮ বা ১২ ঘণ্টা)" }
      }
    ],
    example: {
      speed: "45",
      speed_unit: "m_min",
      width: "1.8",
      width_unit: "m",
      gsm: "180",
      efficiency: "85",
      hours: "8"
    },
    calculate: function (inputs, lang) {
      const spdRaw = parseFloat(inputs.speed);
      const widRaw = parseFloat(inputs.width);
      const gsmRaw = parseFloat(inputs.gsm);
      const effRaw = parseFloat(inputs.efficiency);
      const hrsRaw = parseFloat(inputs.hours);

      if (isNaN(spdRaw) || isNaN(widRaw) || isNaN(gsmRaw) || isNaN(effRaw) || isNaN(hrsRaw)) {
        return { error: I18N[lang].errors.required };
      }
      if (spdRaw <= 0 || widRaw <= 0 || gsmRaw <= 0 || effRaw <= 0 || hrsRaw <= 0) {
        return { error: I18N[lang].errors.positive };
      }

      // Convert speed to m/min
      const spdMmin = inputs.speed_unit === "yd_min" ? spdRaw * 0.9144 : spdRaw;

      // Convert width to meters
      let widM = widRaw;
      if (inputs.width_unit === "inch") widM = widRaw * 0.0254;
      else if (inputs.width_unit === "cm") widM = widRaw * 0.01;

      const effRatio = effRaw / 100.0;

      // Actual speed accounting for efficiency
      const actualSpdMmin = spdMmin * effRatio;
      const metersPerHour = actualSpdMmin * 60;
      const totalMetersShift = metersPerHour * hrsRaw;

      // Weight production:
      // Weight (kg) = (Length in m * Width in m * GSM) / 1000
      const kgPerHour = (metersPerHour * widM * gsmRaw) / 1000;
      const totalKgShift = kgPerHour * hrsRaw;
      const totalKgDay24 = kgPerHour * 24;

      return {
        primary: {
          label: lang === "bn" ? "শিফটের মোট উৎপাদন" : `Shift Production (${hrsRaw} hrs)`,
          value: totalKgShift.toFixed(1),
          unit: "kg"
        },
        secondary: [
          {
            label: lang === "bn" ? "শিফটে মোট দৈর্ঘ্য" : "Shift Output (Meters)",
            value: totalMetersShift.toFixed(0),
            unit: "meters"
          },
          {
            label: lang === "bn" ? "প্রতি ঘণ্টায় উৎপাদন" : "Production Rate",
            value: kgPerHour.toFixed(1),
            unit: "kg/hour"
          },
          {
            label: lang === "bn" ? "২৪ ঘণ্টায় দৈনিক উৎপাদন" : "Daily Capacity (24h)",
            value: totalKgDay24.toFixed(0),
            unit: "kg/day"
          }
        ],
        warning: {
          en: "Calculation assumes continuous processing. For weaving looms or circular knitting, production depends on picks/min or machine RPM and number of feeders.",
          bn: "এই গণনাটি কন্টিনিউয়াস প্রসেসিং ধরে করা হয়েছে। উইভিং বা সার্কুলার নিটিংয়ের ক্ষেত্রে উৎপাদন নির্ভর করে পিক্স/মিনিট বা মেশিন আরপিএম এবং ফিডারের সংখ্যার ওপর।"
        },
        formula: {
          en: "• Actual Speed (m/min) = Set Speed × (Efficiency / 100)\n• Output (m/hr) = Actual Speed × 60\n• Weight (kg/hr) = [Output (m/hr) × Width (m) × GSM] / 1000\n• Shift Production (kg) = Weight (kg/hr) × Shift Hours",
          bn: "• প্রকৃত গতি (মি/মিনিট) = মূল গতি × (এফিশিয়েন্সি ÷ ১০০)\n• দৈর্ঘ্য উৎপাদন (মি/ঘণ্টা) = প্রকৃত গতি × ৬০\n• ওজন (কেজি/ঘণ্টা) = [দৈর্ঘ্য (মিটার) × প্রস্থ (মিটার) × জিএসএম] ÷ ১০০০\n• শিফট উৎপাদন (কেজি) = কেজি/ঘণ্টা × শিফটের সময়কাল"
        },
        steps: [
          {
            title: { en: "Step 1: Calculate actual operating speed with efficiency", bn: "ধাপ ১: এফিশিয়েন্সি সমন্বয় করে প্রকৃত গতি নির্ণয়" },
            calc: `Actual Speed = ${spdMmin.toFixed(2)} m/min × (${effRaw} / 100) = ${actualSpdMmin.toFixed(2)} m/min`
          },
          {
            title: { en: "Step 2: Calculate linear meters per hour", bn: "ধাপ ২: প্রতি ঘণ্টায় প্রস্তুত কাপড়ের দৈর্ঘ্য" },
            calc: `Output (m/hr) = ${actualSpdMmin.toFixed(2)} m/min × 60 = ${metersPerHour.toFixed(1)} m/hr`
          },
          {
            title: { en: "Step 3: Calculate weight per hour using GSM and width", bn: "ধাপ ৩: প্রস্থ ও জিএসএম ব্যবহার করে ঘণ্টায় ওজন হিসাব" },
            calc: `Weight (kg/hr) = (${metersPerHour.toFixed(1)} m × ${widM.toFixed(3)} m × ${gsmRaw}) / 1000 = ${kgPerHour.toFixed(2)} kg/hr`
          },
          {
            title: { en: `Step 4: Multiply by ${hrsRaw} shift hours`, bn: `ধাপ ৪: শিফটের মোট ${hrsRaw} ঘণ্টা দিয়ে গুণ` },
            calc: `Total Shift Weight = ${kgPerHour.toFixed(2)} kg/hr × ${hrsRaw} hrs = ${totalKgShift.toFixed(1)} kg`
          }
        ],
        explanation: {
          en: "Machine capacity estimation allows factory production planners to schedule dyeing lots, organize stenter sequences, forecast delivery lead times, and optimize line balance.",
          bn: "মেশিন উৎপাদনের সক্ষমতা সঠিকভাবে হিসাব করার মাধ্যমে কারখানার উৎপাদন পরিকল্পনাবিদরা ডাইং ব্যাচ শিডিউল, স্টেনটার ফিনিশিং ও সঠিক সময়ে শিপমেন্ট ডেলিভারি নিশ্চিত করতে পারেন।"
        }
      };
    }
  },

  // --------------------------------------------------------------------------
  // 9. PRODUCTION EFFICIENCY CALCULATOR
  // --------------------------------------------------------------------------
  {
    id: "efficiency",
    category: "production",
    icon: "📊",
    title: {
      en: "Production Efficiency Calculator",
      bn: "উৎপাদন দক্ষতা (Efficiency) ক্যালকুলেটর"
    },
    description: {
      en: "Calculate actual machine or sewing line efficiency percentage against standard planned targets, with performance variance analysis.",
      bn: "পরিকল্পিত লক্ষ্যের বিপরীতে মেশিনের বা সুইং লাইনের বাস্তব উৎপাদন দক্ষতা (Efficiency %) এবং পার্থক্যের হিসাব।"
    },
    tags: ["efficiency", "production", "target", "kpi", "oee", "line", "দক্ষতা", "এফিশিয়েন্সি", "টার্গেট"],
    inputs: [
      {
        id: "actual_prod",
        label: { en: "Actual Production Output", bn: "প্রকৃত অর্জিত উৎপাদন" },
        type: "number",
        default: "4250",
        min: 0,
        step: "1",
        unitOptions: [
          { value: "pcs", label: "Pieces (pcs)" },
          { value: "m", label: "Meters (m)" },
          { value: "kg", label: "Kilograms (kg)" },
          { value: "dz", label: "Dozens (dz)" }
        ],
        defaultUnit: "pcs",
        helper: { en: "Finished verified units produced", bn: "বাস্তবে উৎপাদিত মোট পরিমাণ" }
      },
      {
        id: "target_prod",
        label: { en: "Target / Planned Production", bn: "পরিকল্পিত লক্ষ্যমাত্রা (Target)" },
        type: "number",
        default: "5000",
        min: 0.1,
        step: "1",
        unitOptions: [
          { value: "pcs", label: "Pieces (pcs)" },
          { value: "m", label: "Meters (m)" },
          { value: "kg", label: "Kilograms (kg)" },
          { value: "dz", label: "Dozens (dz)" }
        ],
        defaultUnit: "pcs",
        helper: { en: "Expected standard target for the shift", bn: "শিফটের নির্ধারিত স্ট্যান্ডার্ড লক্ষ্যমাত্রা" }
      }
    ],
    example: {
      actual_prod: "4250",
      actual_prod_unit: "pcs",
      target_prod: "5000",
      target_prod_unit: "pcs"
    },
    calculate: function (inputs, lang) {
      const act = parseFloat(inputs.actual_prod);
      const tgt = parseFloat(inputs.target_prod);

      if (isNaN(act) || isNaN(tgt)) {
        return { error: I18N[lang].errors.required };
      }
      if (act < 0 || tgt <= 0) {
        return { error: I18N[lang].errors.positive };
      }
      if (tgt === 0) {
        return { error: I18N[lang].errors.nonZero };
      }

      const effPct = (act / tgt) * 100.0;
      const variance = act - tgt;
      const unitLabel = inputs.actual_prod_unit;

      let statusClass = "status-excellent";
      let statusText = lang === "bn" ? "অসাধারণ দক্ষতা (World Class)" : "Outstanding Performance";

      if (effPct < 70) {
        statusClass = "status-danger";
        statusText = lang === "bn" ? "লক্ষ্যমাত্রার অনেক নিচে - ব্যবস্থা নিন" : "Substandard - Immediate Action Required";
      } else if (effPct < 85) {
        statusClass = "status-warning";
        statusText = lang === "bn" ? "উন্নতির সুযোগ রয়েছে (Average)" : "Average - Room for Improvement";
      } else if (effPct >= 100) {
        statusClass = "status-excellent";
        statusText = lang === "bn" ? "টার্গেট অতিক্রম করেছে (Target Exceeded)" : "Target Exceeded (+)";
      }

      return {
        primary: {
          label: lang === "bn" ? "অর্জিত দক্ষতা (Efficiency)" : "Achieved Efficiency",
          value: effPct.toFixed(2),
          unit: "%"
        },
        status: {
          class: statusClass,
          text: statusText
        },
        secondary: [
          {
            label: lang === "bn" ? "লক্ষ্যমাত্রার পার্থক্য" : "Target Variance",
            value: (variance >= 0 ? "+" : "") + variance.toFixed(0),
            unit: unitLabel
          },
          {
            label: lang === "bn" ? "ঘাটতি শতকরা হার" : "Shortfall Pct",
            value: effPct < 100 ? `-${(100 - effPct).toFixed(2)}%` : `+${(effPct - 100).toFixed(2)}%`,
            unit: ""
          }
        ],
        formula: {
          en: "Efficiency % = (Actual Production / Target Production) × 100\nVariance = Actual Production - Target Production",
          bn: "দক্ষতা % = (প্রকৃত উৎপাদন ÷ টার্গেট উৎপাদন) × ১০০\nপার্থক্য = প্রকৃত উৎপাদন - টার্গেট উৎপাদন"
        },
        steps: [
          {
            title: { en: "Step 1: Divide actual achieved production by target", bn: "ধাপ ১: প্রকৃত উৎপাদনকে টার্গেট দিয়ে ভাগ" },
            calc: `Ratio = ${act} / ${tgt} = ${(act / tgt).toFixed(4)}`
          },
          {
            title: { en: "Step 2: Multiply by 100 to get efficiency percentage", bn: "ধাপ ২: ১০০ দিয়ে গুণ করে শতকরা মান নির্ধারণ" },
            calc: `Efficiency % = ${(act / tgt).toFixed(4)} × 100 = ${effPct.toFixed(2)}%`
          },
          {
            title: { en: "Step 3: Calculate production shortfall or surplus", bn: "ধাপ ৩: উৎপাদন ঘাটতি বা উদ্বৃত্ত হিসাব" },
            calc: `Variance = ${act} - ${tgt} = ${(variance >= 0 ? "+" : "") + variance} ${unitLabel}`
          }
        ],
        explanation: {
          en: "Overall production efficiency benchmarks determine labor productivity, factory operational cost, and capacity planning. World-class apparel and textile factories aim for sustained efficiencies above 85%.",
          bn: "উৎপাদন দক্ষতা সূচক কারখানার সার্বিক উৎপাদনশীলতা, শ্রমিক খরচ এবং সময়মতো ডেলিভারি নিশ্চিত করতে অপরিহার্য। শীর্ষস্থানীয় টেক্সটাইল ও পোশাক কারখানাগুলো সাধারণত ৮৫% বা তার বেশি দক্ষতায় কাজ পরিচালনা করে।"
        }
      };
    }
  },

  // --------------------------------------------------------------------------
  // 10. FABRIC CONSUMPTION CALCULATOR (GARMENTS)
  // --------------------------------------------------------------------------
  {
    id: "fabric-consumption",
    category: "garment",
    icon: "👔",
    title: {
      en: "Fabric Consumption & Booking",
      bn: "পোশাকের ফেব্রিক কনজাম্পশন ক্যালকুলেটর"
    },
    description: {
      en: "Calculate net, wastage, and gross fabric booking requirements (kg or meters) for bulk apparel production orders.",
      bn: "গার্মেন্টস বাল্ক অর্ডারের জন্য নেট ফেব্রিক, ওয়েস্টেজ এবং মোট বুকিং ফেব্রিকের পরিমাণ (কেজি বা মিটার) নির্ণয় করুন।"
    },
    tags: ["consumption", "garment", "booking", "wastage", "kg/dz", "order", "মার্চেন্ডাইজিং", "কনজাম্পশন", "পোশাক"],
    inputs: [
      {
        id: "order_qty",
        label: { en: "Order Quantity", bn: "অর্ডারের মোট পরিমাণ" },
        type: "number",
        default: "10000",
        min: 1,
        step: "10",
        unitOptions: [
          { value: "pcs", label: "Pieces (pcs)" },
          { value: "dz", label: "Dozens (dz)" }
        ],
        defaultUnit: "pcs",
        helper: { en: "Total order pieces to be produced", bn: "মোট প্রস্তুতব্য পোশাকের সংখ্যা" }
      },
      {
        id: "consumption",
        label: { en: "Consumption per Garment / Dozen", bn: "প্রতি পোশাক বা ডজনে কনজাম্পশন" },
        type: "number",
        default: "0.22",
        min: 0.001,
        step: "0.01",
        unitOptions: [
          { value: "kg_pc", label: "kg / piece" },
          { value: "kg_dz", label: "kg / dozen" },
          { value: "m_pc", label: "meters / piece" },
          { value: "yd_pc", label: "yards / piece" }
        ],
        defaultUnit: "kg_pc",
        helper: { en: "Pattern marker consumption allowance", bn: "প্যাটার্ন মার্কার থেকে প্রাপ্ত কনজাম্পশন" }
      },
      {
        id: "wastage_pct",
        label: { en: "Wastage Allowance (%)", bn: "ওয়েস্টেজ বা অপচয় ভাতা (%)" },
        type: "number",
        default: "5",
        min: 0,
        max: 50,
        step: "0.5",
        unitAddon: "%",
        helper: { en: "Allowance for cutting end-bits, shrinkage, and rejections (typically 3% - 7%)", bn: "কাটিং ওয়েস্টেজ, পিন হোল, রিজেকশন ভাতা (সাধারণত ৩% - ৭%)" }
      }
    ],
    example: {
      order_qty: "10000",
      order_qty_unit: "pcs",
      consumption: "0.22",
      consumption_unit: "kg_pc",
      wastage_pct: "5"
    },
    calculate: function (inputs, lang) {
      const qtyRaw = parseFloat(inputs.order_qty);
      const consRaw = parseFloat(inputs.consumption);
      const wasteRaw = parseFloat(inputs.wastage_pct);

      if (isNaN(qtyRaw) || isNaN(consRaw) || isNaN(wasteRaw)) {
        return { error: I18N[lang].errors.required };
      }
      if (qtyRaw <= 0 || consRaw <= 0 || wasteRaw < 0) {
        return { error: I18N[lang].errors.positive };
      }

      // Convert quantity to pieces
      const totalPcs = inputs.order_qty_unit === "dz" ? qtyRaw * 12 : qtyRaw;

      // Normalize consumption to per piece
      let consPerPc = consRaw;
      let unitLabel = "kg";

      if (inputs.consumption_unit === "kg_dz") {
        consPerPc = consRaw / 12.0;
        unitLabel = "kg";
      } else if (inputs.consumption_unit === "m_pc") {
        consPerPc = consRaw;
        unitLabel = "meters";
      } else if (inputs.consumption_unit === "yd_pc") {
        consPerPc = consRaw;
        unitLabel = "yards";
      }

      const netFabric = totalPcs * consPerPc;
      const wastageAmount = netFabric * (wasteRaw / 100.0);
      const grossFabric = netFabric + wastageAmount;

      return {
        primary: {
          label: lang === "bn" ? "মোট গ্রস বুকিং প্রয়োজন" : "Gross Fabric Required",
          value: grossFabric.toFixed(2),
          unit: unitLabel
        },
        secondary: [
          {
            label: lang === "bn" ? "নেট প্রয়োজনীয় ফেব্রিক" : "Net Fabric (CAD/Marker)",
            value: netFabric.toFixed(2),
            unit: unitLabel
          },
          {
            label: lang === "bn" ? `ওয়েস্টেজ ভাতা (${wasteRaw}%)` : `Wastage Fabric (${wasteRaw}%)`,
            value: wastageAmount.toFixed(2),
            unit: unitLabel
          },
          {
            label: lang === "bn" ? "প্রতি পোশাকে গ্রস খরচ" : "Gross Cons. / Garment",
            value: (grossFabric / totalPcs).toFixed(4),
            unit: `${unitLabel}/pc`
          }
        ],
        formula: {
          en: "• Net Fabric = Total Garment Quantity × Consumption per piece\n• Wastage Fabric = Net Fabric × (Wastage % / 100)\n• Gross Booking = Net Fabric + Wastage Fabric",
          bn: "• নেট ফেব্রিক = মোট পোশাকের সংখ্যা × প্রতি পোশাকের কনজাম্পশন\n• ওয়েস্টেজ ফেব্রিক = নেট ফেব্রিক × (ওয়েস্টেজ % ÷ ১০০)\n• মোট গ্রস বুকিং = নেট ফেব্রিক + ওয়েস্টেজ ফেব্রিক"
        },
        steps: [
          {
            title: { en: "Step 1: Calculate total net fabric based on order pieces", bn: "ধাপ ১: মোট পিসের ওপর ভিত্তি করে নেট ফেব্রিক নির্ণয়" },
            calc: `Net = ${totalPcs.toLocaleString()} pcs × ${consPerPc.toFixed(4)} ${unitLabel}/pc = ${netFabric.toFixed(2)} ${unitLabel}`
          },
          {
            title: { en: `Step 2: Add ${wasteRaw}% cutting and process wastage allowance`, bn: `ধাপ ২: ${wasteRaw}% কাটিং ও প্রসেস ওয়েস্টেজ যোগ` },
            calc: `Wastage = ${netFabric.toFixed(2)} × (${wasteRaw} / 100) = ${wastageAmount.toFixed(2)} ${unitLabel}`
          },
          {
            title: { en: "Step 3: Sum Net + Wastage for total factory booking", bn: "ধাপ ৩: নেট এবং ওয়েস্টেজ যোগ করে গ্রস বুকিং নির্ধারণ" },
            calc: `Total Booking = ${netFabric.toFixed(2)} + ${wastageAmount.toFixed(2)} = ${grossFabric.toFixed(2)} ${unitLabel}`
          }
        ],
        explanation: {
          en: "In apparel merchandising, accurate fabric booking avoids both catastrophic fabric shortfalls (line starvation) and costly surplus dead-stock. Wastage allowances account for cutting lay ends, shrinkage variation, and fabric test cuttings.",
          bn: "গার্মেন্টস মার্চেন্ডাইজিংয়ে সঠিক ফেব্রিক বুকিং অত্যন্ত সংবেদনশীল। অতিরিক্ত বুকিং দিলে কারখানার অর্থ অপচয় হয়, আবার কম বুকিং দিলে অর্ডার শর্ট পড়ে। কাটিংয়ের শেষাংশ, প্রিন্ট/এমব্রয়ডারি রিজেকশন এবং ওয়াশ টেস্টের ক্ষতি পোষাতে ওয়েস্টেজ ভাতা যোগ করা হয়।"
        }
      };
    }
  }
];

// ------------------------------------------------------------------------------
// 3. FULL 63 TEXTILE CALCULATOR SUITE ARCHITECTURE REGISTRY
// ------------------------------------------------------------------------------
const FULL_63_CATALOG = [
  {
    category: "fabric",
    categoryTitle: { en: "FABRIC CALCULATORS", bn: "ফেব্রিক ক্যালকুলেটর" },
    items: [
      { id: "gsm", name: "1. GSM Calculator", active: true },
      { id: "fabric-weight", name: "2. Fabric Weight Calculator", active: true },
      { id: "fabric-length", name: "3. Fabric Length Calculator", active: false },
      { id: "fabric-width", name: "4. Fabric Width Calculator", active: false },
      { id: "fabric-area", name: "5. Fabric Area Calculator", active: false },
      { id: "gsm-conversion", name: "6. GSM Conversion (oz/yd²)", active: false },
      { id: "meter-to-kg", name: "7. Meter to Kg Calculator", active: false },
      { id: "kg-to-meter", name: "8. Kg to Meter Calculator", active: false },
      { id: "fabric-consumption", name: "9. Fabric Consumption", active: true },
      { id: "shrinkage", name: "10. Shrinkage Calculator", active: true }
    ]
  },
  {
    category: "yarn",
    categoryTitle: { en: "YARN CALCULATORS", bn: "সুতা ক্যালকুলেটর" },
    items: [
      { id: "yarn-count", name: "11. Yarn Count Calculator", active: true },
      { id: "ne-to-tex", name: "12. Ne to Tex Converter", active: false },
      { id: "tex-to-ne", name: "13. Tex to Ne Converter", active: false },
      { id: "denier-to-tex", name: "14. Denier to Tex Converter", active: false },
      { id: "tex-to-denier", name: "15. Tex to Denier Converter", active: false },
      { id: "nm-to-ne", name: "16. Nm to Ne Converter", active: false },
      { id: "ne-to-nm", name: "17. Ne to Nm Converter", active: false },
      { id: "yarn-weight", name: "18. Yarn Weight Calculator", active: false },
      { id: "yarn-length", name: "19. Yarn Length Calculator", active: false },
      { id: "yarn-consumption", name: "20. Yarn Consumption", active: false }
    ]
  },
  {
    category: "dyeing",
    categoryTitle: { en: "DYEING CALCULATORS", bn: "ডাইং ক্যালকুলেটর" },
    items: [
      { id: "dye-chem", name: "21. Dye Percentage Calculator", active: true },
      { id: "chem-percentage", name: "22. Chemical Percentage", active: false },
      { id: "liquor-ratio", name: "23. Liquor Ratio Calculator", active: true },
      { id: "dyeing-bath-volume", name: "24. Dyeing Bath Volume", active: false },
      { id: "salt-requirement", name: "25. Salt Requirement", active: false },
      { id: "soda-requirement", name: "26. Soda Requirement", active: false },
      { id: "caustic-requirement", name: "27. Caustic Requirement", active: false },
      { id: "chem-dosage", name: "28. Chemical Dosage (g/L)", active: false },
      { id: "stock-solution", name: "29. Stock Solution Calculator", active: false },
      { id: "total-chem", name: "30. Total Chemical Requirement", active: false }
    ]
  },
  {
    category: "finishing",
    categoryTitle: { en: "FINISHING CALCULATORS", bn: "ফিনিশিং ক্যালকুলেটর" },
    items: [
      { id: "stenter-overfeed", name: "31. Stenter Overfeed Calculator", active: true },
      { id: "stenter-width", name: "32. Stenter Width Calculator", active: false },
      { id: "length-shrinkage", name: "33. Length Shrinkage", active: false },
      { id: "width-shrinkage", name: "34. Width Shrinkage", active: false },
      { id: "gsm-before-after", name: "35. GSM Before/After Finishing", active: false },
      { id: "chemical-pick-up", name: "36. Chemical Pick-up", active: false },
      { id: "wet-pick-up", name: "37. Wet Pick-up", active: false },
      { id: "softener-dosage", name: "38. Softener Dosage", active: false },
      { id: "resin-dosage", name: "39. Resin Dosage", active: false },
      { id: "finishing-chem", name: "40. Finishing Chemical Requirement", active: false }
    ]
  },
  {
    category: "production",
    categoryTitle: { en: "PRODUCTION CALCULATORS", bn: "উৎপাদন ক্যালকুলেটর" },
    items: [
      { id: "production", name: "41. Machine Production", active: true },
      { id: "prod-per-hour", name: "42. Production per Hour", active: false },
      { id: "prod-per-shift", name: "43. Production per Shift", active: false },
      { id: "prod-per-day", name: "44. Production per Day", active: false },
      { id: "machine-efficiency", name: "45. Machine Efficiency", active: false },
      { id: "efficiency", name: "46. Production Efficiency", active: true },
      { id: "machine-speed", name: "47. Machine Speed Calculator", active: false },
      { id: "stenter-production", name: "48. Stenter Production", active: false },
      { id: "dyeing-machine-prod", name: "49. Dyeing Machine Production", active: false }
    ]
  },
  {
    category: "quality",
    categoryTitle: { en: "QUALITY CALCULATORS", bn: "কোয়ালিটি ক্যালকুলেটর" },
    items: [
      { id: "defect-percentage", name: "50. Defect Percentage", active: false },
      { id: "rejection-percentage", name: "51. Rejection Percentage", active: false },
      { id: "first-quality-pct", name: "52. First Quality Percentage", active: false },
      { id: "dhu", name: "53. Defects per Hundred Units (DHU)", active: false },
      { id: "aql-calc", name: "54. AQL Calculation", active: false },
      { id: "inspection-qty", name: "55. Inspection Quantity", active: false },
      { id: "gsm-variation", name: "56. GSM Variation Calculator", active: false }
    ]
  },
  {
    category: "garment",
    categoryTitle: { en: "GARMENT CALCULATORS", bn: "গার্মেন্টস ক্যালকুলেটর" },
    items: [
      { id: "fabric-consumption", name: "57. Fabric Consumption", active: true },
      { id: "marker-efficiency", name: "58. Marker Efficiency", active: false },
      { id: "marker-length", name: "59. Marker Length", active: false },
      { id: "garment-costing", name: "60. Garment Costing", active: false },
      { id: "sam-calc", name: "61. Standard Allowed Minute (SAM)", active: false },
      { id: "line-efficiency", name: "62. Line Efficiency", active: false },
      { id: "production-target", name: "63. Production Target", active: false }
    ]
  }
];

// ------------------------------------------------------------------------------
// 4. APPLICATION STATE & LOCAL STORAGE KEYS
// ------------------------------------------------------------------------------
const STORAGE_KEYS = {
  THEME: "textile_calc_theme",
  LANG: "textile_calc_lang",
  FAVORITES: "textile_calc_favorites",
  HISTORY: "textile_calc_history"
};

const AppState = {
  lang: "en",
  theme: "dark",
  currentCategory: "all",
  searchQuery: "",
  activeCalculatorId: null,
  favorites: [],
  history: []
};

// ------------------------------------------------------------------------------
// 5. DOM ELEMENTS CACHE
// ------------------------------------------------------------------------------
const DOM = {
  html: document.documentElement,
  brandLogo: document.getElementById("brandLogo"),
  langToggleBtn: document.getElementById("langToggleBtn"),
  langLabel: document.getElementById("langLabel"),
  themeToggleBtn: document.getElementById("themeToggleBtn"),
  favoritesNavBtn: document.getElementById("favoritesNavBtn"),
  favCountBadge: document.getElementById("favCountBadge"),
  historyNavBtn: document.getElementById("historyNavBtn"),
  historyCountBadge: document.getElementById("historyCountBadge"),
  searchInput: document.getElementById("searchInput"),
  clearSearchBtn: document.getElementById("clearSearchBtn"),
  categoryTabs: document.getElementById("categoryTabs"),
  directoryView: document.getElementById("directoryView"),
  calculatorView: document.getElementById("calculatorView"),
  calculatorsGrid: document.getElementById("calculatorsGrid"),
  noResultsState: document.getElementById("noResultsState"),
  resetSearchBtn: document.getElementById("resetSearchBtn"),
  currentCategoryTitle: document.getElementById("currentCategoryTitle"),
  resultsCount: document.getElementById("resultsCount"),
  backToDirectoryBtn: document.getElementById("backToDirectoryBtn"),
  calcFavToggleBtn: document.getElementById("calcFavToggleBtn"),
  copyShareBtn: document.getElementById("copyShareBtn"),
  activeCalcContainer: document.getElementById("activeCalcContainer"),
  historyDrawer: document.getElementById("historyDrawer"),
  closeHistoryBtn: document.getElementById("closeHistoryBtn"),
  clearAllHistoryBtn: document.getElementById("clearAllHistoryBtn"),
  historyList: document.getElementById("historyList"),
  drawerHistoryBadge: document.getElementById("drawerHistoryBadge"),
  drawerBackdrop: document.getElementById("drawerBackdrop"),
  toastContainer: document.getElementById("toastContainer"),
  viewRoadmapBtn: document.getElementById("viewRoadmapBtn"),
  roadmapModal: document.getElementById("roadmapModal"),
  closeRoadmapBtn: document.getElementById("closeRoadmapBtn"),
  roadmapContent: document.getElementById("roadmapContent")
};

// ------------------------------------------------------------------------------
// 6. INITIALIZATION & STORAGE HELPERS
// ------------------------------------------------------------------------------
function initApp() {
  loadSavedPreferences();
  bindGlobalEvents();
  renderCategoryPills();
  renderCalculatorsGrid();
  renderRoadmapContent();
  updateHistoryBadges();
  updateFavoritesBadges();

  // Check URL hash for direct calculator deep-link (e.g. #calc=gsm)
  handleHashNavigation();
  window.addEventListener("hashchange", handleHashNavigation);
}

function loadSavedPreferences() {
  // Theme
  const savedTheme = localStorage.getItem(STORAGE_KEYS.THEME) || "dark";
  AppState.theme = savedTheme;
  DOM.html.setAttribute("data-theme", savedTheme);

  // Language
  const savedLang = localStorage.getItem(STORAGE_KEYS.LANG) || "en";
  AppState.lang = savedLang;
  DOM.langLabel.textContent = savedLang === "en" ? "বাংলা" : "English";
  updateUILanguageText();

  // Favorites
  try {
    const savedFavs = JSON.parse(localStorage.getItem(STORAGE_KEYS.FAVORITES)) || [];
    AppState.favorites = Array.isArray(savedFavs) ? savedFavs : [];
  } catch (e) {
    AppState.favorites = [];
  }

  // History
  try {
    const savedHist = JSON.parse(localStorage.getItem(STORAGE_KEYS.HISTORY)) || [];
    AppState.history = Array.isArray(savedHist) ? savedHist : [];
  } catch (e) {
    AppState.history = [];
  }
}

function saveHistory() {
  localStorage.setItem(STORAGE_KEYS.HISTORY, JSON.stringify(AppState.history));
  updateHistoryBadges();
}

function saveFavorites() {
  localStorage.setItem(STORAGE_KEYS.FAVORITES, JSON.stringify(AppState.favorites));
  updateFavoritesBadges();
}

// ------------------------------------------------------------------------------
// 7. LANGUAGE SWITCHER LOGIC
// ------------------------------------------------------------------------------
function toggleLanguage() {
  AppState.lang = AppState.lang === "en" ? "bn" : "en";
  localStorage.setItem(STORAGE_KEYS.LANG, AppState.lang);
  DOM.langLabel.textContent = AppState.lang === "en" ? "বাংলা" : "English";

  updateUILanguageText();
  renderCategoryPills();
  renderCalculatorsGrid();
  renderRoadmapContent();

  // Re-render active calculator if open
  if (AppState.activeCalculatorId) {
    renderActiveCalculator(AppState.activeCalculatorId);
  }

  // Re-render history drawer if open
  if (DOM.historyDrawer.classList.contains("open")) {
    renderHistoryList();
  }
}

function updateUILanguageText() {
  const dict = I18N[AppState.lang];

  document.querySelectorAll("[data-i18n]").forEach(elem => {
    const key = elem.getAttribute("data-i18n");
    if (dict[key]) {
      elem.textContent = dict[key];
    }
  });

  document.querySelectorAll("[data-i18n-placeholder]").forEach(elem => {
    const key = elem.getAttribute("data-i18n-placeholder");
    if (dict[key]) {
      elem.placeholder = dict[key];
    }
  });
}

// ------------------------------------------------------------------------------
// 8. THEME TOGGLER
// ------------------------------------------------------------------------------
function toggleTheme() {
  AppState.theme = AppState.theme === "dark" ? "light" : "dark";
  DOM.html.setAttribute("data-theme", AppState.theme);
  localStorage.setItem(STORAGE_KEYS.THEME, AppState.theme);
}

// ------------------------------------------------------------------------------
// 9. CATEGORY PILLS RENDERING
// ------------------------------------------------------------------------------
function renderCategoryPills() {
  const catCounts = {
    all: CALCULATORS.length,
    fabric: 0,
    yarn: 0,
    dyeing: 0,
    finishing: 0,
    production: 0,
    quality: 0,
    garment: 0,
    favorites: AppState.favorites.length
  };

  CALCULATORS.forEach(calc => {
    if (catCounts[calc.category] !== undefined) {
      catCounts[calc.category]++;
    }
  });

  document.getElementById("countAll").textContent = catCounts.all;
  document.getElementById("countFabric").textContent = catCounts.fabric;
  document.getElementById("countYarn").textContent = catCounts.yarn;
  document.getElementById("countDyeing").textContent = catCounts.dyeing;
  document.getElementById("countFinishing").textContent = catCounts.finishing;
  document.getElementById("countProduction").textContent = catCounts.production;
  document.getElementById("countQuality").textContent = catCounts.quality;
  document.getElementById("countGarment").textContent = catCounts.garment;
  document.getElementById("countFavorites").textContent = catCounts.favorites;
}

// ------------------------------------------------------------------------------
// 10. DIRECTORY & SEARCH RENDERING
// ------------------------------------------------------------------------------
function filterCalculators() {
  const q = AppState.searchQuery.trim().toLowerCase();
  const cat = AppState.currentCategory;

  return CALCULATORS.filter(calc => {
    // Category filter
    if (cat === "favorites") {
      if (!AppState.favorites.includes(calc.id)) return false;
    } else if (cat !== "all" && calc.category !== cat) {
      return false;
    }

    // Search query filter
    if (q) {
      const titleEn = calc.title.en.toLowerCase();
      const titleBn = calc.title.bn.toLowerCase();
      const descEn = calc.description.en.toLowerCase();
      const descBn = calc.description.bn.toLowerCase();
      const tags = calc.tags.join(" ").toLowerCase();

      const match = titleEn.includes(q) || titleBn.includes(q) || descEn.includes(q) || descBn.includes(q) || tags.includes(q);
      if (!match) return false;
    }

    return true;
  });
}

function renderCalculatorsGrid() {
  const filtered = filterCalculators();
  const dict = I18N[AppState.lang];

  DOM.calculatorsGrid.innerHTML = "";

  if (filtered.length === 0) {
    DOM.calculatorsGrid.style.display = "none";
    DOM.noResultsState.style.display = "block";
    DOM.resultsCount.textContent = `0 ${dict.availableBadge}`;
    return;
  }

  DOM.calculatorsGrid.style.display = "grid";
  DOM.noResultsState.style.display = "none";
  DOM.resultsCount.textContent = `${filtered.length} ${dict.availableBadge}`;

  filtered.forEach(calc => {
    const isFav = AppState.favorites.includes(calc.id);
    const card = document.createElement("article");
    card.className = "calc-card";
    card.setAttribute("tabindex", "0");
    card.setAttribute("role", "button");

    card.innerHTML = `
      <div>
        <div class="calc-card-top">
          <span class="card-cat-badge">${calc.category}</span>
          <button class="card-fav-btn ${isFav ? "active" : ""}" data-id="${calc.id}" aria-label="Toggle Favorite" title="Bookmark">
            ${isFav ? "★" : "☆"}
          </button>
        </div>
        <div class="calc-card-body">
          <h3 class="calc-card-title">
            <span class="card-title-icon">${calc.icon}</span>
            <span>${calc.title[AppState.lang]}</span>
          </h3>
          <p class="calc-card-desc">${calc.description[AppState.lang]}</p>
        </div>
      </div>
      <div class="calc-card-footer">
        <div class="card-tags">
          ${calc.tags.slice(0, 3).map(t => `<span class="tag-mini">#${t}</span>`).join("")}
        </div>
        <div class="btn-card-launch">
          <span>${dict.calculateBtn}</span>
          <span>→</span>
        </div>
      </div>
    `;

    // Click on entire card opens the calculator
    card.addEventListener("click", (e) => {
      if (e.target.closest(".card-fav-btn")) return;
      openCalculator(calc.id);
    });

    // Keyboard enter opens
    card.addEventListener("keydown", (e) => {
      if (e.key === "Enter" || e.key === " ") {
        if (!e.target.closest(".card-fav-btn")) {
          e.preventDefault();
          openCalculator(calc.id);
        }
      }
    });

    // Favorite star handler
    const favBtn = card.querySelector(".card-fav-btn");
    favBtn.addEventListener("click", (e) => {
      e.stopPropagation();
      toggleFavorite(calc.id);
      renderCalculatorsGrid();
      renderCategoryPills();
    });

    DOM.calculatorsGrid.appendChild(card);
  });
}

// ------------------------------------------------------------------------------
// 11. ACTIVE CALCULATOR WORKSPACE
// ------------------------------------------------------------------------------
function openCalculator(id) {
  const calc = CALCULATORS.find(c => c.id === id);
  if (!calc) return;

  AppState.activeCalculatorId = id;
  window.location.hash = `calc=${id}`;

  // Switch view
  DOM.directoryView.style.display = "none";
  DOM.calculatorView.style.display = "block";
  window.scrollTo({ top: 0, behavior: "smooth" });

  // Update Fav status button in top bar
  const isFav = AppState.favorites.includes(id);
  DOM.calcFavToggleBtn.classList.toggle("active", isFav);
  DOM.calcFavToggleBtn.querySelector(".fav-icon").textContent = isFav ? "★" : "☆";

  renderActiveCalculator(id);
}

function closeCalculator() {
  AppState.activeCalculatorId = null;
  window.location.hash = "";
  DOM.calculatorView.style.display = "none";
  DOM.directoryView.style.display = "block";
  renderCalculatorsGrid();
}

function renderActiveCalculator(id) {
  const calc = CALCULATORS.find(c => c.id === id);
  if (!calc) return;

  const dict = I18N[AppState.lang];
  const container = DOM.activeCalcContainer;

  // Build HTML for calculator form
  let fieldsHtml = "";
  calc.inputs.forEach(field => {
    let unitControl = "";

    if (field.unitOptions && field.unitOptions.length > 0) {
      unitControl = `
        <select id="${field.id}_unit" class="unit-select" aria-label="${field.label[AppState.lang]} Unit">
          ${field.unitOptions.map(opt => `<option value="${opt.value}" ${opt.value === field.defaultUnit ? "selected" : ""}>${opt.label}</option>`).join("")}
        </select>
      `;
    } else if (field.unitAddon) {
      unitControl = `<span class="unit-addon">${field.unitAddon}</span>`;
    }

    if (field.type === "select") {
      fieldsHtml += `
        <div class="form-group" id="group_${field.id}">
          <label class="form-label" for="${field.id}">
            <span>${field.label[AppState.lang]} <span class="field-required">*</span></span>
          </label>
          <div class="input-unit-group">
            <select id="${field.id}" class="form-input" style="background:transparent; cursor:pointer;">
              ${field.options.map(opt => `<option value="${opt.value}" ${opt.value === field.default ? "selected" : ""}>${opt.label}</option>`).join("")}
            </select>
          </div>
          ${field.helper ? `<span class="field-helper">${field.helper[AppState.lang]}</span>` : ""}
          <span class="field-error-msg" id="err_${field.id}"></span>
        </div>
      `;
    } else {
      fieldsHtml += `
        <div class="form-group" id="group_${field.id}">
          <label class="form-label" for="${field.id}">
            <span>${field.label[AppState.lang]} <span class="field-required">*</span></span>
          </label>
          <div class="input-unit-group">
            <input 
              type="number" 
              id="${field.id}" 
              class="form-input" 
              value="${field.default}" 
              step="${field.step || "any"}" 
              ${field.min !== undefined ? `min="${field.min}"` : ""}
              ${field.max !== undefined ? `max="${field.max}"` : ""}
              inputmode="decimal"
              placeholder="0.00"
            />
            ${unitControl}
          </div>
          ${field.helper ? `<span class="field-helper">${field.helper[AppState.lang]}</span>` : ""}
          <span class="field-error-msg" id="err_${field.id}"></span>
        </div>
      `;
    }
  });

  container.innerHTML = `
    <!-- Calculator Header -->
    <div class="calc-header-block">
      <div class="calc-header-meta">
        <span class="card-cat-badge">${calc.category}</span>
        <span class="badge-mini">Deterministic Math</span>
      </div>
      <h2 class="calc-title-main">
        <span>${calc.icon}</span>
        <span>${calc.title[AppState.lang]}</span>
      </h2>
      <p class="calc-desc-main">${calc.description[AppState.lang]}</p>
    </div>

    <!-- Dynamic Form -->
    <form class="calc-form" id="activeForm" novalidate>
      <div class="form-grid ${calc.inputs.length >= 3 ? "cols-3" : "cols-2"}">
        ${fieldsHtml}
      </div>

      <div class="form-actions">
        <button type="submit" class="btn btn-primary" id="btnRunCalculate">
          <span>⚡</span>
          <span>${dict.calculateBtn}</span>
        </button>
        <button type="button" class="btn btn-secondary" id="btnClearInputs">
          <span>✕</span>
          <span>${dict.clearBtn}</span>
        </button>
        <button type="button" class="btn btn-example" id="btnFillExample">
          <span>💡</span>
          <span>${dict.useExampleBtn}</span>
        </button>
      </div>
    </form>

    <!-- Error Alert Container -->
    <div id="calcErrorBanner" class="calc-error-banner" style="display:none;"></div>

    <!-- Output Section (Dynamically Loaded after calculation) -->
    <div id="calcOutputSection" class="results-section"></div>
  `;

  // Bind Form Events
  const form = document.getElementById("activeForm");
  form.addEventListener("submit", (e) => {
    e.preventDefault();
    executeActiveCalculation(calc);
  });

  document.getElementById("btnClearInputs").addEventListener("click", () => {
    clearActiveInputs(calc);
  });

  document.getElementById("btnFillExample").addEventListener("click", () => {
    fillExampleValues(calc);
  });

  // Calculate immediately with default values for optimal UX
  executeActiveCalculation(calc, false);
}

// ------------------------------------------------------------------------------
// 12. CALCULATION EXECUTION & RESULTS PRESENTATION
// ------------------------------------------------------------------------------
function executeActiveCalculation(calc, recordInHistory = true) {
  const dict = I18N[AppState.lang];
  const errorBanner = document.getElementById("calcErrorBanner");
  const outputSection = document.getElementById("calcOutputSection");

  // Reset errors
  errorBanner.style.display = "none";
  errorBanner.textContent = "";
  calc.inputs.forEach(f => {
    const group = document.getElementById(`group_${f.id}`);
    const errSpan = document.getElementById(`err_${f.id}`);
    if (group) group.classList.remove("has-error");
    if (errSpan) errSpan.textContent = "";
  });

  // Collect input values
  const inputValues = {};
  calc.inputs.forEach(field => {
    const inputElem = document.getElementById(field.id);
    if (inputElem) {
      inputValues[field.id] = inputElem.value;
    }
    const unitElem = document.getElementById(`${field.id}_unit`);
    if (unitElem) {
      inputValues[`${field.id}_unit`] = unitElem.value;
    }
  });

  // Execute pure calculation function
  const result = calc.calculate(inputValues, AppState.lang);

  if (result.error) {
    errorBanner.style.display = "flex";
    errorBanner.textContent = `⚠️ ${result.error}`;
    outputSection.innerHTML = "";
    return;
  }

  // Render Result Cards
  let secondaryMetricsHtml = "";
  if (result.secondary && result.secondary.length > 0) {
    secondaryMetricsHtml = `
      <div class="secondary-metrics-grid">
        ${result.secondary.map(m => `
          <div class="metric-card">
            <span class="metric-label">${m.label}</span>
            <span class="metric-value">${m.value} <small style="font-size:0.75rem; color:var(--text-secondary);">${m.unit}</small></span>
          </div>
        `).join("")}
      </div>
    `;
  }

  // Warning Banner (e.g. Stenter overfeed disclaimer, etc.)
  let warningHtml = "";
  if (result.warning) {
    warningHtml = `
      <div class="factory-warning-box">
        <div class="warning-icon">⚠️</div>
        <div class="warning-content">
          <h4>${AppState.lang === "bn" ? "কারখানা ও ইঞ্জিনিয়ারিং সতর্কতা" : "Factory & Process Notice"}</h4>
          <p>${result.warning[AppState.lang] || result.warning.en}</p>
        </div>
      </div>
    `;
  }

  // Step-by-Step Calculation List
  let stepsHtml = "";
  if (result.steps && result.steps.length > 0) {
    stepsHtml = `
      <div class="detail-card">
        <div class="detail-header">
          <span style="font-size:1.1rem;">📝</span>
          <h3 class="detail-title">${dict.stepsHeading}</h3>
        </div>
        <div class="steps-list">
          ${result.steps.map((s, idx) => `
            <div class="step-item">
              <span class="step-number">${idx + 1}</span>
              <div class="step-content">
                <div class="step-heading">${s.title[AppState.lang]}</div>
                <div class="step-calc">${s.calc}</div>
              </div>
            </div>
          `).join("")}
        </div>
      </div>
    `;
  }

  // Mathematical Formula Card
  let formulaHtml = "";
  if (result.formula) {
    const fText = result.formula[AppState.lang] || result.formula.en;
    formulaHtml = `
      <div class="detail-card">
        <div class="detail-header">
          <span style="font-size:1.1rem;">📐</span>
          <h3 class="detail-title">${dict.formulaHeading}</h3>
        </div>
        <pre class="formula-display">${fText}</pre>
      </div>
    `;
  }

  // Bilingual Explanations
  let explanationHtml = "";
  if (result.explanation) {
    explanationHtml = `
      <div class="detail-card">
        <div class="detail-header">
          <span style="font-size:1.1rem;">💡</span>
          <h3 class="detail-title">${dict.technicalNotes}</h3>
        </div>
        <div class="explanation-box">
          <div>
            <div class="lang-tab-pill">🇬🇧 English</div>
            <p class="explanation-text">${result.explanation.en}</p>
          </div>
          <div class="explanation-divider"></div>
          <div>
            <div class="lang-tab-pill">🇧🇩 বাংলা বিবরণ</div>
            <p class="explanation-text">${result.explanation.bn}</p>
          </div>
        </div>
      </div>
    `;
  }

  // Status badge if available
  let statusHtml = "";
  if (result.status) {
    statusHtml = `<div class="result-hero-status ${result.status.class}">${result.status.text}</div>`;
  }

  outputSection.innerHTML = `
    <!-- Primary Hero Result -->
    <div class="result-hero-box">
      <div class="result-hero-label">${result.primary.label}</div>
      <div class="result-hero-value-wrap">
        <span class="result-hero-value" id="primaryResultValue">${result.primary.value}</span>
        <span class="result-hero-unit">${result.primary.unit}</span>
      </div>
      ${statusHtml}
      <div class="result-actions">
        <button id="btnCopyResult" class="btn-result-action" title="Copy Result">
          <span>📋</span>
          <span>${dict.copyResultBtn}</span>
        </button>
      </div>
    </div>

    <!-- Secondary Metrics -->
    ${secondaryMetricsHtml}

    <!-- Industrial Warning if any -->
    ${warningHtml}

    <!-- Technical Details Grid -->
    <div class="tech-details-container">
      ${formulaHtml}
      ${stepsHtml}
      ${explanationHtml}
    </div>
  `;

  // Bind Copy Button
  document.getElementById("btnCopyResult").addEventListener("click", () => {
    const copyText = `${calc.title[AppState.lang]}: ${result.primary.value} ${result.primary.unit}`;
    navigator.clipboard.writeText(copyText).then(() => {
      showToast(dict.copiedToast, "success");
    }).catch(() => {
      showToast(copyText, "info");
    });
  });

  // Add to History
  if (recordInHistory) {
    addToHistory(calc, inputValues, result);
  }
}

function clearActiveInputs(calc) {
  calc.inputs.forEach(field => {
    const el = document.getElementById(field.id);
    if (el) el.value = "";
  });
  const outputSection = document.getElementById("calcOutputSection");
  if (outputSection) outputSection.innerHTML = "";
  const err = document.getElementById("calcErrorBanner");
  if (err) err.style.display = "none";
}

function fillExampleValues(calc) {
  if (!calc.example) return;

  Object.keys(calc.example).forEach(key => {
    const elem = document.getElementById(key);
    if (elem) {
      elem.value = calc.example[key];
    }
  });

  // Run calculation immediately
  executeActiveCalculation(calc, true);
  showToast(AppState.lang === "bn" ? "নমুনা মান প্রদান করা হয়েছে" : "Sample values filled!", "info");
}

// ------------------------------------------------------------------------------
// 13. FAVORITES SYSTEM
// ------------------------------------------------------------------------------
function toggleFavorite(calcId) {
  const idx = AppState.favorites.indexOf(calcId);
  if (idx > -1) {
    AppState.favorites.splice(idx, 1);
    showToast(AppState.lang === "bn" ? "প্রিয় তালিকা থেকে সরানো হয়েছে" : "Removed from favorites", "info");
  } else {
    AppState.favorites.push(calcId);
    showToast(AppState.lang === "bn" ? "প্রিয় তালিকায় যোগ করা হয়েছে" : "Added to favorites", "success");
  }
  saveFavorites();
  updateFavoritesBadges();
}

function updateFavoritesBadges() {
  DOM.favCountBadge.textContent = AppState.favorites.length;
}

// ------------------------------------------------------------------------------
// 14. HISTORY SYSTEM (LocalStorage)
// ------------------------------------------------------------------------------
function addToHistory(calc, inputs, result) {
  const inputSummaryParts = [];
  calc.inputs.forEach(f => {
    const val = inputs[f.id];
    const unit = inputs[`${f.id}_unit`] || f.unitAddon || "";
    if (val !== undefined && val !== "") {
      inputSummaryParts.push(`${f.label.en}: ${val} ${unit}`.trim());
    }
  });

  const historyItem = {
    id: "hist_" + Date.now(),
    calcId: calc.id,
    calcTitle: calc.title,
    category: calc.category,
    inputs: inputs,
    summary: inputSummaryParts.join(" • "),
    result: `${result.primary.label}: ${result.primary.value} ${result.primary.unit}`,
    timestamp: new Date().toISOString()
  };

  // Prepend and limit to max 40 entries
  AppState.history.unshift(historyItem);
  if (AppState.history.length > 40) {
    AppState.history.pop();
  }

  saveHistory();
}

function renderHistoryList() {
  const dict = I18N[AppState.lang];
  DOM.historyList.innerHTML = "";

  if (AppState.history.length === 0) {
    DOM.historyList.innerHTML = `
      <div style="text-align:center; padding:40px 20px; color:var(--text-muted);">
        <div style="font-size:2.5rem; margin-bottom:8px;">⏱️</div>
        <p>${dict.historyEmpty}</p>
      </div>
    `;
    return;
  }

  AppState.history.forEach(item => {
    const card = document.createElement("div");
    card.className = "history-card";

    const dateStr = new Date(item.timestamp).toLocaleString(AppState.lang === "bn" ? "bn-BD" : "en-US", {
      month: "short",
      day: "numeric",
      hour: "2-digit",
      minute: "2-digit"
    });

    card.innerHTML = `
      <div class="history-card-header">
        <span class="history-calc-title">${item.calcTitle[AppState.lang]}</span>
        <span class="history-time">${dateStr}</span>
      </div>
      <div class="history-summary">${item.summary}</div>
      <div class="history-result-badge">${item.result}</div>
      <div class="history-card-actions">
        <button class="btn-hist-load" data-id="${item.id}">↪ ${dict.btnLoadHist}</button>
        <button class="btn-hist-del" data-id="${item.id}">🗑 ${dict.btnDelHist}</button>
      </div>
    `;

    // Load button
    card.querySelector(".btn-hist-load").addEventListener("click", () => {
      loadHistoryItem(item);
    });

    // Delete single item
    card.querySelector(".btn-hist-del").addEventListener("click", () => {
      deleteHistoryItem(item.id);
    });

    DOM.historyList.appendChild(card);
  });
}

function loadHistoryItem(item) {
  openCalculator(item.calcId);
  closeHistoryDrawer();

  // Populate inputs after open
  setTimeout(() => {
    Object.keys(item.inputs).forEach(key => {
      const el = document.getElementById(key);
      if (el) el.value = item.inputs[key];
    });
    const calc = CALCULATORS.find(c => c.id === item.calcId);
    if (calc) {
      executeActiveCalculation(calc, false);
      showToast(AppState.lang === "bn" ? "ইতিহাস থেকে লোড করা হয়েছে" : "Calculation loaded from history", "info");
    }
  }, 50);
}

function deleteHistoryItem(id) {
  AppState.history = AppState.history.filter(h => h.id !== id);
  saveHistory();
  renderHistoryList();
}

function clearAllHistory() {
  if (AppState.history.length === 0) return;
  AppState.history = [];
  saveHistory();
  renderHistoryList();
  showToast(I18N[AppState.lang].historyClearedToast, "info");
}

function updateHistoryBadges() {
  const count = AppState.history.length;
  DOM.historyCountBadge.textContent = count;
  DOM.drawerHistoryBadge.textContent = count;
}

function openHistoryDrawer() {
  renderHistoryList();
  DOM.historyDrawer.classList.add("open");
  DOM.historyDrawer.setAttribute("aria-hidden", "false");
  DOM.drawerBackdrop.style.display = "block";
}

function closeHistoryDrawer() {
  DOM.historyDrawer.classList.remove("open");
  DOM.historyDrawer.setAttribute("aria-hidden", "true");
  DOM.drawerBackdrop.style.display = "none";
}

// ------------------------------------------------------------------------------
// 15. ROADMAP MODAL (Full 63 Suite)
// ------------------------------------------------------------------------------
function renderRoadmapContent() {
  DOM.roadmapContent.innerHTML = "";

  FULL_63_CATALOG.forEach(cat => {
    const section = document.createElement("div");
    section.className = "roadmap-cat-section";

    const title = document.createElement("h4");
    title.className = "roadmap-cat-title";
    title.textContent = cat.categoryTitle[AppState.lang] || cat.categoryTitle.en;

    const grid = document.createElement("div");
    grid.className = "roadmap-items-grid";

    cat.items.forEach(item => {
      const itemEl = document.createElement("div");
      itemEl.className = `roadmap-item ${item.active ? "active-item" : ""}`;
      itemEl.innerHTML = `
        <span>${item.name}</span>
        <span class="roadmap-status-badge ${item.active ? "status-live" : "status-ready"}">
          ${item.active ? (AppState.lang === "bn" ? "সক্রিয়" : "Live") : (AppState.lang === "bn" ? "পরিকল্পিত" : "Planned")}
        </span>
      `;

      if (item.active) {
        itemEl.addEventListener("click", () => {
          DOM.roadmapModal.style.display = "none";
          openCalculator(item.id);
        });
      }

      grid.appendChild(itemEl);
    });

    section.appendChild(title);
    section.appendChild(grid);
    DOM.roadmapContent.appendChild(section);
  });
}

// ------------------------------------------------------------------------------
// 16. TOAST NOTIFICATION UTILITY
// ------------------------------------------------------------------------------
function showToast(message, type = "info") {
  const toast = document.createElement("div");
  toast.className = `toast ${type === "success" ? "toast-success" : type === "error" ? "toast-error" : ""}`;
  toast.innerHTML = `
    <span>${type === "success" ? "✓" : type === "error" ? "⚠️" : "ℹ️"}</span>
    <span>${message}</span>
  `;

  DOM.toastContainer.appendChild(toast);

  setTimeout(() => {
    toast.style.opacity = "0";
    toast.style.transform = "translateY(10px)";
    toast.style.transition = "all 0.3s ease";
    setTimeout(() => {
      if (toast.parentNode) {
        toast.parentNode.removeChild(toast);
      }
    }, 300);
  }, 2800);
}

// ------------------------------------------------------------------------------
// 17. URL DEEP LINK NAVIGATION
// ------------------------------------------------------------------------------
function handleHashNavigation() {
  const hash = window.location.hash;
  if (hash.startsWith("#calc=")) {
    const calcId = hash.replace("#calc=", "");
    if (CALCULATORS.some(c => c.id === calcId)) {
      openCalculator(calcId);
    }
  } else {
    if (AppState.activeCalculatorId) {
      closeCalculator();
    }
  }
}

// ------------------------------------------------------------------------------
// 18. GLOBAL EVENT BINDINGS
// ------------------------------------------------------------------------------
function bindGlobalEvents() {
  // Brand Logo Click -> Reset to directory
  DOM.brandLogo.addEventListener("click", () => {
    AppState.currentCategory = "all";
    AppState.searchQuery = "";
    DOM.searchInput.value = "";
    DOM.clearSearchBtn.style.display = "none";
    updateCategoryPillState("all");
    closeCalculator();
  });

  // Language Switcher
  DOM.langToggleBtn.addEventListener("click", toggleLanguage);

  // Theme Switcher
  DOM.themeToggleBtn.addEventListener("click", toggleTheme);

  // Favorites Nav Button
  DOM.favoritesNavBtn.addEventListener("click", () => {
    AppState.currentCategory = "favorites";
    updateCategoryPillState("favorites");
    if (AppState.activeCalculatorId) {
      closeCalculator();
    } else {
      renderCalculatorsGrid();
    }
  });

  // History Nav Button & Drawer
  DOM.historyNavBtn.addEventListener("click", openHistoryDrawer);
  DOM.closeHistoryBtn.addEventListener("click", closeHistoryDrawer);
  DOM.drawerBackdrop.addEventListener("click", closeHistoryDrawer);
  DOM.clearAllHistoryBtn.addEventListener("click", clearAllHistory);

  // Back button in active calculator workspace
  DOM.backToDirectoryBtn.addEventListener("click", closeCalculator);

  // Active calculator favorite button
  DOM.calcFavToggleBtn.addEventListener("click", () => {
    if (!AppState.activeCalculatorId) return;
    toggleFavorite(AppState.activeCalculatorId);
    const isFav = AppState.favorites.includes(AppState.activeCalculatorId);
    DOM.calcFavToggleBtn.classList.toggle("active", isFav);
    DOM.calcFavToggleBtn.querySelector(".fav-icon").textContent = isFav ? "★" : "☆";
    renderCategoryPills();
  });

  // Copy link to active calculator
  DOM.copyShareBtn.addEventListener("click", () => {
    const url = window.location.href;
    navigator.clipboard.writeText(url).then(() => {
      showToast(AppState.lang === "bn" ? "ক্যালকুলেটরের লিঙ্ক কপি করা হয়েছে!" : "Calculator link copied to clipboard!", "success");
    });
  });

  // Search input live handling with debounce
  let searchDebounce = null;
  DOM.searchInput.addEventListener("input", (e) => {
    clearTimeout(searchDebounce);
    searchDebounce = setTimeout(() => {
      AppState.searchQuery = e.target.value;
      DOM.clearSearchBtn.style.display = e.target.value ? "flex" : "none";
      if (AppState.activeCalculatorId) {
        closeCalculator();
      }
      renderCalculatorsGrid();
    }, 150);
  });

  // Clear search button
  DOM.clearSearchBtn.addEventListener("click", () => {
    DOM.searchInput.value = "";
    AppState.searchQuery = "";
    DOM.clearSearchBtn.style.display = "none";
    renderCalculatorsGrid();
  });

  // Reset search button inside empty state
  DOM.resetSearchBtn.addEventListener("click", () => {
    DOM.searchInput.value = "";
    AppState.searchQuery = "";
    AppState.currentCategory = "all";
    DOM.clearSearchBtn.style.display = "none";
    updateCategoryPillState("all");
    renderCalculatorsGrid();
  });

  // Category Pills Tab switching
  DOM.categoryTabs.addEventListener("click", (e) => {
    const pill = e.target.closest(".cat-pill");
    if (!pill) return;

    const cat = pill.getAttribute("data-category");
    AppState.currentCategory = cat;
    updateCategoryPillState(cat);

    if (AppState.activeCalculatorId) {
      closeCalculator();
    } else {
      renderCalculatorsGrid();
    }
  });

  // Roadmap Modal open/close
  DOM.viewRoadmapBtn.addEventListener("click", () => {
    DOM.roadmapModal.style.display = "flex";
  });
  DOM.closeRoadmapBtn.addEventListener("click", () => {
    DOM.roadmapModal.style.display = "none";
  });
  DOM.roadmapModal.addEventListener("click", (e) => {
    if (e.target === DOM.roadmapModal) {
      DOM.roadmapModal.style.display = "none";
    }
  });

  // Keyboard Shortcuts: Escape to close modals/drawers
  document.addEventListener("keydown", (e) => {
    if (e.key === "Escape") {
      if (DOM.historyDrawer.classList.contains("open")) {
        closeHistoryDrawer();
      }
      if (DOM.roadmapModal.style.display === "flex") {
        DOM.roadmapModal.style.display = "none";
      }
    }
  });
}

function updateCategoryPillState(activeCategory) {
  document.querySelectorAll(".cat-pill").forEach(pill => {
    const isTarget = pill.getAttribute("data-category") === activeCategory;
    pill.classList.toggle("active", isTarget);
    pill.setAttribute("aria-selected", isTarget ? "true" : "false");
  });
}

// ------------------------------------------------------------------------------
// 19. START APPLICATION ON DOM LOAD
// ------------------------------------------------------------------------------
document.addEventListener("DOMContentLoaded", initApp);
```

---

## File Placement & How to Run

### Directory Structure
Create a dedicated folder on your computer (e.g., `textile-ai-calculator`) and place all three files directly side-by-side in the same directory:

```text
textile-ai-calculator/
├── index.html
├── style.css
└── script.js
```

### How to Open & Run the Application

Because this application is built with standard web technologies and zero server dependencies, you have multiple options:

#### Option 1: Direct File Launch (No server required)
- Double-click `index.html` in your file explorer (Windows Explorer, macOS Finder, or Linux file manager).
- It will open immediately in your default browser (Google Chrome, Firefox, Safari, Edge, or mobile browser).
- All calculators, unit conversions, theme switching, language toggling, and local storage (Favorites & History) function directly offline via `file://`.

#### Option 2: Run via any Local Static HTTP Server
If you prefer running through `localhost`:
- Using Node.js:
  ```bash
  npx serve
  # or
  npx http-server .
  ```
- Using Python 3 (standard utility):
  ```bash
  python3 -m http.server 8080
  ```
- Using VS Code:
  Install the **Live Server** extension, right-click `index.html`, and select **"Open with Live Server"**.

### Deep Linking to Specific Calculators
You can share or bookmark any calculator directly using the URL hash:
- `index.html#calc=gsm` (GSM Calculator)
- `index.html#calc=fabric-weight` (Fabric Weight Calculator)
- `index.html#calc=shrinkage` (Shrinkage Calculator)
- `index.html#calc=stenter-overfeed` (Stenter Overfeed Calculator)
- `index.html#calc=yarn-count` (Yarn Count Converter)
- `index.html#calc=dye-chem` (Dye & Chemical Percentage Calculator)
- `index.html#calc=liquor-ratio` (Liquor Ratio Calculator)
- `index.html#calc=production` (Machine Production Calculator)
- `index.html#calc=efficiency` (Production Efficiency Calculator)
- `index.html#calc=fabric-consumption` (Fabric Consumption Calculator)