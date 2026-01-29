<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>Thamam361 | Blog & Produk Digital</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">

<style>
:root{
  --brand:#0ea5e9;
  --brand2:#22c55e;
}

*{
  margin:0;
  padding:0;
  box-sizing:border-box;
  font-family:Poppins,sans-serif;
}

body{
  background:#f4f6fb;
  color:#333;
  padding-bottom:110px;
  font-size:14px;
}

/* HEADER */
header{
  background:linear-gradient(135deg,var(--brand),var(--brand2));
  color:#fff;
  padding:20px 15px;
  text-align:center;
  border-radius:0 0 22px 22px;
}
header img{
  width:65px;
  height:65px;
  border-radius:50%;
  border:3px solid #fff;
  object-fit:cover;
}
header h2{font-size:20px;margin-top:8px}
header p{font-size:13px;opacity:.9}

/* LAYOUT */
.container{
  max-width:100%;
  padding:12px;
}

/* GRID MOBILE FIRST */
.grid{
  display:grid;
  grid-template-columns:1fr;
  gap:14px;
}

/* CARD */
.card{
  background:#fff;
  padding:14px;
  border-radius:16px;
  box-shadow:0 6px 16px rgba(0,0,0,.08);
}
.card img{
  width:100%;
  height:150px;
  object-fit:cover;
  border-radius:12px;
}
.card h4{margin-top:8px;font-size:15px}
.price{
  color:var(--brand);
  font-weight:700;
  margin:4px 0;
}

/* FORM & BUTTON */
button{
  background:var(--brand);
  color:#fff;
  border:none;
  padding:12px;
  border-radius:14px;
  width:100%;
  margin-top:8px;
  font-size:14px;
  font-weight:600;
}
input,select{
  width:100%;
  padding:12px;
  border-radius:12px;
  border:1px solid #ccc;
  margin-bottom:10px;
  font-size:14px;
}

/* FLOATING BUTTON */
.fab{
  position:fixed;
  bottom:95px;
  right:14px;
  background:var(--brand);
  width:52px;
  height:52px;
  border-radius:50%;
  color:#fff;
  font-size:24px;
  display:flex;
  align-items:center;
  justify-content:center;
  box-shadow:0 8px 20px rgba(0,0,0,.25);
  z-index:999;
}

/* CONTACT BAR */
.contact-bar{
  position:fixed;
  bottom:0;
  left:0;
  width:100%;
  background:linear-gradient(135deg,var(--brand),var(--brand2));
  display:flex;
  justify-content:space-around;
  padding:8px 4px;
  z-index:998;
}
.contact-bar a{
  color:#fff;
  font-size:11px;
  text-decoration:none;
  background:rgba(255,255,255,.2);
  padding:7px 10px;
  border-radius:20px;
  font-weight:600;
}

/* TABLET & DESKTOP */
@media (min-width:768px){
  body{font-size:15px}
  .grid{grid-template-columns:repeat(2,1fr)}
  .container{max-width:900px;margin:auto}
}
</style>
</head>

<body>

<header>
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

<div id="checkout" class="card" style="display:none">
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

<div class="fab" onclick="window.scrollTo({top:0,behavior:'smooth'})">⬆️</div>

<div class="contact-bar">
  <a href="https://wa.me/6285123622237">📞 WA</a>
  <a href="https://instagram.com/thamam361">📸 IG</a>
  <a href="https://tiktok.com/@thamam361">🎵 TikTok</a>
  <a href="https://youtube.com/@thamam361">▶️ YT</a>
</div>

<script>
const adminWA="6285123622237";

const products=[
  {n:"Modul Coding Pemula",p:25000,img:"https://images.unsplash.com/photo-1498050108023-c5249f4df085"},
  {n:"Ebook Jualan Digital",p:30000,img:"https://images.unsplash.com/photo-1526378722484-bd91ca387e72"},
  {n:"Template Website Siap Pakai",p:50000,img:"https://images.unsplash.com/photo-1519389950473-47ba0277781c"},
  {n:"Paket Belajar AI Dasar",p:40000,img:"https://images.unsplash.com/photo-1677442136019-21780ecad995"}
];

let cart=[];

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

function add(i){
  cart.push(products[i]);
  renderCart();
}

function renderCart(){
  if(cart.length===0){
    cart.innerHTML="Keranjang kosong";
    checkout.style.display="none";
    return;
  }
  let total=0;
  cart.innerHTML="";
  cart.forEach(x=>{
    total+=x.p;
    cart.innerHTML+=`${x.n} - Rp ${x.p.toLocaleString()}<br>`;
  });
  cart.innerHTML+=`<hr><b>Total: Rp ${total.toLocaleString()}</b>`;
  checkout.style.display="block";
}

function kirimWA(){
  if(!nama.value||!wa.value){
    alert("Lengkapi data!");
    return;
  }
  let pesan=`Halo Admin 👋%0A
Nama: ${nama.value}%0A
WA: ${wa.value}%0A
Pembayaran: ${pay.value}%0AProduk:%0A`;
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
