<!DOCTYPE html>
<html lang="id" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DONIX PARFUME | Luxury Fragrance Collection 2026</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/js/all.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@400;600;700&family=Montserrat:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --gold: #D4AF37;
            --dark: #0A0A0A;
            --luxury-white: #F9F9F9;
        }
        body {
            font-family: 'Montserrat', sans-serif;
            background-color: var(--dark);
            color: white;
            overflow-x: hidden;
        }
        h1, h2, h3, .serif {
            font-family: 'Cormorant Garamond', serif;
        }
        .gold-gradient {
            background: linear-gradient(135deg, #BF953F, #FCF6BA, #B38728, #FBF5B7, #AA771C);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .bg-gold-gradient {
            background: linear-gradient(135deg, #BF953F, #D4AF37, #B38728);
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
        .custom-scrollbar::-webkit-scrollbar {
            width: 5px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
            background: #1a1a1a;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: var(--gold);
            border-radius: 10px;
        }
        .loader-wrapper {
            position: fixed;
            inset: 0;
            z-index: 9999;
            background: var(--dark);
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .floating-wa {
            animation: bounce 2s infinite;
        }
        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }
        .nav-link::after {
            content: '';
            position: absolute;
            width: 0;
            height: 1px;
            bottom: -2px;
            left: 0;
            background-color: var(--gold);
            transition: width 0.3s ease;
        }
        .nav-link:hover::after {
            width: 100%;
        }
    </style>
</head>
<body class="custom-scrollbar" x-data="perfumeApp()">

    <!-- Loading Screen -->
    <div id="loader" class="loader-wrapper">
        <div class="text-center">
            <h1 class="text-4xl md:text-6xl font-bold gold-gradient mb-2 tracking-widest">DONIX PARFUME</h1>
            <div class="w-48 h-1 bg-gray-800 mx-auto rounded-full overflow-hidden">
                <div id="loader-progress" class="h-full bg-gold-gradient w-0"></div>
            </div>
            <p class="text-gray-400 mt-4 text-xs uppercase tracking-widest">Experience True Luxury</p>
        </div>
    </div>

    <!-- Notification Toast -->
    <div id="toast" class="fixed top-24 right-5 z-[100] transform translate-x-full transition-transform duration-300">
        <div class="glass border-l-4 border-yellow-500 p-4 rounded-r shadow-2xl flex items-center gap-3">
            <i class="fas fa-check-circle text-yellow-500"></i>
            <span id="toast-msg" class="text-sm font-medium">Produk ditambahkan ke keranjang!</span>
        </div>
    </div>

    <!-- HEADER / NAVBAR -->
    <nav id="navbar" class="fixed w-full top-0 z-50 transition-all duration-500 px-6 py-4">
        <div class="max-w-7xl mx-auto flex items-center justify-between">
            <!-- Logo -->
            <a href="#" class="text-2xl font-bold tracking-[0.2em] gold-gradient">DONIX PARFUME</a>

            <!-- Desktop Menu -->
            <div class="hidden lg:flex items-center gap-8 text-xs uppercase tracking-widest font-medium">
                <a href="#" class="nav-link relative">Home</a>
                <a href="#shop" class="nav-link relative">Shop</a>
                <a href="#" onclick="filterByGender('Men')" class="nav-link relative">Men</a>
                <a href="#" onclick="filterByGender('Women')" class="nav-link relative">Women</a>
                <a href="#" onclick="filterByGender('Unisex')" class="nav-link relative">Unisex</a>
                <a href="#flash-sale" class="nav-link relative text-yellow-500">Promo</a>
            </div>

            <!-- Icons -->
            <div class="flex items-center gap-5">
                <div class="hidden md:flex relative group">
                    <input type="text" id="searchInput" placeholder="Search Fragrance..." class="bg-transparent border-b border-gray-700 focus:border-yellow-500 outline-none text-xs py-1 w-32 focus:w-48 transition-all duration-300">
                    <i class="fas fa-search absolute right-0 top-1 text-gray-400"></i>
                </div>
                <button onclick="toggleModal('loginModal')" class="hover:text-yellow-500 transition-colors"><i class="far fa-user"></i></button>
                <button onclick="toggleModal('wishlistModal')" class="relative hover:text-yellow-500 transition-colors">
                    <i class="far fa-heart"></i>
                    <span id="wishlist-count" class="absolute -top-2 -right-2 bg-yellow-600 text-[10px] w-4 h-4 rounded-full flex items-center justify-center">0</span>
                </button>
                <button onclick="toggleCart()" class="relative hover:text-yellow-500 transition-colors">
                    <i class="fas fa-shopping-bag"></i>
                    <span id="cart-count" class="absolute -top-2 -right-2 bg-yellow-600 text-[10px] w-4 h-4 rounded-full flex items-center justify-center">0</span>
                </button>
                <button class="lg:hidden" onclick="toggleMobileMenu()"><i class="fas fa-bars"></i></button>
            </div>
        </div>
    </nav>

    <!-- Mobile Menu -->
    <div id="mobileMenu" class="fixed inset-0 bg-black z-[60] flex flex-col items-center justify-center gap-8 text-2xl font-light tracking-widest transform translate-x-full transition-transform duration-500">
        <button onclick="toggleMobileMenu()" class="absolute top-8 right-8"><i class="fas fa-times"></i></button>
        <a href="#" onclick="toggleMobileMenu()">HOME</a>
        <a href="#shop" onclick="toggleMobileMenu()">SHOP ALL</a>
        <a href="#" onclick="filterByGender('Men'); toggleMobileMenu()">MEN</a>
        <a href="#" onclick="filterByGender('Women'); toggleMobileMenu()">WOMEN</a>
        <a href="#admin" onclick="showAdmin(); toggleMobileMenu()" class="text-sm text-gray-500">ADMIN ACCESS</a>
    </div>

    <!-- HERO SECTION -->
    <section class="relative h-screen flex items-center overflow-hidden">
        <!-- Parallax Background -->
        <div class="absolute inset-0 z-0">
            <img src="https://images.unsplash.com/photo-1592945403244-b3fbafd7f539?auto=format&fit=crop&q=80&w=2000" class="w-full h-full object-cover brightness-50 scale-105" id="hero-img">
            <div class="absolute inset-0 bg-gradient-to-t from-black via-transparent to-black/50"></div>
        </div>
        
        <div class="relative z-10 max-w-7xl mx-auto px-6 w-full mt-20">
            <h4 class="text-yellow-500 uppercase tracking-[0.5em] text-sm mb-4 animate-pulse">Exclusive 2026 Collection</h4>
            <h1 class="text-6xl md:text-8xl font-bold mb-6 leading-tight serif">
                Luxury <br> <span class="gold-gradient italic">Fragrance</span>
            </h1>
            <p class="text-gray-300 max-w-md mb-10 text-lg font-light leading-relaxed">
                Temukan aroma terbaik yang mendefinisikan karakter dan prestise Anda. Koleksi parfum premium dunia kini dalam genggaman.
            </p>
            <div class="flex flex-wrap gap-4">
                <a href="#shop" class="bg-gold-gradient px-10 py-4 text-black font-bold uppercase tracking-widest text-xs hover:brightness-110 transition-all rounded-sm shadow-xl">Shop Now</a>
                <button onclick="startQuiz()" class="border border-white/30 hover:border-yellow-500 px-10 py-4 text-white font-bold uppercase tracking-widest text-xs transition-all backdrop-blur-sm rounded-sm">AI Fragrance Quiz</button>
            </div>
        </div>

        <div class="absolute bottom-10 left-1/2 -translate-x-1/2 text-center flex flex-col items-center gap-2">
            <span class="text-[10px] uppercase tracking-[0.3em] text-gray-500">Scroll Explore</span>
            <div class="w-px h-12 bg-gradient-to-b from-yellow-500 to-transparent"></div>
        </div>
    </section>

    <!-- CATEGORY SECTION -->
    <section class="py-24 px-6 bg-[#050505]">
        <div class="max-w-7xl mx-auto">
            <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-6 gap-4">
                <div onclick="filterByTag('Men')" class="group cursor-pointer overflow-hidden relative h-40 flex items-center justify-center border border-white/5 hover:border-yellow-500/50 transition-all">
                    <span class="z-10 uppercase tracking-widest text-xs font-bold group-hover:text-yellow-500 transition-colors">Men</span>
                    <div class="absolute inset-0 bg-white/5 group-hover:bg-white/10 transition-colors"></div>
                </div>
                <div onclick="filterByTag('Women')" class="group cursor-pointer overflow-hidden relative h-40 flex items-center justify-center border border-white/5 hover:border-yellow-500/50 transition-all">
                    <span class="z-10 uppercase tracking-widest text-xs font-bold group-hover:text-yellow-500 transition-colors">Women</span>
                    <div class="absolute inset-0 bg-white/5 group-hover:bg-white/10 transition-colors"></div>
                </div>
                <div onclick="filterByTag('Unisex')" class="group cursor-pointer overflow-hidden relative h-40 flex items-center justify-center border border-white/5 hover:border-yellow-500/50 transition-all">
                    <span class="z-10 uppercase tracking-widest text-xs font-bold group-hover:text-yellow-500 transition-colors">Unisex</span>
                    <div class="absolute inset-0 bg-white/5 group-hover:bg-white/10 transition-colors"></div>
                </div>
                <div onclick="filterByTag('New')" class="group cursor-pointer overflow-hidden relative h-40 flex items-center justify-center border border-white/5 hover:border-yellow-500/50 transition-all">
                    <span class="z-10 uppercase tracking-widest text-xs font-bold group-hover:text-yellow-500 transition-colors text-yellow-500">New Arrivals</span>
                    <div class="absolute inset-0 bg-white/5 group-hover:bg-white/10 transition-colors"></div>
                </div>
                <div onclick="filterByTag('Sale')" class="group cursor-pointer overflow-hidden relative h-40 flex items-center justify-center border border-white/5 hover:border-yellow-500/50 transition-all">
                    <span class="z-10 uppercase tracking-widest text-xs font-bold group-hover:text-yellow-500 transition-colors">Sale</span>
                    <div class="absolute inset-0 bg-white/5 group-hover:bg-white/10 transition-colors"></div>
                </div>
                <div onclick="filterByTag('Best')" class="group cursor-pointer overflow-hidden relative h-40 flex items-center justify-center border border-white/5 hover:border-yellow-500/50 transition-all">
                    <span class="z-10 uppercase tracking-widest text-xs font-bold group-hover:text-yellow-500 transition-colors">Best Sellers</span>
                    <div class="absolute inset-0 bg-white/5 group-hover:bg-white/10 transition-colors"></div>
                </div>
            </div>
        </div>
    </section>

    <!-- FLASH SALE SECTION -->
    <section id="flash-sale" class="py-20 px-6 bg-gold-gradient text-black">
        <div class="max-w-7xl mx-auto flex flex-col md:flex-row items-center justify-between gap-8">
            <div class="text-center md:text-left">
                <h2 class="text-4xl font-bold uppercase tracking-tighter serif">Exclusive Flash Sale</h2>
                <p class="font-medium opacity-80 uppercase tracking-widest text-sm">Diskon Hingga 50% - Terbatas!</p>
            </div>
            <div class="flex gap-4">
                <div class="bg-black text-white p-4 min-w-[80px] rounded text-center">
                    <span id="hours" class="text-2xl font-bold">02</span>
                    <p class="text-[10px] uppercase">Hours</p>
                </div>
                <div class="bg-black text-white p-4 min-w-[80px] rounded text-center">
                    <span id="minutes" class="text-2xl font-bold">45</span>
                    <p class="text-[10px] uppercase">Mins</p>
                </div>
                <div class="bg-black text-white p-4 min-w-[80px] rounded text-center">
                    <span id="seconds" class="text-2xl font-bold">12</span>
                    <p class="text-[10px] uppercase">Secs</p>
                </div>
            </div>
            <a href="#shop" class="bg-black text-white px-10 py-4 uppercase text-xs font-bold tracking-widest hover:scale-105 transition-transform">Explore Deals</a>
        </div>
    </section>

    <!-- PRODUCT SECTION -->
    <section id="shop" class="py-24 px-6">
        <div class="max-w-7xl mx-auto">
            <div class="flex flex-col md:flex-row md:items-end justify-between mb-12 gap-6">
                <div>
                    <h2 class="text-5xl font-bold serif mb-2">Signature <span class="gold-gradient italic">Collection</span></h2>
                    <p class="text-gray-400 uppercase tracking-widest text-xs">Pilih aroma yang mencerminkan jati diri Anda</p>
                </div>
                
                <!-- Filters -->
                <div class="flex flex-wrap gap-4">
                    <select onchange="handleSort(this.value)" class="bg-transparent border border-white/20 px-4 py-2 text-xs uppercase tracking-widest focus:border-yellow-500 outline-none cursor-pointer">
                        <option value="popularity" class="bg-black">Popularity</option>
                        <option value="low" class="bg-black">Price: Low to High</option>
                        <option value="high" class="bg-black">Price: High to Low</option>
                        <option value="newest" class="bg-black">Newest Arrivals</option>
                    </select>
                    <select onchange="handleBrandFilter(this.value)" class="bg-transparent border border-white/20 px-4 py-2 text-xs uppercase tracking-widest focus:border-yellow-500 outline-none cursor-pointer">
                        <option value="all" class="bg-black">All Brands</option>
                        <option value="Dior" class="bg-black">Dior</option>
                        <option value="Chanel" class="bg-black">Chanel</option>
                        <option value="Versace" class="bg-black">Versace</option>
                        <option value="Tom Ford" class="bg-black">Tom Ford</option>
                    </select>
                </div>
            </div>

            <!-- Product Grid -->
            <div id="product-container" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8">
                <!-- Products dynamically generated by JS -->
            </div>

            <div class="mt-20 text-center">
                <button class="border border-yellow-500/50 text-yellow-500 px-12 py-4 uppercase text-xs font-bold tracking-[0.3em] hover:bg-yellow-500 hover:text-black transition-all">Load More Products</button>
            </div>
        </div>
    </section>

    <!-- ABOUT SECTION -->
    <section class="py-24 px-6 glass">
        <div class="max-w-7xl mx-auto flex flex-col lg:flex-row items-center gap-16">
            <div class="lg:w-1/2 relative">
                <div class="absolute -top-10 -left-10 w-40 h-40 border-t border-l border-yellow-500/30"></div>
                <img src="https://images.unsplash.com/photo-1541643600914-78b084683601?auto=format&fit=crop&q=80&w=1000" class="relative z-10 w-full rounded shadow-2xl grayscale hover:grayscale-0 transition-all duration-700">
                <div class="absolute -bottom-10 -right-10 w-40 h-40 border-b border-r border-yellow-500/30"></div>
            </div>
            <div class="lg:w-1/2">
                <h4 class="text-yellow-500 uppercase tracking-widest text-sm mb-4">Our Heritage</h4>
                <h2 class="text-5xl font-bold serif mb-6 leading-tight">Mendefinisikan <br> <span class="gold-gradient italic">Elegansi Modern</span> Sejak 2020</h2>
                <p class="text-gray-400 mb-8 leading-relaxed font-light">
                    DONIX PARFUME adalah destinasi utama bagi para penikmat wewangian mewah. Kami berkomitmen menyajikan koleksi parfum original dengan kurasi terbaik dari seluruh dunia. Di tahun 2026, kami mengintegrasikan teknologi AI untuk membantu Anda menemukan aroma yang benar-benar pas dengan DNA karakter Anda.
                </p>
                <div class="grid grid-cols-2 gap-8 mb-10">
                    <div>
                        <h5 class="text-3xl font-bold gold-gradient serif">100%</h5>
                        <p class="text-xs uppercase tracking-widest text-gray-500">Original Guarantee</p>
                    </div>
                    <div>
                        <h5 class="text-3xl font-bold gold-gradient serif">500+</h5>
                        <p class="text-xs uppercase tracking-widest text-gray-500">Luxury Collections</p>
                    </div>
                </div>
                <button class="bg-white text-black px-10 py-4 uppercase text-xs font-bold tracking-widest hover:bg-yellow-500 transition-colors">Learn More About Us</button>
            </div>
        </div>
    </section>

    <!-- TESTIMONIALS -->
    <section class="py-24 px-6 overflow-hidden">
        <div class="max-w-7xl mx-auto text-center mb-16">
            <h2 class="text-4xl font-bold serif gold-gradient">What Our VIP Say</h2>
        </div>
        <div class="flex gap-8 animate-scroll whitespace-nowrap">
            <!-- Testimonial Cards (Simulated loop) -->
            <div class="glass p-8 min-w-[350px] rounded-lg">
                <div class="flex text-yellow-500 mb-4 gap-1">
                    <i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i>
                </div>
                <p class="text-gray-300 italic mb-6 whitespace-normal">"Pelayanan luar biasa, parfum sampai dengan aman dan kualitas botolnya sangat premium. Benar-benar original!"</p>
                <div class="flex items-center gap-4">
                    <div class="w-10 h-10 bg-gray-700 rounded-full"></div>
                    <div class="text-left">
                        <h6 class="text-sm font-bold">Amanda Clarissa</h6>
                        <p class="text-[10px] text-gray-500 uppercase">Entrepreneur</p>
                    </div>
                </div>
            </div>
            <!-- More cards -->
            <div class="glass p-8 min-w-[350px] rounded-lg">
                <div class="flex text-yellow-500 mb-4 gap-1">
                    <i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i>
                </div>
                <p class="text-gray-300 italic mb-6 whitespace-normal">"Fitur AI Quiz-nya sangat akurat. Saya mendapatkan rekomendasi Dior Sauvage dan ternyata saya sangat menyukainya."</p>
                <div class="flex items-center gap-4">
                    <div class="w-10 h-10 bg-gray-700 rounded-full"></div>
                    <div class="text-left">
                        <h6 class="text-sm font-bold">Rendy Pratama</h6>
                        <p class="text-[10px] text-gray-500 uppercase">Creative Director</p>
                    </div>
                </div>
            </div>
            <div class="glass p-8 min-w-[350px] rounded-lg">
                <div class="flex text-yellow-500 mb-4 gap-1">
                    <i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i>
                </div>
                <p class="text-gray-300 italic mb-6 whitespace-normal">"Donix Parfume adalah toko parfum terpercaya saya. Pengiriman cepat dan packing sangat eksklusif."</p>
                <div class="flex items-center gap-4">
                    <div class="w-10 h-10 bg-gray-700 rounded-full"></div>
                    <div class="text-left">
                        <h6 class="text-sm font-bold">Sisca Kohl</h6>
                        <p class="text-[10px] text-gray-500 uppercase">Influencer</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- FOOTER -->
    <footer class="bg-black pt-24 pb-12 px-6 border-t border-white/5">
        <div class="max-w-7xl mx-auto">
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-12 mb-20">
                <div>
                    <h2 class="text-2xl font-bold gold-gradient mb-6 tracking-widest">DONIX PARFUME</h2>
                    <p class="text-gray-500 text-sm leading-relaxed mb-6">Mewujudkan kepercayaan diri melalui aroma yang prestisius. Kami hanya menyediakan yang terbaik untuk Anda.</p>
                    <div class="flex gap-4">
                        <a href="#" class="w-10 h-10 glass flex items-center justify-center rounded-full hover:bg-yellow-500 hover:text-black transition-all"><i class="fab fa-instagram"></i></a>
                        <a href="#" class="w-10 h-10 glass flex items-center justify-center rounded-full hover:bg-yellow-500 hover:text-black transition-all"><i class="fab fa-tiktok"></i></a>
                        <a href="#" class="w-10 h-10 glass flex items-center justify-center rounded-full hover:bg-yellow-500 hover:text-black transition-all"><i class="fab fa-facebook-f"></i></a>
                    </div>
                </div>
                <div>
                    <h4 class="text-sm font-bold uppercase tracking-widest mb-6 underline underline-offset-8 decoration-yellow-500/50">Collections</h4>
                    <ul class="text-gray-500 text-sm flex flex-col gap-4">
                        <li><a href="#" class="hover:text-yellow-500 transition-colors">Men Fragrance</a></li>
                        <li><a href="#" class="hover:text-yellow-500 transition-colors">Women Fragrance</a></li>
                        <li><a href="#" class="hover:text-yellow-500 transition-colors">Unisex Collection</a></li>
                        <li><a href="#" class="hover:text-yellow-500 transition-colors">Limited Edition</a></li>
                        <li><a href="#" class="hover:text-yellow-500 transition-colors">Best Seller</a></li>
                    </ul>
                </div>
                <div>
                    <h4 class="text-sm font-bold uppercase tracking-widest mb-6 underline underline-offset-8 decoration-yellow-500/50">Company</h4>
                    <ul class="text-gray-500 text-sm flex flex-col gap-4">
                        <li><a href="#" class="hover:text-yellow-500 transition-colors">About Us</a></li>
                        <li><a href="#" class="hover:text-yellow-500 transition-colors">Store Locator</a></li>
                        <li><a href="#" class="hover:text-yellow-500 transition-colors">Terms of Service</a></li>
                        <li><a href="#" class="hover:text-yellow-500 transition-colors">Privacy Policy</a></li>
                        <li><a href="#" class="hover:text-yellow-500 transition-colors">Membership VIP</a></li>
                    </ul>
                </div>
                <div>
                    <h4 class="text-sm font-bold uppercase tracking-widest mb-6 underline underline-offset-8 decoration-yellow-500/50">Newsletter</h4>
                    <p class="text-gray-500 text-sm mb-4">Dapatkan update koleksi terbaru dan promo eksklusif.</p>
                    <div class="flex">
                        <input type="email" placeholder="Email Address" class="bg-white/5 border border-white/10 px-4 py-3 text-xs w-full focus:outline-none focus:border-yellow-500">
                        <button class="bg-gold-gradient text-black px-6 font-bold uppercase text-[10px]">Join</button>
                    </div>
                </div>
            </div>
            <div class="border-t border-white/5 pt-8 flex flex-col md:flex-row justify-between items-center gap-4 text-xs text-gray-600 uppercase tracking-widest">
                <p>&copy; 2026 DONIX PARFUME. All Rights Reserved.</p>
                <div class="flex gap-6">
                    <span>Payment Methods:</span>
                    <i class="fab fa-cc-visa text-lg"></i>
                    <i class="fab fa-cc-mastercard text-lg"></i>
                    <i class="fas fa-qrcode text-lg"></i>
                    <i class="fas fa-wallet text-lg"></i>
                </div>
            </div>
        </div>
    </footer>

    <!-- CART SIDEBAR -->
    <div id="cartSidebar" class="fixed top-0 right-0 h-full w-full md:w-[450px] bg-black z-[100] transform translate-x-full transition-transform duration-500 shadow-2xl flex flex-col">
        <div class="p-8 border-b border-white/10 flex justify-between items-center">
            <h2 class="text-2xl font-bold serif gold-gradient">Your Bag</h2>
            <button onclick="toggleCart()" class="text-xl hover:text-yellow-500 transition-colors"><i class="fas fa-times"></i></button>
        </div>
        <div id="cart-items" class="flex-grow overflow-y-auto p-8 custom-scrollbar">
            <!-- Cart items here -->
        </div>
        <div class="p-8 border-t border-white/10 glass">
            <div class="flex justify-between items-center mb-6">
                <span class="text-gray-400 uppercase tracking-widest text-xs">Subtotal</span>
                <span id="cart-total" class="text-xl font-bold gold-gradient">Rp 0</span>
            </div>
            <button onclick="showCheckout()" class="w-full bg-gold-gradient text-black font-bold py-4 uppercase tracking-widest text-xs hover:brightness-110 transition-all rounded-sm">Checkout Now</button>
        </div>
    </div>

    <!-- MODAL: LOGIN/REGISTER -->
    <div id="loginModal" class="fixed inset-0 z-[110] bg-black/90 flex items-center justify-center p-6 hidden">
        <div class="glass w-full max-w-md p-10 rounded-lg relative">
            <button onclick="toggleModal('loginModal')" class="absolute top-6 right-6"><i class="fas fa-times"></i></button>
            <h2 class="text-3xl font-bold serif gold-gradient mb-8 text-center uppercase tracking-widest">Member Sign In</h2>
            <form class="space-y-6">
                <div>
                    <label class="block text-[10px] uppercase tracking-widest text-gray-500 mb-2">Email Address</label>
                    <input type="email" class="w-full bg-white/5 border border-white/10 px-4 py-3 focus:outline-none focus:border-yellow-500 transition-all rounded-sm text-sm">
                </div>
                <div>
                    <label class="block text-[10px] uppercase tracking-widest text-gray-500 mb-2">Password</label>
                    <input type="password" class="w-full bg-white/5 border border-white/10 px-4 py-3 focus:outline-none focus:border-yellow-500 transition-all rounded-sm text-sm">
                </div>
                <button type="button" class="w-full bg-gold-gradient text-black font-bold py-4 uppercase tracking-widest text-xs rounded-sm">Sign In</button>
                <p class="text-center text-xs text-gray-500">Don't have an account? <a href="#" class="text-yellow-500 hover:underline">Register</a></p>
            </form>
        </div>
    </div>

    <!-- MODAL: CHECKOUT -->
    <div id="checkoutModal" class="fixed inset-0 z-[120] bg-black flex items-center justify-center p-6 hidden">
        <div class="max-w-4xl w-full bg-[#0a0a0a] border border-white/10 p-8 md:p-12 overflow-y-auto max-h-[90vh] custom-scrollbar rounded-lg shadow-2xl">
            <div class="flex justify-between items-center mb-10">
                <h2 class="text-3xl font-bold serif gold-gradient uppercase tracking-widest">Secure Checkout</h2>
                <button onclick="toggleModal('checkoutModal')" class="text-xl"><i class="fas fa-times"></i></button>
            </div>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-12">
                <div class="space-y-6">
                    <h3 class="text-sm font-bold uppercase tracking-widest border-b border-yellow-500/30 pb-2">Shipping Information</h3>
                    <input type="text" placeholder="Full Name" class="w-full bg-white/5 border border-white/10 p-3 text-sm focus:outline-none focus:border-yellow-500">
                    <input type="text" placeholder="Phone Number (WhatsApp)" class="w-full bg-white/5 border border-white/10 p-3 text-sm focus:outline-none focus:border-yellow-500">
                    <textarea placeholder="Full Address" class="w-full bg-white/5 border border-white/10 p-3 text-sm h-32 focus:outline-none focus:border-yellow-500"></textarea>
                    
                    <h3 class="text-sm font-bold uppercase tracking-widest border-b border-yellow-500/30 pb-2">Payment Method</h3>
                    <div class="grid grid-cols-2 gap-4">
                        <label class="border border-white/10 p-4 rounded cursor-pointer hover:border-yellow-500 flex items-center gap-3">
                            <input type="radio" name="payment" class="accent-yellow-500">
                            <span class="text-xs uppercase">Bank Transfer</span>
                        </label>
                        <label class="border border-white/10 p-4 rounded cursor-pointer hover:border-yellow-500 flex items-center gap-3">
                            <input type="radio" name="payment" class="accent-yellow-500">
                            <span class="text-xs uppercase">QRIS / E-Wallet</span>
                        </label>
                        <label class="border border-white/10 p-4 rounded cursor-pointer hover:border-yellow-500 flex items-center gap-3">
                            <input type="radio" name="payment" class="accent-yellow-500">
                            <span class="text-xs uppercase">COD</span>
                        </label>
                        <label class="border border-white/10 p-4 rounded cursor-pointer hover:border-yellow-500 flex items-center gap-3">
                            <input type="radio" name="payment" class="accent-yellow-500">
                            <span class="text-xs uppercase">VIP Points</span>
                        </label>
                    </div>
                </div>
                <div class="space-y-6">
                    <div class="glass p-6 rounded-sm">
                        <h3 class="text-sm font-bold uppercase tracking-widest mb-6">Order Summary</h3>
                        <div id="checkout-summary" class="space-y-4 mb-6">
                            <!-- Items list -->
                        </div>
                        <div class="border-t border-white/10 pt-4 space-y-2">
                            <div class="flex justify-between text-xs text-gray-500 uppercase">
                                <span>Shipping Fee</span>
                                <span>Free</span>
                            </div>
                            <div class="flex justify-between text-xl font-bold gold-gradient pt-4">
                                <span>Total</span>
                                <span id="checkout-total">Rp 0</span>
                            </div>
                        </div>
                    </div>
                    <button onclick="processOrder()" class="w-full bg-gold-gradient text-black font-bold py-5 uppercase tracking-widest text-xs hover:scale-105 transition-all shadow-xl">Complete Purchase</button>
                    <p class="text-[10px] text-gray-500 text-center uppercase tracking-tighter">By clicking complete, you agree to our terms of premium service.</p>
                </div>
            </div>
        </div>
    </div>

    <!-- ADMIN PANEL (MODAL/SECTION) -->
    <div id="adminPanel" class="fixed inset-0 z-[150] bg-black hidden flex-col">
        <div class="bg-[#111] border-b border-white/10 p-6 flex justify-between items-center">
            <h2 class="text-xl font-bold gold-gradient">DONIX ADMIN DASHBOARD 2026</h2>
            <div class="flex items-center gap-6">
                <span class="text-xs text-gray-400">Welcome, Admin Elite</span>
                <button onclick="hideAdmin()" class="bg-red-500/20 text-red-500 px-4 py-2 text-xs uppercase font-bold tracking-widest hover:bg-red-500 hover:text-white transition-all">Logout</button>
            </div>
        </div>
        <div class="flex flex-1 overflow-hidden">
            <!-- Sidebar Admin -->
            <div class="w-64 bg-[#0a0a0a] border-r border-white/10 p-6 flex flex-col gap-4">
                <button class="w-full text-left p-3 text-xs uppercase tracking-widest bg-yellow-500 text-black font-bold">Statistics</button>
                <button class="w-full text-left p-3 text-xs uppercase tracking-widest hover:bg-white/5">Manage Products</button>
                <button class="w-full text-left p-3 text-xs uppercase tracking-widest hover:bg-white/5">Orders Management</button>
                <button class="w-full text-left p-3 text-xs uppercase tracking-widest hover:bg-white/5">Customers</button>
                <button class="w-full text-left p-3 text-xs uppercase tracking-widest hover:bg-white/5">Reports</button>
            </div>
            <!-- Main Admin Content -->
            <div class="flex-1 overflow-y-auto p-10 custom-scrollbar">
                <div class="grid grid-cols-1 md:grid-cols-4 gap-6 mb-10">
                    <div class="glass p-6 rounded border-b-2 border-yellow-500">
                        <p class="text-[10px] text-gray-500 uppercase tracking-widest mb-1">Total Sales</p>
                        <h3 class="text-2xl font-bold gold-gradient">Rp 1.450.000.000</h3>
                    </div>
                    <div class="glass p-6 rounded border-b-2 border-blue-500">
                        <p class="text-[10px] text-gray-500 uppercase tracking-widest mb-1">Active Orders</p>
                        <h3 class="text-2xl font-bold">142 Items</h3>
                    </div>
                    <div class="glass p-6 rounded border-b-2 border-green-500">
                        <p class="text-[10px] text-gray-500 uppercase tracking-widest mb-1">New Customers</p>
                        <h3 class="text-2xl font-bold">1,204 Users</h3>
                    </div>
                    <div class="glass p-6 rounded border-b-2 border-purple-500">
                        <p class="text-[10px] text-gray-500 uppercase tracking-widest mb-1">Top Brand</p>
                        <h3 class="text-2xl font-bold">Dior Fragrance</h3>
                    </div>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-2 gap-10 mb-10">
                    <div class="glass p-8 rounded">
                        <h4 class="text-sm font-bold uppercase tracking-widest mb-6">Sales Performance (Monthly)</h4>
                        <canvas id="salesChart"></canvas>
                    </div>
                    <div class="glass p-8 rounded">
                        <h4 class="text-sm font-bold uppercase tracking-widest mb-6">Add New Product</h4>
                        <form class="space-y-4">
                            <input type="text" placeholder="Product Name" class="w-full bg-white/5 border border-white/10 p-3 text-xs focus:border-yellow-500 outline-none">
                            <div class="grid grid-cols-2 gap-4">
                                <input type="text" placeholder="Brand" class="w-full bg-white/5 border border-white/10 p-3 text-xs focus:border-yellow-500 outline-none">
                                <input type="number" placeholder="Price (Rp)" class="w-full bg-white/5 border border-white/10 p-3 text-xs focus:border-yellow-500 outline-none">
                            </div>
                            <select class="w-full bg-[#0a0a0a] border border-white/10 p-3 text-xs focus:border-yellow-500 outline-none">
                                <option>Category: Men</option>
                                <option>Category: Women</option>
                                <option>Category: Unisex</option>
                            </select>
                            <button class="w-full bg-blue-600 text-white font-bold py-3 uppercase tracking-widest text-[10px] hover:bg-blue-700">Push to Catalog</button>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Floating UI -->
    <a href="https://wa.me/628123456789" target="_blank" class="fixed bottom-6 right-6 z-40 bg-green-500 text-white w-14 h-14 rounded-full flex items-center justify-center text-2xl shadow-2xl floating-wa hover:scale-110 transition-transform">
        <i class="fab fa-whatsapp"></i>
    </a>

    <!-- SCRIPTS -->
    <script>
        // State Management
        let cart = [];
        let wishlist = [];
        let products = [
            { id: 1, name: "Bleu de Chanel", brand: "Chanel", price: 2150000, oldPrice: 2450000, rating: 5, tag: "Best", gender: "Men", img: "https://images.unsplash.com/photo-1541643600914-78b084683601?auto=format&fit=crop&q=80&w=400" },
            { id: 2, name: "Dior Sauvage Elixir", brand: "Dior", price: 3450000, oldPrice: 3800000, rating: 5, tag: "Best", gender: "Men", img: "https://images.unsplash.com/photo-1594035910387-fea47794261f?auto=format&fit=crop&q=80&w=400" },
            { id: 3, name: "Versace Eros", brand: "Versace", price: 1650000, oldPrice: 1950000, rating: 4, tag: "Sale", gender: "Men", img: "https://images.unsplash.com/photo-1592945403244-b3fbafd7f539?auto=format&fit=crop&q=80&w=400" },
            { id: 4, name: "Baccarat Rouge 540", brand: "MFK", price: 5600000, oldPrice: 6200000, rating: 5, tag: "Premium", gender: "Unisex", img: "https://images.unsplash.com/photo-1590736704728-f4730bb30770?auto=format&fit=crop&q=80&w=400" },
            { id: 5, name: "YSL Libre Intense", brand: "YSL", price: 2450000, oldPrice: 2800000, rating: 5, tag: "New", gender: "Women", img: "https://images.unsplash.com/photo-1588405864443-305d92e6206c?auto=format&fit=crop&q=80&w=400" },
            { id: 6, name: "Black Opium", brand: "YSL", price: 2100000, oldPrice: 2400000, rating: 4, tag: "Best", gender: "Women", img: "https://images.unsplash.com/photo-1557170334-a9632e77c6e4?auto=format&fit=crop&q=80&w=400" },
            { id: 7, name: "Acqua di Gio", brand: "Armani", price: 1850000, oldPrice: 2100000, rating: 4, tag: "Best", gender: "Men", img: "https://images.unsplash.com/photo-1595425970377-c9703cf48b6d?auto=format&fit=crop&q=80&w=400" },
            { id: 8, name: "Tom Ford Oud Wood", brand: "Tom Ford", price: 4800000, oldPrice: 5500000, rating: 5, tag: "Premium", gender: "Unisex", img: "https://images.unsplash.com/photo-1563170351-be82bc888bb4?auto=format&fit=crop&q=80&w=400" },
            { id: 9, name: "Jo Malone English Pear", brand: "Jo Malone", price: 2200000, oldPrice: 2500000, rating: 5, tag: "Best", gender: "Women", img: "https://images.unsplash.com/photo-1615395884261-d8594fbc6872?auto=format&fit=crop&q=80&w=400" },
            { id: 10, name: "Jean Paul Gaultier Le Male", brand: "JPG", price: 1750000, oldPrice: 2000000, rating: 4, tag: "Sale", gender: "Men", img: "https://images.unsplash.com/photo-1512563514751-31ffa0cb217d?auto=format&fit=crop&q=80&w=400" },
            { id: 11, name: "Gucci Bloom", brand: "Gucci", price: 2300000, oldPrice: 2600000, rating: 5, tag: "Women", gender: "Women", img: "https://images.unsplash.com/photo-1616984748474-202021241511?auto=format&fit=crop&q=80&w=400" },
            { id: 12, name: "Creed Aventus", brand: "Creed", price: 5900000, oldPrice: 6500000, rating: 5, tag: "Premium", gender: "Men", img: "https://images.unsplash.com/photo-1523293182086-7651a899d37f?auto=format&fit=crop&q=80&w=400" },
        ];

        let filteredProducts = [...products];

        // Loader
        window.addEventListener('load', () => {
            const progress = document.getElementById('loader-progress');
            let width = 0;
            const interval = setInterval(() => {
                if (width >= 100) {
                    clearInterval(interval);
                    gsap.to('#loader', { opacity: 0, duration: 1, onComplete: () => {
                        document.getElementById('loader').style.display = 'none';
                    }});
                } else {
                    width += 5;
                    progress.style.width = width + '%';
                }
            }, 50);
            renderProducts();
        });

        // Navbar Scroll Effect
        window.addEventListener('scroll', () => {
            const nav = document.getElementById('navbar');
            if (window.scrollY > 50) {
                nav.classList.add('glass', 'py-3');
                nav.classList.remove('py-4');
            } else {
                nav.classList.remove('glass', 'py-3');
                nav.classList.add('py-4');
            }
        });

        // Search Realtime
        document.getElementById('searchInput').addEventListener('input', (e) => {
            const val = e.target.value.toLowerCase();
            filteredProducts = products.filter(p => p.name.toLowerCase().includes(val) || p.brand.toLowerCase().includes(val));
            renderProducts();
        });

        // Render Products
        function renderProducts() {
            const container = document.getElementById('product-container');
            container.innerHTML = filteredProducts.map(p => `
                <div class="product-card group relative overflow-hidden glass rounded p-4 hover:border-yellow-500/50 transition-all duration-500">
                    <div class="absolute top-4 left-4 z-10 flex flex-col gap-2">
                        ${p.tag ? `<span class="bg-yellow-500 text-black text-[9px] font-bold px-2 py-1 uppercase tracking-tighter rounded-sm">${p.tag}</span>` : ''}
                        <span class="bg-white/10 backdrop-blur-md text-white text-[9px] font-bold px-2 py-1 uppercase tracking-tighter rounded-sm">${p.gender}</span>
                    </div>
                    <div class="relative overflow-hidden h-64 mb-6 rounded">
                        <img src="${p.img}" class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110">
                        <div class="product-action absolute bottom-4 left-0 right-0 px-4 opacity-0 translate-y-4 transition-all duration-300">
                            <button onclick="addToCart(${p.id})" class="w-full bg-white text-black text-[10px] font-bold py-3 uppercase tracking-widest hover:bg-yellow-500 transition-colors">Add to Bag</button>
                        </div>
                    </div>
                    <div class="text-center">
                        <p class="text-gray-500 text-[10px] uppercase tracking-widest mb-1">${p.brand}</p>
                        <h3 class="text-sm font-bold tracking-wide mb-2 truncate">${p.name}</h3>
                        <div class="flex items-center justify-center gap-1 text-[10px] text-yellow-500 mb-3">
                            ${'<i class="fas fa-star"></i>'.repeat(p.rating)}${'<i class="far fa-star"></i>'.repeat(5 - p.rating)}
                        </div>
                        <div class="flex items-center justify-center gap-3">
                            <span class="text-gray-600 line-through text-xs italic">Rp ${p.oldPrice.toLocaleString()}</span>
                            <span class="text-yellow-500 font-bold text-sm">Rp ${p.price.toLocaleString()}</span>
                        </div>
                    </div>
                    <button onclick="toggleWishlist(${p.id})" class="absolute top-4 right-4 text-gray-500 hover:text-red-500 transition-colors">
                        <i class="${wishlist.includes(p.id) ? 'fas fa-heart text-red-500' : 'far fa-heart'}"></i>
                    </button>
                </div>
            `).join('');
        }

        // Cart Logic
        function toggleCart() {
            const sidebar = document.getElementById('cartSidebar');
            sidebar.classList.toggle('translate-x-full');
        }

        function addToCart(id) {
            const prod = products.find(p => p.id === id);
            const exists = cart.find(item => item.id === id);
            if (exists) {
                exists.qty++;
            } else {
                cart.push({ ...prod, qty: 1 });
            }
            updateUI();
            showToast(`${prod.name} added to bag.`);
        }

        function removeFromCart(id) {
            cart = cart.filter(item => item.id !== id);
            updateUI();
        }

        function updateUI() {
            // Update Cart
            const cartItems = document.getElementById('cart-items');
            cartItems.innerHTML = cart.length === 0 ? '<p class="text-center text-gray-500 uppercase text-xs mt-10 tracking-[0.3em]">Bag is empty</p>' : cart.map(item => `
                <div class="flex gap-4 mb-6 group">
                    <div class="w-20 h-24 overflow-hidden rounded">
                        <img src="${item.img}" class="w-full h-full object-cover">
                    </div>
                    <div class="flex-grow">
                        <h4 class="text-xs font-bold uppercase tracking-wider mb-1">${item.name}</h4>
                        <p class="text-[10px] text-gray-500 mb-2">${item.brand} | ${item.qty} pcs</p>
                        <p class="text-sm font-bold gold-gradient">Rp ${(item.price * item.qty).toLocaleString()}</p>
                    </div>
                    <button onclick="removeFromCart(${item.id})" class="text-gray-600 hover:text-white transition-colors"><i class="fas fa-trash-alt"></i></button>
                </div>
            `).join('');

            const total = cart.reduce((sum, item) => sum + (item.price * item.qty), 0);
            document.getElementById('cart-total').innerText = `Rp ${total.toLocaleString()}`;
            document.getElementById('cart-count').innerText = cart.reduce((sum, item) => sum + item.qty, 0);
            document.getElementById('wishlist-count').innerText = wishlist.length;
        }

        // Wishlist
        function toggleWishlist(id) {
            if (wishlist.includes(id)) {
                wishlist = wishlist.filter(x => x !== id);
                showToast("Dihapus dari wishlist");
            } else {
                wishlist.push(id);
                showToast("Ditambahkan ke wishlist");
            }
            renderProducts();
            updateUI();
        }

        // Toast
        function showToast(msg) {
            const toast = document.getElementById('toast');
            document.getElementById('toast-msg').innerText = msg;
            toast.classList.remove('translate-x-full');
            setTimeout(() => {
                toast.classList.add('translate-x-full');
            }, 3000);
        }

        // Countdown Timer
        function updateTimer() {
            const now = new Date();
            const h = 23 - now.getHours();
            const m = 59 - now.getMinutes();
            const s = 59 - now.getSeconds();
            document.getElementById('hours').innerText = h < 10 ? '0' + h : h;
            document.getElementById('minutes').innerText = m < 10 ? '0' + m : m;
            document.getElementById('seconds').innerText = s < 10 ? '0' + s : s;
        }
        setInterval(updateTimer, 1000);

        // Sorting & Filters
        function handleSort(val) {
            if (val === 'low') filteredProducts.sort((a,b) => a.price - b.price);
            else if (val === 'high') filteredProducts.sort((a,b) => b.price - a.price);
            else if (val === 'newest') filteredProducts = [...products].reverse();
            else filteredProducts = [...products];
            renderProducts();
        }

        function handleBrandFilter(val) {
            if (val === 'all') filteredProducts = [...products];
            else filteredProducts = products.filter(p => p.brand === val);
            renderProducts();
        }

        function filterByGender(gender) {
            filteredProducts = products.filter(p => p.gender === gender);
            renderProducts();
            document.getElementById('shop').scrollIntoView();
        }

        function filterByTag(tag) {
            if (tag === 'Best') filteredProducts = products.filter(p => p.tag === 'Best' || p.rating === 5);
            else if (tag === 'New') filteredProducts = products.filter(p => p.tag === 'New');
            else if (tag === 'Sale') filteredProducts = products.filter(p => p.tag === 'Sale');
            else filteredProducts = products.filter(p => p.gender === tag);
            renderProducts();
            document.getElementById('shop').scrollIntoView();
        }

        // Modals
        function toggleModal(id) {
            const modal = document.getElementById(id);
            modal.classList.toggle('hidden');
        }

        function showCheckout() {
            if (cart.length === 0) return showToast("Keranjang Anda kosong");
            toggleCart();
            const summary = document.getElementById('checkout-summary');
            summary.innerHTML = cart.map(item => `
                <div class="flex justify-between text-xs">
                    <span class="text-gray-400">${item.name} x${item.qty}</span>
                    <span>Rp ${(item.price * item.qty).toLocaleString()}</span>
                </div>
            `).join('');
            const total = cart.reduce((sum, item) => sum + (item.price * item.qty), 0);
            document.getElementById('checkout-total').innerText = `Rp ${total.toLocaleString()}`;
            toggleModal('checkoutModal');
        }

        function processOrder() {
            showToast("Pesanan sedang diproses. Mengalihkan ke WhatsApp...");
            setTimeout(() => {
                const total = cart.reduce((sum, item) => sum + (item.price * item.qty), 0);
                const text = `Halo DONIX PARFUME, Saya ingin memesan: \n${cart.map(i => `- ${i.name} (${i.qty})`).join('\n')}\n\nTotal: Rp ${total.toLocaleString()}`;
                window.open(`https://wa.me/628123456789?text=${encodeURIComponent(text)}`);
                cart = [];
                updateUI();
                toggleModal('checkoutModal');
            }, 2000);
        }

        // Mobile Menu
        function toggleMobileMenu() {
            document.getElementById('mobileMenu').classList.toggle('translate-x-full');
        }

        // Admin Panel Logic
        function showAdmin() {
            const password = prompt("Enter Admin Access Key (Hint: 2026):");
            if (password === '2026') {
                document.getElementById('adminPanel').classList.remove('hidden');
                document.getElementById('adminPanel').classList.add('flex');
                initChart();
            } else {
                alert("Access Denied.");
            }
        }

        function hideAdmin() {
            document.getElementById('adminPanel').classList.add('hidden');
            document.getElementById('adminPanel').classList.remove('flex');
        }

        function initChart() {
            const ctx = document.getElementById('salesChart').getContext('2d');
            new Chart(ctx, {
                type: 'line',
                data: {
                    labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun'],
                    datasets: [{
                        label: 'Sales Revenue',
                        data: [12, 19, 15, 25, 22, 30],
                        borderColor: '#D4AF37',
                        tension: 0.4,
                        fill: true,
                        backgroundColor: 'rgba(212, 175, 55, 0.1)'
                    }]
                },
                options: {
                    plugins: { legend: { display: false } },
                    scales: {
                        y: { display: false },
                        x: { grid: { color: 'rgba(255,255,255,0.05)' }, ticks: { color: '#555' } }
                    }
                }
            });
        }

        // Quiz Fragrance
        function startQuiz() {
            const char = prompt("Pilih karakter Anda: (1) Bold/Kuat, (2) Sweet/Romantis, (3) Fresh/Sporty");
            if (char === '1') {
                filterByGender('Men');
                showToast("Kami merekomendasikan Dior Sauvage Elixir untuk karakter Bold Anda.");
            } else if (char === '2') {
                filterByGender('Women');
                showToast("Karakter Romantis Anda sangat cocok dengan YSL Libre Intense.");
            } else {
                filterByGender('Unisex');
                showToast("Kesegaran Baccarat Rouge 540 cocok untuk karakter Fresh Anda.");
            }
        }

        // GSAP Animations
        gsap.from('#hero-img', { scale: 1.2, duration: 20, repeat: -1, yoyo: true, ease: "none" });
    </script>
</body>
</html>
