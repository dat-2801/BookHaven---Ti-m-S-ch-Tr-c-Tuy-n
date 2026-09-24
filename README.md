<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BookHaven - Tri Thức Cho Mọi Nhà</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        primary: {
                            50: '#f0fdf4',
                            100: '#dcfce7',
                            500: '#22c55e',
                            600: '#16a34a',
                            700: '#15803d',
                            800: '#166534',
                            900: '#14532d',
                        },
                        navy: {
                            800: '#1e293b',
                            900: '#0f172a',
                        },
                        warm: {
                            50: '#fdfbf7',
                            100: '#f7f3ea',
                            200: '#efe6d5',
                            500: '#d97706',
                        }
                    },
                    fontFamily: {
                        sans: ['Plus Jakarta Sans', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <style>
        ::-webkit-scrollbar { width: 8px; height: 8px; }
        ::-webkit-scrollbar-track { background: #f1f1f1; }
        ::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: #94a3b8; }
        .hide-scrollbar::-webkit-scrollbar { display: none; }
        .hide-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
    </style>
</head>
<body class="bg-warm-50 text-slate-800 font-sans antialiased min-h-screen flex flex-col justify-between selection:bg-primary-500 selection:text-white">

    <!-- HEADER -->
    <header class="sticky top-0 z-40 bg-white/95 backdrop-blur-md border-b border-slate-200 shadow-sm transition-all duration-300" id="main-header">
        <div class="bg-navy-900 text-white text-xs py-2 px-4 text-center font-medium">
            <span class="inline-block bg-primary-600 text-white text-[10px] uppercase font-bold px-2 py-0.5 rounded-full mr-2">Ưu đãi</span>
            Miễn phí vận chuyển cho đơn hàng từ 300.000đ | Nhập mã <span class="text-amber-300 font-bold">BOOKHAVEN</span> giảm 10%
        </div>

        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-20 gap-4">
                <a href="#" class="flex items-center gap-3 shrink-0 group">
                    <div class="w-11 h-11 bg-primary-600 rounded-xl flex items-center justify-center text-white text-xl font-black shadow-lg shadow-primary-600/30 group-hover:scale-105 transition-transform">
                        <i class="fa-solid me-0.5 fa-book-open"></i>
                    </div>
                    <div>
                        <span class="text-2xl font-extrabold text-navy-900 tracking-tight block leading-none">Book<span class="text-primary-600">Haven</span></span>
                        <span class="text-[10px] text-slate-400 font-medium tracking-widest uppercase">Thế Giới Sách Hay</span>
                    </div>
                </a>

                <!-- Search Bar -->
                <div class="flex-1 max-w-xl mx-4 hidden md:block">
                    <div class="relative">
                        <input type="text" id="search-input" onkeyup="handleSearch()" placeholder="Tìm kiếm theo tên sách, tác giả, thể loại..." class="w-full bg-slate-100/80 text-sm text-slate-800 border border-slate-200 rounded-full py-2.5 pl-11 pr-10 focus:outline-none focus:ring-2 focus:ring-primary-500 focus:bg-white transition-all shadow-inner">
                        <i class="fa-solid fa-magnifying-glass absolute left-4 top-1/2 -translate-y-1/2 text-slate-400"></i>
                        <button onclick="clearSearch()" id="clear-search-btn" class="hidden absolute right-3 top-1/2 -translate-y-1/2 text-slate-400 hover:text-slate-600">
                            <i class="fa-solid fa-circle-xmark"></i>
                        </button>
                    </div>
                </div>

                <!-- Navigation Actions -->
                <div class="flex items-center gap-2 sm:gap-4">
                    <button class="p-2.5 text-slate-600 hover:text-rose-500 hover:bg-slate-100 rounded-full transition relative hidden sm:flex" title="Yêu thích">
                        <i class="fa-regular fa-heart text-xl"></i>
                    </button>

                    <button onclick="toggleCartDrawer()" class="p-2.5 text-slate-700 hover:text-primary-600 hover:bg-slate-100 rounded-full transition relative flex items-center gap-2">
                        <div class="relative">
                            <i class="fa-solid fa-cart-shopping text-xl"></i>
                            <span id="cart-badge" class="absolute -top-1.5 -right-2 bg-rose-500 text-white text-[11px] font-bold rounded-full h-5 w-5 flex items-center justify-center animate-pulse border-2 border-white">0</span>
                        </div>
                        <span class="hidden lg:inline text-xs font-semibold text-slate-600">Giỏ hàng</span>
                    </button>

                    <div class="h-6 w-px bg-slate-200 hidden sm:block"></div>

                    <button onclick="openAuthModal()" class="flex items-center gap-2 bg-slate-100 hover:bg-slate-200 text-slate-800 font-semibold text-xs sm:text-sm px-4 py-2.5 rounded-full transition">
                        <i class="fa-regular fa-user text-base"></i>
                        <span class="hidden sm:inline">Tài khoản</span>
                    </button>
                </div>
            </div>

            <!-- Mobile Search Bar -->
            <div class="pb-3 block md:hidden">
                <div class="relative">
                    <input type="text" id="search-input-mobile" onkeyup="handleSearchMobile()" placeholder="Tìm sách, tác giả..." class="w-full bg-slate-100 text-sm border border-slate-200 rounded-full py-2 pl-10 pr-4 focus:outline-none focus:ring-2 focus:ring-primary-500">
                    <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-1/2 -translate-y-1/2 text-slate-400 text-sm"></i>
                </div>
            </div>
        </div>
    </header>

    <!-- HERO BANNER SECTION -->
    <section class="relative bg-gradient-to-r from-navy-900 via-slate-900 to-navy-800 text-white overflow-hidden py-12 md:py-16">
        <div class="absolute inset-0 opacity-10 bg-[radial-gradient(#22c55e_1px,transparent_1px)] [background-size:16px_16px]"></div>
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
            <div class="grid grid-cols-1 md:grid-cols-12 gap-8 items-center">
                <div class="md:col-span-7 space-y-5 text-center md:text-left">
                    <span class="inline-flex items-center gap-2 bg-primary-500/20 text-primary-400 text-xs font-bold px-3 py-1.5 rounded-full border border-primary-500/30">
                        <i class="fa-solid fa-fire text-amber-400"></i> Bán Chạy Nhất Tháng 9/2026
                    </span>
                    <h1 class="text-3xl sm:text-4xl lg:text-5xl font-black text-white leading-tight">
                        Đánh Thức Tiềm Năng <br class="hidden sm:inline"/>Cùng <span class="text-transparent bg-clip-text bg-gradient-to-r from-primary-400 to-amber-300">Tri Thức Mới</span>
                    </h1>
                    <p class="text-slate-300 text-sm sm:text-base max-w-xl mx-auto md:mx-0 leading-relaxed">
                        Khám phá hàng ngàn tựa sách từ Văn học, Kinh tế, Công nghệ đến Kỹ năng sống. Giảm giá lên tới <strong class="text-amber-400 font-semibold">40%</strong> cho các thành viên mới hôm nay!
                    </p>
                    <div class="flex flex-wrap justify-center md:justify-start gap-4 pt-2">
                        <a href="#book-list-section" class="bg-primary-600 hover:bg-primary-500 text-white font-bold text-sm px-6 py-3.5 rounded-xl transition shadow-lg shadow-primary-600/30 flex items-center gap-2">
                            <span>Khám Phá Ngay</span>
                            <i class="fa-solid fa-arrow-right text-xs"></i>
                        </a>
                        <a href="#featured-section" class="bg-white/10 hover:bg-white/20 text-white font-semibold text-sm px-6 py-3.5 rounded-xl transition backdrop-blur-md">
                            Sách Nổi Bật
                        </a>
                    </div>
                </div>
                <div class="md:col-span-5 flex justify-center relative">
                    <div class="relative w-64 sm:w-72 md:w-80 h-96 group">
                        <div class="absolute inset-0 bg-primary-500/20 rounded-2xl blur-2xl transform rotate-6 scale-95 group-hover:rotate-12 transition duration-500"></div>
                        <img src="https://images.unsplash.com/photo-1544716278-ca5e3f4abd8c?auto=format&fit=crop&q=80&w=600" alt="Sách nổi bật" class="relative z-10 w-full h-full object-cover rounded-2xl shadow-2xl border-2 border-white/10 transform -rotate-3 group-hover:rotate-0 transition duration-500">
                        <div class="absolute -bottom-4 -left-4 z-20 bg-white text-navy-900 p-3.5 rounded-2xl shadow-xl flex items-center gap-3 border border-slate-100">
                            <div class="w-10 h-10 rounded-xl bg-amber-100 text-amber-600 flex items-center justify-center font-bold text-lg">
                                <i class="fa-solid fa-star"></i>
                            </div>
                            <div>
                                <p class="text-xs font-bold text-slate-800">4.9 / 5.0 Rating</p>
                                <p class="text-[11px] text-slate-500">Từ +2,500 độc giả</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- MAIN CONTENT AREA -->
    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-10 flex-grow w-full">
        
        <!-- Category Pill Navigation -->
        <div class="mb-8">
            <h2 class="text-xs font-bold text-slate-400 uppercase tracking-widest mb-3">Danh mục phổ biến</h2>
            <div class="flex items-center gap-2 overflow-x-auto pb-2 hide-scrollbar" id="category-pills">
                <button onclick="filterCategory('all')" class="cat-pill active bg-primary-600 text-white font-semibold text-xs sm:text-sm px-5 py-2.5 rounded-full transition whitespace-nowrap shadow-sm">
                    Tất Cả Sách
                </button>
                <button onclick="filterCategory('Văn Học')" class="cat-pill bg-white text-slate-700 hover:bg-slate-100 font-semibold text-xs sm:text-sm px-5 py-2.5 rounded-full border border-slate-200 transition whitespace-nowrap">
                    📚 Văn Học
                </button>
                <button onclick="filterCategory('Kinh Tế')" class="cat-pill bg-white text-slate-700 hover:bg-slate-100 font-semibold text-xs sm:text-sm px-5 py-2.5 rounded-full border border-slate-200 transition whitespace-nowrap">
                    📈 Kinh Tế & Quản Lý
                </button>
                <button onclick="filterCategory('Kỹ Năng')" class="cat-pill bg-white text-slate-700 hover:bg-slate-100 font-semibold text-xs sm:text-sm px-5 py-2.5 rounded-full border border-slate-200 transition whitespace-nowrap">
                    💡 Kỹ Năng Sống
                </button>
                <button onclick="filterCategory('CNTT')" class="cat-pill bg-white text-slate-700 hover:bg-slate-100 font-semibold text-xs sm:text-sm px-5 py-2.5 rounded-full border border-slate-200 transition whitespace-nowrap">
                    💻 Công Nghệ Thông Tin
                </button>
                <button onclick="filterCategory('Thiếu Nhi')" class="cat-pill bg-white text-slate-700 hover:bg-slate-100 font-semibold text-xs sm:text-sm px-5 py-2.5 rounded-full border border-slate-200 transition whitespace-nowrap">
                    🎨 Thiếu Nhi
                </button>
            </div>
        </div>

        <!-- Filter & Sorting Control Bar -->
        <div id="book-list-section" class="bg-white p-4 rounded-2xl border border-slate-200 shadow-sm mb-8 flex flex-wrap items-center justify-between gap-4">
            <div class="flex items-center gap-4 flex-wrap">
                <div class="flex items-center gap-2 text-xs font-semibold text-slate-600">
                    <label for="price-range">Mức giá tối đa:</label>
                    <input type="range" id="price-range" min="50000" max="300000" step="10000" value="300000" oninput="handlePriceFilter(this.value)" class="accent-primary-600 cursor-pointer">
                    <span id="price-range-val" class="text-primary-700 font-bold bg-primary-50 px-2 py-1 rounded">300.000đ</span>
                </div>

                <div class="flex items-center gap-2 text-xs font-semibold text-slate-600">
                    <span>Đánh giá:</span>
                    <select id="rating-filter" onchange="applyFilters()" class="bg-slate-100 border border-slate-200 rounded-lg text-xs font-medium px-2.5 py-1.5 focus:outline-none focus:ring-2 focus:ring-primary-500">
                        <option value="0">Tất cả sao</option>
                        <option value="5">5 Sao</option>
                        <option value="4">Từ 4 Sao trở lên</option>
                    </select>
                </div>
            </div>

            <div class="flex items-center gap-2 text-xs font-semibold text-slate-600 ml-auto">
                <i class="fa-solid fa-arrow-down-short-wide text-slate-400"></i>
                <label for="sort-select">Sắp xếp:</label>
                <select id="sort-select" onchange="applyFilters()" class="bg-slate-100 border border-slate-200 rounded-lg text-xs font-medium px-3 py-1.5 focus:outline-none focus:ring-2 focus:ring-primary-500">
                    <option value="popular">Bán chạy nhất</option>
                    <option value="price-low">Giá: Thấp đến Cao</option>
                    <option value="price-high">Giá: Cao đến Thấp</option>
                    <option value="newest">Mới nhất</option>
                </select>
            </div>
        </div>

        <!-- Books Count Indicator -->
        <div class="flex justify-between items-center mb-6">
            <h3 class="text-xl font-bold text-navy-900 flex items-center gap-2">
                <span>Danh Sách Sách</span>
                <span id="results-count" class="text-xs bg-slate-200 text-slate-700 font-semibold px-2.5 py-0.5 rounded-full">12</span>
            </h3>
        </div>

        <!-- Book Grid -->
        <div id="book-grid" class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-4 gap-4 sm:gap-6">
            <!-- Dynamic Books Loaded Here via JS -->
        </div>

        <!-- Empty State Notification -->
        <div id="no-results" class="hidden text-center py-16 bg-white rounded-2xl border border-dashed border-slate-300 my-6">
            <i class="fa-solid fa-book-open-reader text-5xl text-slate-300 mb-3"></i>
            <h4 class="text-lg font-bold text-slate-700">Không tìm thấy cuốn sách nào!</h4>
            <p class="text-xs text-slate-500 mt-1">Hãy thử tìm kiếm từ khóa khác hoặc điều chỉnh bộ lọc.</p>
            <button onclick="resetFilters()" class="mt-4 bg-primary-600 text-white font-semibold text-xs px-4 py-2 rounded-lg hover:bg-primary-700 transition">Đặt lại bộ lọc</button>
        </div>

    </main>

    <!-- SHOPPING CART DRAWER -->
    <div id="cart-drawer-overlay" class="fixed inset-0 bg-navy-900/60 backdrop-blur-sm z-50 transition-opacity opacity-0 pointer-events-none" onclick="toggleCartDrawer()"></div>
    <aside id="cart-drawer" class="fixed top-0 right-0 w-full sm:w-96 h-full bg-white z-50 shadow-2xl transform translate-x-full transition-transform duration-300 flex flex-col">
        <div class="p-4 border-b border-slate-100 flex items-center justify-between bg-slate-50">
            <div class="flex items-center gap-2">
                <i class="fa-solid fa-bag-shopping text-primary-600 text-lg"></i>
                <h3 class="font-bold text-slate-800">Giỏ Hàng Của Bạn</h3>
                <span id="cart-drawer-count" class="text-xs bg-primary-100 text-primary-700 font-bold px-2 py-0.5 rounded-full">0</span>
            </div>
            <button onclick="toggleCartDrawer()" class="p-1.5 text-slate-400 hover:text-slate-600 rounded-lg hover:bg-slate-200/50 transition">
                <i class="fa-solid fa-xmark text-lg"></i>
            </button>
        </div>

        <div id="cart-items-container" class="flex-grow overflow-y-auto p-4 space-y-4 divide-y divide-slate-100">
            <!-- Dynamic Cart Items Loaded Here -->
        </div>

        <div class="p-4 border-t border-slate-200 bg-slate-50/80 space-y-3">
            <div class="flex gap-2">
                <input type="text" id="promo-input" placeholder="Mã giảm giá (BOOKHAVEN)" class="w-full bg-white text-xs border border-slate-200 rounded-lg px-3 py-2 uppercase focus:outline-none focus:ring-1 focus:ring-primary-500">
                <button onclick="applyPromoCode()" class="bg-slate-800 text-white font-semibold text-xs px-3 py-2 rounded-lg hover:bg-slate-900 transition shrink-0">Áp dụng</button>
            </div>
            <div id="promo-message" class="text-[11px] font-semibold hidden"></div>

            <div class="space-y-1.5 text-xs text-slate-600 pt-2">
                <div class="flex justify-between">
                    <span>Tạm tính:</span>
                    <span id="cart-subtotal" class="font-medium">0đ</span>
                </div>
                <div class="flex justify-between">
                    <span>Giảm giá:</span>
                    <span id="cart-discount" class="font-medium text-emerald-600">-0đ</span>
                </div>
                <div class="flex justify-between">
                    <span>Phí vận chuyển:</span>
                    <span id="cart-shipping" class="font-medium">0đ</span>
                </div>
                <div class="flex justify-between text-base font-extrabold text-navy-900 pt-2 border-t border-slate-200">
                    <span>Tổng tiền:</span>
                    <span id="cart-total" class="text-primary-600">0đ</span>
                </div>
            </div>

            <button onclick="openCheckoutModal()" class="w-full bg-primary-600 hover:bg-primary-500 text-white font-bold text-sm py-3.5 rounded-xl transition shadow-lg shadow-primary-600/20 flex items-center justify-center gap-2">
                <i class="fa-solid fa-credit-card"></i>
                <span>Tiến Hành Thanh Toán</span>
            </button>
        </div>
    </aside>

    <!-- QUICK VIEW / BOOK DETAIL MODAL -->
    <div id="quickview-modal" class="fixed inset-0 bg-navy-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 opacity-0 pointer-events-none transition-opacity duration-300">
        <div class="bg-white w-full max-w-3xl rounded-3xl shadow-2xl overflow-hidden relative transform scale-95 transition-transform duration-300 max-h-[90vh] flex flex-col md:flex-row">
            <button onclick="closeQuickView()" class="absolute top-3 right-3 z-10 w-9 h-9 bg-white/80 backdrop-blur hover:bg-slate-100 rounded-full flex items-center justify-center text-slate-600 transition">
                <i class="fa-solid fa-xmark text-lg"></i>
            </button>
            <div class="md:w-1/2 bg-slate-100 p-6 flex items-center justify-center shrink-0">
                <img id="qv-img" src="" alt="" class="max-h-80 object-contain rounded-xl shadow-lg">
            </div>
            <div class="md:w-1/2 p-6 flex flex-col justify-between overflow-y-auto">
                <div class="space-y-3">
                    <span id="qv-category" class="inline-block bg-primary-100 text-primary-700 text-[11px] font-bold px-2.5 py-1 rounded-full uppercase"></span>
                    <h3 id="qv-title" class="text-xl font-bold text-navy-900 leading-snug"></h3>
                    <p class="text-xs text-slate-500">Tác giả: <span id="qv-author" class="font-semibold text-slate-700"></span></p>
                    
                    <div class="flex items-center gap-3">
                        <div id="qv-price" class="text-2xl font-black text-primary-600"></div>
                        <div id="qv-old-price" class="text-sm text-slate-400 line-through"></div>
                    </div>

                    <div id="qv-stars" class="flex items-center gap-1 text-amber-400 text-xs"></div>

                    <hr class="border-slate-100 my-2">

                    <div>
                        <h4 class="text-xs font-bold text-slate-800 uppercase tracking-wider mb-1">Tóm tắt nội dung</h4>
                        <p id="qv-description" class="text-xs text-slate-600 leading-relaxed max-h-32 overflow-y-auto pr-1"></p>
                    </div>
                </div>

                <div class="pt-4 mt-4 border-t border-slate-100 flex items-center gap-3">
                    <button id="qv-add-btn" class="flex-grow bg-primary-600 hover:bg-primary-500 text-white font-bold text-sm py-3 rounded-xl transition shadow-md flex items-center justify-center gap-2">
                        <i class="fa-solid fa-cart-plus"></i>
                        <span>Thêm Vào Giỏ hàng</span>
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- AUTHENTICATION MODAL -->
    <div id="auth-modal" class="fixed inset-0 bg-navy-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 opacity-0 pointer-events-none transition-opacity duration-300">
        <div class="bg-white w-full max-w-md rounded-3xl shadow-2xl p-6 sm:p-8 relative">
            <button onclick="closeAuthModal()" class="absolute top-4 right-4 text-slate-400 hover:text-slate-600">
                <i class="fa-solid fa-xmark text-lg"></i>
            </button>
            <div class="text-center mb-6">
                <div class="w-12 h-12 bg-primary-100 text-primary-600 rounded-2xl flex items-center justify-center mx-auto text-xl font-bold mb-2">
                    <i class="fa-solid fa-user-lock"></i>
                </div>
                <h3 class="text-xl font-bold text-navy-900">Tài Khoản BookHaven</h3>
                <p class="text-xs text-slate-500">Đăng nhập để nhận các ưu đãi hấp dẫn!</p>
            </div>
            
            <form onsubmit="handleAuthSubmit(event)" class="space-y-4">
                <div>
                    <label class="block text-xs font-semibold text-slate-700 mb-1">Email / Số điện thoại</label>
                    <input type="text" required placeholder="vidu@email.com" class="w-full bg-slate-50 border border-slate-200 rounded-xl px-3.5 py-2.5 text-sm focus:outline-none focus:ring-2 focus:ring-primary-500">
                </div>
                <div>
                    <label class="block text-xs font-semibold text-slate-700 mb-1">Mật khẩu</label>
                    <input type="password" required placeholder="••••••••" class="w-full bg-slate-50 border border-slate-200 rounded-xl px-3.5 py-2.5 text-sm focus:outline-none focus:ring-2 focus:ring-primary-500">
                </div>
                <div class="flex items-center justify-between text-xs">
                    <label class="flex items-center gap-2 cursor-pointer">
                        <input type="checkbox" class="accent-primary-600 rounded">
                        <span class="text-slate-600">Ghi nhớ đăng nhập</span>
                    </label>
                    <a href="#" class="text-primary-600 font-semibold hover:underline">Quên mật khẩu?</a>
                </div>
                <button type="submit" class="w-full bg-navy-900 hover:bg-slate-800 text-white font-bold py-3 rounded-xl transition text-sm shadow-md">
                    Đăng Nhập
                </button>
            </form>
            
            <div class="mt-6 text-center text-xs text-slate-500">
                Chưa có tài khoản? <a href="#" onclick="showNotification('Tính năng Đăng Ký đang được phát triển!')" class="text-primary-600 font-bold hover:underline">Đăng ký ngay</a>
            </div>
        </div>
    </div>

    <!-- CHECKOUT MODAL WITH ADVANCED FORM VALIDATION & VIETQR INTEGRATION -->
    <div id="checkout-modal" class="fixed inset-0 bg-navy-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 opacity-0 pointer-events-none transition-opacity duration-300">
        <div class="bg-white w-full max-w-lg rounded-3xl shadow-2xl p-6 sm:p-8 relative max-h-[90vh] overflow-y-auto">
            <button onclick="closeCheckoutModal()" class="absolute top-4 right-4 text-slate-400 hover:text-slate-600">
                <i class="fa-solid fa-xmark text-lg"></i>
            </button>
            <h3 class="text-xl font-bold text-navy-900 mb-4 flex items-center gap-2">
                <i class="fa-solid fa-truck-fast text-primary-600"></i> Thông Tin Giao Hàng & Thanh Toán
            </h3>
            
            <form id="checkout-form" onsubmit="handleCheckoutSubmit(event)" class="space-y-3 text-xs">
                <div>
                    <label class="block font-semibold text-slate-700 mb-1">Họ và tên người nhận *</label>
                    <input type="text" id="cust-name" required placeholder="Nguyễn Văn A" class="w-full bg-slate-50 border border-slate-200 rounded-xl px-3.5 py-2.5 text-sm focus:outline-none focus:ring-2 focus:ring-primary-500">
                </div>
                
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                    <div>
                        <label class="block font-semibold text-slate-700 mb-1">Số điện thoại (10 số VN) *</label>
                        <input type="tel" id="cust-phone" required placeholder="0901234567" pattern="^(0[3|5|7|8|9])[0-9]{8}$" title="Vui lòng nhập đúng số điện thoại di động Việt Nam (10 chữ số)" class="w-full bg-slate-50 border border-slate-200 rounded-xl px-3.5 py-2.5 text-sm focus:outline-none focus:ring-2 focus:ring-primary-500">
                    </div>
                    <div>
                        <label class="block font-semibold text-slate-700 mb-1">Email liên hệ</label>
                        <input type="email" id="cust-email" placeholder="a@gmail.com" class="w-full bg-slate-50 border border-slate-200 rounded-xl px-3.5 py-2.5 text-sm focus:outline-none focus:ring-2 focus:ring-primary-500">
                    </div>
                </div>

                <!-- Detailed Address Fields -->
                <div class="grid grid-cols-1 sm:grid-cols-3 gap-2">
                    <div>
                        <label class="block font-semibold text-slate-700 mb-1">Tỉnh / Thành *</label>
                        <input type="text" id="cust-city" required placeholder="Hà Nội / TP.HCM..." class="w-full bg-slate-50 border border-slate-200 rounded-xl px-3 py-2 text-xs focus:outline-none focus:ring-2 focus:ring-primary-500">
                    </div>
                    <div>
                        <label class="block font-semibold text-slate-700 mb-1">Quận / Huyện *</label>
                        <input type="text" id="cust-district" required placeholder="Quận Cầu Giấy..." class="w-full bg-slate-50 border border-slate-200 rounded-xl px-3 py-2 text-xs focus:outline-none focus:ring-2 focus:ring-primary-500">
                    </div>
                    <div>
                        <label class="block font-semibold text-slate-700 mb-1">Phường / Xã *</label>
                        <input type="text" id="cust-ward" required placeholder="Phường Dịch Vọng..." class="w-full bg-slate-50 border border-slate-200 rounded-xl px-3 py-2 text-xs focus:outline-none focus:ring-2 focus:ring-primary-500">
                    </div>
                </div>

                <div>
                    <label class="block font-semibold text-slate-700 mb-1">Địa chỉ cụ thể (Số nhà, Tên đường) *</label>
                    <input type="text" id="cust-address" required placeholder="Số 123 Đường Nguyễn Phong Sắc" class="w-full bg-slate-50 border border-slate-200 rounded-xl px-3.5 py-2.5 text-sm focus:outline-none focus:ring-2 focus:ring-primary-500">
                </div>

                <div>
                    <label class="block font-semibold text-slate-700 mb-1">Phương thức thanh toán</label>
                    <div class="space-y-2 mt-1">
                        <label class="flex items-center gap-2 p-2.5 border border-slate-200 rounded-xl cursor-pointer hover:bg-slate-50 transition">
                            <input type="radio" name="payment" value="cod" checked class="accent-primary-600">
                            <i class="fa-solid fa-money-bill-wave text-emerald-600 text-sm"></i>
                            <span class="font-medium text-slate-800">Thanh toán khi nhận hàng (COD)</span>
                        </label>
                        <label class="flex items-center gap-2 p-2.5 border border-slate-200 rounded-xl cursor-pointer hover:bg-slate-50 transition">
                            <input type="radio" name="payment" value="vietqr" class="accent-primary-600">
                            <i class="fa-solid fa-qrcode text-blue-600 text-sm"></i>
                            <span class="font-medium text-slate-800">Chuyển khoản qua Mã VietQR (MB Bank)</span>
                        </label>
                    </div>
                </div>

                <div class="pt-3 border-t border-slate-100 flex items-center justify-between font-bold text-sm text-navy-900">
                    <span>Tổng số tiền thanh toán:</span>
                    <span id="checkout-final-total" class="text-primary-600 text-base">0đ</span>
                </div>

                <button type="submit" class="w-full bg-primary-600 hover:bg-primary-500 text-white font-bold text-sm py-3.5 rounded-xl transition shadow-lg shadow-primary-600/20 mt-2 flex items-center justify-center gap-2">
                    <i class="fa-solid fa-paper-plane"></i>
                    <span>Xác Nhận Đặt Hàng</span>
                </button>
            </form>
        </div>
    </div>

    <!-- DYNAMIC VIETQR PAYMENT MODAL -->
    <div id="vietqr-modal" class="fixed inset-0 bg-navy-900/70 backdrop-blur-md z-50 flex items-center justify-center p-4 opacity-0 pointer-events-none transition-opacity duration-300">
        <div class="bg-white w-full max-w-md rounded-3xl shadow-2xl p-6 relative flex flex-col items-center text-center">
            <button onclick="closeVietQRModal()" class="absolute top-4 right-4 text-slate-400 hover:text-slate-600">
                <i class="fa-solid fa-xmark text-lg"></i>
            </button>
            
            <div class="flex items-center gap-2 mb-2">
                <span class="bg-blue-100 text-blue-700 text-[10px] font-extrabold px-2.5 py-1 rounded-full uppercase">MB BANK - VIETQR</span>
            </div>
            
            <h3 class="text-lg font-bold text-navy-900">Quét Mã QR Để Thanh Toán</h3>
            <p class="text-xs text-slate-500 mb-4">Mở ứng dụng Ngân hàng hoặc Ví điện tử để quét mã</p>

            <!-- Dynamic VietQR Image Box -->
            <div class="relative bg-gradient-to-b from-blue-50 to-slate-50 p-4 rounded-2xl border border-blue-100 shadow-inner mb-4 w-full flex justify-center">
                <img id="vietqr-img" src="" alt="Mã VietQR Thanh Toán" class="w-64 h-auto rounded-xl shadow-md border border-white">
            </div>

            <!-- Transfer Details Summary -->
            <div class="w-full bg-slate-50 rounded-xl p-3 text-left text-xs space-y-2 border border-slate-200 mb-4">
                <div class="flex justify-between items-center">
                    <span class="text-slate-500">Chủ tài khoản:</span>
                    <span class="font-bold text-navy-900" id="qr-account-name">NGUYEN LE THANH DAT</span>
                </div>
                <div class="flex justify-between items-center">
                    <span class="text-slate-500">Số tài khoản:</span>
                    <div class="flex items-center gap-1">
                        <span class="font-bold text-blue-600 font-mono text-sm" id="qr-account-no">0814235089</span>
                        <button onclick="copyText('0814235089')" class="text-slate-400 hover:text-blue-600 px-1" title="Sao chép STK"><i class="fa-regular fa-copy"></i></button>
                    </div>
                </div>
                <div class="flex justify-between items-center">
                    <span class="text-slate-500">Số tiền:</span>
                    <span class="font-black text-rose-600 text-sm" id="qr-amount">0đ</span>
                </div>
                <div class="flex justify-between items-center pt-1 border-t border-slate-200">
                    <span class="text-slate-500">Nội dung chuyển khoản:</span>
                    <div class="flex items-center gap-1">
                        <span class="font-bold text-amber-600 font-mono" id="qr-memo">BOOKHAVEN</span>
                        <button onclick="copyText(document.getElementById('qr-memo').innerText)" class="text-slate-400 hover:text-amber-600 px-1" title="Sao chép Nội dung"><i class="fa-regular fa-copy"></i></button>
                    </div>
                </div>
            </div>

            <div class="w-full space-y-2">
                <button onclick="confirmVietQRPayment()" class="w-full bg-emerald-600 hover:bg-emerald-500 text-white font-bold text-sm py-3 rounded-xl transition shadow-lg shadow-emerald-600/20 flex items-center justify-center gap-2">
                    <i class="fa-solid fa-circle-check"></i>
                    <span>Tôi đã chuyển khoản thành công</span>
                </button>
                <button onclick="closeVietQRModal()" class="w-full bg-slate-100 text-slate-600 hover:bg-slate-200 font-semibold text-xs py-2.5 rounded-xl transition">
                    Hủy / Chọn phương thức khác
                </button>
            </div>
        </div>
    </div>

    <!-- NOTIFICATION TOAST -->
    <div id="toast-container" class="fixed bottom-5 right-5 z-50 flex flex-col gap-2 pointer-events-none"></div>

    <!-- FOOTER -->
    <footer class="bg-navy-900 text-slate-300 pt-12 pb-8 border-t border-slate-800 mt-auto">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-5 gap-8 pb-10 border-b border-slate-800">
                <div class="lg:col-span-2 space-y-4">
                    <div class="flex items-center gap-3">
                        <div class="w-9 h-9 bg-primary-600 rounded-lg flex items-center justify-center text-white text-lg font-bold">
                            <i class="fa-solid fa-book-open"></i>
                        </div>
                        <span class="text-xl font-extrabold text-white tracking-tight">Book<span class="text-primary-500">Haven</span></span>
                    </div>
                    <p class="text-xs text-slate-400 leading-relaxed max-w-sm">
                        BookHaven là không gian trực tuyến kết nối độc giả với hàng ngàn tựa sách giá trị. Cam kết mang đến trải nghiệm mua sắm tuyệt vời, giao hàng nhanh chóng và sản phẩm 100% chính hãng.
                    </p>
                </div>

                <div>
                    <h4 class="text-white font-bold text-sm mb-3 uppercase tracking-wider">Danh Mục</h4>
                    <ul class="space-y-2 text-xs text-slate-400">
                        <li><a href="#" class="hover:text-primary-400 transition">Văn Học Trong Nước</a></li>
                        <li><a href="#" class="hover:text-primary-400 transition">Kinh Tế & Doanh Nghiệp</a></li>
                        <li><a href="#" class="hover:text-primary-400 transition">Kỹ Năng Phát Triển Bản Thân</a></li>
                        <li><a href="#" class="hover:text-primary-400 transition">Sách Công Nghệ & Lập Trình</a></li>
                    </ul>
                </div>

                <div>
                    <h4 class="text-white font-bold text-sm mb-3 uppercase tracking-wider">Hỗ Trợ Khách Hàng</h4>
                    <ul class="space-y-2 text-xs text-slate-400">
                        <li><a href="#" class="hover:text-primary-400 transition">Hướng dẫn đặt hàng</a></li>
                        <li><a href="#" class="hover:text-primary-400 transition">Chính sách vận chuyển</a></li>
                        <li><a href="#" class="hover:text-primary-400 transition">Chính sách đổi trả 7 ngày</a></li>
                        <li><a href="#" class="hover:text-primary-400 transition">Bảo mật thông tin</a></li>
                    </ul>
                </div>

                <div>
                    <h4 class="text-white font-bold text-sm mb-3 uppercase tracking-wider">Đăng Ký Nhận Tin</h4>
                    <p class="text-xs text-slate-400 mb-3">Nhận tin tức sách mới và ưu đãi đặc biệt!</p>
                    <form onsubmit="event.preventDefault(); showNotification('Đã đăng ký nhận tin thành công!');" class="space-y-2">
                        <input type="email" required placeholder="Email của bạn..." class="w-full bg-slate-800 border border-slate-700 rounded-lg px-3 py-2 text-xs text-white focus:outline-none focus:ring-1 focus:ring-primary-500">
                        <button type="submit" class="w-full bg-primary-600 hover:bg-primary-500 text-white font-bold text-xs py-2 rounded-lg transition">Đăng Ký Ngay</button>
                    </form>
                </div>
            </div>

            <div class="pt-6 flex flex-col sm:flex-row items-center justify-between text-xs text-slate-500 gap-4">
                <p>&copy; 2026 BookHaven. Tất cả quyền được bảo lưu. Tích hợp thanh toán MB Bank VietQR.</p>
                <div class="flex items-center gap-4 text-slate-400">
                    <i class="fa-brands fa-cc-visa text-xl"></i>
                    <i class="fa-brands fa-cc-mastercard text-xl"></i>
                    <i class="fa-solid fa-qrcode text-xl text-blue-400"></i>
                </div>
            </div>
        </div>
    </footer>

    <!-- JAVASCRIPT LOGIC -->
    <script>
        // Sample Book Data
        const booksData = [
            {
                id: 1,
                title: "Nhà Giả Kim",
                author: "Paulo Coelho",
                category: "Văn Học",
                price: 79000,
                originalPrice: 99000,
                rating: 5,
                sales: 1240,
                isNew: false,
                image: "https://images.unsplash.com/photo-1544947950-fa07a98d237f?auto=format&fit=crop&q=80&w=500",
                description: "Nhà Giả Kim là một trong những cuốn sách bán chạy nhất mọi thời đại. Câu chuyện kể về hành trình đi tìm kho báu của cậu bé chăn cừu Santiago."
            },
            {
                id: 2,
                title: "Đắc Nhân Tâm",
                author: "Dale Carnegie",
                category: "Kỹ Năng",
                price: 85000,
                originalPrice: 110000,
                rating: 5,
                sales: 2300,
                isNew: false,
                image: "https://images.unsplash.com/photo-1589829085413-56de8ae18c73?auto=format&fit=crop&q=80&w=500",
                description: "Đắc Nhân Tâm là cuốn sách nghệ thuật giao tiếp và ứng xử nổi tiếng thế giới giúp bạn thu phục lòng người và thành công trong cuộc sống."
            },
            {
                id: 3,
                title: "Tuần Làm Việc 4 Giờ",
                author: "Timothy Ferriss",
                category: "Kinh Tế",
                price: 135000,
                originalPrice: 165000,
                rating: 4,
                sales: 850,
                isNew: false,
                image: "https://images.unsplash.com/photo-1512820790803-83ca734da794?auto=format&fit=crop&q=80&w=500",
                description: "Tải bản thiết kế lại cuộc đời bạn! Cuốn sách dạy bạn cách thoát khỏi vòng quẩn quẩn 9-to-5, tự động hóa thu nhập và tận hưởng tự do."
            },
            {
                id: 4,
                title: "Clean Code - Mã Sạch",
                author: "Robert C. Martin",
                category: "CNTT",
                price: 245000,
                originalPrice: 290000,
                rating: 5,
                sales: 510,
                isNew: true,
                image: "https://images.unsplash.com/photo-1532012197267-da84d127e765?auto=format&fit=crop&q=80&w=500",
                description: "Cẩm nang không thể thiếu cho lập trình viên chuyên nghiệp. Hướng dẫn cách viết mã nguồn sạch, dễ bảo trì và cấu trúc tối ưu."
            },
            {
                id: 5,
                title: "Dế Mèn Phiêu Lưu Ký",
                author: "Tô Hoài",
                category: "Thiếu Nhi",
                price: 55000,
                originalPrice: 70000,
                rating: 5,
                sales: 1900,
                isNew: false,
                image: "https://images.unsplash.com/photo-1516979187457-637abb4f9353?auto=format&fit=crop&q=80&w=500",
                description: "Tác phẩm văn học thiếu nhi kinh điển của Việt Nam. Cuộc phiêu lưu đầy thú vị và những bài học làm người sâu sắc."
            },
            {
                id: 6,
                title: "Tâm Lý Học Về Tiền",
                author: "Morgan Housel",
                category: "Kinh Tế",
                price: 128000,
                originalPrice: 159000,
                rating: 5,
                sales: 1420,
                isNew: true,
                image: "https://images.unsplash.com/photo-1554415707-6e8cfc93fe23?auto=format&fit=crop&q=80&w=500",
                description: "Quản lý tiền bạc phụ thuộc nhiều vào hành vi của bạn. 19 câu chuyện ngắn khám phá những góc nhìn lạ lẫm về tài chính cá nhân."
            },
            {
                id: 7,
                title: "Thói Quản Nguyên Tử (Atomic Habits)",
                author: "James Clear",
                category: "Kỹ Năng",
                price: 142000,
                originalPrice: 189000,
                rating: 5,
                sales: 3100,
                isNew: false,
                image: "https://images.unsplash.com/photo-1543002588-bfa74002ed7e?auto=format&fit=crop&q=80&w=500",
                description: "Thay đổi nhỏ, kết quả kinh ngạc! Phương pháp từng bước giúp bạn xây dựng thói quen tốt và loại bỏ thói quen xấu."
            },
            {
                id: 8,
                title: "Thiết Kế Web Với HTML & CSS",
                author: "Jon Duckett",
                category: "CNTT",
                price: 280000,
                originalPrice: 320000,
                rating: 4,
                sales: 420,
                isNew: true,
                image: "https://images.unsplash.com/photo-1507842217343-583bb7270b66?auto=format&fit=crop&q=80&w=500",
                description: "Sách nhập môn thiết kế trang web vô cùng trực quan và đẹp mắt. Phù hợp cho người mới bắt đầu học lập trình web."
            }
        ];

        // MB Bank Account Details Config
        const BANK_CONFIG = {
            bankId: 'MB',
            accountNo: '0814235089',
            accountName: 'NGUYEN LE THANH DAT'
        };

        // State Management
        let cart = [];
        let activeCategory = 'all';
        let currentSearchQuery = '';
        let maxPrice = 300000;
        let selectedRating = 0;
        let selectedSort = 'popular';
        let promoDiscount = 0;
        let currentCalculatedTotal = 0;

        window.addEventListener('DOMContentLoaded', () => {
            renderBooks();
            updateCartUI();
        });

        function renderBooks() {
            const gridContainer = document.getElementById('book-grid');
            const noResults = document.getElementById('no-results');
            
            let filtered = booksData.filter(book => {
                const matchCategory = activeCategory === 'all' || book.category === activeCategory;
                const matchSearch = book.title.toLowerCase().includes(currentSearchQuery.toLowerCase()) || 
                                    book.author.toLowerCase().includes(currentSearchQuery.toLowerCase()) ||
                                    book.category.toLowerCase().includes(currentSearchQuery.toLowerCase());
                const matchPrice = book.price <= maxPrice;
                const matchRating = selectedRating == 0 || book.rating >= parseInt(selectedRating);

                return matchCategory && matchSearch && matchPrice && matchRating;
            });

            if (selectedSort === 'price-low') filtered.sort((a, b) => a.price - b.price);
            else if (selectedSort === 'price-high') filtered.sort((a, b) => b.price - a.price);
            else if (selectedSort === 'popular') filtered.sort((a, b) => b.sales - a.sales);
            else if (selectedSort === 'newest') filtered.sort((a, b) => (b.isNew ? 1 : 0) - (a.isNew ? 1 : 0));

            document.getElementById('results-count').innerText = filtered.length;

            if (filtered.length === 0) {
                gridContainer.innerHTML = '';
                noResults.classList.remove('hidden');
                return;
            } else {
                noResults.classList.add('hidden');
            }

            gridContainer.innerHTML = filtered.map(book => {
                const discountPercent = Math.round(((book.originalPrice - book.price) / book.originalPrice) * 100);
                return `
                    <div class="group bg-white rounded-2xl p-3 sm:p-4 border border-slate-200/80 shadow-sm hover:shadow-xl hover:-translate-y-1 transition duration-300 flex flex-col justify-between">
                        <div>
                            <div class="relative overflow-hidden rounded-xl bg-slate-100 aspect-[3/4] mb-3">
                                <img src="${book.image}" alt="${book.title}" class="w-full h-full object-cover group-hover:scale-105 transition duration-500">
                                ${discountPercent > 0 ? `<span class="absolute top-2 left-2 bg-rose-500 text-white text-[10px] font-extrabold px-2 py-0.5 rounded-full shadow-md">-${discountPercent}%</span>` : ''}
                                ${book.isNew ? `<span class="absolute top-2 right-2 bg-emerald-500 text-white text-[10px] font-extrabold px-2 py-0.5 rounded-full shadow-md">MỚI</span>` : ''}

                                <div class="absolute inset-0 bg-navy-900/40 opacity-0 group-hover:opacity-100 transition duration-300 flex items-center justify-center gap-2 p-2">
                                    <button onclick="openQuickView(${book.id})" class="bg-white text-slate-800 p-2.5 rounded-full shadow-lg hover:bg-primary-600 hover:text-white transition transform hover:scale-110" title="Xem nhanh">
                                        <i class="fa-solid fa-eye text-sm"></i>
                                    </button>
                                    <button onclick="addToCart(${book.id})" class="bg-primary-600 text-white p-2.5 rounded-full shadow-lg hover:bg-primary-500 transition transform hover:scale-110" title="Thêm vào giỏ">
                                        <i class="fa-solid fa-cart-plus text-sm"></i>
                                    </button>
                                </div>
                            </div>

                            <span class="text-[10px] font-bold text-slate-400 uppercase tracking-wider block mb-1">${book.category}</span>
                            <h4 class="font-bold text-slate-800 text-sm line-clamp-2 hover:text-primary-600 transition cursor-pointer mb-1" onclick="openQuickView(${book.id})">${book.title}</h4>
                            <p class="text-xs text-slate-500 mb-2 truncate">${book.author}</p>
                        </div>

                        <div>
                            <div class="flex items-center gap-1 text-amber-400 text-[10px] mb-2">
                                ${Array(book.rating).fill('<i class="fa-solid fa-star"></i>').join('')}
                                <span class="text-slate-400 text-[10px] ml-1">(${book.sales})</span>
                            </div>

                            <div class="flex items-center justify-between pt-2 border-t border-slate-100">
                                <div>
                                    <span class="text-sm sm:text-base font-extrabold text-primary-600 block leading-tight">${formatCurrency(book.price)}</span>
                                    <span class="text-[11px] text-slate-400 line-through block">${formatCurrency(book.originalPrice)}</span>
                                </div>
                                <button onclick="addToCart(${book.id})" class="w-8 h-8 sm:w-9 sm:h-9 bg-slate-100 hover:bg-primary-600 text-slate-700 hover:text-white rounded-xl flex items-center justify-center transition shadow-sm">
                                    <i class="fa-solid fa-plus text-xs"></i>
                                </button>
                            </div>
                        </div>
                    </div>
                `;
            }).join('');
        }

        // Filter functions
        function filterCategory(cat) {
            activeCategory = cat;
            document.querySelectorAll('.cat-pill').forEach(btn => {
                btn.classList.remove('bg-primary-600', 'text-white', 'shadow-sm');
                btn.classList.add('bg-white', 'text-slate-700');
            });
            event.target.classList.remove('bg-white', 'text-slate-700');
            event.target.classList.add('bg-primary-600', 'text-white', 'shadow-sm');
            renderBooks();
        }

        function handleSearch() {
            const val = document.getElementById('search-input').value;
            currentSearchQuery = val;
            document.getElementById('clear-search-btn').classList.toggle('hidden', val === '');
            renderBooks();
        }

        function handleSearchMobile() {
            currentSearchQuery = document.getElementById('search-input-mobile').value;
            renderBooks();
        }

        function clearSearch() {
            document.getElementById('search-input').value = '';
            currentSearchQuery = '';
            document.getElementById('clear-search-btn').classList.add('hidden');
            renderBooks();
        }

        function handlePriceFilter(val) {
            maxPrice = parseInt(val);
            document.getElementById('price-range-val').innerText = formatCurrency(maxPrice);
            renderBooks();
        }

        function applyFilters() {
            selectedRating = document.getElementById('rating-filter').value;
            selectedSort = document.getElementById('sort-select').value;
            renderBooks();
        }

        function resetFilters() {
            activeCategory = 'all';
            currentSearchQuery = '';
            maxPrice = 300000;
            selectedRating = 0;
            selectedSort = 'popular';
            document.getElementById('price-range').value = 300000;
            document.getElementById('price-range-val').innerText = '300.000đ';
            document.getElementById('rating-filter').value = '0';
            document.getElementById('sort-select').value = 'popular';
            document.getElementById('search-input').value = '';
            renderBooks();
        }

        // CART OPERATIONS
        function addToCart(bookId) {
            const book = booksData.find(b => b.id === bookId);
            const existingItem = cart.find(item => item.id === bookId);

            if (existingItem) {
                existingItem.quantity += 1;
            } else {
                cart.push({ ...book, quantity: 1 });
            }

            updateCartUI();
            showNotification(`Đã thêm "${book.title}" vào giỏ hàng!`);
        }

        function updateCartQuantity(bookId, delta) {
            const item = cart.find(i => i.id === bookId);
            if (item) {
                item.quantity += delta;
                if (item.quantity <= 0) {
                    cart = cart.filter(i => i.id !== bookId);
                }
            }
            updateCartUI();
        }

        function removeFromCart(bookId) {
            cart = cart.filter(i => i.id !== bookId);
            updateCartUI();
            showNotification('Đã xóa sách khỏi giỏ hàng.');
        }

        function updateCartUI() {
            const totalCount = cart.reduce((sum, item) => sum + item.quantity, 0);
            document.getElementById('cart-badge').innerText = totalCount;
            document.getElementById('cart-drawer-count').innerText = totalCount;

            const cartContainer = document.getElementById('cart-items-container');

            if (cart.length === 0) {
                cartContainer.innerHTML = `
                    <div class="text-center py-12 text-slate-400 space-y-3">
                        <i class="fa-solid fa-cart-flatbed text-4xl text-slate-300"></i>
                        <p class="text-xs font-semibold">Giỏ hàng của bạn đang trống</p>
                    </div>
                `;
            } else {
                cartContainer.innerHTML = cart.map(item => `
                    <div class="flex items-center gap-3 pt-3">
                        <img src="${item.image}" class="w-12 h-16 object-cover rounded-lg shadow-sm shrink-0">
                        <div class="flex-grow min-w-0">
                            <h5 class="text-xs font-bold text-slate-800 truncate">${item.title}</h5>
                            <p class="text-[11px] text-primary-600 font-semibold">${formatCurrency(item.price)}</p>
                            <div class="flex items-center gap-2 mt-1">
                                <div class="flex items-center border border-slate-200 rounded-md bg-slate-50">
                                    <button onclick="updateCartQuantity(${item.id}, -1)" class="px-2 py-0.5 text-xs text-slate-600 hover:bg-slate-200 rounded-l-md">-</button>
                                    <span class="px-2 text-xs font-bold text-slate-800">${item.quantity}</span>
                                    <button onclick="updateCartQuantity(${item.id}, 1)" class="px-2 py-0.5 text-xs text-slate-600 hover:bg-slate-200 rounded-r-md">+</button>
                                </div>
                                <button onclick="removeFromCart(${item.id})" class="text-[11px] text-rose-500 hover:underline">Xóa</button>
                            </div>
                        </div>
                    </div>
                `).join('');
            }

            const subtotal = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
            const discountAmount = subtotal * (promoDiscount / 100);
            const shipping = (subtotal >= 300000 || subtotal === 0) ? 0 : 30000;
            currentCalculatedTotal = Math.max(0, subtotal - discountAmount + shipping);

            document.getElementById('cart-subtotal').innerText = formatCurrency(subtotal);
            document.getElementById('cart-discount').innerText = `-${formatCurrency(discountAmount)}`;
            document.getElementById('cart-shipping').innerText = shipping === 0 ? 'FREE' : formatCurrency(shipping);
            document.getElementById('cart-total').innerText = formatCurrency(currentCalculatedTotal);
            document.getElementById('checkout-final-total').innerText = formatCurrency(currentCalculatedTotal);
        }

        function applyPromoCode() {
            const input = document.getElementById('promo-input').value.trim().toUpperCase();
            const msg = document.getElementById('promo-message');

            if (input === 'BOOKHAVEN') {
                promoDiscount = 10;
                msg.innerText = 'Áp dụng mã giảm giá 10% thành công!';
                msg.className = 'text-[11px] font-semibold text-emerald-600 block';
            } else {
                promoDiscount = 0;
                msg.innerText = 'Mã giảm giá không hợp lệ!';
                msg.className = 'text-[11px] font-semibold text-rose-500 block';
            }
            updateCartUI();
        }

        // CHECKOUT & VIETQR HANDLERS
        function handleCheckoutSubmit(e) {
            e.preventDefault();
            
            const selectedPayment = document.querySelector('input[name="payment"]:checked').value;
            const phoneInput = document.getElementById('cust-phone').value.trim();

            if (!/^(0[3|5|7|8|9])[0-9]{8}$/.test(phoneInput)) {
                showNotification('Số điện thoại không hợp lệ! Vui lòng nhập 10 chữ số chuẩn VN.');
                return;
            }

            if (selectedPayment === 'vietqr') {
                // Generate Order ID & Open VietQR Modal
                const orderId = 'BH' + Math.floor(100000 + Math.random() * 900000);
                const memo = `BOOKHAVEN ${orderId}`;
                
                // VietQR API URL template
                const encodedAccountName = encodeURIComponent(BANK_CONFIG.accountName);
                const encodedMemo = encodeURIComponent(memo);
                const qrUrl = `https://img.vietqr.io/image/${BANK_CONFIG.bankId}-${BANK_CONFIG.accountNo}-compact2.png?amount=${currentCalculatedTotal}&addInfo=${encodedMemo}&accountName=${encodedAccountName}`;

                document.getElementById('vietqr-img').src = qrUrl;
                document.getElementById('qr-amount').innerText = formatCurrency(currentCalculatedTotal);
                document.getElementById('qr-memo').innerText = memo;

                closeCheckoutModal();
                openVietQRModal();
            } else {
                // COD Flow
                closeCheckoutModal();
                cart = [];
                updateCartUI();
                showNotification('🎉 Đặt hàng thành công! Đơn hàng COD của bạn đã được ghi nhận.');
            }
        }

        function confirmVietQRPayment() {
            closeVietQRModal();
            cart = [];
            updateCartUI();
            showNotification('🎉 Cảm ơn bạn! Đơn hàng đã được xác nhận sau khi chuyển khoản.');
        }

        // MODAL TOGGLES
        function toggleCartDrawer() {
            const drawer = document.getElementById('cart-drawer');
            const overlay = document.getElementById('cart-drawer-overlay');
            const isOpen = !drawer.classList.contains('translate-x-full');

            if (isOpen) {
                drawer.classList.add('translate-x-full');
                overlay.classList.add('opacity-0', 'pointer-events-none');
            } else {
                drawer.classList.remove('translate-x-full');
                overlay.classList.remove('opacity-0', 'pointer-events-none');
            }
        }

        function openQuickView(bookId) {
            const book = booksData.find(b => b.id === bookId);
            if (!book) return;

            document.getElementById('qv-img').src = book.image;
            document.getElementById('qv-category').innerText = book.category;
            document.getElementById('qv-title').innerText = book.title;
            document.getElementById('qv-author').innerText = book.author;
            document.getElementById('qv-price').innerText = formatCurrency(book.price);
            document.getElementById('qv-old-price').innerText = formatCurrency(book.originalPrice);
            document.getElementById('qv-description').innerText = book.description;
            
            document.getElementById('qv-stars').innerHTML = Array(book.rating).fill('<i class="fa-solid fa-star"></i>').join('') + `<span class="text-slate-500 text-xs ml-1">(${book.sales} đánh giá)</span>`;

            document.getElementById('qv-add-btn').onclick = () => {
                addToCart(book.id);
                closeQuickView();
            };

            const modal = document.getElementById('quickview-modal');
            modal.classList.remove('opacity-0', 'pointer-events-none');
            modal.children[0].classList.remove('scale-95');
        }

        function closeQuickView() {
            const modal = document.getElementById('quickview-modal');
            modal.classList.add('opacity-0', 'pointer-events-none');
            modal.children[0].classList.add('scale-95');
        }

        function openAuthModal() {
            document.getElementById('auth-modal').classList.remove('opacity-0', 'pointer-events-none');
        }

        function closeAuthModal() {
            document.getElementById('auth-modal').classList.add('opacity-0', 'pointer-events-none');
        }

        function openCheckoutModal() {
            if (cart.length === 0) {
                showNotification('Giỏ hàng của bạn đang trống!');
                return;
            }
            toggleCartDrawer();
            document.getElementById('checkout-modal').classList.remove('opacity-0', 'pointer-events-none');
        }

        function closeCheckoutModal() {
            document.getElementById('checkout-modal').classList.add('opacity-0', 'pointer-events-none');
        }

        function openVietQRModal() {
            document.getElementById('vietqr-modal').classList.remove('opacity-0', 'pointer-events-none');
        }

        function closeVietQRModal() {
            document.getElementById('vietqr-modal').classList.add('opacity-0', 'pointer-events-none');
        }

        function handleAuthSubmit(e) {
            e.preventDefault();
            closeAuthModal();
            showNotification('Đăng nhập thành công! Chào mừng trở lại.');
        }

        // UTILS
        function formatCurrency(amount) {
            return new Intl.NumberFormat('vi-VN', { style: 'currency', currency: 'VND' }).format(amount);
        }

        function copyText(text) {
            const tempInput = document.createElement('input');
            tempInput.value = text;
            document.body.appendChild(tempInput);
            tempInput.select();
            document.execCommand('copy');
            document.body.removeChild(tempInput);
            showNotification(`Đã sao chép: ${text}`);
        }

        function showNotification(message) {
            const container = document.getElementById('toast-container');
            const toast = document.createElement('div');
            toast.className = 'bg-navy-900 text-white text-xs font-semibold px-4 py-3 rounded-xl shadow-xl flex items-center gap-2 transition duration-300 transform translate-y-2 pointer-events-auto';
            toast.innerHTML = `<i class="fa-solid fa-circle-check text-primary-500"></i> <span>${message}</span>`;
            
            container.appendChild(toast);

            setTimeout(() => {
                toast.classList.add('opacity-0', 'translate-y-2');
                setTimeout(() => toast.remove(), 300);
            }, 3000);
        }
    </script>
</body>
</html>
