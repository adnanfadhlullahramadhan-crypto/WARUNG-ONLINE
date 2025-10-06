# WARUNG-ONLINE<!doctype html>
<html lang="id">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Warung Online — Toko Kecil</title>
<style>
  :root{
    --bg:#fff9f0;
    --card:#ffffff;
    --accent:#ff6b6b;
    --muted:#6b6b6b;
    --text:#1f2937;
    --success:#16a34a;
    --glass: rgba(255,255,255,0.6);
    --shadow: 0 6px 18px rgba(31,41,55,0.08);
  }
  *{box-sizing:border-box}
  body{
    margin:0;
    font-family:Inter,system-ui,Segoe UI,Roboto,Arial;
    background:linear-gradient(180deg,#fff9f0,#fff3ee);
    color:var(--text);
    -webkit-font-smoothing:antialiased;
    -moz-osx-font-smoothing:grayscale;
  }

  header{
    display:flex;
    gap:16px;
    align-items:center;
    justify-content:space-between;
    padding:18px 24px;
    background:linear-gradient(90deg,#fff,#fff9f0);
    box-shadow:var(--shadow);
    position:sticky;
    top:0;
    z-index:50;
  }
  .brand{display:flex;gap:12px;align-items:center}
  .logo{
    width:52px;height:52px;border-radius:10px;background:linear-gradient(135deg,var(--accent),#ff9a9a);display:flex;align-items:center;justify-content:center;color:white;font-weight:700;font-size:20px;box-shadow:0 6px 18px rgba(255,107,107,0.18)
  }
  h1{font-size:18px;margin:0}
  .header-actions{display:flex;gap:12px;align-items:center}

  main{max-width:1200px;margin:20px auto;padding:0 18px}

  .controls{display:flex;gap:12px;flex-wrap:wrap;align-items:center;margin-bottom:16px}
  .search{
    flex:1;min-width:200px;
    display:flex;gap:8px;align-items:center;
    background:var(--card);padding:8px;border-radius:10px;border:1px solid rgba(0,0,0,0.04);
    box-shadow:var(--shadow);
  }
  .search input{border:0;outline:none;background:transparent;font-size:14px;flex:1;padding:6px}
  select, button{padding:8px 10px;border-radius:8px;border:0;background:var(--accent);color:white;cursor:pointer;font-weight:600}
  .filter-btn{background:transparent;border:1px solid rgba(0,0,0,0.06);color:var(--text);padding:8px 10px;border-radius:8px;cursor:pointer}
  .small{padding:6px 10px;font-size:13px}

  .layout{
    display:grid;
    grid-template-columns: 1fr 360px;
    gap:18px;
    align-items:start;
  }

  /* Product list */
  .product-grid{
    display:grid;
    grid-template-columns:repeat(auto-fill,minmax(220px,1fr));
    gap:16px;
  }
  .card{
    background:var(--card);
    border-radius:12px;
    overflow:hidden;
    border:1px solid rgba(0,0,0,0.04);
    box-shadow:var(--shadow);
    display:flex;
    flex-direction:column;
  }
  .media{
    height:160px;
    background:#f3f4f6;
    display:block;
  }
  .media img{width:100%;height:160px;object-fit:cover;display:block}
  .card-body{padding:12px;flex:1;display:flex;flex-direction:column}
  .title{font-weight:700;margin:0 0 6px;font-size:15px}
  .cat{font-size:12px;color:var(--muted);margin-bottom:8px}
  .desc{font-size:13px;color:var(--muted);flex:1;margin-bottom:8px}
  .row{display:flex;align-items:center;justify-content:space-between;gap:8px}
  .price{font-weight:800;color:var(--accent)}
  .add-btn{background:linear-gradient(90deg,var(--accent),#ff9a9a);border:0;color:white;padding:8px 10px;border-radius:8px;cursor:pointer;font-weight:700}

  /* Cart */
  .cart{
    position:sticky;top:84px;
  }
  .cart .cart-card{padding:12px;}
  .cart-list{display:flex;flex-direction:column;gap:8px;max-height:420px;overflow:auto;padding-right:6px}
  .cart-item{display:flex;gap:10px;align-items:center;background:rgba(255,255,255,0.02);padding:8px;border-radius:8px}
  .cart-item img{width:56px;height:56px;object-fit:cover;border-radius:8px}
  .cart-item .name{font-weight:700;font-size:13px}
  .qty{display:flex;gap:6px;align-items:center}
  .qty button{background:transparent;border:1px solid rgba(0,0,0,0.06);padding:4px 8px;border-radius:6px;cursor:pointer}
  .total{display:flex;justify-content:space-between;align-items:center;padding-top:8px;border-top:1px dashed rgba(0,0,0,0.06);margin-top:8px}
  .checkout{background:var(--success);border:0;color:white;padding:10px 12px;border-radius:8px;font-weight:800;cursor:pointer}

  /* Empty state */
  .empty{padding:28px;text-align:center;color:var(--muted);border:1px dashed rgba(0,0,0,0.04);border-radius:10px}

  /* Responsive */
  @media(max-width:980px){
    .layout{grid-template-columns:1fr}
    .cart{position:relative;top:0}
  }
</style>
</head>
<body>
  <header>
    <div class="brand">
      <div class="logo">W</div>
      <div>
        <h1>WarungOnline</h1>
        <div style="font-size:13px;color:var(--muted)">Belanja cepat & mudah</div>
      </div>
    </div>

    <div class="header-actions">
      <div style="font-size:14px;color:var(--muted)">Buka: 08:00 - 20:00</div>
      <button id="viewCartTop" class="small">Lihat Keranjang</button>
    </div>
  </header>

  <main>
    <div class="controls">
      <div class="search card" style="min-width:260px">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none"><path d="M21 21l-4.35-4.35" stroke="#9CA3AF" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/><circle cx="11" cy="11" r="6" stroke="#9CA3AF" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/></svg>
        <input id="q" placeholder="Cari produk (nasi, kopi, gula...)">
        <button id="clearSearch" class="filter-btn small">✖</button>
      </div>

      <select id="categoryFilter" class="filter-btn small">
        <option value="all">Semua Kategori</option>
        <option value="Makanan">Makanan</option>
        <option value="Minuman">Minuman</option>
        <option value="Sembako">Sembako</option>
        <option value="Cemilan">Cemilan</option>
      </select>

      <select id="sortBy" class="filter-btn small">
        <option value="reco">Rekomendasi</option>
        <option value="price-asc">Harga: Rendah → Tinggi</option>
        <option value="price-desc">Harga: Tinggi → Rendah</option>
      </select>

      <button id="resetFilters" class="filter-btn small">Reset Filter</button>
    </div>

    <div class="layout">
      <!-- product list -->
      <section>
        <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:12px">
          <h2 style="margin:0">Produk</h2>
          <div style="color:var(--muted);font-size:14px" id="resultCount"></div>
        </div>
        <div id="grid" class="product-grid"></div>
      </section>

      <!-- cart -->
      <aside class="cart">
        <div class="card cart-card">
          <h3 style="margin:0 0 8px">Keranjang</h3>
          <div id="cartList" class="cart-list"></div>
          <div id="emptyCart" class="empty" style="display:none">Keranjang kosong — tambahkan produk!</div>
          <div class="total">
            <div style="font-weight:700">Total</div>
            <div id="totalAmount" style="font-weight:900">Rp 0</div>
          </div>
          <div style="margin-top:10px;display:flex;gap:8px">
            <button id="clearCart" class="filter-btn small">Hapus Semua</button>
            <button id="checkout" class="checkout">Checkout</button>
          </div>
        </div>
      </aside>
    </div>
  </main>

<script>
/* =========================
   DATA SAMPLE PRODUK
   ========================= */
const PRODUCTS = [
  // Makanan
  {id:'p1',title:'Nasi Bungkus Ayam',price:15000,cat:'Makanan',desc:'Nasi hangat + ayam goreng krispi',img:'https://images.unsplash.com/photo-1604908177522-0d77f2a1f56a?auto=format&fit=crop&w=800&q=60'},
  {id:'p2',title:'Nasi Goreng Spesial',price:18000,cat:'Makanan',desc:'Nasi goreng dengan telur dan saus spesial',img:'https://images.unsplash.com/photo-1604908177360-6d03e724a3b3?auto=format&fit=crop&w=800&q=60'},
  {id:'p3',title:'Mie Ayam Bakso',price:17000,cat:'Makanan',desc:'Mie kenyal + ayam cincang + siomay',img:'https://images.unsplash.com/photo-1543353071-087092ec3937?auto=format&fit=crop&w=800&q=60'},

  // Minuman
  {id:'p4',title:'Kopi Tubruk',price:8000,cat:'Minuman',desc:'Kopi hitam khas warung',img:'https://images.unsplash.com/photo-1498804103079-a6351b050096?auto=format&fit=crop&w=800&q=60'},
  {id:'p5',title:'Teh Manis Es',price:7000,cat:'Minuman',desc:'Teh manis dingin menyegarkan',img:'https://images.unsplash.com/photo-1551022378-3f2c0b78f2d3?auto=format&fit=crop&w=800&q=60'},
  {id:'p6',title:'Jus Jeruk',price:12000,cat:'Minuman',desc:'Jus jeruk segar peras langsung',img:'https://images.unsplash.com/photo-1572441710269-30f120f3f6b4?auto=format&fit=crop&w=800&q=60'},

  // Sembako
  {id:'p7',title:'Beras 5kg',price:65000,cat:'Sembako',desc:'Beras medium, cocok untuk keluarga',img:'https://images.unsplash.com/photo-1589308078059-1b2b40e1d7d9?auto=format&fit=crop&w=800&q=60'},
  {id:'p8',title:'Minyak Goreng 2L',price:30000,cat:'Sembako',desc:'Minyak goreng kualitas baik',img:'https://images.unsplash.com/photo-1603046891432-0b6a8a2ee1b4?auto=format&fit=crop&w=800&q=60'},
  {id:'p9',title:'Gula Pasir 1kg',price:15000,cat:'Sembako',desc:'Gula pasir putih kemasan',img:'https://images.unsplash.com/photo-1544025162-d76694265947?auto=format&fit=crop&w=800&q=60'},

  // Cemilan
  {id:'p10',title:'Keripik Singkong',price:12000,cat:'Cemilan',desc:'Keripik gurih renyah',img:'https://images.unsplash.com/photo-1544025162-d76694265947?auto=format&fit=crop&w=800&q=60'},
  {id:'p11',title:'Kacang Goreng',price:10000,cat:'Cemilan',desc:'Kacang gurih dengan rasa pedas manis',img:'https://images.unsplash.com/photo-1601924582975-4a4f8b3b7b57?auto=format&fit=crop&w=800&q=60'},
  {id:'p12',title:'Biskuit Cokelat',price:8000,cat:'Cemilan',desc:'Biskuit renyah dengan lapisan cokelat',img:'https://images.unsplash.com/photo-1578985545062-69928b1d9587?auto=format&fit=crop&w=800&q=60'}
];

/* =========================
   STATE: CART (localStorage)
   ========================= */
const CART_KEY = 'warung_cart_v1';
let cart = JSON.parse(localStorage.getItem(CART_KEY) || '{}'); // { productId: qty }

/* =========================
   HELPERS
   ========================= */
const rupiah = v => 'Rp ' + Number(v).toLocaleString('id-ID');

function saveCart(){ localStorage.setItem(CART_KEY, JSON.stringify(cart)); renderCart(); }

function addToCart(id, qty=1){
  cart[id] = (cart[id] || 0) + qty;
  saveCart();
  flashAdded(id);
}

function setQty(id, qty){
  if(qty <= 0) delete cart[id];
  else cart[id] = qty;
  saveCart();
}

function clearCart(){
  cart = {};
  saveCart();
}

/* =========================
   RENDER PRODUCTS
   ========================= */
const gridEl = document.getElementById('grid');
const qEl = document.getElementById('q');
const catEl = document.getElementById('categoryFilter');
const sortEl = document.getElementById('sortBy');
const resultCount = document.getElementById('resultCount');

function renderProducts(){
  const q = (qEl.value || '').trim().toLowerCase();
  const cat = catEl.value;
  const sort = sortEl.value;

  let list = PRODUCTS.filter(p=>{
    if(cat !== 'all' && p.cat !== cat) return false;
    if(q && !(p.title.toLowerCase().includes(q) || p.desc.toLowerCase().includes(q) || p.cat.toLowerCase().includes(q))) return false;
    return true;
  });

  if(sort === 'price-asc') list.sort((a,b)=>a.price-b.price);
  else if(sort === 'price-desc') list.sort((a,b)=>b.price-a.price);

  resultCount.textContent = `${list.length} produk`;
  gridEl.innerHTML = list.map(p=>`
    <article class="card">
      <a class="media" href="javascript:void(0)" onclick="openQuick(${JSON.stringify(p.id)})">
        <img src="${p.img}" alt="${escapeHtml(p.title)}">
      </a>
      <div class="card-body">
        <div style="display:flex;justify-content:space-between;align-items:start">
          <div>
            <div class="title">${escapeHtml(p.title)}</div>
            <div class="cat">${escapeHtml(p.cat)}</div>
          </div>
          <div class="price">${rupiah(p.price)}</div>
        </div>
        <div class="desc">${escapeHtml(p.desc)}</div>
        <div class="row" style="margin-top:6px">
          <button class="add-btn" onclick='addToCart("${p.id}",1)'>+ Keranjang</button>
          <button class="filter-btn small" onclick='buyNow("${p.id}")'>Beli Sekarang</button>
        </div>
      </div>
    </article>
  `).join('');
}

/* small escape */
function escapeHtml(s){
  return String(s).replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":"&#39;"}[c]));
}

/* =========================
   CART RENDER
   ========================= */
const cartListEl = document.getElementById('cartList');
const emptyCartEl = document.getElementById('emptyCart');
const totalAmountEl = document.getElementById('totalAmount');

function renderCart(){
  const entries = Object.keys(cart).map(id => {
    const product = PRODUCTS.find(p=>p.id===id);
    return {id, product, qty: cart[id]};
  });

  if(entries.length === 0){
    cartListEl.innerHTML = '';
    emptyCartEl.style.display = 'block';
    totalAmountEl.textContent = rupiah(0);
    return;
  }
  emptyCartEl.style.display = 'none';
  cartListEl.innerHTML = entries.map(e=>`
    <div class="cart-item">
      <img src="${e.product.img}" alt="${escapeHtml(e.product.title)}">
      <div style="flex:1">
        <div class="name">${escapeHtml(e.product.title)}</div>
        <div style="font-size:13px;color:var(--muted)">${rupiah(e.product.price)} x ${e.qty} = <strong>${rupiah(e.product.price*e.qty)}</strong></div>
      </div>
      <div style="display:flex;flex-direction:column;align-items:flex-end;gap:6px">
        <div class="qty">
          <button onclick='changeQty("${e.id}", -1)'>−</button>
          <div style="padding:4px 8px;border-radius:6px;border:1px solid rgba(0,0,0,0.06);min-width:36px;text-align:center">${e.qty}</div>
          <button onclick='changeQty("${e.id}", 1)'>＋</button>
        </div>
        <button style="background:transparent;border:0;color:#ff5c5c;cursor:pointer" onclick='removeItem("${e.id}")'>Hapus</button>
      </div>
    </div>
  `).join('');

  const total = entries.reduce((s,e)=>s + e.product.price * e.qty, 0);
  totalAmountEl.textContent = rupiah(total);
}

/* cart ops called from HTML */
function changeQty(id, delta){
  const current = cart[id] || 0;
  const next = current + delta;
  if(next <= 0) { delete cart[id]; }
  else cart[id] = next;
  saveCart();
}
function removeItem(id){ delete cart[id]; saveCart(); }
function buyNow(id){
  addToCart(id,1);
  // simulate quick checkout
  setTimeout(()=>alert('Produk ditambahkan. Lanjut ke checkout di panel kanan.'),120);
}

/* small visual feedback */
function flashAdded(id){
  // minimal feedback: alert kecil di pojok (simple)
  const p = PRODUCTS.find(x=>x.id===id);
  if(!p) return;
  const n = document.createElement('div');
  n.style.position='fixed';
  n.style.right='18px';
  n.style.bottom='18px';
  n.style.background='linear-gradient(90deg,var(--accent),#ff9a9a)';
  n.style.color='white';
  n.style.padding='10px 14px';
  n.style.borderRadius='10px';
  n.style.boxShadow='0 8px 24px rgba(255,107,107,0.2)';
  n.style.zIndex=9999;
  n.textContent = `${p.title} ditambahkan ke keranjang`;
  document.body.appendChild(n);
  setTimeout(()=>n.style.opacity='0',2200);
  setTimeout(()=>n.remove(),2600);
}

/* =========================
   CHECKOUT (simulasi)
   ========================= */
document.getElementById('checkout').onclick = ()=>{
  const entries = Object.keys(cart);
  if(entries.length === 0){ alert('Keranjang kosong. Tambahkan produk dulu.'); return; }
  const total = Object.keys(cart).reduce((s,id)=>{
    const p = PRODUCTS.find(x=>x.id===id);
    return s + p.price * cart[id];
  },0);
  const name = prompt('Masukkan nama penerima:');
  if(!name) return alert('Checkout dibatalkan.');
  const addr = prompt('Masukkan alamat (contoh: Jl. Mawar No.10):');
  if(!addr) return alert('Checkout dibatalkan.');
  // Simulasi konfirmasi
  alert(`Terima kasih ${name}!\nTotal: ${rupiah(total)}\nPesanan akan dikirim ke:\n${addr}\n\n(NB: ini simulasi — tidak ada transaksi nyata)`);
  clearCart();
};

/* =========================
   EVENTS & INIT
   ========================= */
document.getElementById('clearSearch').onclick = ()=>{ qEl.value=''; renderProducts(); };
document.getElementById('resetFilters').onclick = ()=>{
  qEl.value=''; catEl.value='all'; sortEl.value='reco'; renderProducts();
};
qEl.addEventListener('input', ()=>{ renderProducts(); });
catEl.addEventListener('change', ()=>{ renderProducts(); });
sortEl.addEventListener('change', ()=>{ renderProducts(); });

document.getElementById('clearCart').onclick = ()=>{
  if(confirm('Hapus semua item di keranjang?')) clearCart();
};

document.getElementById('viewCartTop').onclick = ()=>{
  window.scrollTo({top:document.body.scrollHeight, behavior:'smooth'});
};

/* initial render */
renderProducts();
renderCart();
saveCart(); // ensure stored

/* =========================
   Optional: keyboard quick add (1..9)
   ========================= */
window.addEventListener('keydown', e=>{
  if(e.key >= '1' && e.key <= '9'){
    const idx = parseInt(e.key)-1;
    const p = PRODUCTS[idx];
    if(p) addToCart(p.id,1);
  }
});
</script>
</body>
</html>
