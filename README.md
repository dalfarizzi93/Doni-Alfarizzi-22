<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DONIX PARFUME | Premium Luxury Fragrance</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.9.1/chart.min.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css"/>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&family=Plus+Jakarta+Sans:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        gold: {
                            50: '#fdfbf2',
                            100: '#f9f4da',
                            200: '#f1e6a7',
                            300: '#e7d16a',
                            400: '#ddb93e',
                            500: '#c5a028',
                            600: '#a67f1e',
                            700: '#85611b',
                            800: '#6f4e1c',
                            900: '#5f431c',
                            950: '#37230d',
                        },
                        dark: '#0a0a0a',
                    },
                    fontFamily: {
                        serif: ['Playfair Display', 'serif'],
                        sans: ['Plus Jakarta Sans', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <style>
        ::-webkit-scrollbar { width: 6px; }
        ::-webkit-scrollbar-track { background: #1a1a1a; }
        ::-webkit-scrollbar-thumb { background: #c5a028; border-radius: 10px; }
        
        .glass { background: rgba(255, 255, 255, 0.05); backdrop-filter: blur(10px); border: 1px solid rgba(255, 255, 255, 0.1); }
        .gold-gradient { background: linear-gradient(45deg, #c5a028, #f1e6a7, #a67f1e); }
        .text-gold-gradient { background: linear-gradient(45deg, #c5a028, #f1e6a7, #a67f1e); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        
        .product-card:hover .product-action { opacity: 1; transform: translateY(0); }
        .sticky-nav { position: fixed; top: 0; width: 100%; z-index: 50; transition: all 0.3s ease; }
        .nav-scrolled { background: rgba(10, 10, 10, 0.95); backdrop-filter: blur(10px); box-shadow: 0 4px 20px rgba(0,0,0,0.5); }
        
        input:focus { outline: none; border-color: #c5a028; ring: 0; }
    </style>
</head>
<body class="bg-dark text-gray-200 font-sans selection:bg-gold-500 selection:text-dark overflow-x-hidden">

    <!-- Loading Screen -->
    <div id="loading-screen" class="fixed inset-0 z-[100] bg-dark flex flex-col items-center justify-center">
        <div class="mb-4 text-4xl font-serif text-gold-500 animate-pulse">DONIX</div>
        <div class="w-48 h-1 bg-gray-800 rounded-full overflow-hidden">
            <div class="h-full bg-gold-500 animate-[loading_2s_ease-in-out_infinite]" style="width: 30%"></div>
        </div>
    </div>

    <!-- Notification Toast -->
    <div id="toast" class="fixed top-24 right-5 z-[60] transform translate-x-full transition-all duration-300 pointer-events-none">
        <div class="bg-white text-dark px-6 py-3 rounded-lg shadow-2xl flex items-center border-l-4 border-gold-500">
            <span id="toast-msg" class="font-semibold text-sm">Produk ditambahkan ke keranjang!</span>
        </div>
    </div>

    <!-- MAIN APP WRAPPER -->
    <div id="app">
        
        <!-- CUSTOMER VIEW -->
        <div id="customer-view">
            <!-- Header/Navbar -->
            <nav id="navbar" class="sticky-nav px-6 py-4 flex items-center justify-between transition-all duration-500">
                <div class="flex items-center gap-8">
                    <a href="#" class="text-3xl font-serif tracking-widest text-gold-500">DONIX<span class="text-white ml-2 text-sm tracking-normal font-sans uppercase">Parfume</span></a>
                    <div class="hidden lg:flex items-center gap-6 text-xs uppercase tracking-widest font-semibold">
                        <a href="#" onclick="scrollToSection('hero')" class="hover:text-gold-400 transition">Home</a>
                        <a href="#" onclick="scrollToSection('products')" class="hover:text-gold-400 transition">Shop</a>
                        <a href="#" class="hover:text-gold-400 transition">Men</a>
                        <a href="#" class="hover:text-gold-400 transition">Women</a>
                        <a href="#" class="hover:text-gold-400 transition">Unisex</a>
                        <a href="#" class="hover:text-gold-400 transition text-red-400">Promo</a>
                    </div>
                </div>

                <div class="flex items-center gap-6">
                    <div class="hidden md:flex relative">
                        <input type="text" id="search-input" placeholder="Cari aroma mewah..." class="bg-white/5 border border-white/10 rounded-full py-2 px-4 text-xs w-64 focus:w-80 transition-all focus:bg-white/10">
                        <svg class="w-4 h-4 absolute right-3 top-2.5 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path></svg>
                    </div>
                    <button onclick="toggleAuthModal()" class="hover:text-gold-400 transition"><svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"></path></svg></button>
                    <button class="relative hover:text-gold-400 transition">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z"></path></svg>
                        <span id="wishlist-count" class="absolute -top-1 -right-1 bg-gold-600 text-[10px] text-white w-4 h-4 rounded-full flex items-center justify-center">0</span>
                    </button>
                    <button onclick="toggleCart()" class="relative hover:text-gold-400 transition">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z"></path></svg>
                        <span id="cart-count" class="absolute -top-1 -right-1 bg-gold-600 text-[10px] text-white w-4 h-4 rounded-full flex items-center justify-center">0</span>
                    </button>
                    <button onclick="goToSellerLogin()" class="ml-4 text-[10px] border border-gold-500/50 px-2 py-1 rounded text-gold-500 hover:bg-gold-500 hover:text-dark transition uppercase font-bold">Seller Panel</button>
                </div>
            </nav>

            <!-- Hero Section -->
            <section id="hero" class="relative h-screen flex items-center overflow-hidden">
                <div class="absolute inset-0 z-0">
                    <div class="absolute inset-0 bg-gradient-to-r from-dark via-dark/70 to-transparent z-10"></div>
                    <img src="https://images.unsplash.com/photo-1594035910387-fea47794261f?auto=format&fit=crop&q=80&w=2000" class="w-full h-full object-cover scale-105 animate-[kenburns_20s_ease-in-out_infinite]" alt="Luxury Perfume">
                </div>
                
                <div class="container mx-auto px-12 relative z-20 mt-20">
                    <h4 class="text-gold-500 uppercase tracking-[0.3em] font-bold text-sm mb-4 animate__animated animate__fadeInUp">New 2026 Collection</h4>
                    <h1 class="text-6xl md:text-8xl font-serif text-white leading-tight mb-6 animate__animated animate__fadeInUp animate__delay-1s">Luxury Fragrance <br> <span class="text-gold-400">Collection</span></h1>
                    <p class="max-w-xl text-gray-300 text-lg mb-10 animate__animated animate__fadeInUp animate__delay-2s">Temukan aroma eksklusif yang mendefinisikan karakter dan kelas Anda. Originalitas yang tak tertandingi dengan sentuhan kemewahan modern.</p>
                    <div class="flex gap-4 animate__animated animate__fadeInUp animate__delay-3s">
                        <button onclick="scrollToSection('products')" class="px-8 py-4 bg-gold-600 hover:bg-gold-500 text-dark font-bold uppercase tracking-widest transition-all rounded-sm shadow-xl shadow-gold-900/20">Shop Now</button>
                        <button class="px-8 py-4 border border-white/20 hover:border-gold-400 text-white font-bold uppercase tracking-widest transition-all rounded-sm backdrop-blur-sm">Explore More</button>
                    </div>
                </div>
                
                <div class="absolute bottom-10 left-12 flex gap-10 text-xs tracking-widest text-gray-400 font-bold uppercase z-20">
                    <div class="flex items-center gap-2"><span class="w-10 h-[1px] bg-gold-500"></span> 01 ELEGANCE</div>
                    <div class="flex items-center gap-2 opacity-50"><span class="w-10 h-[1px] bg-gray-500"></span> 02 QUALITY</div>
                    <div class="flex items-center gap-2 opacity-50"><span class="w-10 h-[1px] bg-gray-500"></span> 03 CLASSIC</div>
                </div>
            </section>

            <!-- Category Section -->
            <section class="py-24 bg-dark">
                <div class="container mx-auto px-6">
                    <div class="flex flex-col items-center mb-16">
                        <div class="w-12 h-[2px] bg-gold-500 mb-4"></div>
                        <h2 class="text-4xl font-serif text-white">Top Categories</h2>
                    </div>
                    <div class="grid grid-cols-2 lg:grid-cols-6 gap-6">
                        <!-- Category Cards -->
                        <div class="group relative h-80 overflow-hidden rounded-sm cursor-pointer border border-white/5">
                            <img src="https://images.unsplash.com/photo-1541643600914-78b084683601?auto=format&fit=crop&q=80&w=400" class="w-full h-full object-cover grayscale group-hover:grayscale-0 transition-all duration-700 group-hover:scale-110">
                            <div class="absolute inset-0 bg-dark/40 group-hover:bg-dark/20 transition-all"></div>
                            <div class="absolute bottom-6 left-6">
                                <span class="text-white font-bold uppercase tracking-widest text-sm">Men</span>
                                <div class="w-0 group-hover:w-full h-[1px] bg-gold-500 transition-all duration-500"></div>
                            </div>
                        </div>
                        <div class="group relative h-80 overflow-hidden rounded-sm cursor-pointer border border-white/5">
                            <img src="https://images.unsplash.com/photo-1592945403244-b3fbafd7f539?auto=format&fit=crop&q=80&w=400" class="w-full h-full object-cover grayscale group-hover:grayscale-0 transition-all duration-700 group-hover:scale-110">
                            <div class="absolute inset-0 bg-dark/40 group-hover:bg-dark/20 transition-all"></div>
                            <div class="absolute bottom-6 left-6">
                                <span class="text-white font-bold uppercase tracking-widest text-sm">Women</span>
                                <div class="w-0 group-hover:w-full h-[1px] bg-gold-500 transition-all duration-500"></div>
                            </div>
                        </div>
                        <div class="group relative h-80 overflow-hidden rounded-sm cursor-pointer border border-white/5">
                            <img src="https://images.unsplash.com/photo-1615484477778-ca3b77940c25?auto=format&fit=crop&q=80&w=400" class="w-full h-full object-cover grayscale group-hover:grayscale-0 transition-all duration-700 group-hover:scale-110">
                            <div class="absolute inset-0 bg-dark/40 group-hover:bg-dark/20 transition-all"></div>
                            <div class="absolute bottom-6 left-6">
                                <span class="text-white font-bold uppercase tracking-widest text-sm">Unisex</span>
                                <div class="w-0 group-hover:w-full h-[1px] bg-gold-500 transition-all duration-500"></div>
                            </div>
                        </div>
                        <div class="group relative h-80 overflow-hidden rounded-sm cursor-pointer border border-white/5">
                            <img src="https://images.unsplash.com/photo-1523293182086-7651a899d37f?auto=format&fit=crop&q=80&w=400" class="w-full h-full object-cover grayscale group-hover:grayscale-0 transition-all duration-700 group-hover:scale-110">
                            <div class="absolute inset-0 bg-dark/40 group-hover:bg-dark/20 transition-all"></div>
                            <div class="absolute bottom-6 left-6">
                                <span class="text-white font-bold uppercase tracking-widest text-sm">Premium</span>
                                <div class="w-0 group-hover:w-full h-[1px] bg-gold-500 transition-all duration-500"></div>
                            </div>
                        </div>
                        <div class="group relative h-80 overflow-hidden rounded-sm cursor-pointer border border-white/5">
                            <img src="https://images.unsplash.com/photo-1588405864443-30510f279585?auto=format&fit=crop&q=80&w=400" class="w-full h-full object-cover grayscale group-hover:grayscale-0 transition-all duration-700 group-hover:scale-110">
                            <div class="absolute inset-0 bg-dark/40 group-hover:bg-dark/20 transition-all"></div>
                            <div class="absolute bottom-6 left-6">
                                <span class="text-white font-bold uppercase tracking-widest text-sm">Gift Set</span>
                                <div class="w-0 group-hover:w-full h-[1px] bg-gold-500 transition-all duration-500"></div>
                            </div>
                        </div>
                        <div class="group relative h-80 overflow-hidden rounded-sm cursor-pointer border border-white/5">
                            <img src="https://images.unsplash.com/photo-1594035910387-fea47794261f?auto=format&fit=crop&q=80&w=400" class="w-full h-full object-cover grayscale group-hover:grayscale-0 transition-all duration-700 group-hover:scale-110">
                            <div class="absolute inset-0 bg-dark/40 group-hover:bg-dark/20 transition-all"></div>
                            <div class="absolute bottom-6 left-6">
                                <span class="text-white font-bold uppercase tracking-widest text-sm">Best Seller</span>
                                <div class="w-0 group-hover:w-full h-[1px] bg-gold-500 transition-all duration-500"></div>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Flash Sale -->
            <section class="py-12 bg-gold-600">
                <div class="container mx-auto px-6 flex flex-col md:flex-row items-center justify-between">
                    <div class="flex items-center gap-6 mb-6 md:mb-0">
                        <div class="bg-dark text-gold-500 p-4 rounded-sm animate-pulse">
                            <svg class="w-8 h-8" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M11.3 1.046A1 1 0 0112 2v5h4a1 1 0 01.82 1.573l-7 10A1 1 0 018 18v-5H4a1 1 0 01-.82-1.573l7-10a1 1 0 011.12-.38z" clip-rule="evenodd"></path></svg>
                        </div>
                        <div>
                            <h3 class="text-dark font-serif text-3xl font-bold">Midnight Flash Sale</h3>
                            <p class="text-dark/80 font-medium">Penawaran terbatas hingga akhir pekan ini!</p>
                        </div>
                    </div>
                    <div class="flex gap-4">
                        <div class="flex flex-col items-center bg-dark text-white p-3 min-w-[70px] rounded-sm shadow-xl">
                            <span id="hours" class="text-2xl font-bold">12</span>
                            <span class="text-[10px] uppercase">Hours</span>
                        </div>
                        <div class="flex flex-col items-center bg-dark text-white p-3 min-w-[70px] rounded-sm shadow-xl">
                            <span id="minutes" class="text-2xl font-bold">45</span>
                            <span class="text-[10px] uppercase">Min</span>
                        </div>
                        <div class="flex flex-col items-center bg-dark text-white p-3 min-w-[70px] rounded-sm shadow-xl">
                            <span id="seconds" class="text-2xl font-bold">30</span>
                            <span class="text-[10px] uppercase">Sec</span>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Product Grid & Filter -->
            <section id="products" class="py-24 bg-dark">
                <div class="container mx-auto px-6">
                    <div class="flex flex-col md:flex-row justify-between items-end mb-12">
                        <div>
                            <h2 class="text-4xl font-serif text-white mb-4">Our Signature Selection</h2>
                            <p class="text-gray-400">Pilihan kurasi parfum terbaik dari brand ternama dunia.</p>
                        </div>
                        <div class="mt-8 md:mt-0 flex gap-4">
                            <select id="filter-gender" class="bg-transparent border-b border-white/20 text-white text-sm py-2 focus:border-gold-500">
                                <option value="all">All Genders</option>
                                <option value="men">Men</option>
                                <option value="women">Women</option>
                                <option value="unisex">Unisex</option>
                            </select>
                            <select id="sort-price" class="bg-transparent border-b border-white/20 text-white text-sm py-2 focus:border-gold-500">
                                <option value="popular">Popularity</option>
                                <option value="low">Price: Low to High</option>
                                <option value="high">Price: High to Low</option>
                            </select>
                        </div>
                    </div>

                    <div id="product-container" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-x-8 gap-y-12">
                        <!-- Product Item Template -->
                    </div>
                    
                    <div class="mt-16 flex justify-center">
                        <button class="px-12 py-4 border border-gold-500 text-gold-500 hover:bg-gold-500 hover:text-dark transition-all uppercase tracking-widest font-bold text-xs">Load More Collection</button>
                    </div>
                </div>
            </section>

            <!-- Quiz / AI Recom Section -->
            <section class="py-24 bg-[#050505] relative">
                <div class="container mx-auto px-6 flex flex-col lg:flex-row items-center gap-16">
                    <div class="lg:w-1/2 relative">
                        <div class="absolute -top-10 -left-10 w-40 h-40 border border-gold-500/20 rounded-full animate-ping"></div>
                        <img src="https://images.unsplash.com/photo-1592945403244-b3fbafd7f539?auto=format&fit=crop&q=80&w=800" class="rounded-sm relative z-10 shadow-2xl grayscale" alt="AI Quiz">
                        <div class="absolute -bottom-6 -right-6 bg-gold-600 p-8 z-20 shadow-xl">
                            <p class="text-dark font-serif text-2xl italic">"The right scent defines who you are."</p>
                        </div>
                    </div>
                    <div class="lg:w-1/2">
                        <span class="text-gold-500 font-bold tracking-[0.2em] text-xs uppercase mb-4 block">AI Scent Advisor</span>
                        <h2 class="text-4xl md:text-5xl font-serif text-white mb-6 leading-tight">Bingung Pilih Parfum yang Cocok?</h2>
                        <p class="text-gray-400 mb-10 text-lg leading-relaxed">Gunakan teknologi AI kami untuk mendapatkan rekomendasi aroma berdasarkan kepribadian, aktivitas harian, dan preferensi mood Anda. Hanya butuh 1 menit.</p>
                        <button class="flex items-center gap-4 group">
                            <span class="w-16 h-16 rounded-full border border-gold-500 flex items-center justify-center group-hover:bg-gold-500 transition-all">
                                <svg class="w-6 h-6 text-gold-500 group-hover:text-dark" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM9.555 7.168A1 1 0 008 8v4a1 1 0 001.555.832l3-2a1 1 0 000-1.664l-3-2z" clip-rule="evenodd"></path></svg>
                            </span>
                            <span class="text-white font-bold uppercase tracking-widest">Start Scent Quiz</span>
                        </button>
                    </div>
                </div>
            </section>

            <!-- Footer -->
            <footer class="bg-dark border-t border-white/5 pt-24 pb-12">
                <div class="container mx-auto px-6">
                    <div class="grid grid-cols-1 md:grid-cols-4 gap-12 mb-16">
                        <div class="col-span-1 md:col-span-1">
                            <h2 class="text-2xl font-serif text-gold-500 mb-6">DONIX PARFUME</h2>
                            <p class="text-gray-400 text-sm leading-relaxed mb-8">Destinasi parfum premium terpercaya sejak 2020. Menghadirkan kemewahan aroma internasional ke genggaman Anda dengan jaminan keaslian 100%.</p>
                            <div class="flex gap-4">
                                <a href="#" class="w-10 h-10 rounded-full border border-white/10 flex items-center justify-center hover:border-gold-500 transition"><svg class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24"><path d="M24 4.557c-.883.392-1.832.656-2.828.775 1.017-.609 1.798-1.574 2.165-2.724-.951.564-2.005.974-3.127 1.195-.897-.957-2.178-1.555-3.594-1.555-3.179 0-5.515 2.966-4.797 6.045-4.091-.205-7.719-2.165-10.148-5.144-1.29 2.213-.669 5.108 1.523 6.574-.806-.026-1.566-.247-2.229-.616-.054 2.281 1.581 4.415 3.949 4.89-.693.188-1.452.232-2.224.084.626 1.956 2.444 3.379 4.6 3.419-2.07 1.623-4.678 2.348-7.29 2.04 2.179 1.397 4.768 2.212 7.548 2.212 9.142 0 14.307-7.721 13.995-14.646.962-.695 1.797-1.562 2.457-2.549z"/></svg></a>
                                <a href="#" class="w-10 h-10 rounded-full border border-white/10 flex items-center justify-center hover:border-gold-500 transition"><svg class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.162 6.162 6.162 6.162-2.759 6.162-6.162-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/></svg></a>
                            </div>
                        </div>
                        <div>
                            <h4 class="text-white font-bold uppercase tracking-widest text-sm mb-6">Quick Links</h4>
                            <ul class="space-y-4 text-gray-400 text-sm">
                                <li><a href="#" class="hover:text-gold-500 transition">Shop All</a></li>
                                <li><a href="#" class="hover:text-gold-500 transition">New Arrivals</a></li>
                                <li><a href="#" class="hover:text-gold-500 transition">Flash Sale</a></li>
                                <li><a href="#" class="hover:text-gold-500 transition">Track Order</a></li>
                                <li><a href="#" class="hover:text-gold-500 transition">Affiliate Program</a></li>
                            </ul>
                        </div>
                        <div>
                            <h4 class="text-white font-bold uppercase tracking-widest text-sm mb-6">Customer Care</h4>
                            <ul class="space-y-4 text-gray-400 text-sm">
                                <li><a href="#" class="hover:text-gold-500 transition">Help Center</a></li>
                                <li><a href="#" class="hover:text-gold-500 transition">Shipping Policy</a></li>
                                <li><a href="#" class="hover:text-gold-500 transition">Returns & Exchanges</a></li>
                                <li><a href="#" class="hover:text-gold-500 transition">Privacy Policy</a></li>
                                <li><a href="#" class="hover:text-gold-500 transition">FAQ</a></li>
                            </ul>
                        </div>
                        <div>
                            <h4 class="text-white font-bold uppercase tracking-widest text-sm mb-6">Contact Us</h4>
                            <div class="space-y-4 text-gray-400 text-sm">
                                <p class="flex items-start gap-3"><svg class="w-5 h-5 text-gold-500 shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"></path><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"></path></svg> Senayan City Mall, Level 2, Jakarta Pusat</p>
                                <p class="flex items-center gap-3"><svg class="w-5 h-5 text-gold-500 shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"></path></svg> +62 881-0223-62914</p>
                                <p class="flex items-center gap-3"><svg class="w-5 h-5 text-gold-500 shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 01-2 2H7a2 2 0 01-2-2V7a2 2 0 012-2h14a2 2 0 012 2v10"></path></svg> cs@donixparfume.com</p>
                            </div>
                        </div>
                    </div>
                    <div class="border-t border-white/5 pt-8 flex flex-col md:flex-row justify-between items-center">
                        <p class="text-gray-500 text-xs mb-4 md:mb-0">&copy; 2026 DONIX PARFUME. All rights reserved. Elegant Fragrance for Elegant People.</p>
                        <div class="flex items-center gap-6">
                            <img src="https://upload.wikimedia.org/wikipedia/commons/b/b5/PayPal.svg" class="h-4 grayscale opacity-50">
                            <img src="https://upload.wikimedia.org/wikipedia/commons/5/5e/Visa_Inc._logo.svg" class="h-3 grayscale opacity-50">
                            <img src="https://upload.wikimedia.org/wikipedia/commons/2/2a/Mastercard-logo.svg" class="h-6 grayscale opacity-50">
                        </div>
                    </div>
                </div>
            </footer>
        </div>

        <!-- SELLER DASHBOARD VIEW (HIDDEN BY DEFAULT) -->
        <div id="seller-view" class="hidden min-h-screen bg-[#0f0f0f] flex">
            <!-- Sidebar -->
            <div class="w-64 bg-dark border-r border-white/10 flex flex-col shrink-0">
                <div class="p-6">
                    <div class="text-xl font-serif text-gold-500 mb-8">DONIX SELLER</div>
                    <nav class="space-y-1">
                        <a href="#" onclick="showDashboardSection('main')" class="flex items-center gap-3 px-4 py-3 text-sm font-semibold text-gold-500 bg-gold-500/10 rounded-lg">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2V6zM14 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2V6zM4 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2v-2zM14 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2v-2z"></path></svg>
                            Dashboard
                        </a>
                        <a href="#" onclick="showDashboardSection('products-mgmt')" class="flex items-center gap-3 px-4 py-3 text-sm font-semibold text-gray-400 hover:text-white hover:bg-white/5 transition rounded-lg">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4"></path></svg>
                            Manajemen Produk
                        </a>
                        <a href="#" onclick="showDashboardSection('orders')" class="flex items-center gap-3 px-4 py-3 text-sm font-semibold text-gray-400 hover:text-white hover:bg-white/5 transition rounded-lg">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2"></path></svg>
                            Pesanan
                        </a>
                        <a href="#" class="flex items-center gap-3 px-4 py-3 text-sm font-semibold text-gray-400 hover:text-white hover:bg-white/5 transition rounded-lg">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m.5-1c.28 0 .546-.073.784-.202M12 15c-1.012 0-1.867-.321-2.401-.827"></path></svg>
                            Keuangan
                        </a>
                    </nav>
                </div>
                <div class="mt-auto p-6 border-t border-white/5">
                    <button onclick="exitSellerView()" class="w-full flex items-center gap-3 px-4 py-3 text-sm font-semibold text-red-400 hover:bg-red-400/10 rounded-lg transition">
                        <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1"></path></svg>
                        Keluar Panel
                    </button>
                </div>
            </div>

            <!-- Content -->
            <div class="flex-1 p-10 overflow-y-auto">
                <header class="flex justify-between items-center mb-10">
                    <div>
                        <h1 class="text-3xl font-bold text-white mb-2">Halo, Owner!</h1>
                        <p class="text-gray-400">Inilah statistik performa DONIX PARFUME hari ini.</p>
                    </div>
                    <div class="flex items-center gap-4">
                        <div class="bg-white/5 px-4 py-2 rounded-lg border border-white/10 text-sm">
                            <span class="text-gray-400">Status Toko:</span> <span class="text-green-400 font-bold ml-1">BUKA</span>
                        </div>
                        <img src="https://i.pravatar.cc/150?u=owner" class="w-12 h-12 rounded-full border-2 border-gold-500">
                    </div>
                </header>

                <!-- Section: Dashboard Main -->
                <div id="section-main" class="space-y-10">
                    <div class="grid grid-cols-1 md:grid-cols-4 gap-6">
                        <div class="bg-white/5 p-6 rounded-2xl border border-white/10">
                            <div class="text-gray-400 text-sm mb-4">Total Penjualan</div>
                            <div class="text-2xl font-bold text-white mb-2">Rp 45.820.000</div>
                            <div class="text-xs text-green-400 flex items-center gap-1">
                                <svg class="w-3 h-3" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M12 7a1 1 0 110-2h5a1 1 0 011 1v5a1 1 0 11-2 0V8.414l-4.293 4.293a1 1 0 01-1.414 0L8 10.414l-4.293 4.293a1 1 0 01-1.414-1.414l5-5a1 1 0 011.414 0L11 10.586 14.586 7H12z" clip-rule="evenodd"></path></svg>
                                +12% vs kemarin
                            </div>
                        </div>
                        <div class="bg-white/5 p-6 rounded-2xl border border-white/10">
                            <div class="text-gray-400 text-sm mb-4">Order Masuk</div>
                            <div class="text-2xl font-bold text-white mb-2">24 Pesanan</div>
                            <div class="text-xs text-blue-400">4 Perlu diproses</div>
                        </div>
                        <div class="bg-white/5 p-6 rounded-2xl border border-white/10">
                            <div class="text-gray-400 text-sm mb-4">Produk Habis</div>
                            <div class="text-2xl font-bold text-white mb-2">2 Item</div>
                            <div class="text-xs text-red-400">Segera restock!</div>
                        </div>
                        <div class="bg-white/5 p-6 rounded-2xl border border-white/10">
                            <div class="text-gray-400 text-sm mb-4">Total Customer</div>
                            <div class="text-2xl font-bold text-white mb-2">1,248</div>
                            <div class="text-xs text-gold-400">58 Baru bulan ini</div>
                        </div>
                    </div>

                    <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                        <div class="lg:col-span-2 bg-white/5 p-8 rounded-2xl border border-white/10">
                            <h3 class="text-xl font-bold text-white mb-6">Analitik Penjualan</h3>
                            <canvas id="salesChart" height="250"></canvas>
                        </div>
                        <div class="bg-white/5 p-8 rounded-2xl border border-white/10">
                            <h3 class="text-xl font-bold text-white mb-6">Stok Menipis</h3>
                            <div class="space-y-6">
                                <div class="flex items-center gap-4">
                                    <div class="w-12 h-12 bg-white/10 rounded overflow-hidden"><img src="https://images.unsplash.com/photo-1541643600914-78b084683601?w=100"></div>
                                    <div class="flex-1">
                                        <div class="text-sm font-bold">Dior Sauvage</div>
                                        <div class="text-xs text-gray-400">Sisa: 2 pcs</div>
                                    </div>
                                    <button class="text-gold-500 text-xs font-bold uppercase underline">Restock</button>
                                </div>
                                <div class="flex items-center gap-4">
                                    <div class="w-12 h-12 bg-white/10 rounded overflow-hidden"><img src="https://images.unsplash.com/photo-1523293182086-7651a899d37f?w=100"></div>
                                    <div class="flex-1">
                                        <div class="text-sm font-bold">Baccarat Rouge</div>
                                        <div class="text-xs text-gray-400">Sisa: 1 pcs</div>
                                    </div>
                                    <button class="text-gold-500 text-xs font-bold uppercase underline">Restock</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Section: Management Products -->
                <div id="section-products-mgmt" class="hidden animate__animated animate__fadeIn">
                    <div class="flex justify-between items-center mb-8">
                        <h2 class="text-2xl font-bold text-white">Daftar Produk</h2>
                        <button onclick="openAddProductModal()" class="bg-gold-600 hover:bg-gold-500 text-dark px-6 py-2 rounded-lg font-bold flex items-center gap-2">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6"></path></svg>
                            Tambah Produk Baru
                        </button>
                    </div>
                    
                    <div class="bg-white/5 rounded-2xl border border-white/10 overflow-hidden">
                        <table class="w-full text-left">
                            <thead class="bg-white/10 text-gray-400 text-xs uppercase tracking-widest">
                                <tr>
                                    <th class="px-6 py-4">Produk</th>
                                    <th class="px-6 py-4">Kategori</th>
                                    <th class="px-6 py-4">Harga</th>
                                    <th class="px-6 py-4">Stok</th>
                                    <th class="px-6 py-4">Status</th>
                                    <th class="px-6 py-4">Aksi</th>
                                </tr>
                            </thead>
                            <tbody id="seller-product-table" class="text-sm">
                                <!-- Data will be filled by JS -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>

        <!-- AUTH MODAL -->
        <div id="auth-modal" class="hidden fixed inset-0 z-[70] bg-dark/90 backdrop-blur-sm flex items-center justify-center p-6">
            <div class="bg-dark border border-white/10 w-full max-w-md p-10 rounded-sm relative shadow-2xl">
                <button onclick="toggleAuthModal()" class="absolute top-6 right-6 text-gray-500 hover:text-white"><svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l18 18"></path></svg></button>
                <div class="text-center mb-10">
                    <h2 class="text-3xl font-serif text-white mb-2">Selamat Datang</h2>
                    <p class="text-gray-400 text-sm">Masuk untuk pengalaman belanja yang lebih personal.</p>
                </div>
                <form onsubmit="event.preventDefault(); alert('Login berhasil!')" class="space-y-6">
                    <div>
                        <label class="block text-xs uppercase tracking-widest font-bold text-gold-500 mb-2">Email Address</label>
                        <input type="email" required class="w-full bg-white/5 border border-white/10 px-4 py-3 text-white focus:border-gold-500 transition-all rounded-sm" placeholder="email@anda.com">
                    </div>
                    <div>
                        <label class="block text-xs uppercase tracking-widest font-bold text-gold-500 mb-2">Password</label>
                        <input type="password" required class="w-full bg-white/5 border border-white/10 px-4 py-3 text-white focus:border-gold-500 transition-all rounded-sm" placeholder="••••••••">
                    </div>
                    <button class="w-full py-4 bg-gold-600 hover:bg-gold-500 text-dark font-bold uppercase tracking-widest transition-all rounded-sm mt-4">Log In</button>
                    <div class="text-center text-xs text-gray-500">
                        Belum punya akun? <a href="#" class="text-gold-400 hover:underline">Daftar Sekarang</a>
                    </div>
                </form>
            </div>
        </div>

        <!-- CART SIDEBAR -->
        <div id="cart-sidebar" class="fixed inset-y-0 right-0 z-[80] w-full max-w-md bg-dark border-l border-white/10 translate-x-full transition-all duration-500 shadow-2xl flex flex-col">
            <div class="p-6 border-b border-white/10 flex justify-between items-center">
                <h3 class="text-xl font-serif text-white">Your Shopping Bag</h3>
                <button onclick="toggleCart()" class="text-gray-400 hover:text-white"><svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l18 18"></path></svg></button>
            </div>
            
            <div id="cart-items" class="flex-1 overflow-y-auto p-6 space-y-6">
                <!-- Cart items appear here -->
            </div>
            
            <div class="p-6 border-t border-white/10 bg-white/5">
                <div class="flex justify-between items-center mb-6">
                    <span class="text-gray-400 uppercase tracking-widest text-xs font-bold">Subtotal</span>
                    <span id="cart-total" class="text-xl font-serif text-gold-500">Rp 0</span>
                </div>
                <button onclick="showCheckout()" class="w-full py-4 bg-gold-600 hover:bg-gold-500 text-dark font-bold uppercase tracking-widest transition-all rounded-sm">Proceed to Checkout</button>
            </div>
        </div>

        <!-- CHECKOUT MODAL -->
        <div id="checkout-modal" class="hidden fixed inset-0 z-[90] bg-dark flex items-center justify-center p-4">
            <div class="bg-dark border border-white/10 w-full max-w-4xl max-h-[90vh] overflow-y-auto p-10 rounded-sm">
                <div class="flex justify-between items-center mb-10">
                    <h2 class="text-3xl font-serif text-white">Complete Your Order</h2>
                    <button onclick="toggleModal('checkout-modal')" class="text-gray-500 hover:text-white"><svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l18 18"></path></svg></button>
                </div>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-12">
                    <div class="space-y-8">
                        <h4 class="text-gold-500 font-bold uppercase tracking-widest text-sm border-b border-white/10 pb-2">Informasi Pengiriman</h4>
                        <div class="space-y-4">
                            <input type="text" id="co-name" placeholder="Nama Lengkap" class="w-full bg-white/5 border border-white/10 px-4 py-3 rounded-sm">
                            <input type="text" id="co-wa" placeholder="Nomor WhatsApp" class="w-full bg-white/5 border border-white/10 px-4 py-3 rounded-sm">
                            <textarea id="co-address" placeholder="Alamat Lengkap" rows="3" class="w-full bg-white/5 border border-white/10 px-4 py-3 rounded-sm"></textarea>
                            <div class="grid grid-cols-2 gap-4">
                                <select id="co-courier" class="bg-white/5 border border-white/10 px-4 py-3 rounded-sm text-gray-400">
                                    <option>Pilih Kurir</option>
                                    <option>JNE Premium</option>
                                    <option>SiCepat Best</option>
                                    <option>Instan (Gojek/Grab)</option>
                                </select>
                                <select id="co-payment" class="bg-white/5 border border-white/10 px-4 py-3 rounded-sm text-gray-400">
                                    <option>Pilih Pembayaran</option>
                                    <option>Transfer Bank (BCA/Mandiri)</option>
                                    <option>QRIS / E-Wallet</option>
                                    <option>Cash on Delivery (COD)</option>
                                </select>
                            </div>
                        </div>
                    </div>
                    <div class="bg-white/5 p-8 rounded-sm">
                        <h4 class="text-gold-500 font-bold uppercase tracking-widest text-sm border-b border-white/10 pb-4 mb-6">Ringkasan Pesanan</h4>
                        <div id="co-summary-items" class="space-y-4 mb-8">
                            <!-- Items list -->
                        </div>
                        <div class="border-t border-white/10 pt-4 space-y-2">
                            <div class="flex justify-between text-xs text-gray-400">
                                <span>Subtotal</span>
                                <span id="co-subtotal">Rp 0</span>
                            </div>
                            <div class="flex justify-between text-xs text-gray-400">
                                <span>Ongkos Kirim</span>
                                <span>Rp 25.000</span>
                            </div>
                            <div class="flex justify-between text-lg font-bold text-white pt-2">
                                <span>Total</span>
                                <span id="co-total" class="text-gold-500">Rp 0</span>
                            </div>
                        </div>
                        <button onclick="processCheckout()" class="w-full py-4 bg-gold-600 hover:bg-gold-500 text-dark font-bold uppercase tracking-widest transition-all rounded-sm mt-8">Konfirmasi & Bayar via WhatsApp</button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Float WA Button -->
        <a href="https://wa.me/62881022362914" target="_blank" class="fixed bottom-6 left-6 z-50 bg-[#25D366] text-white p-4 rounded-full shadow-2xl hover:scale-110 transition-transform">
            <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
        </a>

    </div>

    <script>
        // DATA PRODUK
        const initialProducts = [
            { id: 1, name: "Bleu de Chanel", brand: "Chanel", price: 2450000, oldPrice: 2800000, category: "men", rating: 5, stock: 15, img: "https://images.unsplash.com/photo-1541643600914-78b084683601?w=500", badge: "New" },
            { id: 2, name: "Sauvage Elixir", brand: "Dior", price: 3100000, oldPrice: 3500000, category: "men", rating: 5, stock: 2, img: "https://images.unsplash.com/photo-1583467875263-d50dec37a88c?w=500", badge: "Best Seller" },
            { id: 3, name: "Baccarat Rouge 540", brand: "MFK", price: 5800000, oldPrice: 6500000, category: "unisex", rating: 5, stock: 1, img: "https://images.unsplash.com/photo-1523293182086-7651a899d37f?w=500", badge: "Exclusive" },
            { id: 4, name: "Libre Intense", brand: "YSL", price: 2200000, oldPrice: 2500000, category: "women", rating: 4, stock: 12, img: "https://images.unsplash.com/photo-1588405864443-30510f279585?w=500", badge: "Sale" },
            { id: 5, name: "Black Opium", brand: "YSL", price: 1950000, oldPrice: 2200000, category: "women", rating: 5, stock: 8, img: "https://images.unsplash.com/photo-1594035910387-fea47794261f?w=500", badge: "" },
            { id: 6, name: "Eros Flame", brand: "Versace", price: 1750000, oldPrice: 2000000, category: "men", rating: 4, stock: 20, img: "https://images.unsplash.com/photo-1592945403244-b3fbafd7f539?w=500", badge: "Popular" },
            { id: 7, name: "Oud Wood", brand: "Tom Ford", price: 4200000, oldPrice: 4800000, category: "unisex", rating: 5, stock: 5, img: "https://images.unsplash.com/photo-1585232351009-aa87416fca90?w=500", badge: "Rare" },
            { id: 8, name: "Acqua di Gio", brand: "Armani", price: 1850000, oldPrice: 2100000, category: "men", rating: 4, stock: 10, img: "https://images.unsplash.com/photo-1615484477778-ca3b77940c25?w=500", badge: "" }
        ];

        let cart = [];
        let wishlist = [];
        let currentProducts = [...initialProducts];

        // INITIALIZATION
        window.onload = () => {
            setTimeout(() => {
                document.getElementById('loading-screen').classList.add('hidden');
                renderProducts();
                initSalesChart();
                updateClock();
            }, 1500);

            window.onscroll = () => {
                const nav = document.getElementById('navbar');
                if (window.scrollY > 50) nav.classList.add('nav-scrolled');
                else nav.classList.remove('nav-scrolled');
            };
        };

        // RENDER PRODUCTS
        function renderProducts(products = currentProducts) {
            const container = document.getElementById('product-container');
            container.innerHTML = '';
            
            products.forEach(p => {
                container.innerHTML += `
                    <div class="product-card group animate__animated animate__fadeIn">
                        <div class="relative aspect-[3/4] overflow-hidden bg-[#111] mb-6 border border-white/5 rounded-sm">
                            ${p.badge ? `<span class="absolute top-4 left-4 z-10 bg-gold-600 text-dark text-[10px] font-bold uppercase px-3 py-1 rounded-sm">${p.badge}</span>` : ''}
                            <img src="${p.img}" alt="${p.name}" class="w-full h-full object-cover grayscale group-hover:grayscale-0 transition-all duration-700 group-hover:scale-110">
                            
                            <div class="product-action absolute bottom-0 left-0 right-0 p-4 translate-y-full opacity-0 transition-all duration-300 flex gap-2">
                                <button onclick="addToCart(${p.id})" class="flex-1 bg-white text-dark py-3 text-xs font-bold uppercase tracking-widest hover:bg-gold-500 transition-colors">Add to Bag</button>
                                <button onclick="addToWishlist(${p.id})" class="w-12 bg-dark/80 backdrop-blur-md text-white border border-white/10 flex items-center justify-center hover:bg-gold-600 transition-colors">
                                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z"></path></svg>
                                </button>
                            </div>
                        </div>
                        <div class="text-center">
                            <h5 class="text-gray-500 uppercase text-[10px] tracking-widest mb-1 font-bold">${p.brand}</h5>
                            <h4 class="text-white font-serif text-lg mb-2">${p.name}</h4>
                            <div class="flex items-center justify-center gap-1 mb-2">
                                ${Array(5).fill(0).map((_, i) => `<svg class="w-3 h-3 ${i < p.rating ? 'text-gold-500' : 'text-gray-700'}" fill="currentColor" viewBox="0 0 20 20"><path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path></svg>`).join('')}
                            </div>
                            <div class="flex items-center justify-center gap-3">
                                <span class="text-gold-500 font-bold">Rp ${p.price.toLocaleString('id-ID')}</span>
                                <span class="text-gray-600 line-through text-xs">Rp ${p.oldPrice.toLocaleString('id-ID')}</span>
                            </div>
                        </div>
                    </div>
                `;
            });
        }

        // CART LOGIC
        function addToCart(id) {
            const product = initialProducts.find(p => p.id === id);
            const inCart = cart.find(i => i.id === id);
            if (inCart) inCart.qty++;
            else cart.push({...product, qty: 1});
            
            updateUI();
            showToast(`Aroma ${product.name} siap dikirim!`);
        }

        function updateUI() {
            const cartCount = cart.reduce((acc, curr) => acc + curr.qty, 0);
            document.getElementById('cart-count').innerText = cartCount;
            document.getElementById('wishlist-count').innerText = wishlist.length;
            
            renderCart();
        }

        function renderCart() {
            const container = document.getElementById('cart-items');
            const totalEl = document.getElementById('cart-total');
            container.innerHTML = '';
            
            let total = 0;
            cart.forEach(item => {
                total += item.price * item.qty;
                container.innerHTML += `
                    <div class="flex gap-4 group">
                        <div class="w-20 h-24 bg-[#111] overflow-hidden rounded-sm">
                            <img src="${item.img}" class="w-full h-full object-cover">
                        </div>
                        <div class="flex-1">
                            <div class="flex justify-between">
                                <h4 class="text-white text-sm font-bold">${item.name}</h4>
                                <button onclick="removeFromCart(${item.id})" class="text-gray-600 hover:text-red-400 transition-colors"><svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"></path></svg></button>
                            </div>
                            <p class="text-xs text-gray-500 mb-2">${item.brand}</p>
                            <div class="flex justify-between items-center">
                                <div class="flex items-center gap-2">
                                    <button onclick="changeQty(${item.id}, -1)" class="w-6 h-6 border border-white/10 flex items-center justify-center text-xs hover:bg-white/10">-</button>
                                    <span class="text-xs font-bold text-white">${item.qty}</span>
                                    <button onclick="changeQty(${item.id}, 1)" class="w-6 h-6 border border-white/10 flex items-center justify-center text-xs hover:bg-white/10">+</button>
                                </div>
                                <span class="text-gold-500 font-bold text-sm">Rp ${(item.price * item.qty).toLocaleString('id-ID')}</span>
                            </div>
                        </div>
                    </div>
                `;
            });
            totalEl.innerText = `Rp ${total.toLocaleString('id-ID')}`;
        }

        function removeFromCart(id) {
            cart = cart.filter(i => i.id !== id);
            updateUI();
        }

        function changeQty(id, delta) {
            const item = cart.find(i => i.id === id);
            if (item) {
                item.qty += delta;
                if (item.qty <= 0) removeFromCart(id);
                else updateUI();
            }
        }

        // NAVIGATION
        function toggleCart() {
            document.getElementById('cart-sidebar').classList.toggle('translate-x-full');
        }

        function toggleAuthModal() {
            document.getElementById('auth-modal').classList.toggle('hidden');
        }

        function showCheckout() {
            if (cart.length === 0) return alert('Keranjang Anda kosong');
            toggleCart();
            document.getElementById('checkout-modal').classList.remove('hidden');
            renderCheckoutSummary();
        }

        function renderCheckoutSummary() {
            const list = document.getElementById('co-summary-items');
            list.innerHTML = '';
            let subtotal = 0;
            
            cart.forEach(item => {
                subtotal += item.price * item.qty;
                list.innerHTML += `
                    <div class="flex justify-between items-center text-sm">
                        <span class="text-gray-400">${item.name} x ${item.qty}</span>
                        <span class="text-white">Rp ${(item.price * item.qty).toLocaleString('id-ID')}</span>
                    </div>
                `;
            });
            
            document.getElementById('co-subtotal').innerText = `Rp ${subtotal.toLocaleString('id-ID')}`;
            document.getElementById('co-total').innerText = `Rp ${(subtotal + 25000).toLocaleString('id-ID')}`;
        }

        function processCheckout() {
            const name = document.getElementById('co-name').value;
            const wa = document.getElementById('co-wa').value;
            const address = document.getElementById('co-address').value;
            const courier = document.getElementById('co-courier').value;
            const pay = document.getElementById('co-payment').value;
            const total = document.getElementById('co-total').innerText;

            if (!name || !wa || !address) return alert('Mohon lengkapi data pengiriman');

            const orderList = cart.map(i => `- ${i.name} (${i.qty}x)`).join('%0A');
            const message = `Halo DONIX PARFUME,%0A%0ASaya ingin memesan parfum premium:%0A${orderList}%0A%0A*Total Pembayaran:* ${total}%0A%0A*Detail Pengiriman:*%0ANama: ${name}%0AWhatsApp: ${wa}%0AAlamat: ${address}%0AKurir: ${courier}%0APembayaran: ${pay}%0A%0AMohon diproses segera. Terima kasih!`;
            
            window.open(`https://wa.me/62881022362914?text=${message}`);
            cart = [];
            updateUI();
            document.getElementById('checkout-modal').classList.add('hidden');
        }

        // UTILITIES
        function scrollToSection(id) {
            document.getElementById(id).scrollIntoView({ behavior: 'smooth' });
        }

        function showToast(msg) {
            const toast = document.getElementById('toast');
            document.getElementById('toast-msg').innerText = msg;
            toast.classList.remove('translate-x-full');
            setTimeout(() => toast.classList.add('translate-x-full'), 3000);
        }

        function updateClock() {
            let h = 12, m = 45, s = 30;
            setInterval(() => {
                s--;
                if (s < 0) { s = 59; m--; }
                if (m < 0) { m = 59; h--; }
                document.getElementById('hours').innerText = String(h).padStart(2, '0');
                document.getElementById('minutes').innerText = String(m).padStart(2, '0');
                document.getElementById('seconds').innerText = String(s).padStart(2, '0');
            }, 1000);
        }

        function toggleModal(id) {
            document.getElementById(id).classList.toggle('hidden');
        }

        // SELLER LOGIC
        function goToSellerLogin() {
            const pass = prompt("Masukkan Password Admin:");
            if (pass === "admin123") {
                document.getElementById('customer-view').classList.add('hidden');
                document.getElementById('seller-view').classList.remove('hidden');
                renderSellerProducts();
            } else {
                alert("Password Salah!");
            }
        }

        function exitSellerView() {
            document.getElementById('seller-view').classList.add('hidden');
            document.getElementById('customer-view').classList.remove('hidden');
        }

        function showDashboardSection(id) {
            document.querySelectorAll('#seller-view [id^="section-"]').forEach(s => s.classList.add('hidden'));
            document.getElementById('section-' + id).classList.remove('hidden');
        }

        function renderSellerProducts() {
            const tbody = document.getElementById('seller-product-table');
            tbody.innerHTML = '';
            initialProducts.forEach(p => {
                tbody.innerHTML += `
                    <tr class="border-b border-white/5 hover:bg-white/5 transition">
                        <td class="px-6 py-4 flex items-center gap-3">
                            <img src="${p.img}" class="w-10 h-10 rounded object-cover">
                            <div>
                                <div class="font-bold text-white">${p.name}</div>
                                <div class="text-[10px] text-gray-500">${p.brand}</div>
                            </div>
                        </td>
                        <td class="px-6 py-4 capitalize text-gray-400">${p.category}</td>
                        <td class="px-6 py-4 text-gold-500 font-bold">Rp ${p.price.toLocaleString('id-ID')}</td>
                        <td class="px-6 py-4 text-gray-400">${p.stock} pcs</td>
                        <td class="px-6 py-4">
                            <span class="px-2 py-1 ${p.stock > 5 ? 'bg-green-400/10 text-green-400' : 'bg-red-400/10 text-red-400'} text-[10px] rounded-full font-bold">
                                ${p.stock > 5 ? 'Ready' : 'Low Stock'}
                            </span>
                        </td>
                        <td class="px-6 py-4">
                            <button class="text-gray-400 hover:text-white mr-2"><svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15.232 5.232l3.536 3.536m-2.036-5.036a2.5 2.5 0 113.536 3.536L6.5 21.036H3v-3.572L16.732 3.732z"></path></svg></button>
                            <button class="text-gray-400 hover:text-red-400"><svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"></path></svg></button>
                        </td>
                    </tr>
                `;
            });
        }

        function initSalesChart() {
            const ctx = document.getElementById('salesChart').getContext('2d');
            new Chart(ctx, {
                type: 'line',
                data: {
                    labels: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
                    datasets: [{
                        label: 'Penjualan (Juta)',
                        data: [12, 19, 15, 25, 32, 45, 40],
                        borderColor: '#c5a028',
                        tension: 0.4,
                        fill: true,
                        backgroundColor: 'rgba(197, 160, 40, 0.1)'
                    }]
                },
                options: {
                    plugins: { legend: { display: false } },
                    scales: {
                        y: { grid: { color: 'rgba(255,255,255,0.05)' }, ticks: { color: '#999' } },
                        x: { grid: { display: false }, ticks: { color: '#999' } }
                    }
                }
            });
        }
    </script>
</body>
</html>
