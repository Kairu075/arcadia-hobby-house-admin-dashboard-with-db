<style>
  /* ══════════════════════════════════════
     NAVBAR — Arcadia Hobby House
  ══════════════════════════════════════ */
  .top-navbar {
    background: #ffffff;
    border-bottom: 1px solid #e2e8f0;
    box-shadow: 0 2px 12px rgba(30, 58, 95, 0.07);
    padding: 10px 0;
    z-index: 50;
  }

  /* ── Brand ── */
  .navbar-brand-text .brand-name {
    font-size: 1rem;
    font-weight: 800;
    color: #1e2d5a;
    line-height: 1.1;
    letter-spacing: -.02em;
  }
  .navbar-brand-text .brand-sub {
    font-size: .68rem;
    color: #3b82f6;
    font-weight: 600;
    letter-spacing: .04em;
    text-transform: uppercase;
  }

  /* ── Search ── */
  .search-bar-wrapper { min-width: 0; flex: 1; }

  .search-input {
    background: #f8faff;
    border: 1.5px solid #dbeafe;
    border-radius: 10px;
    padding: 9px 42px 9px 14px;
    color: #1e293b;
    font-size: 14px;
    transition: all .2s;
    width: 100%;
  }
  .search-input::placeholder { color: #94a3b8; }
  .search-input:focus {
    outline: none;
    border-color: #3b82f6;
    background: #fff;
    box-shadow: 0 0 0 3px rgba(59,130,246,.12);
  }
  .search-btn {
    position: absolute;
    right: 10px;
    top: 50%;
    transform: translateY(-50%);
    background: none;
    border: none;
    color: #94a3b8;
    padding: 0;
    z-index: 10;
    transition: color .2s;
  }
  .search-btn:hover { color: #3b82f6; }

  .suggestions-list {
    position: absolute;
    top: calc(100% + 6px);
    left: 0;
    width: 100%;
    max-height: 260px;
    overflow-y: auto;
    background: #fff;
    border: 1.5px solid #dbeafe;
    border-radius: 12px;
    box-shadow: 0 8px 24px rgba(30,58,95,.12);
    z-index: 100;
    padding: 6px;
  }
  .suggestion-item {
    padding: 9px 12px;
    cursor: pointer;
    font-size: 13.5px;
    color: #334155;
    border-radius: 8px;
    transition: background .15s;
  }
  .suggestion-item:hover,
  .suggestion-item.active {
    background: #eff6ff;
    color: #2550d4;
  }

  /* ── Nav links ── */
  .nav-link-custom {
    color: #334155 !important;
    font-size: 14px;
    font-weight: 600;
    padding: 8px 12px !important;
    border-radius: 8px;
    transition: all .2s;
    text-decoration: none;
  }
  .nav-link-custom:hover {
    color: #2550d4 !important;
    background: #eff6ff;
  }
  .nav-link-custom.active-link {
    color: #2550d4 !important;
    background: #eff6ff;
  }

  /* ── Dropdown ── */
  .dropdown-menu-custom {
    border-radius: 12px;
    border: 1.5px solid #dbeafe;
    box-shadow: 0 8px 24px rgba(30,58,95,.12);
    padding: 8px;
    min-width: 200px;
  }
  .dropdown-item-custom {
    padding: 9px 12px;
    font-size: 13.5px;
    color: #334155;
    border-radius: 8px;
    transition: background .15s;
    display: flex;
    align-items: center;
    gap: 10px;
    text-decoration: none;
  }
  .dropdown-item-custom:hover {
    background: #eff6ff;
    color: #2550d4;
  }
  .dropdown-item-custom .cat-emoji {
    width: 26px;
    height: 26px;
    border-radius: 6px;
    background: #f0f4ff;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: .9rem;
    flex-shrink: 0;
  }

  /* ── Profile icon ── */
  .profile-icon {
    width: 36px;
    height: 36px;
    border-radius: 50%;
    background: #1e2d5a;
    color: #fff !important;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 17px;
    transition: all .2s;
    text-decoration: none;
    flex-shrink: 0;
  }
  .profile-icon:hover {
    background: #2550d4;
    transform: scale(1.06);
  }

  /* ── Cart icon ── */
  .cart-icon {
    position: relative;
    color: #334155 !important;
    font-size: 20px;
    display: flex;
    align-items: center;
    transition: all .2s;
    text-decoration: none;
    flex-shrink: 0;
  }
  .cart-icon:hover { color: #2550d4 !important; }
  .cart-badge {
    position: absolute;
    top: -7px;
    right: -8px;
    background: #ef4444;
    color: #fff;
    border-radius: 50%;
    width: 18px;
    height: 18px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 10px;
    font-weight: 700;
    border: 2px solid #fff;
  }

  /* ── Toggler ── */
  .navbar-toggler {
    border: 1.5px solid #dbeafe;
    border-radius: 8px;
    padding: 5px 8px;
    background: #f8faff;
  }
  .navbar-toggler:focus { box-shadow: none; outline: none; }
  .navbar-toggler-icon {
    background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 30 30'%3e%3cpath stroke='%231e2d5a' stroke-linecap='round' stroke-miterlimit='10' stroke-width='2' d='M4 7h22M4 15h22M4 23h22'/%3e%3c/svg%3e");
  }

  /* ── Mobile collapse ── */
  .mobile-menu-inner {
    padding: 12px 0 8px;
    border-top: 1.5px solid #e2e8f0;
    margin-top: 8px;
  }
  .mobile-nav-link {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 11px 14px;
    border-radius: 10px;
    color: #334155;
    font-size: 14px;
    font-weight: 600;
    text-decoration: none;
    transition: background .15s;
    margin-bottom: 2px;
  }
  .mobile-nav-link:hover,
  .mobile-nav-link.active {
    background: #eff6ff;
    color: #2550d4;
  }
  .mobile-nav-link .link-icon {
    width: 30px;
    height: 30px;
    border-radius: 8px;
    background: #f0f4ff;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: .9rem;
  }
  .mobile-divider {
    border: none;
    border-top: 1.5px solid #e2e8f0;
    margin: 8px 0;
  }

  /* ── Category chips ── */
  .category-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
    padding: 6px 4px;
  }
  .category-chip {
    background: #f0f4ff;
    border: 1.5px solid #dbeafe;
    border-radius: 8px;
    padding: 6px 12px;
    font-size: 12.5px;
    font-weight: 600;
    color: #334155;
    text-decoration: none;
    transition: all .18s;
  }
  .category-chip:hover {
    background: #2550d4;
    border-color: #2550d4;
    color: #fff;
  }

  /* ── RESPONSIVE ── */
  @media (max-width: 991px) {
    .desktop-only { display: none !important; }
  }
  @media (min-width: 992px) {
    .mobile-only { display: none !important; }
    .search-bar-wrapper { margin: 0 16px !important; }
  }
</style>

{{-- ══════════════════════════════════════
     NAVBAR
══════════════════════════════════════ --}}
<nav class="top-navbar navbar navbar-expand-lg sticky-top">
  <div class="container">
    <div class="d-flex align-items-center w-100 gap-2">

      {{-- ── Brand ── --}}
      <a class="d-flex align-items-center gap-2 text-decoration-none flex-shrink-0"
         href="{{ route('home') }}">
        <img src="{{ asset('images/logo.png') }}?v=2"
             style="height:42px; width:42px; border-radius:10px; object-fit:cover;">
        <div class="navbar-brand-text d-none d-lg-block">
          <div class="brand-name">Arcadia</div>
          <div class="brand-sub">Hobby House</div>
        </div>
      </a>

      {{-- ── Desktop search ── --}}
      <div class="search-bar-wrapper d-none d-lg-block mx-3 flex-grow-1">
        <form class="position-relative"
              id="searchForm"
              autocomplete="off"
              method="POST"
              action="{{ route('searchProduct') }}">
          @csrf
          <input type="text"
                 id="searchInput"
                 class="search-input"
                 placeholder="Search products, categories..."
                 name="search">
          <button class="search-btn" type="submit">
            <i class="bi bi-search"></i>
          </button>
          <div id="suggestions" class="suggestions-list d-none"></div>
        </form>
      </div>

      {{-- ── Desktop nav ── --}}
      <div class="d-none d-lg-flex align-items-center gap-1 flex-shrink-0">

        {{-- Categories dropdown --}}
        <div class="dropdown">
          <a class="nav-link-custom dropdown-toggle"
             href="#"
             data-bs-toggle="dropdown">
            Categories
          </a>
          <ul class="dropdown-menu dropdown-menu-custom dropdown-menu-end">
            <li>
              <a class="dropdown-item-custom" href="{{ route('category.show','board games') }}">
                <span class="cat-emoji">🎲</span> Board Games
              </a>
            </li>
            <li>
              <a class="dropdown-item-custom" href="{{ route('category.show','trading cards') }}">
                <span class="cat-emoji">🃏</span> Trading Cards
              </a>
            </li>
            <li>
              <a class="dropdown-item-custom" href="{{ route('category.show','lego sets') }}">
                <span class="cat-emoji">🧱</span> LEGO Sets
              </a>
            </li>
            <li>
              <a class="dropdown-item-custom" href="{{ route('category.show','collectibles') }}">
                <span class="cat-emoji">⭐</span> Collectibles
              </a>
            </li>
            <li>
              <a class="dropdown-item-custom" href="{{ route('category.show','puzzles') }}">
                <span class="cat-emoji">🧩</span> Puzzles
              </a>
            </li>
            <li>
              <a class="dropdown-item-custom" href="{{ route('category.show','art supplies') }}">
                <span class="cat-emoji">🎨</span> Art Supplies
              </a>
            </li>
            <li><hr style="border-color:#dbeafe; margin:6px 12px;"></li>
            <li>
              <a class="dropdown-item-custom" href="{{ route('category.show','all categories') }}">
                <span class="cat-emoji">🗂️</span> All Categories
              </a>
            </li>
          </ul>
        </div>

        <a class="nav-link-custom" href="{{ route('navigate', 'featured') }}">Featured</a>
        <a class="nav-link-custom" href="{{ route('navigate', 'best-seller') }}">Best Sellers</a>

        {{-- Divider --}}
        <div style="width:1px;height:24px;background:#e2e8f0;margin:0 4px;"></div>

        {{-- Profile --}}
        <a class="profile-icon" href="{{ route('profile') }}" title="My Account">
          <i class="bi bi-person-fill"></i>
        </a>

        {{-- Cart --}}
        <a class="cart-icon ms-1" href="{{ route('cart') }}" title="Cart">
          <i class="bi bi-cart2"></i>
          <span class="cart-badge">
            {{ Auth::check() ? \App\Models\Cart::where('user_id', Auth::id())->count() : 0 }}
          </span>
        </a>

      </div>

      {{-- ── Mobile right side ── --}}
      <div class="d-flex align-items-center gap-2 d-lg-none ms-auto flex-shrink-0">
        <a class="profile-icon" href="{{ route('profile') }}">
          <i class="bi bi-person-fill"></i>
        </a>
        <a class="cart-icon" href="{{ route('cart') }}">
          <i class="bi bi-cart2"></i>
          <span class="cart-badge">
            {{ Auth::check() ? \App\Models\Cart::where('user_id', Auth::id())->count() : 0 }}
          </span>
        </a>
        <button class="navbar-toggler"
                type="button"
                data-bs-toggle="collapse"
                data-bs-target="#navbarMenu">
          <span class="navbar-toggler-icon"></span>
        </button>
      </div>

    </div>

    {{-- ── Mobile collapse ── --}}
    <div class="collapse navbar-collapse w-100" id="navbarMenu">
      <div class="mobile-menu-inner">

        {{-- Mobile search --}}
        <form class="position-relative mb-3"
              id="searchFormMobile"
              autocomplete="off"
              method="POST"
              action="{{ route('searchProduct') }}">
          @csrf
          <input type="text"
                 id="searchInputMobile"
                 class="search-input"
                 placeholder="Search products..."
                 name="search">
          <button class="search-btn" type="submit">
            <i class="bi bi-search"></i>
          </button>
          <div id="suggestionsMobile" class="suggestions-list d-none"></div>
        </form>

        {{-- Mobile nav links --}}
        <a class="mobile-nav-link" href="{{ route('navigate', 'featured') }}">
          <span class="link-icon">⚡</span> Featured
        </a>
        <a class="mobile-nav-link" href="{{ route('navigate', 'best-seller') }}">
          <span class="link-icon">🏆</span> Best Sellers
        </a>

        <hr class="mobile-divider">

        {{-- Mobile category chips --}}
        <div class="px-1 mb-1">
          <div style="font-size:.72rem;font-weight:700;color:#94a3b8;
                      text-transform:uppercase;letter-spacing:.06em;
                      padding:0 4px 6px;">
            Categories
          </div>
          <div class="category-grid">
            <a href="{{ route('category.show','board games') }}"    class="category-chip">🎲 Board Games</a>
            <a href="{{ route('category.show','trading cards') }}"  class="category-chip">🃏 Trading Cards</a>
            <a href="{{ route('category.show','lego sets') }}"      class="category-chip">🧱 LEGO Sets</a>
            <a href="{{ route('category.show','collectibles') }}"   class="category-chip">⭐ Collectibles</a>
            <a href="{{ route('category.show','puzzles') }}"        class="category-chip">🧩 Puzzles</a>
            <a href="{{ route('category.show','art supplies') }}"   class="category-chip">🎨 Art Supplies</a>
          </div>
        </div>

      </div>
    </div>

  </div>
</nav>

<script>
  let mockDB = { products: [] };

  const searchInputs = [
    { input: document.getElementById('searchInput'),       box: document.getElementById('suggestions') },
    { input: document.getElementById('searchInputMobile'), box: document.getElementById('suggestionsMobile') }
  ];

  // Load products
  fetch('/products')
    .then(res => res.json())
    .then(data => { mockDB.products = data; })
    .catch(err => console.error('Failed to load products', err));

  function createSuggestionItem(product, inputList) {
    const item = document.createElement('div');
    item.className = 'suggestion-item';
    item.innerHTML = `<strong>${product.name}</strong>
      <span style="color:#94a3b8;font-size:.78rem;margin-left:6px;">· ${product.category}</span>`;

    item.addEventListener('mousedown', function (e) {
      e.preventDefault();
      inputList.forEach(i => { if (i.input) i.input.value = product.name; });
      hideAllSuggestions();
      const form = document.getElementById('searchForm');
      if (form) form.submit();
    });
    return item;
  }

  function showSuggestions(matches, box, inputList) {
    box.innerHTML = '';
    if (!matches.length) { box.classList.add('d-none'); return; }
    matches.slice(0, 6).forEach(p => box.appendChild(createSuggestionItem(p, inputList)));
    box.classList.remove('d-none');
  }

  function hideAllSuggestions() {
    searchInputs.forEach(s => { if (s.box) s.box.classList.add('d-none'); });
  }

  function filterProducts(query) {
    const q = query.trim().toLowerCase();
    if (!q) return [];
    return (mockDB.products || []).filter(p => p.name.toLowerCase().startsWith(q));
  }

  searchInputs.forEach(({ input, box }) => {
    if (!input) return;
    input.addEventListener('input', function () {
      if (!this.value) { box.classList.add('d-none'); return; }
      showSuggestions(filterProducts(this.value), box, searchInputs);
    });
    input.addEventListener('focus', function () {
      if (this.value.trim()) {
        const b = searchInputs.find(s => s.input === this)?.box;
        if (b) showSuggestions(filterProducts(this.value), b, searchInputs);
      }
    });
    input.addEventListener('blur', () => setTimeout(hideAllSuggestions, 150));
  });

  const desktopForm = document.getElementById('searchForm');
  if (desktopForm) {
    desktopForm.addEventListener('submit', function (e) {
      const q = document.getElementById('searchInput')?.value.trim();
      if (!q) e.preventDefault();
      hideAllSuggestions();
    });
  }
</script>
