<!DOCTYPE html>
<html lang="id" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DONIX PARFUME | Luxury Fragrance Collection 2026</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; }
        h1, h2, h3, .font-luxury { font-family: 'Playfair Display', serif; }
        
        .gold-gradient {
            background: linear-gradient(135deg, #BF953F, #FCF6BA, #B38728, #FBF5B7, #AA771C);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .bg-gold-metallic {
            background: linear-gradient(135deg, #BF953F, #AA771C);
        }
        .glass {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        .product-card:hover .product-action {
            opacity: 1;
            transform: translateY(0);
        }
        .animate-fade-in {
            animation: fadeIn 0.8s ease-out forwards;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .sticky-nav {
            background: rgba(0, 0, 0, 0.9);
            backdrop-filter: blur(15px);
            border-bottom: 1px solid #BF953F;
        }
        /* Custom Scrollbar */
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: #111; }
        ::-webkit-scrollbar-thumb { background: #BF953F; border-radius: 4px; }
    </style>
</head>
<body class="bg-black text-white overflow-x-hidden">

    <!-- LOADING SCREEN -->
    <div id="loading-screen" class="fixed inset-0 z-[100] bg-black flex flex-col items-center justify-center transition-opacity duration-700">
        <div class="w-24 h-24 border-4 border-gold-metallic border-t-transparent rounded-full animate-spin mb-4"></div>
        <h2 class="font-luxury text-2xl gold-gradient tracking-widest uppercase">Donix Parfume</h2>
    </div>

    <!-- NOTIFICATION TOAST -->
    <div id="toast" class="fixed top-24 right-5 z-[80] transform translate-x-full transition-transform duration-300">
        <div class="bg-white text-black px-6 py-3 rounded shadow-2xl border-l-4 border-yellow-600 flex items-center space-x-3">
            <i class="fas fa-check-circle text-green-600"></i>
            <span id="toast-msg">Item ditambahkan ke keranjang!</span>
        </div>
    </div>

    <!-- MAIN WRAPPER (STOREFRONT) -->
    <div id="storefront" class="block">
        <!-- HEADER / NAVBAR -->
        <nav id="navbar" class="fixed w-full z-50 transition-all duration-300 py-6 px-4 md:px-12 flex items-center justify-between border-b border-white/10">
            <div class="flex items-center space-x-8">
                <a href="#" class="text-2xl md:text-3xl font-luxury font-bold tracking-tighter gold-gradient">DONIX PARFUME</a>
                <div class="hidden lg:flex space-x-6 text-xs uppercase tracking-widest font-medium">
                    <a href="#" class="hover:text-yellow-500 transition">Home</a>
                    <a href="#shop" class="hover:text-yellow-500 transition">Shop</a>
                    <a href="#" class="hover:text-yellow-500 transition">Men</a>
                    <a href="#" class="hover:text-yellow-500 transition">Women</a>
                    <a href="#" class="hover:text-yellow-500 transition">Unisex</a>
                </div>
            </div>

            <div class="flex items-center space-x-5">
                <div class="hidden md:flex relative">
                    <input type="text" id="searchInput" placeholder="Cari parfum..." class="bg-white/10 border border-white/20 rounded-full py-1 px-4 text-sm focus:outline-none focus:border-yellow-500 w-48">
                    <i class="fas fa-search absolute right-3 top-2 text-gray-400"></i>
                </div>
                <button onclick="toggleAdminPanel()" class="hover:text-yellow-500 transition"><i class="fas fa-user-shield"></i></button>
                <button class="hover:text-yellow-500 transition relative">
                    <i class="fas fa-heart"></i>
                    <span class="absolute -top-2 -right-2 bg-yellow-600 text-[10px] rounded-full w-4 h-4 flex items-center justify-center">0</span>
                </button>
                <button onclick="toggleCart()" class="hover:text-yellow-500 transition relative">
                    <i class="fas fa-shopping-bag"></i>
                    <span id="cart-count" class="absolute -top-2 -right-2 bg-yellow-600 text-[10px] rounded-full w-4 h-4 flex items-center justify-center">0</span>
                </button>
                <button class="md:hidden text-2xl"><i class="fas fa-bars"></i></button>
            </div>
        </nav>

        <!-- HERO SECTION -->
        <section class="relative h-screen flex items-center justify-center overflow-hidden">
            <div class="absolute inset-0">
                <img src="https://images.unsplash.com/photo-1541643600914-78b084683601?auto=format&fit=crop&q=80&w=1920" alt="Hero" class="w-full h-full object-cover scale-105 opacity-60">
                <div class="absolute inset-0 bg-gradient-to-t from-black via-transparent to-black"></div>
            </div>
            <div class="relative z-10 text-center px-4 animate-fade-in">
                <h3 class="text-yellow-500 uppercase tracking-[0.5em] mb-4 text-sm">Exclusive Release 2026</h3>
                <h1 class="text-5xl md:text-8xl font-luxury mb-6 leading-tight">Luxury Fragrance<br><span class="gold-gradient italic">Collection</span></h1>
                <p class="text-gray-300 max-w-lg mx-auto mb-10 text-lg leading-relaxed font-light">Temukan aroma terbaik yang mendefinisikan karakter dan kemewahan Anda di setiap tetesnya.</p>
                <div class="flex flex-col md:flex-row items-center justify-center space-y-4 md:space-y-0 md:space-x-6">
                    <a href="#shop" class="bg-gold-metallic text-black px-10 py-4 rounded-full font-bold uppercase tracking-widest text-xs hover:scale-105 transition-transform duration-300">Shop Now</a>
                    <a href="#" class="border border-white/30 backdrop-blur-md px-10 py-4 rounded-full font-bold uppercase tracking-widest text-xs hover:bg-white hover:text-black transition-all">Explore Collection</a>
                </div>
            </div>
        </section>

        <!-- FLASH SALE -->
        <section class="py-12 bg-zinc-950 border-y border-yellow-900/30">
            <div class="container mx-auto px-6 flex flex-col md:flex-row items-center justify-between">
                <div class="flex items-center space-x-4 mb-6 md:mb-0">
                    <div class="bg-yellow-600 p-3 rounded-lg"><i class="fas fa-bolt text-black text-xl"></i></div>
                    <div>
                        <h2 class="font-luxury text-2xl uppercase tracking-wider">Flash Sale</h2>
                        <p class="text-gray-500 text-sm">Berakhir dalam:</p>
                    </div>
                </div>
                <div class="flex space-x-4 text-center">
                    <div class="bg-black border border-yellow-600/50 p-3 rounded w-16 md:w-20">
                        <span id="timer-h" class="text-xl md:text-2xl font-bold block">02</span>
                        <span class="text-[10px] text-gray-500 uppercase">Jam</span>
                    </div>
                    <div class="bg-black border border-yellow-600/50 p-3 rounded w-16 md:w-20">
                        <span id="timer-m" class="text-xl md:text-2xl font-bold block">45</span>
                        <span class="text-[10px] text-gray-500 uppercase">Menit</span>
                    </div>
                    <div class="bg-black border border-yellow-600/50 p-3 rounded w-16 md:w-20">
                        <span id="timer-s" class="text-xl md:text-2xl font-bold block">12</span>
                        <span class="text-[10px] text-gray-500 uppercase">Detik</span>
                    </div>
                </div>
                <a href="#" class="mt-6 md:mt-0 text-yellow-500 font-bold uppercase tracking-widest text-xs border-b border-yellow-500 pb-1">Lihat Semua Promo</a>
            </div>
        </section>

        <!-- SHOP SECTION -->
        <section id="shop" class="py-24 container mx-auto px-6">
            <div class="flex flex-col md:flex-row items-end justify-between mb-16 space-y-6">
                <div>
                    <h2 class="text-4xl md:text-5xl font-luxury mb-4">Our Masterpieces</h2>
                    <div class="h-1 w-24 bg-gold-metallic"></div>
                </div>
                <div class="flex flex-wrap gap-4 text-xs uppercase tracking-widest font-semibold">
                    <button onclick="filterProducts('all')" class="px-6 py-2 border border-yellow-600 bg-yellow-600 text-black rounded-full">All</button>
                    <button onclick="filterProducts('men')" class="px-6 py-2 border border-white/20 hover:border-yellow-600 rounded-full transition">Men</button>
                    <button onclick="filterProducts('women')" class="px-6 py-2 border border-white/20 hover:border-yellow-600 rounded-full transition">Women</button>
                    <button onclick="filterProducts('unisex')" class="px-6 py-2 border border-white/20 hover:border-yellow-600 rounded-full transition">Unisex</button>
                </div>
            </div>

            <div id="product-grid" class="grid grid-cols-2 lg:grid-cols-4 gap-8">
                <!-- Products will be injected here by JS -->
            </div>
        </section>

        <!-- ABOUT SECTION -->
        <section class="py-24 bg-zinc-950">
            <div class="container mx-auto px-6 grid md:grid-cols-2 gap-16 items-center">
                <div class="relative">
                    <img src="https://images.unsplash.com/photo-1594035910387-fea47794261f?auto=format&fit=crop&q=80&w=800" alt="Craftsmanship" class="rounded-lg shadow-2xl grayscale hover:grayscale-0 transition-all duration-700">
                    <div class="absolute -bottom-10 -right-10 bg-gold-metallic p-10 hidden lg:block">
                        <p class="text-black font-luxury text-4xl">Since<br>2022</p>
                    </div>
                </div>
                <div>
                    <h4 class="text-yellow-600 uppercase tracking-widest mb-4">The Legacy of Donix</h4>
                    <h2 class="text-4xl md:text-6xl font-luxury mb-8">Kualitas Tanpa Kompromi</h2>
                    <p class="text-gray-400 mb-8 leading-relaxed text-lg">Donix Parfume menghadirkan standar baru dalam dunia wewangian premium. Kami hanya menggunakan bahan-bahan terbaik dari Prancis dan Swiss untuk memastikan ketahanan aroma hingga 24 jam dengan sillage yang memikat.</p>
                    <div class="grid grid-cols-2 gap-8 mb-10">
                        <div>
                            <h5 class="text-xl font-luxury mb-2">Original 100%</h5>
                            <p class="text-xs text-gray-500 uppercase tracking-tighter">Garansi keaslian setiap produk</p>
                        </div>
                        <div>
                            <h5 class="text-xl font-luxury mb-2">Long Lasting</h5>
                            <p class="text-xs text-gray-500 uppercase tracking-tighter">Konsentrasi Extrait de Parfum</p>
                        </div>
                    </div>
                    <button class="bg-white text-black px-8 py-3 rounded-full text-xs font-bold uppercase tracking-widest">About Our Brand</button>
                </div>
            </div>
        </section>

        <!-- TESTIMONIALS -->
        <section class="py-24 overflow-hidden">
            <div class="text-center mb-16">
                <h2 class="text-4xl font-luxury">What Our VIP Say</h2>
            </div>
            <div class="flex animate-marquee whitespace-nowrap space-x-8">
                <!-- Simple loop generated via CSS animation -->
                <div class="inline-block glass p-8 rounded-2xl w-[350px] shrink-0">
                    <div class="flex text-yellow-500 mb-4"><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i></div>
                    <p class="text-gray-300 italic mb-4 whitespace-normal">"Baunya sangat mewah, tahan lama banget dipakai seharian di kantor. Donix emang gak main-main!"</p>
                    <p class="font-bold text-yellow-600">Andini - Jakarta</p>
                </div>
                <div class="inline-block glass p-8 rounded-2xl w-[350px] shrink-0">
                    <div class="flex text-yellow-500 mb-4"><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i></div>
                    <p class="text-gray-300 italic mb-4 whitespace-normal">"Pelayanannya cepat, packing kayu aman banget. Dior Sauvage nya beneran ori!"</p>
                    <p class="font-bold text-yellow-600">Rizky - Bandung</p>
                </div>
                <div class="inline-block glass p-8 rounded-2xl w-[350px] shrink-0">
                    <div class="flex text-yellow-500 mb-4"><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i></div>
                    <p class="text-gray-300 italic mb-4 whitespace-normal">"Gak nyesel beli Baccarat di sini. Worth every penny! Wanginya semerbak ke seluruh ruangan."</p>
                    <p class="font-bold text-yellow-600">Jessica - Surabaya</p>
                </div>
            </div>
        </section>

        <!-- FOOTER -->
        <footer class="bg-zinc-950 pt-24 pb-12 border-t border-white/5">
            <div class="container mx-auto px-6 grid grid-cols-1 md:grid-cols-4 gap-12 mb-20">
                <div class="col-span-1 md:col-span-2">
                    <h2 class="text-3xl font-luxury gold-gradient mb-6 tracking-tighter">DONIX PARFUME</h2>
                    <p class="text-gray-500 max-w-sm mb-8 leading-relaxed">Penyedia parfum premium, original, dan berkelas dunia untuk mereka yang menghargai kualitas dan eksklusivitas.</p>
                    <div class="flex space-x-6">
                        <a href="#" class="text-2xl text-gray-500 hover:text-yellow-600 transition"><i class="fab fa-instagram"></i></a>
                        <a href="#" class="text-2xl text-gray-500 hover:text-yellow-600 transition"><i class="fab fa-tiktok"></i></a>
                        <a href="#" class="text-2xl text-gray-500 hover:text-yellow-600 transition"><i class="fab fa-facebook"></i></a>
                    </div>
                </div>
                <div>
                    <h4 class="text-sm font-bold uppercase tracking-[0.2em] mb-6">Contact Us</h4>
                    <ul class="space-y-4 text-gray-400 text-sm">
                        <li class="flex items-start space-x-3">
                            <i class="fas fa-map-marker-alt text-yellow-600 mt-1"></i>
                            <span>Dusun panjunan, RT.018/RW.003, Susukan, Kec. Susukan, Cirebon, Jawa Barat</span>
                        </li>
                        <li class="flex items-center space-x-3">
                            <i class="fas fa-phone text-yellow-600"></i>
                            <span>+62 881-0223-62914</span>
                        </li>
                        <li class="flex items-center space-x-3">
                            <i class="fas fa-envelope text-yellow-600"></i>
                            <span>dalfarizzi93@gmail.com</span>
                        </li>
                    </ul>
                </div>
                <div>
                    <h4 class="text-sm font-bold uppercase tracking-[0.2em] mb-6">Newsletter</h4>
                    <p class="text-xs text-gray-500 mb-4">Dapatkan update koleksi terbaru dan promo eksklusif.</p>
                    <div class="flex border-b border-white/20 pb-2">
                        <input type="email" placeholder="Your email..." class="bg-transparent border-none outline-none w-full text-sm">
                        <button class="text-yellow-600"><i class="fas fa-paper-plane"></i></button>
                    </div>
                </div>
            </div>
            <div class="text-center text-gray-600 text-[10px] uppercase tracking-widest">
                &copy; 2026 DONIX PARFUME LUXURY. All Rights Reserved. Designed by Elite Dev Team.
            </div>
        </footer>
    </div>

    <!-- CART SLIDEOVER -->
    <div id="cart-drawer" class="fixed inset-0 z-[100] hidden">
        <div class="absolute inset-0 bg-black/80 backdrop-blur-sm" onclick="toggleCart()"></div>
        <div class="absolute top-0 right-0 h-full w-full max-w-md bg-zinc-950 border-l border-yellow-600 shadow-2xl p-8 flex flex-col">
            <div class="flex items-center justify-between mb-10">
                <h2 class="text-2xl font-luxury">Shopping Bag</h2>
                <button onclick="toggleCart()" class="text-2xl text-gray-400 hover:text-white"><i class="fas fa-times"></i></button>
            </div>
            <div id="cart-items" class="flex-grow overflow-y-auto space-y-6">
                <!-- Cart items here -->
                <p class="text-center text-gray-500 py-10">Keranjang Anda kosong.</p>
            </div>
            <div class="border-t border-white/10 pt-6 mt-6">
                <div class="flex justify-between text-xl mb-6">
                    <span class="font-light">Subtotal</span>
                    <span id="cart-total" class="font-bold gold-gradient">Rp 0</span>
                </div>
                <button onclick="openCheckout()" class="w-full bg-gold-metallic text-black py-4 rounded-full font-bold uppercase tracking-widest text-xs hover:scale-[1.02] transition">Process to Checkout</button>
            </div>
        </div>
    </div>

    <!-- CHECKOUT MODAL -->
    <div id="checkout-modal" class="fixed inset-0 z-[110] hidden flex items-center justify-center p-4">
        <div class="absolute inset-0 bg-black/90 backdrop-blur-md"></div>
        <div class="relative bg-zinc-900 border border-yellow-600/30 w-full max-w-2xl rounded-2xl overflow-hidden shadow-2xl">
            <div class="p-8">
                <div class="flex justify-between items-center mb-8">
                    <h2 class="text-3xl font-luxury">Complete Order</h2>
                    <button onclick="closeCheckout()" class="text-gray-400"><i class="fas fa-times"></i></button>
                </div>
                <form id="orderForm" onsubmit="handleOrderSubmit(event)" class="grid md:grid-cols-2 gap-6">
                    <div class="space-y-4">
                        <div>
                            <label class="text-[10px] uppercase tracking-widest text-gray-500 mb-1 block">Nama Lengkap</label>
                            <input type="text" required id="custName" class="w-full bg-black/50 border border-white/10 rounded-lg p-3 text-sm focus:border-yellow-600 outline-none">
                        </div>
                        <div>
                            <label class="text-[10px] uppercase tracking-widest text-gray-500 mb-1 block">WhatsApp</label>
                            <input type="tel" required id="custWa" class="w-full bg-black/50 border border-white/10 rounded-lg p-3 text-sm focus:border-yellow-600 outline-none">
                        </div>
                        <div>
                            <label class="text-[10px] uppercase tracking-widest text-gray-500 mb-1 block">Alamat Pengiriman</label>
                            <textarea id="custAddress" required rows="3" class="w-full bg-black/50 border border-white/10 rounded-lg p-3 text-sm focus:border-yellow-600 outline-none"></textarea>
                        </div>
                    </div>
                    <div class="space-y-4">
                        <div>
                            <label class="text-[10px] uppercase tracking-widest text-gray-500 mb-1 block">Metode Pembayaran</label>
                            <select id="payMethod" class="w-full bg-black/50 border border-white/10 rounded-lg p-3 text-sm focus:border-yellow-600 outline-none">
                                <option value="Transfer Bank">Transfer Bank (BCA/Mandiri)</option>
                                <option value="QRIS">QRIS / E-Wallet</option>
                                <option value="COD">Bayar di Tempat (COD)</option>
                            </select>
                        </div>
                        <div>
                            <label class="text-[10px] uppercase tracking-widest text-gray-500 mb-1 block">Kurir</label>
                            <select id="courier" class="w-full bg-black/50 border border-white/10 rounded-lg p-3 text-sm focus:border-yellow-600 outline-none">
                                <option value="J&T Express">J&T Express</option>
                                <option value="JNE YES">JNE YES</option>
                                <option value="Sicepat">Sicepat Best</option>
                                <option value="Grab/Gojek">Instan (Grab/Gojek)</option>
                            </select>
                        </div>
                        <div class="bg-black/80 p-4 rounded-xl border border-yellow-600/20 mt-4">
                            <p class="text-xs text-gray-500 mb-2">Ringkasan Pesanan:</p>
                            <div id="checkout-summary" class="max-h-24 overflow-y-auto text-xs space-y-1"></div>
                            <div class="mt-4 pt-2 border-t border-white/10 flex justify-between font-bold text-yellow-600">
                                <span>Total Tagihan:</span>
                                <span id="checkout-final-total"></span>
                            </div>
                        </div>
                    </div>
                    <button type="submit" class="col-span-full bg-gold-metallic text-black py-4 rounded-full font-bold uppercase tracking-widest mt-4">Pesan Sekarang (WhatsApp)</button>
                </form>
            </div>
        </div>
    </div>

    <!-- ADMIN LOGIN MODAL -->
    <div id="admin-login-modal" class="fixed inset-0 z-[120] hidden flex items-center justify-center p-4">
        <div class="absolute inset-0 bg-black/95 backdrop-blur-xl"></div>
        <div class="relative bg-zinc-900 border border-yellow-600 w-full max-w-sm rounded-2xl p-10 shadow-3xl">
            <h2 class="text-center font-luxury text-3xl mb-8 gold-gradient">SELLER PANEL</h2>
            <div class="space-y-6">
                <div>
                    <input type="text" id="adminUser" placeholder="Username" class="w-full bg-black border border-white/10 p-4 rounded-lg outline-none focus:border-yellow-600">
                </div>
                <div>
                    <input type="password" id="adminPass" placeholder="Password" class="w-full bg-black border border-white/10 p-4 rounded-lg outline-none focus:border-yellow-600">
                </div>
                <button onclick="loginAdmin()" class="w-full bg-gold-metallic text-black py-4 rounded-lg font-bold uppercase tracking-widest">Login Portal</button>
                <button onclick="toggleAdminPanel()" class="w-full text-gray-500 text-xs">Batal</button>
            </div>
        </div>
    </div>

    <!-- ADMIN DASHBOARD PANEL -->
    <div id="admin-panel" class="fixed inset-0 z-[150] bg-black hidden flex">
        <!-- Sidebar -->
        <aside class="w-64 bg-zinc-950 border-r border-white/10 flex flex-col">
            <div class="p-8 border-b border-white/10">
                <h3 class="font-luxury gold-gradient text-xl">DONIX ADMIN</h3>
            </div>
            <nav class="flex-grow p-4 space-y-2">
                <button onclick="showAdminSection('dashboard')" class="w-full text-left p-3 hover:bg-yellow-600/10 rounded flex items-center space-x-3 text-yellow-500"><i class="fas fa-chart-line"></i> <span>Dashboard</span></button>
                <button onclick="showAdminSection('products')" class="w-full text-left p-3 hover:bg-yellow-600/10 rounded flex items-center space-x-3 text-gray-400"><i class="fas fa-box"></i> <span>Produk</span></button>
                <button onclick="showAdminSection('orders')" class="w-full text-left p-3 hover:bg-yellow-600/10 rounded flex items-center space-x-3 text-gray-400"><i class="fas fa-shopping-cart"></i> <span>Pesanan</span></button>
                <button onclick="showAdminSection('stock')" class="w-full text-left p-3 hover:bg-yellow-600/10 rounded flex items-center space-x-3 text-gray-400"><i class="fas fa-warehouse"></i> <span>Stok</span></button>
                <button onclick="showAdminSection('finance')" class="w-full text-left p-3 hover:bg-yellow-600/10 rounded flex items-center space-x-3 text-gray-400"><i class="fas fa-wallet"></i> <span>Keuangan</span></button>
            </nav>
            <div class="p-4 border-t border-white/10">
                <button onclick="logoutAdmin()" class="w-full bg-red-900/20 text-red-500 p-3 rounded text-sm font-bold flex items-center justify-center space-x-2">
                    <i class="fas fa-sign-out-alt"></i> <span>Logout</span>
                </button>
            </div>
        </aside>

        <!-- Main Content -->
        <main class="flex-grow overflow-y-auto p-10">
            <!-- Section Dashboard -->
            <div id="section-dashboard" class="admin-section">
                <div class="flex justify-between items-center mb-10">
                    <h2 class="text-3xl font-luxury">Real-time Statistics</h2>
                    <div class="bg-zinc-900 px-4 py-2 rounded border border-white/10 text-xs">April 2026</div>
                </div>
                <div class="grid grid-cols-1 md:grid-cols-4 gap-6 mb-10">
                    <div class="bg-zinc-900 p-6 rounded-2xl border border-white/5">
                        <p class="text-gray-500 text-xs uppercase mb-2">Penjualan Hari Ini</p>
                        <h4 class="text-3xl font-bold">Rp 12,450k</h4>
                        <p class="text-green-500 text-[10px] mt-2">+15% dari kemarin</p>
                    </div>
                    <div class="bg-zinc-900 p-6 rounded-2xl border border-white/5">
                        <p class="text-gray-500 text-xs uppercase mb-2">Order Masuk</p>
                        <h4 class="text-3xl font-bold">24</h4>
                        <p class="text-yellow-500 text-[10px] mt-2">6 perlu dikirim</p>
                    </div>
                    <div class="bg-zinc-900 p-6 rounded-2xl border border-white/5">
                        <p class="text-gray-500 text-xs uppercase mb-2">Total Customer</p>
                        <h4 class="text-3xl font-bold">1,248</h4>
                        <p class="text-blue-500 text-[10px] mt-2">10 Member VIP baru</p>
                    </div>
                    <div class="bg-zinc-900 p-6 rounded-2xl border border-white/5">
                        <p class="text-gray-500 text-xs uppercase mb-2">Laba Bersih</p>
                        <h4 class="text-3xl font-bold text-yellow-500">Rp 84,2M</h4>
                        <p class="text-gray-500 text-[10px] mt-2">Target bulan ini 90%</p>
                    </div>
                </div>
                <div class="bg-zinc-900 p-8 rounded-2xl border border-white/5 mb-10">
                    <h4 class="text-lg font-bold mb-6">Sales Analytics (Trend 2026)</h4>
                    <canvas id="salesChart" height="100"></canvas>
                </div>
            </div>

            <!-- Section Products -->
            <div id="section-products" class="admin-section hidden">
                <div class="flex justify-between items-center mb-10">
                    <h2 class="text-3xl font-luxury">Product Catalog</h2>
                    <button onclick="openProductForm()" class="bg-yellow-600 text-black px-6 py-2 rounded font-bold text-xs uppercase">Tambah Produk Baru</button>
                </div>
                <div class="bg-zinc-900 rounded-2xl border border-white/5 overflow-hidden">
                    <table class="w-full text-left text-sm">
                        <thead class="bg-black/50 border-b border-white/10 uppercase text-[10px] tracking-widest text-gray-500">
                            <tr>
                                <th class="p-4">Produk</th>
                                <th class="p-4">Brand</th>
                                <th class="p-4">Harga</th>
                                <th class="p-4">Stok</th>
                                <th class="p-4">Status</th>
                                <th class="p-4 text-center">Aksi</th>
                            </tr>
                        </thead>
                        <tbody id="admin-product-table">
                            <!-- Injected by JS -->
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- Add Product Modal (Nested) -->
            <div id="product-form-modal" class="fixed inset-0 bg-black/80 hidden z-[200] flex items-center justify-center">
                <div class="bg-zinc-900 w-full max-w-2xl p-8 rounded-2xl border border-yellow-600">
                    <h3 class="text-2xl font-luxury mb-6">Master Produk Data</h3>
                    <div class="grid grid-cols-2 gap-6">
                        <input type="text" id="p_name" placeholder="Nama Parfum" class="bg-black border border-white/10 p-3 rounded">
                        <input type="text" id="p_brand" placeholder="Brand" class="bg-black border border-white/10 p-3 rounded">
                        <input type="number" id="p_price" placeholder="Harga Jual" class="bg-black border border-white/10 p-3 rounded">
                        <input type="number" id="p_stock" placeholder="Jumlah Stok" class="bg-black border border-white/10 p-3 rounded">
                        <select id="p_category" class="bg-black border border-white/10 p-3 rounded">
                            <option value="men">Men</option>
                            <option value="women">Women</option>
                            <option value="unisex">Unisex</option>
                        </select>
                        <input type="text" id="p_img" placeholder="URL Foto (Unsplash/Imgur)" class="bg-black border border-white/10 p-3 rounded">
                    </div>
                    <div class="flex space-x-4 mt-8">
                        <button onclick="saveProduct()" class="flex-grow bg-yellow-600 text-black py-3 rounded font-bold">Simpan ke Database</button>
                        <button onclick="closeProductForm()" class="px-8 bg-zinc-800 rounded">Batal</button>
                    </div>
                </div>
            </div>
        </main>
    </div>

    <!-- WHATSAPP FLOATING BUTTON -->
    <a href="https://wa.me/62881022362914" target="_blank" class="fixed bottom-6 right-6 z-[60] bg-green-600 w-16 h-16 rounded-full flex items-center justify-center text-3xl shadow-2xl hover:scale-110 transition cursor-pointer">
        <i class="fab fa-whatsapp"></i>
        <span class="absolute -top-1 -right-1 flex h-4 w-4">
            <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-green-400 opacity-75"></span>
            <span class="relative inline-flex rounded-full h-4 w-4 bg-green-500"></span>
        </span>
    </a>

    <script>
        // DATA MASTER
        let products = [
            { id: 1, name: "Bleu de Chanel", brand: "Chanel", price: 2450000, oldPrice: 2800000, cat: "men", img: "https://images.unsplash.com/photo-1592945403244-b3fbafd7f539?auto=format&fit=crop&q=80&w=400", stock: 15, tag: "Best Seller" },
            { id: 2, name: "Dior Sauvage Elixir", brand: "Dior", price: 3100000, oldPrice: 3500000, cat: "men", img: "https://images.unsplash.com/photo-1541643600914-78b084683601?auto=format&fit=crop&q=80&w=400", stock: 8, tag: "Hot" },
            { id: 3, name: "Baccarat Rouge 540", brand: "MFK", price: 5400000, oldPrice: 6200000, cat: "unisex", img: "https://images.unsplash.com/photo-1594035910387-fea47794261f?auto=format&fit=crop&q=80&w=400", stock: 5, tag: "Exclusive" },
            { id: 4, name: "Black Opium", brand: "YSL", price: 1850000, oldPrice: 2100000, cat: "women", img: "https://images.unsplash.com/photo-1523293182086-7651a899d37f?auto=format&fit=crop&q=80&w=400", stock: 20, tag: "Popular" },
            { id: 5, name: "Versace Eros", brand: "Versace", price: 1450000, oldPrice: 1600000, cat: "men", img: "https://images.unsplash.com/photo-1595428774223-ef52624120d2?auto=format&fit=crop&q=80&w=400", stock: 25, tag: "Sale" },
            { id: 6, name: "J'adore", brand: "Dior", price: 2200000, oldPrice: 2400000, cat: "women", img: "https://images.unsplash.com/photo-1590736704728-f4730bb30770?auto=format&fit=crop&q=80&w=400", stock: 12, tag: "Elegance" },
            { id: 7, name: "Acqua di Gio", brand: "Armani", price: 1650000, oldPrice: 1900000, cat: "men", img: "https://images.unsplash.com/photo-1557170334-a7c3c467b1f4?auto=format&fit=crop&q=80&w=400", stock: 30, tag: "New" },
            { id: 8, name: "Oud Wood", brand: "Tom Ford", price: 4200000, oldPrice: 4800000, cat: "unisex", img: "https://images.unsplash.com/photo-1563170339-2c97a17622dc?auto=format&fit=crop&q=80&w=400", stock: 4, tag: "Limited" },
        ];

        let cart = [];

        // UI INITIALIZATION
        window.onload = () => {
            setTimeout(() => {
                document.getElementById('loading-screen').style.opacity = '0';
                setTimeout(() => document.getElementById('loading-screen').classList.add('hidden'), 700);
            }, 1500);
            renderProducts(products);
            startCountdown();
            initChart();
        };

        // RENDER PRODUCTS
        function renderProducts(items) {
            const grid = document.getElementById('product-grid');
            grid.innerHTML = items.map(p => `
                <div class="product-card group relative animate-fade-in">
                    <div class="relative overflow-hidden rounded-2xl aspect-[4/5] bg-zinc-900 border border-white/5">
                        <img src="${p.img}" alt="${p.name}" class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110">
                        <div class="absolute top-4 left-4">
                            <span class="bg-gold-metallic text-black text-[10px] font-bold px-3 py-1 rounded-full uppercase tracking-tighter shadow-lg">${p.tag}</span>
                        </div>
                        <div class="product-action absolute bottom-6 left-0 right-0 flex justify-center space-x-3 opacity-0 translate-y-4 transition-all duration-300">
                            <button onclick="addToCart(${p.id})" class="bg-white text-black w-12 h-12 rounded-full flex items-center justify-center hover:bg-yellow-600 transition shadow-xl"><i class="fas fa-shopping-cart"></i></button>
                            <button class="bg-black/50 backdrop-blur text-white w-12 h-12 rounded-full flex items-center justify-center hover:bg-red-600 transition shadow-xl"><i class="fas fa-heart"></i></button>
                        </div>
                    </div>
                    <div class="mt-6">
                        <p class="text-[10px] text-gray-500 uppercase tracking-[0.2em] mb-1">${p.brand}</p>
                        <h3 class="text-lg font-luxury mb-2 tracking-tight group-hover:text-yellow-600 transition">${p.name}</h3>
                        <div class="flex items-center space-x-3">
                            <span class="text-yellow-600 font-bold">Rp ${(p.price/1000000).toFixed(1)}M</span>
                            <span class="text-gray-600 line-through text-xs">Rp ${(p.oldPrice/1000000).toFixed(1)}M</span>
                        </div>
                    </div>
                </div>
            `).join('');
        }

        // FILTER SYSTEM
        function filterProducts(cat) {
            if (cat === 'all') {
                renderProducts(products);
            } else {
                const filtered = products.filter(p => p.cat === cat);
                renderProducts(filtered);
            }
        }

        // SEARCH SYSTEM
        document.getElementById('searchInput').addEventListener('input', (e) => {
            const val = e.target.value.toLowerCase();
            const filtered = products.filter(p => p.name.toLowerCase().includes(val) || p.brand.toLowerCase().includes(val));
            renderProducts(filtered);
        });

        // CART LOGIC
        function toggleCart() {
            document.getElementById('cart-drawer').classList.toggle('hidden');
        }

        function addToCart(id) {
            const product = products.find(p => p.id === id);
            cart.push(product);
            updateCart();
            showToast(`"${product.name}" berhasil ditambahkan!`);
        }

        function updateCart() {
            const list = document.getElementById('cart-items');
            const count = document.getElementById('cart-count');
            const totalDisplay = document.getElementById('cart-total');

            count.innerText = cart.length;

            if (cart.length === 0) {
                list.innerHTML = `<p class="text-center text-gray-500 py-10">Keranjang Anda kosong.</p>`;
                totalDisplay.innerText = "Rp 0";
                return;
            }

            let total = 0;
            list.innerHTML = cart.map((item, index) => {
                total += item.price;
                return `
                    <div class="flex items-center space-x-4 border-b border-white/5 pb-4">
                        <img src="${item.img}" class="w-16 h-20 object-cover rounded">
                        <div class="flex-grow">
                            <h4 class="text-sm font-bold">${item.name}</h4>
                            <p class="text-xs text-yellow-600">Rp ${item.price.toLocaleString('id-ID')}</p>
                        </div>
                        <button onclick="removeFromCart(${index})" class="text-gray-500 hover:text-red-500"><i class="fas fa-trash"></i></button>
                    </div>
                `;
            }).join('');

            totalDisplay.innerText = "Rp " + total.toLocaleString('id-ID');
        }

        function removeFromCart(index) {
            cart.splice(index, 1);
            updateCart();
        }

        // CHECKOUT FLOW
        function openCheckout() {
            if (cart.length === 0) return showToast("Keranjang masih kosong!");
            toggleCart();
            document.getElementById('checkout-modal').classList.remove('hidden');
            
            let summaryHtml = "";
            let total = 0;
            cart.forEach(item => {
                summaryHtml += `<div class="flex justify-between"><span>${item.name}</span><span>Rp ${item.price.toLocaleString('id-ID')}</span></div>`;
                total += item.price;
            });
            document.getElementById('checkout-summary').innerHTML = summaryHtml;
            document.getElementById('checkout-final-total').innerText = "Rp " + total.toLocaleString('id-ID');
        }

        function closeCheckout() {
            document.getElementById('checkout-modal').classList.add('hidden');
        }

        function handleOrderSubmit(e) {
            e.preventDefault();
            const name = document.getElementById('custName').value;
            const wa = document.getElementById('custWa').value;
            const address = document.getElementById('custAddress').value;
            const pay = document.getElementById('payMethod').value;
            const courier = document.getElementById('courier').value;

            let total = 0;
            let productText = "";
            cart.forEach((item, i) => {
                total += item.price;
                productText += `${i+1}. ${item.name} (${item.brand}) - Rp ${item.price.toLocaleString('id-ID')}\n`;
            });

            const message = `*DONIX PARFUME - ORDER INVOICE*\n\n` +
                          `Halo Admin Donix, saya ingin memesan:\n\n` +
                          `${productText}\n` +
                          `*TOTAL TAGIHAN: Rp ${total.toLocaleString('id-ID')}*\n\n` +
                          `*DATA PENGIRIMAN:*\n` +
                          `- Nama: ${name}\n` +
                          `- No. WA: ${wa}\n` +
                          `- Alamat: ${address}\n` +
                          `- Kurir: ${courier}\n` +
                          `- Pembayaran: ${pay}\n\n` +
                          `Mohon diproses segera, terima kasih!`;

            const encodedMsg = encodeURIComponent(message);
            window.open(`https://wa.me/62881022362914?text=${encodedMsg}`, '_blank');
            
            // Success reset
            cart = [];
            updateCart();
            closeCheckout();
            showToast("Pesanan diteruskan ke WhatsApp!");
        }

        // UI HELPERS
        function showToast(msg) {
            const toast = document.getElementById('toast');
            document.getElementById('toast-msg').innerText = msg;
            toast.style.transform = "translateX(0)";
            setTimeout(() => { toast.style.transform = "translateX(150%)"; }, 3000);
        }

        function startCountdown() {
            let h = 2, m = 45, s = 12;
            setInterval(() => {
                s--;
                if(s < 0) { s = 59; m--; }
                if(m < 0) { m = 59; h--; }
                document.getElementById('timer-h').innerText = h.toString().padStart(2, '0');
                document.getElementById('timer-m').innerText = m.toString().padStart(2, '0');
                document.getElementById('timer-s').innerText = s.toString().padStart(2, '0');
            }, 1000);
        }

        window.addEventListener('scroll', () => {
            const nav = document.getElementById('navbar');
            if (window.scrollY > 50) {
                nav.classList.add('sticky-nav');
                nav.classList.remove('py-6');
                nav.classList.add('py-4');
            } else {
                nav.classList.remove('sticky-nav');
                nav.classList.remove('py-4');
                nav.classList.add('py-6');
            }
        });

        // ADMIN LOGIC
        function toggleAdminPanel() {
            document.getElementById('admin-login-modal').classList.toggle('hidden');
        }

        function loginAdmin() {
            const u = document.getElementById('adminUser').value;
            const p = document.getElementById('adminPass').value;
            if (u === "Donix" && p === "Doni0896") {
                document.getElementById('admin-login-modal').classList.add('hidden');
                document.getElementById('storefront').classList.add('hidden');
                document.getElementById('admin-panel').classList.remove('hidden');
                renderAdminProducts();
                showToast("Selamat Datang, Owner Donix!");
            } else {
                showToast("Login Gagal! Username/Password salah.");
            }
        }

        function logoutAdmin() {
            document.getElementById('admin-panel').classList.add('hidden');
            document.getElementById('storefront').classList.remove('hidden');
        }

        function showAdminSection(id) {
            document.querySelectorAll('.admin-section').forEach(s => s.classList.add('hidden'));
            document.getElementById('section-' + id).classList.remove('hidden');
            
            // Update sidebar UI
            document.querySelectorAll('aside nav button').forEach(btn => btn.classList.replace('text-yellow-500', 'text-gray-400'));
            event.currentTarget.classList.replace('text-gray-400', 'text-yellow-500');
        }

        function renderAdminProducts() {
            const tbody = document.getElementById('admin-product-table');
            tbody.innerHTML = products.map(p => `
                <tr class="border-b border-white/5 hover:bg-white/5">
                    <td class="p-4 flex items-center space-x-3">
                        <img src="${p.img}" class="w-10 h-10 object-cover rounded">
                        <span class="font-bold">${p.name}</span>
                    </td>
                    <td class="p-4">${p.brand}</td>
                    <td class="p-4">Rp ${p.price.toLocaleString('id-ID')}</td>
                    <td class="p-4">${p.stock}</td>
                    <td class="p-4"><span class="bg-green-900/30 text-green-500 px-2 py-1 rounded text-[10px]">Ready Stock</span></td>
                    <td class="p-4 text-center">
                        <button class="text-blue-500 mr-2"><i class="fas fa-edit"></i></button>
                        <button onclick="deleteProduct(${p.id})" class="text-red-500"><i class="fas fa-trash"></i></button>
                    </td>
                </tr>
            `).join('');
        }

        function openProductForm() {
            document.getElementById('product-form-modal').classList.remove('hidden');
        }

        function closeProductForm() {
            document.getElementById('product-form-modal').classList.add('hidden');
        }

        function saveProduct() {
            const newP = {
                id: products.length + 1,
                name: document.getElementById('p_name').value,
                brand: document.getElementById('p_brand').value,
                price: parseInt(document.getElementById('p_price').value),
                oldPrice: parseInt(document.getElementById('p_price').value) * 1.2,
                cat: document.getElementById('p_category').value,
                img: document.getElementById('p_img').value || "https://images.unsplash.com/photo-1594035910387-fea47794261f?auto=format&fit=crop&q=80&w=400",
                stock: parseInt(document.getElementById('p_stock').value),
                tag: "NEW"
            };
            products.unshift(newP);
            renderAdminProducts();
            renderProducts(products);
            closeProductForm();
            showToast("Produk Baru Berhasil Disimpan!");
        }

        function deleteProduct(id) {
            if(confirm('Hapus produk ini dari database?')) {
                products = products.filter(p => p.id !== id);
                renderAdminProducts();
                renderProducts(products);
                showToast("Produk Telah Dihapus.");
            }
        }

        function initChart() {
            const ctx = document.getElementById('salesChart').getContext('2d');
            new Chart(ctx, {
                type: 'line',
                data: {
                    labels: ['Jan', 'Feb', 'Mar', 'Apr', 'Mei', 'Jun'],
                    datasets: [{
                        label: 'Revenue (dalam Juta Rp)',
                        data: [650, 890, 720, 1200, 1100, 1600],
                        borderColor: '#BF953F',
                        backgroundColor: 'rgba(191, 149, 63, 0.1)',
                        fill: true,
                        tension: 0.4
                    }]
                },
                options: {
                    responsive: true,
                    plugins: { legend: { display: false } },
                    scales: {
                        y: { grid: { color: 'rgba(255,255,255,0.05)' }, ticks: { color: '#666' } },
                        x: { grid: { display: false }, ticks: { color: '#666' } }
                    }
                }
            });
        }
    </script>
</body>
</html>
