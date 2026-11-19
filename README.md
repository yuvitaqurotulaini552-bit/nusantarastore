<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Nusantara Store — Katalog Produk Nusantara</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://unpkg.com/lucide@latest"></script>
  <style>
    body { font-family: ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, sans-serif; }
    .line-clamp-2 { display:-webkit-box; -webkit-line-clamp:2; -webkit-box-orient:vertical; overflow:hidden; }
    .fade-in { animation: fadeIn .25s ease-out; }
    @keyframes fadeIn { from { opacity:0; transform: translateY(6px);} to { opacity:1; transform:none; } }
    .drawer { transition: transform .3s ease; }
  </style>
</head>
<body class="bg-stone-50 text-stone-800">

  <!-- NAVBAR -->
  <header class="sticky top-0 z-40 bg-white/90 backdrop-blur border-b border-stone-200">
    <div class="max-w-7xl mx-auto px-4 h-16 flex items-center gap-4">
      <a href="#" class="flex items-center gap-2 shrink-0">
        <span class="w-9 h-9 rounded-xl bg-gradient-to-br from-red-600 to-amber-500 text-white flex items-center justify-center"><i data-lucide="store" class="w-5 h-5"></i></span>
        <span class="font-bold text-lg tracking-tight">Nusantara<span class="text-red-600">Store</span></span>
      </a>

      <div class="hidden md:flex flex-1 max-w-xl mx-auto relative">
        <i data-lucide="search" class="w-4 h-4 absolute left-3 top-1/2 -translate-y-1/2 text-stone-400"></i>
        <input id="searchInput" type="search" placeholder="Cari batik, kopi, kerajinan..." class="w-full pl-9 pr-3 py-2 rounded-full bg-stone-100 border border-transparent focus:bg-white focus:border-red-400 focus:outline-none text-sm" />
      </div>

      <nav class="ml-auto flex items-center gap-2">
        <span id="adminBadge" class="hidden text-xs font-medium bg-amber-100 text-amber-800 px-2 py-1 rounded-full">Mode Admin</span>
        <button id="cartBtn" class="relative p-2 rounded-full hover:bg-stone-100" aria-label="Keranjang">
          <i data-lucide="shopping-cart" class="w-5 h-5"></i>
          <span id="cartCount" class="hidden absolute -top-0.5 -right-0.5 bg-red-600 text-white text-[10px] font-bold min-w-[18px] h-[18px] rounded-full flex items-center justify-center">0</span>
        </button>
        <button id="authBtn" class="flex items-center gap-1.5 px-4 py-2 rounded-full bg-stone-900 text-white text-sm font-medium hover:bg-stone-700">
          <i data-lucide="log-in" class="w-4 h-4"></i><span id="authLabel">Login</span>
        </button>
      </nav>
    </div>
    <div class="md:hidden px-4 pb-3">
      <input id="searchInputMobile" type="search" placeholder="Cari produk..." class="w-full px-4 py-2 rounded-full bg-stone-100 text-sm focus:outline-none focus:ring-2 focus:ring-red-300" />
    </div>
  </header>

  <!-- HERO -->
  <section class="bg-gradient-to-r from-red-700 via-red-600 to-amber-500 text-white">
    <div class="max-w-7xl mx-auto px-4 py-12 md:py-16 grid md:grid-cols-2 gap-6 items-center">
      <div>
        <p class="text-amber-200 text-sm font-semibold uppercase tracking-widest mb-2">Bangga Produk Lokal</p>
        <h1 class="text-3xl md:text-5xl font-extrabold leading-tight">Kekayaan Nusantara dalam Satu Katalog</h1>
        <p class="mt-3 text-red-50 max-w-lg">Temukan batik, kopi, kerajinan, dan kuliner khas dari Sabang sampai Merauke, langsung dari pengrajin dan UMKM pilihan.</p>
        <a href="#katalog" class="inline-flex items-center gap-2 mt-6 bg-white text-red-700 font-semibold px-5 py-2.5 rounded-full hover:bg-amber-50">
          Belanja Sekarang <i data-lucide="arrow-right" class="w-4 h-4"></i>
        </a>
      </div>
      <div class="hidden md:flex justify-end gap-4 text-6xl select-none" aria-hidden="true">
        <span class="bg-white/15 rounded-3xl p-6 rotate-[-6deg]">🧵</span>
        <span class="bg-white/15 rounded-3xl p-6 translate-y-4">☕</span>
        <span class="bg-white/15 rounded-3xl p-6 rotate-[6deg]">🪘</span>
      </div>
    </div>
  </section>

  <!-- KATALOG -->
  <main id="katalog" class="max-w-7xl mx-auto px-4 py-8">
    <div class="flex flex-wrap items-center gap-3 mb-5">
      <div id="categoryChips" class="flex flex-wrap gap-2"></div>
      <div class="ml-auto flex items-center gap-2">
        <select id="sortSelect" class="text-sm border border-stone-300 rounded-lg px-3 py-2 bg-white focus:outline-none focus:ring-2 focus:ring-red-300">
          <option value="default">Urutkan: Terbaru</option>
          <option value="low">Harga terendah</option>
          <option value="high">Harga tertinggi</option>
          <option value="name">Nama A–Z</option>
        </select>
        <button id="addProductBtn" class="hidden items-center gap-1.5 text-sm font-medium bg-red-600 hover:bg-red-700 text-white px-4 py-2 rounded-lg">
          <i data-lucide="plus" class="w-4 h-4"></i> Tambah Produk
        </button>
      </div>
    </div>

    <p id="resultInfo" class="text-sm text-stone-500 mb-4"></p>
    <div id="productGrid" class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4 md:gap-6"></div>
    <div id="emptyState" class="hidden text-center py-20 text-stone-500">
      <i data-lucide="package-search" class="w-12 h-12 mx-auto mb-3 text-stone-300"></i>
      <p class="font-medium">Produk tidak ditemukan</p>
      <p class="text-sm">Coba kata kunci atau kategori lain.</p>
    </div>
  </main>

  <footer class="border-t border-stone-200 bg-white mt-8">
    <div class="max-w-7xl mx-auto px-4 py-8 text-sm text-stone-500 flex flex-col md:flex-row gap-2 md:items-center md:justify-between">
      <p class="font-semibold text-stone-700">Nusantara Store</p>
      <p>© <span id="year"></span> Nusantara Store. Dibuat dengan bangga untuk UMKM Indonesia.</p>
    </div>
  </footer>

  <!-- CART DRAWER -->
  <div id="cartOverlay" class="hidden fixed inset-0 bg-black/50 z-50"></div>
  <aside id="cartDrawer" class="drawer fixed top-0 right-0 h-full w-full max-w-md bg-white z-50 translate-x-full flex flex-col shadow-2xl">
    <div class="flex items-center justify-between px-5 py-4 border-b">
      <h2 class="font-bold text-lg flex items-center gap-2"><i data-lucide="shopping-bag" class="w-5 h-5"></i> Keranjang</h2>
      <button id="closeCart" class="p-2 rounded-full hover:bg-stone-100" aria-label="Tutup"><i data-lucide="x" class="w-5 h-5"></i></button>
    </div>
    <div id="cartItems" class="flex-1 overflow-y-auto p-5 space-y-4"></div>
    <div class="border-t p-5 space-y-3">
      <div class="flex justify-between font-semibold"><span>Total</span><span id="cartTotal">Rp 0</span></div>
      <button id="checkoutBtn" class="w-full bg-red-600 hover:bg-red-700 text-white font-semibold py-3 rounded-xl disabled:opacity-40 disabled:cursor-not-allowed">Checkout</button>
      <button id="clearCartBtn" class="w-full text-sm text-stone-500 hover:text-red-600">Kosongkan keranjang</button>
    </div>
  </aside>

  <!-- MODAL: DETAIL PRODUK -->
  <div id="detailModal" class="hidden fixed inset-0 z-50 bg-black/50 flex items-center justify-center p-4">
    <div class="bg-white rounded-2xl max-w-3xl w-full max-h-[90vh] overflow-y-auto fade-in relative">
      <button data-close="detailModal" class="absolute top-3 right-3 p-2 rounded-full bg-white/90 hover:bg-stone-100 z-10" aria-label="Tutup"><i data-lucide="x" class="w-5 h-5"></i></button>
      <div id="detailContent"></div>
    </div>
  </div>

  <!-- MODAL: LOGIN -->
  <div id="loginModal" class="hidden fixed inset-0 z-50 bg-black/50 flex items-center justify-center p-4">
    <div class="bg-white rounded-2xl max-w-sm w-full p-6 fade-in relative">
      <button data-close="loginModal" class="absolute top-3 right-3 p-2 rounded-full hover:bg-stone-100" aria-label="Tutup"><i data-lucide="x" class="w-5 h-5"></i></button>
      <div class="w-12 h-12 rounded-2xl bg-red-100 text-red-600 flex items-center justify-center mb-3"><i data-lucide="lock" class="w-6 h-6"></i></div>
      <h2 class="text-xl font-bold">Login Admin</h2>
      <p class="text-sm text-stone-500 mb-4">Masuk untuk mengelola produk toko.</p>
      <form id="loginForm" class="space-y-3" autocomplete="off">
        <div>
          <label for="loginUser" class="text-sm font-medium">Username</label>
          <input id="loginUser" type="text" required class="mt-1 w-full border border-stone-300 rounded-lg px-3 py-2 focus:outline-none focus:ring-2 focus:ring-red-300" />
        </div>
        <div>
          <label for="loginPass" class="text-sm font-medium">Password</label>
          <input id="loginPass" type="password" required class="mt-1 w-full border border-stone-300 rounded-lg px-3 py-2 focus:outline-none focus:ring-2 focus:ring-red-300" />
        </div>
        <p id="loginError" class="hidden text-sm text-red-600">Username atau password salah.</p>
        <button type="submit" class="w-full bg-stone-900 hover:bg-stone-700 text-white font-semibold py-2.5 rounded-lg">Login</button>
      </form>
    </div>
  </div>

  <!-- MODAL: FORM PRODUK (ADMIN) -->
  <div id="productModal" class="hidden fixed inset-0 z-50 bg-black/50 flex items-center justify-center p-4">
    <div class="bg-white rounded-2xl max-w-lg w-full max-h-[90vh] overflow-y-auto p-6 fade-in relative">
      <button data-close="productModal" class="absolute top-3 right-3 p-2 rounded-full hover:bg-stone-100" aria-label="Tutup"><i data-lucide="x" class="w-5 h-5"></i></button>
      <h2 id="productModalTitle" class="text-xl font-bold mb-4">Tambah Produk</h2>
      <form id="productForm" class="space-y-3">
        <input type="hidden" id="pId" />
        <div>
          <label class="text-sm font-medium">Nama Produk</label>
          <input id="pName" required class="mt-1 w-full border border-stone-300 rounded-lg px-3 py-2 focus:outline-none focus:ring-2 focus:ring-red-300" />
        </div>
        <div class="grid grid-cols-2 gap-3">
          <div>
            <label class="text-sm font-medium">Kategori</label>
            <input id="pCategory" required list="categoryList" class="mt-1 w-full border border-stone-300 rounded-lg px-3 py-2 focus:outline-none focus:ring-2 focus:ring-red-300" />
            <datalist id="categoryList"></datalist>
          </div>
          <div>
            <label class="text-sm font-medium">Harga (Rp)</label>
            <input id="pPrice" type="number" min="0" required class="mt-1 w-full border border-stone-300 rounded-lg px-3 py-2 focus:outline-none focus:ring-2 focus:ring-red-300" />
          </div>
        </div>
        <div class="grid grid-cols-2 gap-3">
          <div>
            <label class="text-sm font-medium">Stok</label>
            <input id="pStock" type="number" min="0" required class="mt-1 w-full border border-stone-300 rounded-lg px-3 py-2 focus:outline-none focus:ring-2 focus:ring-red-300" />
          </div>
          <div>
            <label class="text-sm font-medium">Emoji (opsional)</label>
            <input id="pEmoji" maxlength="4" placeholder="🎁" class="mt-1 w-full border border-stone-300 rounded-lg px-3 py-2 focus:outline-none focus:ring-2 focus:ring-red-300" />
          </div>
        </div>
        <div>
          <label class="text-sm font-medium">URL Gambar (opsional)</label>
          <input id="pImage" type="url" placeholder="https://..." class="mt-1 w-full border border-stone-300 rounded-lg px-3 py-2 focus:outline-none focus:ring-2 focus:ring-red-300" />
        </div>
        <div>
          <label class="text-sm font-medium">Deskripsi</label>
          <textarea id="pDesc" rows="3" required class="mt-1 w-full border border-stone-300 rounded-lg px-3 py-2 focus:outline-none focus:ring-2 focus:ring-red-300"></textarea>
        </div>
        <div class="flex gap-2 pt-2">
          <button type="button" data-close="productModal" class="flex-1 border border-stone-300 rounded-lg py-2.5 font-medium hover:bg-stone-50">Batal</button>
          <button type="submit" class="flex-1 bg-red-600 hover:bg-red-700 text-white rounded-lg py-2.5 font-semibold">Simpan</button>
        </div>
      </form>
    </div>
  </div>

  <!-- TOAST -->
  <div id="toast" class="fixed bottom-5 left-1/2 -translate-x-1/2 z-[60] hidden bg-stone-900 text-white text-sm px-4 py-2.5 rounded-full shadow-lg"></div>

