# blog-thamam361
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Thamam361 | Blog & Produk Digital</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">

<style>
/* ===== BRANDING ===== */
:root{
  --brand:#0ea5e9;      /* GANTI WARNA BRAND */
  --brand2:#22c55e;
}

/* ===== RESET ===== */
*{margin:0;padding:0;box-sizing:border-box;font-family:Poppins}
body{background:#f4f6fb;color:#333;padding-bottom:90px}

/* ===== HEADER ===== */
header{
  background:linear-gradient(135deg,var(--brand),var(--brand2));
  color:#fff;
  padding:20px;
  text-align:center;
  border-radius:0 0 25px 25px;
}
header img{
  width:70px;
  height:70px;
  border-radius:50%;
  border:3px solid #fff;
  object-fit:cover;
}

/* ===== LAYOUT ===== */
.container{max-width:900px;margin:auto;padding:15px}
.grid{display:grid;gap:15px}

/* ===== CARD ===== */
.card{
  background:#fff;
  padding:15px;
  border-radius:16px;
  box-shadow:0 8px 20px rgba(0,0,0,.08);
}
.card img{
  width:100%;
  height:160px;
  object-fit:cover;
  border-radius:12px;
}
.price{color:var(--brand);font-weight:700}

/* ===== FORM & BUTTON ===== */
button{
  background:var(--brand);
  color:#fff;
  border:none;
  padding:10px;
  border-radius:12px;
  width:100%;
  margin-top:8px;
  font-weight:600;
}
input,select{
  width:100%;
  padding:10px;
  border-radius:10px;
  border:1px solid #ccc;
  margin-bottom:10px;
}

/* ===== FLOATING BUTTON ===== */
.fab{
  position:fixed;
  bottom:85px;
  right:15px;
  background:var(--brand);
  width:55px;
  height:55px;
  border-radius:50%;
  color:#fff;
  font-size:26px;
  display:flex;
  align-items:center;
  justify-content:center;
  box-shadow:0 8px 20px rgba(0,0,0,.25);
  z-index:999;
  cursor:pointer;
}

/* ===== CONTACT BAR ===== */
.contact-bar{
  position:fixed;
  bottom:0;
  left:0;
  width:100%;
  background:linear-gradient(135deg,var(--brand),var(--brand2));
  display:flex;
  justify-content:space-around;
  padding:10px 5px;
  z-index:998;
}
.contact-bar a{
  color:#fff;
  font-size:12px;
  text-decoration:none;
  background:rgba(255,255,255,.2);
  padding:8px 12px;
  border-radius:20px;
  font-weight:600;
}

/* ===== HIDDEN ===== */
.hidden{display:none}
</style>
</head>

<body>

<!-- ===== HEADER ===== -->
<header>
  <!-- GANTI LOGO -->
  <img src="https://i.imgur.com/7k12EPD.png">
  <h2>Thamam361</h2>
  <p>Blog • Produk Digital • Edukasi</p>
</header>

<div class="container">

<h3>📦 Produk Digital</h3>
<div id="produk" class="grid"></div>

<br>
<h3>🛒 Keranjang</h3>
<div id="cart" class="card">Keranjang kosong</div>

<div id="checkout" class="card hidden">
  <h3>🧾 Form Order</h3>
  <input id="nama" placeholder="Nama">
  <input id="wa" placeholder="Nomor WhatsApp">
  <select id="pay">
    <option>QRIS</option>
    <option>DANA</option>
    <option>OVO</option>
  </select>
  <button onclick="kirimWA()">Kirim Pesanan via WhatsApp</button>
</div>

</div>

<!-- ===== FLOATING BUTTON ===== -->
<div class="fab" onclick="scrollTo({top:0,behavior:'smooth'})">⬆️</div>

<!-- ===== CONTACT BAR ===== -->
<div class="contact-bar">
  <a href="https://wa.me/62895367231635" target="_blank">📞 WA</a>
  <a href="https://instagram.com/thamam361" target="_blank">📸 IG</a>
  <a href="https://tiktok.com/@thamam361" target="_blank">🎵 TikTok</a>
  <a href="https://youtube.com/@thamam361" target="_blank">▶️ YT</a>
</div>

<script>
/* ===== DATA PRODUK ===== */
const adminWA="62895367231635"; // NOMOR ADMIN

const products=[
  {n:"Modul Coding Pemula",p:25000,img:"https://images.unsplash.com/photo-1498050108023-c5249f4df085"},
  {n:"Ebook Jualan Digital",p:30000,img:"https://images.unsplash.com/photo-1526378722484-bd91ca387e72"},
  {n:"Template Website Siap Pakai",p:50000,img:"https://images.unsplash.com/photo-1519389950473-47ba0277781c"},
  {n:"Paket Belajar AI Dasar",p:40000,img:"https://images.unsplash.com/photo-1677442136019-21780ecad995"}
];

let cart=[];

/* ===== RENDER PRODUK ===== */
function renderProduk(){
  produk.innerHTML="";
  products.forEach((x,i)=>{
    produk.innerHTML+=`
    <div class="card">
      <img src="${x.img}">
      <h4>${x.n}</h4>
      <p class="price">Rp ${x.p.toLocaleString()}</p>
      <button onclick="add(${i})">Tambah ke Keranjang</button>
    </div>`;
  });
}
renderProduk();

/* ===== CART ===== */
function add(i){
  cart.push(products[i]);
  renderCart();
}

function renderCart(){
  if(cart.length===0){
    cart.innerHTML="Keranjang kosong";
    checkout.classList.add("hidden");
    return;
  }
  let total=0;
  cart.innerHTML="";
  cart.forEach(x=>{
    total+=x.p;
    cart.innerHTML+=`${x.n} - Rp ${x.p.toLocaleString()}<br>`;
  });
  cart.innerHTML+=`<hr><b>Total: Rp ${total.toLocaleString()}</b>`;
  checkout.classList.remove("hidden");
}

/* ===== KIRIM ORDER KE WHATSAPP ===== */
function kirimWA(){
  if(!nama.value || !wa.value){
    alert("Lengkapi data!");
    return;
  }
  let pesan=`Halo Admin 👋%0A
Nama: ${nama.value}%0A
WA: ${wa.value}%0A
Pembayaran: ${pay.value}%0A
Produk:%0A`;

  let total=0;
  cart.forEach(p=>{
    pesan+=`- ${p.n} (Rp ${p.p.toLocaleString()})%0A`;
    total+=p.p;
  });

  pesan+=`%0ATotal: Rp ${total.toLocaleString()}`;

  window.open(`https://wa.me/${adminWA}?text=${pesan}`,"_blank");
}
</script>

</body>
</html>