<script>
(() => {
  // ====== STORAGE KEYS ======
  const K_PRODUCTS = 'nusantara_products_v1';
  const K_CART = 'nusantara_cart_v1';
  const K_ADMIN = 'nusantara_admin_v1';

  // Kredensial admin (hanya untuk logika login di balik layar, tidak ditampilkan di UI)
  const ADMIN_USER = 'admin';
  const ADMIN_PASS = 'admin123';

  const gradients = [
    'from-red-200 to-amber-100', 'from-amber-200 to-yellow-100', 'from-emerald-200 to-lime-100',
    'from-sky-200 to-indigo-100', 'from-rose-200 to-orange-100', 'from-teal-200 to-cyan-100'
  ];

  const seedProducts = [
    { id: 1, name: 'Batik Tulis Pekalongan', category: 'Fashion', price: 450000, stock: 12, emoji: '👘', image: '', desc: 'Batik tulis asli Pekalongan dengan motif klasik, dibuat manual oleh pengrajin selama berhari-hari. Bahan katun primisima yang adem dan nyaman.' },
    { id: 2, name: 'Kopi Gayo Arabika 250g', category: 'Makanan & Minuman', price: 85000, stock: 40, emoji: '☕', image: '', desc: 'Biji kopi arabika Gayo Aceh dengan aroma floral, body medium, dan keasaman lembut. Sangrai medium roast.' },
    { id: 3, name: 'Tenun Ikat Sumba', category: 'Fashion', price: 750000, stock: 5, emoji: '🧣', image: '', desc: 'Kain tenun ikat khas Sumba dengan pewarna alami dan motif kuda serta pohon kehidupan.' },
    { id: 4, name: 'Keris Miniatur Jawa', category: 'Kerajinan', price: 325000, stock: 8, emoji: '🗡️', image: '', desc: 'Keris miniatur untuk hiasan dan koleksi, lengkap dengan warangka kayu jati dan stand display.' },
    { id: 5, name: 'Rendang Kemasan Premium', category: 'Makanan & Minuman', price: 95000, stock: 30, emoji: '🍛', image: '', desc: 'Rendang daging sapi khas Minang dengan bumbu rempah pekat, kemasan vakum tahan hingga 6 bulan.' },
    { id: 6, name: 'Anyaman Tas Rotan', category: 'Kerajinan', price: 220000, stock: 15, emoji: '👜', image: '', desc: 'Tas anyaman rotan handmade dari pengrajin Lombok, ringan, kuat, dan cocok untuk gaya santai.' },
    { id: 7, name: 'Angklung Bambu 8 Nada', category: 'Alat Musik', price: 280000, stock: 10, emoji: '🎼', image: '', desc: 'Satu set angklung bambu 8 nada dengan stand, sudah disetel dengan tangga nada diatonis.' },
    { id: 8, name: 'Gamelan Saron Mini', category: 'Alat Musik', price: 540000, stock: 4, emoji: '🪘', image: '', desc: 'Saron mini untuk edukasi dan koleksi, berbahan perunggu dengan rangka kayu jati berukir.' },
    { id: 9, name: 'Teh Melati Bubuk 100g', category: 'Makanan & Minuman', price: 35000, stock: 60, emoji: '🍵', image: '', desc: 'Teh hijau melati wangi dari perkebunan Jawa Tengah, cocok diseduh hangat maupun dingin.' },
    { id: 10, name: 'Wayang Kulit Arjuna', category: 'Kerajinan', price: 390000, stock: 6, emoji: '🎭', image: '', desc: 'Wayang kulit kerbau tokoh Arjuna dengan sunggingan warna emas, dilengkapi gapit tanduk.' },
    { id: 11, name: 'Sambal Roa Manado', category: 'Makanan & Minuman', price: 48000, stock: 50, emoji: '🌶️', image: '', desc: 'Sambal ikan roa asap khas Manado, pedas gurih dan sangat cocok untuk nasi hangat.' },
    { id: 12, name: 'Songket Palembang', category: 'Fashion', price: 1250000, stock: 3, emoji: '✨', image: '', desc: 'Kain songket Palembang dengan benang emas, motif bunga tanjung. Cocok untuk acara adat dan pernikahan.' }
  ];

  // ====== STATE ======
  const load = (k, fb) => { try { const v = JSON.parse(localStorage.getItem(k)); return v ?? fb; } catch { return fb; } };
  const save = (k, v) => { try { localStorage.setItem(k, JSON.stringify(v)); } catch {} };

  let products = load(K_PRODUCTS, null);
  if (!Array.isArray(products) || !products.length) { products = seedProducts; save(K_PRODUCTS, products); }
  let cart = load(K_CART, []);
  let isAdmin = load(K_ADMIN, false) === true;
  let activeCategory = 'Semua';
  let query = '';
  let sortBy = 'default';

  // ====== HELPERS ======
  const $ = (s, r = document) => r.querySelector(s);
  const $$ = (s, r = document) => [...r.querySelectorAll(s)];
  const rupiah = n => 'Rp ' + Number(n).toLocaleString('id-ID');
  const esc = s => String(s ?? '').replace(/[&<>"']/g, c => ({ '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;' }[c]));
  const icons = () => window.lucide && lucide.createIcons();
  const grad = id => gradients[Math.abs(id) % gradients.length];

  let toastTimer;
  function toast(msg) {
    const t = $('#toast');
    t.textContent = msg; t.classList.remove('hidden');
    clearTimeout(toastTimer);
    toastTimer = setTimeout(() => t.classList.add('hidden'), 2200);
  }

  const openModal = id => $('#' + id).classList.remove('hidden');
  const closeModal = id => $('#' + id).classList.add('hidden');

  function productVisual(p, size = 'text-6xl') {
    if (p.image) {
      return `<img src="${esc(p.image)}" alt="${esc(p.name)}" class="w-full h-full object-cover" loading="lazy" onerror="this.outerHTML='<div class=&quot;w-full h-full flex items-center justify-center ${size}&quot;>${esc(p.emoji || '🎁')}</div>'" />`;
    }
    return `<div class="w-full h-full flex items-center justify-center ${size}">${esc(p.emoji || '🎁')}</div>`;
  }

  // ====== RENDER: KATEGORI ======
  function renderCategories() {
    const cats = ['Semua', ...new Set(products.map(p => p.category))];
    if (!cats.includes(activeCategory)) activeCategory = 'Semua';
    $('#categoryChips').innerHTML = cats.map(c => `
      <button data-cat="${esc(c)}" class="px-4 py-1.5 rounded-full text-sm font-medium border transition ${c === activeCategory ? 'bg-red-600 border-red-600 text-white' : 'bg-white border-stone-300 text-stone-600 hover:border-red-400'}">${esc(c)}</button>
    `).join('');
    $('#categoryList').innerHTML = cats.filter(c => c !== 'Semua').map(c => `<option value="${esc(c)}">`).join('');
  }

  // ====== RENDER: PRODUK ======
  function filtered() {
    let list = products.filter(p =>
      (activeCategory === 'Semua' || p.category === activeCategory) &&
      (!query || (p.name + ' ' + p.category + ' ' + p.desc).toLowerCase().includes(query))
    );
    if (sortBy === 'low') list.sort((a, b) => a.price - b.price);
    else if (sortBy === 'high') list.sort((a, b) => b.price - a.price);
    else if (sortBy === 'name') list.sort((a, b) => a.name.localeCompare(b.name, 'id'));
    else list.sort((a, b) => b.id - a.id);
    return list;
  }

  function renderProducts() {
    const list = filtered();
    $('#resultInfo').textContent = `Menampilkan ${list.length} produk`;
    $('#emptyState').classList.toggle('hidden', list.length > 0);
    $('#productGrid').innerHTML = list.map(p => `
      <article class="group bg-white rounded-2xl border border-stone-200 overflow-hidden hover:shadow-lg transition fade-in flex flex-col">
        <button data-detail="${p.id}" class="aspect-square bg-gradient-to-br ${grad(p.id)} overflow-hidden relative block w-full" aria-label="Lihat ${esc(p.name)}">
          ${productVisual(p)}
          ${p.stock <= 0 ? '<span class="absolute top-2 left-2 text-[11px] font-semibold bg-stone-800 text-white px-2 py-0.5 rounded-full">Habis</span>' : (p.stock <= 5 ? '<span class="absolute top-2 left-2 text-[11px] font-semibold bg-amber-500 text-white px-2 py-0.5 rounded-full">Stok terbatas</span>' : '')}
        </button>
        <div class="p-3 md:p-4 flex flex-col flex-1">
          <span class="text-[11px] uppercase tracking-wide text-red-600 font-semibold">${esc(p.category)}</span>
          <h3 class="font-semibold leading-snug line-clamp-2 mt-0.5">${esc(p.name)}</h3>
          <p class="font-bold text-stone-900 mt-1">${rupiah(p.price)}</p>
          <div class="mt-3 flex gap-2 mt-auto pt-3">
            <button data-add="${p.id}" ${p.stock <= 0 ? 'disabled' : ''} class="flex-1 flex items-center justify-center gap-1.5 text-sm font-medium bg-red-600 hover:bg-red-700 text-white py-2 rounded-lg disabled:opacity-40 disabled:cursor-not-allowed">
              <i data-lucide="shopping-cart" class="w-4 h-4"></i> Tambah
            </button>
            ${isAdmin ? `
              <button data-edit="${p.id}" class="p-2 rounded-lg border border-stone-300 hover:bg-stone-100" aria-label="Edit"><i data-lucide="pencil" class="w-4 h-4"></i></button>
              <button data-delete="${p.id}" class="p-2 rounded-lg border border-red-200 text-red-600 hover:bg-red-50" aria-label="Hapus"><i data-lucide="trash-2" class="w-4 h-4"></i></button>` : ''}
          </div>
        </div>
      </article>
    `).join('');
    icons();
  }

  // ====== DETAIL ======
  function showDetail(id) {
    const p = products.find(x => x.id === id);
    if (!p) return;
    $('#detailContent').innerHTML = `
      <div class="grid md:grid-cols-2">
        <div class="aspect-square bg-gradient-to-br ${grad(p.id)} md:rounded-l-2xl rounded-t-2xl md:rounded-tr-none overflow-hidden">${productVisual(p, 'text-8xl')}</div>
        <div class="p-6 flex flex-col">
          <span class="text-xs uppercase tracking-wide text-red-600 font-semibold">${esc(p.category)}</span>
          <h2 class="text-2xl font-bold mt-1">${esc(p.name)}</h2>
          <p class="text-2xl font-extrabold mt-2">${rupiah(p.price)}</p>
          <p class="text-sm text-stone-500 mt-1">${p.stock > 0 ? 'Stok tersedia: ' + p.stock : 'Stok habis'}</p>
          <p class="mt-4 text-stone-600 leading-relaxed">${esc(p.desc)}</p>
          <button data-add="${p.id}" ${p.stock <= 0 ? 'disabled' : ''} class="mt-auto pt-0 w-full flex items-center justify-center gap-2 bg-red-600 hover:bg-red-700 text-white font-semibold py-3 rounded-xl mt-6 disabled:opacity-40 disabled:cursor-not-allowed">
            <i data-lucide="shopping-cart" class="w-5 h-5"></i> Tambah ke Keranjang
          </button>
        </div>
      </div>`;
    openModal('detailModal');
    icons();
  }

  // ====== KERANJANG ======
  function cartTotals() {
    let count = 0, total = 0;
    cart.forEach(i => { const p = products.find(x => x.id === i.id); if (p) { count += i.qty; total += i.qty * p.price; } });
    return { count, total };
  }

  function renderCart() {
    // buang item yang produknya sudah dihapus
    cart = cart.filter(i => products.some(p => p.id === i.id));
    save(K_CART, cart);
    const { count, total } = cartTotals();
    const badge = $('#cartCount');
    badge.textContent = count; badge.classList.toggle('hidden', count === 0);
    $('#cartTotal').textContent = rupiah(total);
    $('#checkoutBtn').disabled = count === 0;

    $('#cartItems').innerHTML = cart.length ? cart.map(i => {
      const p = products.find(x => x.id === i.id);
      return `
      <div class="flex gap-3">
        <div class="w-16 h-16 rounded-xl bg-gradient-to-br ${grad(p.id)} overflow-hidden shrink-0">${productVisual(p, 'text-3xl')}</div>
        <div class="flex-1 min-w-0">
          <p class="font-medium leading-snug line-clamp-2">${esc(p.name)}</p>
          <p class="text-sm text-stone-500">${rupiah(p.price)}</p>
          <div class="flex items-center gap-2 mt-1">
            <button data-dec="${p.id}" class="w-7 h-7 rounded-full border border-stone-300 hover:bg-stone-100 flex items-center justify-center" aria-label="Kurangi"><i data-lucide="minus" class="w-3.5 h-3.5"></i></button>
            <span class="w-6 text-center text-sm font-medium">${i.qty}</span>
            <button data-inc="${p.id}" class="w-7 h-7 rounded-full border border-stone-300 hover:bg-stone-100 flex items-center justify-center" aria-label="Tambah"><i data-lucide="plus" class="w-3.5 h-3.5"></i></button>
            <button data-remove="${p.id}" class="ml-auto p-1.5 text-stone-400 hover:text-red-600" aria-label="Hapus"><i data-lucide="trash-2" class="w-4 h-4"></i></button>
          </div>
        </div>
      </div>`;
    }).join('') : `
      <div class="text-center text-stone-500 py-16">
        <i data-lucide="shopping-bag" class="w-12 h-12 mx-auto mb-3 text-stone-300"></i>
        <p class="font-medium">Keranjang masih kosong</p>
      </div>`;
    icons();
  }

  function addToCart(id) {
    const p = products.find(x => x.id === id);
    if (!p || p.stock <= 0) return;
    const item = cart.find(i => i.id === id);
    if (item) {
      if (item.qty >= p.stock) return toast('Stok tidak mencukupi');
      item.qty++;
    } else cart.push({ id, qty: 1 });
    renderCart();
    toast('Ditambahkan ke keranjang');
  }

  function changeQty(id, delta) {
    const item = cart.find(i => i.id === id);
    const p = products.find(x => x.id === id);
    if (!item || !p) return;
    const next = item.qty + delta;
    if (next <= 0) cart = cart.filter(i => i.id !== id);
    else if (next > p.stock) return toast('Stok tidak mencukupi');
    else item.qty = next;
    renderCart();
  }

  const openCart = () => { $('#cartOverlay').classList.remove('hidden'); $('#cartDrawer').classList.remove('translate-x-full'); };
  const closeCart = () => { $('#cartOverlay').classList.add('hidden'); $('#cartDrawer').classList.add('translate-x-full'); };

  function checkout() {
    const { count, total } = cartTotals();
    if (!count) return;
    // kurangi stok
    cart.forEach(i => { const p = products.find(x => x.id === i.id); if (p) p.stock = Math.max(0, p.stock - i.qty); });
    save(K_PRODUCTS, products);
    cart = [];
    renderCart(); renderProducts(); closeCart();
    toast(`Pesanan ${count} item (${rupiah(total)}) berhasil dibuat. Terima kasih!`);
  }

  // ====== AUTH ======
  function updateAuthUI() {
    $('#authLabel').textContent = isAdmin ? 'Logout' : 'Login';
    const iconHolder = $('#authBtn');
    const oldIcon = iconHolder.querySelector('i, svg');
    if (oldIcon) oldIcon.outerHTML = `<i data-lucide="${isAdmin ? 'log-out' : 'log-in'}" class="w-4 h-4"></i>`;
    $('#adminBadge').classList.toggle('hidden', !isAdmin);
    const add = $('#addProductBtn');
    add.classList.toggle('hidden', !isAdmin);
    add.classList.toggle('inline-flex', isAdmin);
    icons();
  }

  function login(u, p) {
    if (u === ADMIN_USER && p === ADMIN_PASS) {
      isAdmin = true; save(K_ADMIN, true);
      updateAuthUI(); renderProducts();
      closeModal('loginModal');
      toast('Berhasil masuk sebagai admin');
      return true;
    }
    return false;
  }

  function logout() {
    isAdmin = false; save(K_ADMIN, false);
    updateAuthUI(); renderProducts();
    toast('Anda telah logout');
  }

  // ====== ADMIN: CRUD ======
  function openProductForm(id) {
    const p = id ? products.find(x => x.id === id) : null;
    $('#productModalTitle').textContent = p ? 'Edit Produk' : 'Tambah Produk';
    $('#pId').value = p ? p.id : '';
    $('#pName').value = p?.name || '';
    $('#pCategory').value = p?.category || '';
    $('#pPrice').value = p?.price ?? '';
    $('#pStock').value = p?.stock ?? '';
    $('#pEmoji').value = p?.emoji || '';
    $('#pImage').value = p?.image || '';
    $('#pDesc').value = p?.desc || '';
    openModal('productModal');
  }

  function saveProduct(e) {
    e.preventDefault();
    if (!isAdmin) return;
    const idVal = $('#pId').value;
    const data = {
      name: $('#pName').value.trim(),
      category: $('#pCategory').value.trim(),
      price: Math.max(0, Number($('#pPrice').value) || 0),
      stock: Math.max(0, parseInt($('#pStock').value, 10) || 0),
      emoji: $('#pEmoji').value.trim(),
      image: $('#pImage').value.trim(),
      desc: $('#pDesc').value.trim()
    };
    if (idVal) {
      const p = products.find(x => x.id === Number(idVal));
      if (p) Object.assign(p, data);
      toast('Produk diperbarui');
    } else {
      const id = products.reduce((m, x) => Math.max(m, x.id), 0) + 1;
      products.push({ id, ...data });
      toast('Produk ditambahkan');
    }
    save(K_PRODUCTS, products);
    closeModal('productModal');
    renderCategories(); renderProducts(); renderCart();
  }

  function deleteProduct(id) {
    if (!isAdmin) return;
    const p = products.find(x => x.id === id);
    if (!p || !confirm(`Hapus produk "${p.name}"?`)) return;
    products = products.filter(x => x.id !== id);
    save(K_PRODUCTS, products);
    renderCategories(); renderProducts(); renderCart();
    toast('Produk dihapus');
  }

  // ====== EVENTS ======
  document.addEventListener('click', e => {
    const t = e.target.closest('button, [data-close]');
    if (!t) {
      // klik pada latar modal
      if (e.target.id && ['detailModal', 'loginModal', 'productModal'].includes(e.target.id)) closeModal(e.target.id);
      return;
    }
    if (t.dataset.cat) { activeCategory = t.dataset.cat; renderCategories(); renderProducts(); }
    else if (t.dataset.detail) showDetail(Number(t.dataset.detail));
    else if (t.dataset.add) addToCart(Number(t.dataset.add));
    else if (t.dataset.edit) openProductForm(Number(t.dataset.edit));
    else if (t.dataset.delete) deleteProduct(Number(t.dataset.delete));
    else if (t.dataset.inc) changeQty(Number(t.dataset.inc), 1);
    else if (t.dataset.dec) changeQty(Number(t.dataset.dec), -1);
    else if (t.dataset.remove) { cart = cart.filter(i => i.id !== Number(t.dataset.remove)); renderCart(); }
    else if (t.dataset.close) closeModal(t.dataset.close);
  });

  $('#cartBtn').addEventListener('click', openCart);
  $('#closeCart').addEventListener('click', closeCart);
  $('#cartOverlay').addEventListener('click', closeCart);
  $('#checkoutBtn').addEventListener('click', checkout);
  $('#clearCartBtn').addEventListener('click', () => { cart = []; renderCart(); });

  $('#authBtn').addEventListener('click', () => {
    if (isAdmin) return logout();
    $('#loginForm').reset(); $('#loginError').classList.add('hidden');
    openModal('loginModal');
    setTimeout(() => $('#loginUser').focus(), 50);
  });

  $('#loginForm').addEventListener('submit', e => {
    e.preventDefault();
    const ok = login($('#loginUser').value.trim(), $('#loginPass').value);
    $('#loginError').classList.toggle('hidden', ok);
  });

  $('#addProductBtn').addEventListener('click', () => openProductForm());
  $('#productForm').addEventListener('submit', saveProduct);

  const onSearch = e => {
    query = e.target.value.trim().toLowerCase();
    $('#searchInput').value = e.target.value;
    $('#searchInputMobile').value = e.target.value;
    renderProducts();
  };
  $('#searchInput').addEventListener('input', onSearch);
  $('#searchInputMobile').addEventListener('input', onSearch);
  $('#sortSelect').addEventListener('change', e => { sortBy = e.target.value; renderProducts(); });

  document.addEventListener('keydown', e => {
    if (e.key === 'Escape') { ['detailModal', 'loginModal', 'productModal'].forEach(closeModal); closeCart(); }
  });

  // ====== INIT ======
  $('#year').textContent = new Date().getFullYear();
  renderCategories();
  renderProducts();
  renderCart();
  updateAuthUI();
  icons();
})();
</script>
</body>
</html>
