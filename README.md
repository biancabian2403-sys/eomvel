# eomvel
membaca novel
  <!DOCTYPE html>
<html lang="id" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NusaVerse - Platform Novel & Studio Penulis</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#f0fdf4',
                            100: '#dcfce7',
                            500: '#22c55e',
                            600: '#16a34a',
                            700: '#15803d',
                            900: '#14532d',
                        },
                        amber: {
                            50: '#fffbe1',
                            100: '#fef3c7',
                            800: '#92400e',
                            900: '#78350f',
                        }
                    },
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        serif: ['Merriweather', 'serif'],
                        lora: ['Lora', 'serif'],
                    }
                }
            }
        }
    </script>
    <!-- Font Awesome CDN -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Lora:ital,wght@0,400;0,600;1,400&family=Merriweather:ital,wght@0,300;0,400;0,700;1,300&display=swap" rel="stylesheet">
    <style>
        .sepia-mode {
            background-color: #fbf0d9 !important;
            color: #5f4b32 !important;
        }
        .sepia-mode .bg-card {
            background-color: #f3e5ab !important;
            color: #5f4b32 !important;
        }
        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: transparent;
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 9999px;
        }
        .dark ::-webkit-scrollbar-thumb {
            background: #334155;
        }
    </style>
</head>
<body class="bg-slate-50 dark:bg-slate-900 text-slate-800 dark:text-slate-100 transition-colors duration-200 min-h-screen flex flex-col font-sans">

    <!-- NAVBAR UTAMA -->
    <header class="sticky top-0 z-40 w-full border-b border-slate-200 dark:border-slate-800 bg-white/90 dark:bg-slate-900/90 backdrop-blur">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-16">
                
                <!-- Logo (Dengan Pemicu Rahasia Klik 5x) -->
                <div class="flex items-center gap-3">
                    <div id="logoTrigger" onclick="handleLogoClick()" class="cursor-pointer select-none flex items-center gap-2 group">
                        <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-brand-600 to-teal-400 flex items-center justify-center text-white font-bold text-xl shadow-md group-hover:scale-105 transition-transform">
                            NV
                        </div>
                        <div class="flex flex-col">
                            <span class="font-bold text-xl tracking-tight bg-gradient-to-r from-brand-600 to-teal-500 bg-clip-text text-transparent">NusaVerse</span>
                            <span id="badgeAuthorView" class="hidden text-[10px] font-semibold tracking-widest text-brand-600 dark:text-brand-400 uppercase">Studio Penulis</span>
                        </div>
                    </div>
                </div>

                <!-- Navigasi Pembaca -->
                <nav class="hidden md:flex items-center space-x-6 text-sm font-medium">
                    <button onclick="switchTab('home')" class="hover:text-brand-600 dark:hover:text-brand-400 transition">Beranda</button>
                    <button onclick="switchTab('catalog')" class="hover:text-brand-600 dark:hover:text-brand-400 transition">Katalog Novel</button>
                    <button onclick="switchTab('bookmark')" class="hover:text-brand-600 dark:hover:text-brand-400 transition">Favorit Saya</button>
                </nav>

                <!-- Alat & Aksi -->
                <div class="flex items-center space-x-3">
                    <!-- Toggle Theme Mode -->
                    <button onclick="toggleDarkMode()" class="p-2.5 text-slate-500 hover:text-slate-700 dark:text-slate-400 dark:hover:text-slate-200 rounded-lg hover:bg-slate-100 dark:hover:bg-slate-800 transition">
                        <i id="themeIcon" class="fa-solid fa-moon text-lg"></i>
                    </button>

                    <!-- Tombol Kembali ke Reader (Hanya Muncul saat Mode Penulis Aktif) -->
                    <button id="btnSwitchToReader" onclick="switchToReaderView()" class="hidden px-3.5 py-1.5 text-xs font-semibold text-slate-700 dark:text-slate-200 bg-slate-100 dark:bg-slate-800 hover:bg-slate-200 dark:hover:bg-slate-700 rounded-lg transition items-center gap-1.5">
                        <i class="fa-solid fa-book-open"></i> Look Reader View
                    </button>

                    <!-- Navigasi HP Hamburger -->
                    <button onclick="toggleMobileNav()" class="md:hidden p-2 text-slate-600 dark:text-slate-300">
                        <i class="fa-solid fa-bars text-xl"></i>
                    </button>
                </div>
            </div>
        </div>

        <!-- Mobile Menu Navigasi -->
        <div id="mobileMenu" class="hidden md:hidden border-b border-slate-200 dark:border-slate-800 bg-white dark:bg-slate-900 px-4 py-3 space-y-2 text-sm font-medium">
            <button onclick="switchTab('home'); toggleMobileNav()" class="block w-full text-left py-2 hover:text-brand-600">Beranda</button>
            <button onclick="switchTab('catalog'); toggleMobileNav()" class="block w-full text-left py-2 hover:text-brand-600">Katalog Novel</button>
            <button onclick="switchTab('bookmark'); toggleMobileNav()" class="block w-full text-left py-2 hover:text-brand-600">Favorit Saya</button>
        </div>
    </header>

    <!-- KONTEN UTAMA - BERANDA & PEMBACA (DEFAULT VIEW) -->
    <main id="publicReaderSection" class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8">
        
        <!-- HERO BANNER -->
        <section id="tabHome" class="space-y-8">
            <div class="relative overflow-hidden rounded-3xl bg-gradient-to-r from-slate-900 via-brand-900 to-slate-900 text-white p-8 sm:p-12 shadow-xl">
                <div class="relative z-10 max-w-2xl space-y-4">
                    <span class="inline-block px-3 py-1 bg-brand-500/20 text-brand-300 border border-brand-500/30 text-xs font-semibold tracking-wider rounded-full uppercase">Koleksi Novel Pilihan</span>
                    <h1 class="text-3xl sm:text-5xl font-extrabold tracking-tight leading-tight">Jelajahi Dunia Tanpa Batas Melalui Cerita</h1>
                    <p class="text-slate-300 text-sm sm:text-base">Nikmati ribuan bab novel menarik secara gratis. Pengalaman membaca terbaik dengan berbagai mode kenyamanan mata.</p>
                    <div class="pt-2 flex flex-wrap gap-3">
                        <button onclick="switchTab('catalog')" class="px-6 py-3 bg-brand-600 hover:bg-brand-500 text-white font-semibold rounded-xl shadow-lg shadow-brand-600/30 transition">Mulai Membaca</button>
                    </div>
                </div>
                <div class="absolute -right-10 -bottom-10 opacity-10 pointer-events-none">
                    <i class="fa-solid fa-book-open text-[280px]"></i>
                </div>
            </div>

            <!-- Novel Pilihan Pembaca -->
            <div class="space-y-4">
                <div class="flex items-center justify-between">
                    <h2 class="text-xl font-bold tracking-tight">Sedang Hangat Dibaca 🔥</h2>
                    <button onclick="switchTab('catalog')" class="text-sm text-brand-600 dark:text-brand-400 font-semibold hover:underline">Lihat Semua</button>
                </div>
                <div id="featuredNovelGrid" class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 gap-4 sm:gap-6">
                    <!-- Dynamic Novel Cards injected by JS -->
                </div>
            </div>
        </section>

        <!-- KATALOG & PENCARIAN -->
        <section id="tabCatalog" class="hidden space-y-6">
            <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 bg-white dark:bg-slate-800 p-4 rounded-2xl shadow-sm border border-slate-200/60 dark:border-slate-700">
                <!-- Search Input -->
                <div class="relative flex-grow max-w-md">
                    <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-1/2 -translate-y-1/2 text-slate-400"></i>
                    <input type="text" id="searchInput" oninput="filterNovels()" placeholder="Cari judul novel, genre, atau kata kunci..." class="w-full pl-10 pr-4 py-2 bg-slate-100 dark:bg-slate-700/50 rounded-xl text-sm border-none focus:ring-2 focus:ring-brand-500 outline-none">
                </div>
                <!-- Genre Filter -->
                <div class="flex items-center gap-2 overflow-x-auto pb-2 md:pb-0">
                    <button onclick="setGenreFilter('All')" class="genre-btn px-3.5 py-1.5 text-xs font-semibold rounded-lg bg-brand-600 text-white whitespace-nowrap">Semua</button>
                    <button onclick="setGenreFilter('Fantasy')" class="genre-btn px-3.5 py-1.5 text-xs font-semibold rounded-lg bg-slate-100 dark:bg-slate-700 text-slate-600 dark:text-slate-300 hover:bg-slate-200 whitespace-nowrap">Fantasy</button>
                    <button onclick="setGenreFilter('Romance')" class="genre-btn px-3.5 py-1.5 text-xs font-semibold rounded-lg bg-slate-100 dark:bg-slate-700 text-slate-600 dark:text-slate-300 hover:bg-slate-200 whitespace-nowrap">Romance</button>
                    <button onclick="setGenreFilter('Sci-Fi')" class="genre-btn px-3.5 py-1.5 text-xs font-semibold rounded-lg bg-slate-100 dark:bg-slate-700 text-slate-600 dark:text-slate-300 hover:bg-slate-200 whitespace-nowrap">Sci-Fi</button>
                    <button onclick="setGenreFilter('Action')" class="genre-btn px-3.5 py-1.5 text-xs font-semibold rounded-lg bg-slate-100 dark:bg-slate-700 text-slate-600 dark:text-slate-300 hover:bg-slate-200 whitespace-nowrap">Action</button>
                </div>
            </div>

            <!-- List Grid Novel Catalog -->
            <div id="catalogNovelGrid" class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 gap-4 sm:gap-6">
                <!-- Dynamic injected -->
            </div>
        </section>

        <!-- BOOKMARK / FAVORIT -->
        <section id="tabBookmark" class="hidden space-y-6">
            <h2 class="text-2xl font-bold">Novel Favorit Saya 🔖</h2>
            <div id="bookmarkGrid" class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 gap-4 sm:gap-6">
                <!-- Dynamic injected -->
            </div>
        </section>

        <!-- DETAIL NOVEL VIEW -->
        <section id="novelDetailSection" class="hidden space-y-8">
            <button onclick="backToPrevTab()" class="inline-flex items-center gap-2 text-sm font-semibold text-slate-500 hover:text-brand-600 transition">
                <i class="fa-solid fa-arrow-left"></i> Kembali
            </button>

            <div id="novelDetailContent">
                <!-- Injected via JS -->
            </div>
        </section>

        <!-- READER CANVAS MODE (MODE MEMBACA NOVEL) -->
        <section id="readerCanvasSection" class="hidden max-w-3xl mx-auto space-y-6 py-4">
            <!-- Reader Bar Controls -->
            <div class="sticky top-20 z-30 flex items-center justify-between bg-white/95 dark:bg-slate-800/95 backdrop-blur p-3 rounded-2xl shadow-lg border border-slate-200/80 dark:border-slate-700 text-xs sm:text-sm">
                <button onclick="exitReaderMode()" class="px-3 py-1.5 text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-700 rounded-lg">
                    <i class="fa-solid fa-arrow-left"></i> Tutup
                </button>

                <div class="flex items-center space-x-2 sm:space-x-4">
                    <!-- Font Family Switch -->
                    <select id="readerFontFamily" onchange="changeReaderFont(this.value)" class="bg-slate-100 dark:bg-slate-700 text-xs rounded-lg px-2 py-1 outline-none border-none">
                        <option value="font-sans">Sans-Serif</option>
                        <option value="font-serif">Serif</option>
                        <option value="font-lora" selected>Lora</option>
                    </select>

                    <!-- Text Size Controls -->
                    <div class="flex items-center border border-slate-200 dark:border-slate-700 rounded-lg overflow-hidden">
                        <button onclick="adjustReaderFontSize(-1)" class="px-2.5 py-1 bg-slate-50 dark:bg-slate-700 hover:bg-slate-200 text-xs">-A</button>
                        <span id="fontSizeLabel" class="px-2 font-mono text-xs">18px</span>
                        <button onclick="adjustReaderFontSize(1)" class="px-2.5 py-1 bg-slate-50 dark:bg-slate-700 hover:bg-slate-200 text-xs">+A</button>
                    </div>

                    <!-- Sepia Theme Toggle -->
                    <button onclick="toggleSepiaMode()" class="px-2.5 py-1 rounded-lg bg-amber-100 text-amber-900 font-semibold text-xs border border-amber-300">
                        Sepia
                    </button>
                </div>
            </div>

            <!-- Container Isi Naskah Cerita -->
            <div id="readerPaper" class="bg-white dark:bg-slate-800 p-6 sm:p-12 rounded-3xl shadow-sm border border-slate-200/60 dark:border-slate-700/60 transition-all duration-200">
                <div id="readerHeader" class="border-b border-slate-200 dark:border-slate-700 pb-6 mb-8 text-center space-y-2">
                    <span id="readerNovelTitle" class="text-xs font-bold text-brand-600 dark:text-brand-400 uppercase tracking-widest">Judul Novel</span>
                    <h1 id="readerChapterTitle" class="text-2xl sm:text-3xl font-extrabold tracking-tight">Bab 1: Awal Mulai</h1>
                    <p id="readerMeta" class="text-xs text-slate-400">Dipublikasikan pada 2026</p>
                </div>

                <div id="readerBodyText" class="font-lora text-lg leading-relaxed space-y-6 text-slate-800 dark:text-slate-200">
                    <!-- Text Story Content Injected Here -->
                </div>

                <!-- Navigasi Bab Atas/Bawah -->
                <div class="flex items-center justify-between pt-10 border-t border-slate-200 dark:border-slate-700 mt-12">
                    <button id="btnPrevChapter" onclick="navigateChapter(-1)" class="px-4 py-2 bg-slate-100 dark:bg-slate-700 hover:bg-slate-200 rounded-xl font-medium text-xs sm:text-sm transition flex items-center gap-2">
                        <i class="fa-solid fa-chevron-left"></i> Bab Sebelumnya
                    </button>
                    <button id="btnNextChapter" onclick="navigateChapter(1)" class="px-5 py-2 bg-brand-600 hover:bg-brand-500 text-white rounded-xl font-medium text-xs sm:text-sm transition flex items-center gap-2">
                        Bab Selanjutnya <i class="fa-solid fa-chevron-right"></i>
                    </button>
                </div>
            </div>

            <!-- Komentar Pembaca -->
            <div class="bg-white dark:bg-slate-800 p-6 rounded-3xl border border-slate-200/60 dark:border-slate-700 space-y-4">
                <h3 class="font-bold text-lg"><i class="fa-regular fa-comments"></i> Komentar Pembaca</h3>
                <div class="flex gap-2">
                    <input type="text" id="commentInput" placeholder="Tulis tanggapan kamu..." class="flex-grow px-4 py-2 bg-slate-100 dark:bg-slate-700/50 rounded-xl text-sm outline-none border-none focus:ring-2 focus:ring-brand-500">
                    <button onclick="postComment()" class="px-4 py-2 bg-brand-600 text-white text-sm font-semibold rounded-xl hover:bg-brand-500">Kirim</button>
                </div>
                <div id="commentsList" class="space-y-3 pt-2">
                    <!-- Dynamic Comments -->
                </div>
            </div>
        </section>

    </main>


    <!-- SECTION KANVAS KHUSUS PENULIS (HIDDEN SECARA DEFAULT - HANYA BISA DIAKSES PEMILIK/PEMBUAT) -->
    <main id="authorStudioSection" class="hidden flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8">
        
        <!-- Header Studio Penulis -->
        <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 mb-8 pb-6 border-b border-slate-200 dark:border-slate-800">
            <div>
                <div class="flex items-center gap-2">
                    <span class="px-2.5 py-0.5 bg-brand-100 dark:bg-brand-900/40 text-brand-700 dark:text-brand-300 text-xs font-bold rounded-full">Sesi Aktif Permanen</span>
                    <h1 class="text-2xl font-bold">Studio Dashboard Penulis</h1>
                </div>
                <p class="text-sm text-slate-500 dark:text-slate-400">Kelola naskah, buat bab baru, dan pantau statistik karya novel kamu.</p>
            </div>
            
            <div class="flex items-center gap-3">
                <button onclick="openCreateNovelModal()" class="px-4 py-2 bg-brand-600 hover:bg-brand-500 text-white text-sm font-semibold rounded-xl shadow-md transition flex items-center gap-2">
                    <i class="fa-solid fa-plus"></i> Buat Novel Baru
                </button>
            </div>
        </div>

        <!-- Metric Cards -->
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4 mb-8">
            <div class="p-5 bg-white dark:bg-slate-800 rounded-2xl border border-slate-200/60 dark:border-slate-700 shadow-sm">
                <div class="flex items-center justify-between text-slate-400 mb-2">
                    <span class="text-xs font-semibold uppercase">Total Judul Karya</span>
                    <i class="fa-solid fa-book text-brand-500"></i>
                </div>
                <div id="statTotalNovels" class="text-2xl font-bold">1</div>
            </div>
            <div class="p-5 bg-white dark:bg-slate-800 rounded-2xl border border-slate-200/60 dark:border-slate-700 shadow-sm">
                <div class="flex items-center justify-between text-slate-400 mb-2">
                    <span class="text-xs font-semibold uppercase">Total Bab Terbit</span>
                    <i class="fa-solid fa-file-pen text-teal-500"></i>
                </div>
                <div id="statTotalChapters" class="text-2xl font-bold">2</div>
            </div>
            <div class="p-5 bg-white dark:bg-slate-800 rounded-2xl border border-slate-200/60 dark:border-slate-700 shadow-sm">
                <div class="flex items-center justify-between text-slate-400 mb-2">
                    <span class="text-xs font-semibold uppercase">Est. Jumlah Kata</span>
                    <i class="fa-solid fa-font text-indigo-500"></i>
                </div>
                <div id="statTotalWords" class="text-2xl font-bold">1,420</div>
            </div>
            <div class="p-5 bg-white dark:bg-slate-800 rounded-2xl border border-slate-200/60 dark:border-slate-700 shadow-sm">
                <div class="flex items-center justify-between text-slate-400 mb-2">
                    <span class="text-xs font-semibold uppercase">Total Dibaca</span>
                    <i class="fa-solid fa-eye text-amber-500"></i>
                </div>
                <div id="statTotalViews" class="text-2xl font-bold">12.4K</div>
            </div>
        </div>

        <!-- Tabs Studio Penulis -->
        <div class="flex border-b border-slate-200 dark:border-slate-700 mb-6 space-x-6 text-sm font-semibold">
            <button onclick="switchAuthorTab('my-novels')" id="tabBtnMyNovels" class="pb-3 border-b-2 border-brand-600 text-brand-600">Daftar Karya Novel</button>
            <button onclick="switchAuthorTab('editor')" id="tabBtnEditor" class="pb-3 border-b-2 border-transparent text-slate-500 hover:text-slate-800 dark:hover:text-slate-200">Editor Naskah Bab</button>
        </div>

        <!-- TAB AUTHOR: DAFTAR KARYA NOVEL -->
        <div id="authorTabMyNovels" class="space-y-6">
            <div id="authorNovelList" class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <!-- Dynamic Injected Author Novel Cards -->
            </div>
        </div>

        <!-- TAB AUTHOR: EDITOR NASKAH BAB -->
        <div id="authorTabEditor" class="hidden space-y-6 max-w-4xl mx-auto">
            <div class="bg-white dark:bg-slate-800 p-6 sm:p-8 rounded-3xl border border-slate-200/60 dark:border-slate-700 shadow-sm space-y-6">
                
                <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4 border-b border-slate-200 dark:border-slate-700 pb-4">
                    <h2 class="text-lg font-bold">Penulisan Bab Cerita</h2>
                    <div class="flex items-center gap-2">
                        <select id="editorSelectNovel" class="bg-slate-100 dark:bg-slate-700 text-xs font-medium rounded-xl px-3 py-2 border-none outline-none">
                            <!-- Injected -->
                        </select>
                        <button onclick="saveChapterDraft()" class="px-4 py-2 bg-brand-600 hover:bg-brand-500 text-white text-xs font-semibold rounded-xl shadow transition">
                            <i class="fa-solid fa-paper-plane mr-1"></i> Terbitkan Bab
                        </button>
                    </div>
                </div>

                <!-- Form Editor Input -->
                <div class="space-y-4">
                    <div>
                        <label class="block text-xs font-semibold text-slate-500 uppercase mb-1">Judul Bab</label>
                        <input type="text" id="editorChapterTitle" placeholder="misal: Bab 3 - Jejak Pertanda Pertama" class="w-full px-4 py-2.5 bg-slate-100 dark:bg-slate-700/50 rounded-xl text-sm outline-none border-none focus:ring-2 focus:ring-brand-500">
                    </div>

                    <!-- Toolbar Formatting Sederhana -->
                    <div class="flex items-center space-x-1 p-2 bg-slate-100 dark:bg-slate-700/40 rounded-xl text-slate-600 dark:text-slate-300 text-sm">
                        <button onclick="formatEditorText('bold')" class="p-2 hover:bg-white dark:hover:bg-slate-600 rounded"><i class="fa-solid fa-bold"></i></button>
                        <button onclick="formatEditorText('italic')" class="p-2 hover:bg-white dark:hover:bg-slate-600 rounded"><i class="fa-solid fa-italic"></i></button>
                        <button onclick="formatEditorText('underline')" class="p-2 hover:bg-white dark:hover:bg-slate-600 rounded"><i class="fa-solid fa-underline"></i></button>
                    </div>

                    <!-- Text Area Naskah -->
                    <div>
                        <textarea id="editorChapterBody" oninput="updateWordCount()" rows="16" placeholder="Mulai ketik naskah cerita kamu di sini..." class="w-full p-4 bg-slate-50 dark:bg-slate-900/60 rounded-2xl text-base leading-relaxed border border-slate-200 dark:border-slate-700 focus:outline-none focus:ring-2 focus:ring-brand-500 font-lora"></textarea>
                    </div>

                    <!-- Counter Info -->
                    <div class="flex items-center justify-between text-xs text-slate-400">
                        <span id="editorWordCounter">0 Kata | 0 Karakter</span>
                        <span class="text-brand-600 font-medium"><i class="fa-solid fa-circle-check"></i> Auto-saved ke LocalStorage</span>
                    </div>
                </div>
            </div>
        </div>

    </main>


    <!-- MODAL PENULIS: BIKIN NOVEL BARU -->
    <div id="modalCreateNovel" class="hidden fixed inset-0 z-50 flex items-center justify-center bg-slate-900/60 backdrop-blur-sm p-4">
        <div class="bg-white dark:bg-slate-800 w-full max-w-lg rounded-3xl p-6 sm:p-8 shadow-2xl space-y-6">
            <div class="flex items-center justify-between border-b border-slate-200 dark:border-slate-700 pb-4">
                <h3 class="text-lg font-bold">Tambah Karya Novel Baru</h3>
                <button onclick="closeCreateNovelModal()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark text-xl"></i></button>
            </div>

            <form onsubmit="handleCreateNovel(event)" class="space-y-4">
                <div>
                    <label class="block text-xs font-semibold text-slate-500 uppercase mb-1">Judul Novel</label>
                    <input type="text" id="newNovelTitle" required placeholder="Judul Novel Utama" class="w-full px-4 py-2.5 bg-slate-100 dark:bg-slate-700/50 rounded-xl text-sm border-none outline-none focus:ring-2 focus:ring-brand-500">
                </div>
                <div class="grid grid-cols-2 gap-4">
                    <div>
                        <label class="block text-xs font-semibold text-slate-500 uppercase mb-1">Genre Utama</label>
                        <select id="newNovelGenre" class="w-full px-4 py-2.5 bg-slate-100 dark:bg-slate-700/50 rounded-xl text-sm border-none outline-none">
                            <option value="Fantasy">Fantasy</option>
                            <option value="Romance">Romance</option>
                            <option value="Sci-Fi">Sci-Fi</option>
                            <option value="Action">Action</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-xs font-semibold text-slate-500 uppercase mb-1">URL Cover Gambar</label>
                        <input type="text" id="newNovelCover" placeholder="https://..." class="w-full px-4 py-2.5 bg-slate-100 dark:bg-slate-700/50 rounded-xl text-sm border-none outline-none focus:ring-2 focus:ring-brand-500">
                    </div>
                </div>
                <div>
                    <label class="block text-xs font-semibold text-slate-500 uppercase mb-1">Sinopsis Singkat</label>
                    <textarea id="newNovelSynopsis" rows="3" required placeholder="Tuliskan ringkasan cerita..." class="w-full p-3 bg-slate-100 dark:bg-slate-700/50 rounded-xl text-sm border-none outline-none focus:ring-2 focus:ring-brand-500"></textarea>
                </div>

                <div class="pt-2 flex justify-end space-x-3">
                    <button type="button" onclick="closeCreateNovelModal()" class="px-4 py-2 text-sm font-semibold text-slate-600 dark:text-slate-300">Batal</button>
                    <button type="submit" class="px-5 py-2 bg-brand-600 hover:bg-brand-500 text-white text-sm font-semibold rounded-xl">Simpan & Buat</button>
                </div>
            </form>
        </div>
    </div>


    <!-- MODAL PENULIS: VERIFIKASI SANDI RAHASIA PENULIS -->
    <div id="modalAuthorAuth" class="hidden fixed inset-0 z-50 flex items-center justify-center bg-slate-900/70 backdrop-blur-md p-4">
        <div class="bg-white dark:bg-slate-800 w-full max-w-sm rounded-3xl p-6 sm:p-8 shadow-2xl space-y-6 text-center">
            <div class="w-16 h-16 mx-auto bg-brand-100 dark:bg-brand-900/40 text-brand-600 dark:text-brand-400 rounded-full flex items-center justify-center text-2xl shadow-inner">
                <i class="fa-solid fa-lock"></i>
            </div>
            
            <div class="space-y-1">
                <h3 class="text-xl font-bold">Akses Khusus Pemilik</h3>
                <p class="text-xs text-slate-500 dark:text-slate-400">Masukkan kata sandi khusus kamu untuk membuka dashboard penulis.</p>
            </div>

            <form onsubmit="verifyAuthorPassword(event)" class="space-y-4">
                <div>
                    <input type="password" id="authorPassInput" autocomplete="off" placeholder="Kata Sandi..." class="w-full px-4 py-3 text-center bg-slate-100 dark:bg-slate-700/60 rounded-xl text-base font-mono tracking-widest border-none outline-none focus:ring-2 focus:ring-brand-500">
                    <p id="authErrorMsg" class="hidden text-xs text-red-500 mt-2 font-medium">Sandi tidak cocok!</p>
                </div>

                <div class="flex items-center gap-2">
                    <button type="button" onclick="closeAuthModal()" class="w-1/2 py-2.5 text-sm font-semibold text-slate-500 bg-slate-100 dark:bg-slate-700 rounded-xl">Batal</button>
                    <button type="submit" class="w-1/2 py-2.5 bg-brand-600 hover:bg-brand-500 text-white text-sm font-semibold rounded-xl transition">Buka</button>
                </div>
            </form>
        </div>
    </div>


    <!-- FOOTER Sederhana -->
    <footer class="mt-auto border-t border-slate-200 dark:border-slate-800 bg-white dark:bg-slate-900 py-6">
        <div class="max-w-7xl mx-auto px-4 text-center text-xs text-slate-400 space-y-1">
            <p>&copy; 2026 NusaVerse Platform Novel. Hak Cipta Dilindungi.</p>
            <p class="text-[11px] opacity-75">Sistem Multi-Role Sempurna untuk Penulis & Pembaca Umum.</p>
        </div>
    </footer>


    <!-- LOGIKA JAVASCRIPT LENGKAP UTUH -->
    <script>
        /* =================================================================
           DATABASE INTERNAL (LOCALSTORAGE SYNCHRONIZED)
        ================================================================== */
        const DEFAULT_NOVELS = [
            {
                id: 'novel-1',
                title: 'Legenda Sang Pengembara Angin',
                author: 'NusaVerse Studio',
                genre: 'Fantasy',
                cover: 'https://images.unsplash.com/photo-1518709268805-4e9042af9f23?w=500&auto=format&fit=crop&q=80',
                synopsis: 'Di benak benua Aetheria, seorang pemuda menemukan pecahan pedang kuno yang menyimpan jiwa naga angin terakhir.',
                views: '12.4K',
                rating: '4.9',
                bookmarks: false,
                chapters: [
                    {
                        title: 'Bab 1: Pedang di Reruntuhan Kuno',
                        date: '09 Sep 2026',
                        content: `Angin malam berhembus kencang melintasi pepohonan Lembah Hitam. Arka mempererat jubah lusuhnya, menggenggam erat obor bambu yang apinya hampir padam diguncang udara dingin.

"Di sekitar sini..." gumam Arka sembari menatap peta kulit lembu yang sudah usang.

Langkah kakinya terhenti tepat di depan sebuah pintu batu raksasa yang setengah tertimbun tanah. Simbol-simbol runik purba berpendar samar dalam kegelapan, seolah menyambut kedatangannya yang telah ditakdirkan ratusan tahun.

Dengan dorongan perlahan, pintu raksasa itu terbuka memicu suara gemuruh batu bertabrakan. Di tengah ruangan, melayang sebuah bilah pedang berkilau kebiruan.`
                    },
                    {
                        title: 'Bab 2: Panggilan Jiwa Naga',
                        date: '10 Sep 2026',
                        content: `Saat jemari Arka menyentuh gagang pedang dingin tersebut, sebuah sengatan energi mendadak menjalar ke seluruh tubuhnya.

"Siapa yang berani mengusik tidur panjangku?" sebuah suara berat menggema langsung di dalam pikirannya.

Itu bukanlah suara manusia. Itu adalah peninggalan kehendak dari Vaelor, Naga Angin Terakhir yang pernah menguasai langit Aetheria sebelum Perang Takhta Paripurna.`
                    }
                ]
            }
        ];

        // Status Aplikasi & Akses Penulis
        let dbNovels = JSON.parse(localStorage.getItem('nv_novels')) || DEFAULT_NOVELS;
        let isAuthorAuthenticated = localStorage.getItem('nv_is_author') === 'true'; // Permanen di perangkat
        let logoClickCount = 0;
        let logoClickTimer = null;
        let currentActiveTab = 'home';
        let currentActiveNovelId = null;
        let currentChapterIndex = 0;
        let currentFontSize = 18;
        let currentGenreFilter = 'All';

        /* =================================================================
           INITIALIZATION & ROUTING AUTO-CHECK
        ================================================================== */
        window.addEventListener('DOMContentLoaded', () => {
            saveToLocalStorage();
            
            // Check Parameter URL rahasia ?mode=author
            const urlParams = new URLSearchParams(window.location.search);
            if (urlParams.get('mode') === 'author') {
                if (isAuthorAuthenticated) {
                    switchToAuthorStudioView();
                } else {
                    openAuthModal();
                }
            } else {
                // Default Selalu Tampilan Pembaca
                if (isAuthorAuthenticated) {
                    // Jika penulis membuka di perangkatnya, tunjukkan indikator
                    document.getElementById('badgeAuthorView').classList.remove('hidden');
                    document.getElementById('btnSwitchToReader').classList.remove('hidden');
                }
                renderReaderHome();
            }
        });

        function saveToLocalStorage() {
            localStorage.setItem('nv_novels', JSON.stringify(dbNovels));
        }

        /* =================================================================
           LOGIKA PEMICU RAHASIA AKSES PENULIS
        ================================================================== */
        function handleLogoClick() {
            logoClickCount++;
            clearTimeout(logoClickTimer);

            logoClickTimer = setTimeout(() => {
                logoClickCount = 0;
            }, 2000);

            // Ketuk 5x berturut-turut untuk membuka modal login/studio
            if (logoClickCount >= 5) {
                logoClickCount = 0;
                if (isAuthorAuthenticated) {
                    switchToAuthorStudioView();
                } else {
                    openAuthModal();
                }
            }
        }

        function openAuthModal() {
            document.getElementById('modalAuthorAuth').classList.remove('hidden');
            document.getElementById('authorPassInput').value = '';
            document.getElementById('authErrorMsg').classList.add('hidden');
        }

        function closeAuthModal() {
            document.getElementById('modalAuthorAuth').classList.add('hidden');
        }

        function verifyAuthorPassword(e) {
            e.preventDefault();
            const pass = document.getElementById('authorPassInput').value;
            
            // Kata sandi eksklusif milik kamu
            if (pass === 'yangjungwon09') {
                isAuthorAuthenticated = true;
                localStorage.setItem('nv_is_author', 'true'); // Tersimpan selamanya di HP kamu
                closeAuthModal();
                document.getElementById('badgeAuthorView').classList.remove('hidden');
                document.getElementById('btnSwitchToReader').classList.remove('hidden');
                switchToAuthorStudioView();
            } else {
                document.getElementById('authErrorMsg').classList.remove('hidden');
            }
        }

        /* =================================================================
           SWITCH VIEW (PEMBACA VS PENULIS)
        ================================================================== */
        function switchToAuthorStudioView() {
            document.getElementById('publicReaderSection').classList.add('hidden');
            document.getElementById('authorStudioSection').classList.remove('hidden');
            renderAuthorDashboard();
        }

        function switchToReaderView() {
            document.getElementById('authorStudioSection').classList.add('hidden');
            document.getElementById('publicReaderSection').classList.remove('hidden');
            switchTab('home');
        }

        /* =================================================================
           PEMBACA (PUBLIC READER VIEW) LOGIC
        ================================================================== */
        function switchTab(tabName) {
            currentActiveTab = tabName;
            document.getElementById('tabHome').classList.add('hidden');
            document.getElementById('tabCatalog').classList.add('hidden');
            document.getElementById('tabBookmark').classList.add('hidden');
            document.getElementById('novelDetailSection').classList.add('hidden');
            document.getElementById('readerCanvasSection').classList.add('hidden');

            if (tabName === 'home') {
                document.getElementById('tabHome').classList.remove('hidden');
                renderReaderHome();
            } else if (tabName === 'catalog') {
                document.getElementById('tabCatalog').classList.remove('hidden');
                renderCatalog();
            } else if (tabName === 'bookmark') {
                document.getElementById('tabBookmark').classList.remove('hidden');
                renderBookmarks();
            }
        }

        function renderReaderHome() {
            const grid = document.getElementById('featuredNovelGrid');
            grid.innerHTML = dbNovels.map(novel => createNovelCardHTML(novel)).join('');
        }

        function renderCatalog() {
            filterNovels();
        }

        function filterNovels() {
            const query = document.getElementById('searchInput').value.toLowerCase();
            const filtered = dbNovels.filter(n => {
                const matchQuery = n.title.toLowerCase().includes(query) || n.synopsis.toLowerCase().includes(query);
                const matchGenre = currentGenreFilter === 'All' || n.genre === currentGenreFilter;
                return matchQuery && matchGenre;
            });

            document.getElementById('catalogNovelGrid').innerHTML = filtered.map(novel => createNovelCardHTML(novel)).join('');
        }

        function setGenreFilter(genre) {
            currentGenreFilter = genre;
            filterNovels();
        }

        function renderBookmarks() {
            const bookmarked = dbNovels.filter(n => n.bookmarks);
            const grid = document.getElementById('bookmarkGrid');
            if(bookmarked.length === 0) {
                grid.innerHTML = `<p class="col-span-full text-slate-400 text-sm italic">Belum ada novel yang ditambahkan ke favorit.</p>`;
            } else {
                grid.innerHTML = bookmarked.map(novel => createNovelCardHTML(novel)).join('');
            }
        }

        function createNovelCardHTML(novel) {
            return `
                <div onclick="openNovelDetail('${novel.id}')" class="group bg-white dark:bg-slate-800 rounded-2xl overflow-hidden border border-slate-200/60 dark:border-slate-700 shadow-sm hover:shadow-md transition cursor-pointer flex flex-col">
                    <div class="relative aspect-[3/4] overflow-hidden bg-slate-200">
                        <img src="${novel.cover}" alt="${novel.title}" class="w-full h-full object-cover group-hover:scale-105 transition duration-300">
                        <span class="absolute top-2 right-2 px-2 py-0.5 bg-slate-900/80 backdrop-blur text-white text-[10px] font-bold rounded-md">${novel.genre}</span>
                    </div>
                    <div class="p-3.5 flex flex-col flex-grow justify-between space-y-2">
                        <div>
                            <h3 class="font-bold text-sm line-clamp-2 leading-snug group-hover:text-brand-600 transition">${novel.title}</h3>
                            <p class="text-[11px] text-slate-400 mt-1">${novel.chapters.length} Bab • ⭐ ${novel.rating}</p>
                        </div>
                    </div>
                </div>
            `;
        }

        function openNovelDetail(novelId) {
            currentActiveNovelId = novelId;
            const novel = dbNovels.find(n => n.id === novelId);
            if (!novel) return;

            document.getElementById('tabHome').classList.add('hidden');
            document.getElementById('tabCatalog').classList.add('hidden');
            document.getElementById('tabBookmark').classList.add('hidden');
            document.getElementById('novelDetailSection').classList.remove('hidden');

            const container = document.getElementById('novelDetailContent');
            container.innerHTML = `
                <div class="flex flex-col md:flex-row gap-8 bg-white dark:bg-slate-800 p-6 sm:p-8 rounded-3xl border border-slate-200/60 dark:border-slate-700">
                    <div class="w-48 sm:w-56 flex-shrink-0 mx-auto md:mx-0">
                        <img src="${novel.cover}" class="w-full aspect-[3/4] object-cover rounded-2xl shadow-lg">
                    </div>
                    <div class="flex-grow space-y-4">
                        <div class="flex items-center gap-2">
                            <span class="px-3 py-1 bg-brand-100 dark:bg-brand-900/40 text-brand-600 dark:text-brand-300 text-xs font-bold rounded-lg">${novel.genre}</span>
                            <span class="text-xs text-slate-400">⭐ ${novel.rating} (${novel.views} Pembaca)</span>
                        </div>
                        <h1 class="text-2xl sm:text-3xl font-extrabold tracking-tight">${novel.title}</h1>
                        <p class="text-xs text-slate-400">Penulis: <span class="font-semibold text-slate-600 dark:text-slate-200">${novel.author}</span></p>
                        <p class="text-sm text-slate-600 dark:text-slate-300 leading-relaxed">${novel.synopsis}</p>

                        <div class="pt-2 flex items-center space-x-3">
                            <button onclick="readChapter(0)" class="px-5 py-2.5 bg-brand-600 hover:bg-brand-500 text-white font-semibold text-sm rounded-xl shadow-lg shadow-brand-600/30">Mulai Baca Bab 1</button>
                            <button onclick="toggleBookmark('${novel.id}')" class="px-4 py-2.5 bg-slate-100 dark:bg-slate-700 hover:bg-slate-200 text-sm font-semibold rounded-xl">
                                ${novel.bookmarks ? '❤️ Favorit' : '🤍 Tambah Favorit'}
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Daftar Bab -->
                <div class="space-y-4 pt-4">
                    <h3 class="font-bold text-lg">Daftar Bab (${novel.chapters.length})</h3>
                    <div class="space-y-2">
                        ${novel.chapters.map((ch, idx) => `
                            <div onclick="readChapter(${idx})" class="p-4 bg-white dark:bg-slate-800 rounded-2xl border border-slate-200/60 dark:border-slate-700 flex items-center justify-between hover:border-brand-500 cursor-pointer transition">
                                <span class="font-semibold text-sm">${ch.title}</span>
                                <span class="text-xs text-slate-400">${ch.date || 'Terbaru'}</span>
                            </div>
                        `).join('')}
                    </div>
                </div>
            `;
        }

        function toggleBookmark(novelId) {
            const novel = dbNovels.find(n => n.id === novelId);
            if (novel) {
                novel.bookmarks = !novel.bookmarks;
                saveToLocalStorage();
                openNovelDetail(novelId);
            }
        }

        function backToPrevTab() {
            switchTab(currentActiveTab);
        }

        /* =================================================================
           READER CANVAS LOGIC
        ================================================================== */
        function readChapter(index) {
            currentChapterIndex = index;
            const novel = dbNovels.find(n => n.id === currentActiveNovelId);
            if (!novel || !novel.chapters[index]) return;

            const chapter = novel.chapters[index];

            document.getElementById('novelDetailSection').classList.add('hidden');
            document.getElementById('readerCanvasSection').classList.remove('hidden');

            document.getElementById('readerNovelTitle').innerText = novel.title;
            document.getElementById('readerChapterTitle').innerText = chapter.title;
            document.getElementById('readerMeta').innerText = `Dipublikasikan pada ${chapter.date || '2026'}`;
            
            // Format Paragraf
            const formattedText = chapter.content.split('\n\n').map(p => `<p class="indent-6">${p}</p>`).join('');
            document.getElementById('readerBodyText').innerHTML = formattedText;

            // Navigasi
            document.getElementById('btnPrevChapter').style.visibility = index > 0 ? 'visible' : 'hidden';
            document.getElementById('btnNextChapter').style.visibility = index < novel.chapters.length - 1 ? 'visible' : 'hidden';

            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function navigateChapter(direction) {
            readChapter(currentChapterIndex + direction);
        }

        function exitReaderMode() {
            document.getElementById('readerCanvasSection').classList.add('hidden');
            document.getElementById('novelDetailSection').classList.remove('hidden');
        }

        function changeReaderFont(fontClass) {
            const body = document.getElementById('readerBodyText');
            body.classList.remove('font-sans', 'font-serif', 'font-lora');
            body.classList.add(fontClass);
        }

        function adjustReaderFontSize(delta) {
            currentFontSize = Math.min(Math.max(14, currentFontSize + delta), 28);
            document.getElementById('readerBodyText').style.fontSize = `${currentFontSize}px`;
            document.getElementById('fontSizeLabel').innerText = `${currentFontSize}px`;
        }

        function toggleSepiaMode() {
            document.getElementById('readerPaper').classList.toggle('sepia-mode');
        }

        function postComment() {
            const input = document.getElementById('commentInput');
            if(!input.value.trim()) return;

            const list = document.getElementById('commentsList');
            const commentHTML = `
                <div class="p-3 bg-slate-50 dark:bg-slate-700/50 rounded-xl text-xs space-y-1">
                    <span class="font-bold text-brand-600">Pembaca Pembuka</span>
                    <p class="text-slate-700 dark:text-slate-300">${input.value}</p>
                </div>
            `;
            list.insertAdjacentHTML('afterbegin', commentHTML);
            input.value = '';
        }

        /* =================================================================
           STUDIO PENULIS (AUTHOR DASHBOARD & EDITOR) LOGIC
        ================================================================== */
        function renderAuthorDashboard() {
            document.getElementById('statTotalNovels').innerText = dbNovels.length;
            
            let totalCh = 0;
            let totalWords = 0;
            dbNovels.forEach(n => {
                totalCh += n.chapters.length;
                n.chapters.forEach(c => {
                    totalWords += c.content.split(/\s+/).filter(Boolean).length;
                });
            });

            document.getElementById('statTotalChapters').innerText = totalCh;
            document.getElementById('statTotalWords').innerText = totalWords.toLocaleString();

            renderAuthorNovelList();
            populateEditorNovelSelect();
        }

        function switchAuthorTab(tab) {
            if(tab === 'my-novels') {
                document.getElementById('authorTabMyNovels').classList.remove('hidden');
                document.getElementById('authorTabEditor').classList.add('hidden');
                document.getElementById('tabBtnMyNovels').className = 'pb-3 border-b-2 border-brand-600 text-brand-600';
                document.getElementById('tabBtnEditor').className = 'pb-3 border-b-2 border-transparent text-slate-500';
            } else {
                document.getElementById('authorTabMyNovels').classList.add('hidden');
                document.getElementById('authorTabEditor').classList.remove('hidden');
                document.getElementById('tabBtnEditor').className = 'pb-3 border-b-2 border-brand-600 text-brand-600';
                document.getElementById('tabBtnMyNovels').className = 'pb-3 border-b-2 border-transparent text-slate-500';
            }
        }

        function renderAuthorNovelList() {
            const container = document.getElementById('authorNovelList');
            container.innerHTML = dbNovels.map(novel => `
                <div class="p-5 bg-white dark:bg-slate-800 rounded-3xl border border-slate-200/60 dark:border-slate-700 flex gap-4">
                    <img src="${novel.cover}" class="w-20 h-28 object-cover rounded-xl shadow">
                    <div class="flex-grow flex flex-col justify-between">
                        <div>
                            <span class="text-[10px] font-bold text-brand-600 uppercase tracking-widest">${novel.genre}</span>
                            <h3 class="font-bold text-base line-clamp-1">${novel.title}</h3>
                            <p class="text-xs text-slate-400 mt-1">${novel.chapters.length} Bab Terbit</p>
                        </div>
                        <div class="flex items-center gap-2 pt-2">
                            <button onclick="openWriteEditorForNovel('${novel.id}')" class="px-3 py-1.5 bg-brand-600 hover:bg-brand-500 text-white text-xs font-semibold rounded-lg">Tulis Bab Baru</button>
                        </div>
                    </div>
                </div>
            `).join('');
        }

        function populateEditorNovelSelect() {
            const select = document.getElementById('editorSelectNovel');
            select.innerHTML = dbNovels.map(n => `<option value="${n.id}">${n.title}</option>`).join('');
        }

        function openWriteEditorForNovel(novelId) {
            switchAuthorTab('editor');
            document.getElementById('editorSelectNovel').value = novelId;
        }

        function updateWordCount() {
            const text = document.getElementById('editorChapterBody').value;
            const words = text.trim() ? text.trim().split(/\s+/).length : 0;
            const chars = text.length;
            document.getElementById('editorWordCounter').innerText = `${words} Kata | ${chars} Karakter`;
        }

        function saveChapterDraft() {
            const novelId = document.getElementById('editorSelectNovel').value;
            const title = document.getElementById('editorChapterTitle').value;
            const body = document.getElementById('editorChapterBody').value;

            if(!title.trim() || !body.trim()) {
                alert('Judul Bab dan Naskah tidak boleh kosong!');
                return;
            }

            const novel = dbNovels.find(n => n.id === novelId);
            if(novel) {
                const today = new Date().toLocaleDateString('id-ID', { day: '2-digit', month: 'short', year: 'numeric' });
                novel.chapters.push({
                    title: title,
                    date: today,
                    content: body
                });

                saveToLocalStorage();
                alert(`Bab Baru "${title}" Berhasil Diterbitkan dan Otomatis Sinkron ke Tampilan Pembaca!`);

                document.getElementById('editorChapterTitle').value = '';
                document.getElementById('editorChapterBody').value = '';
                updateWordCount();
                renderAuthorDashboard();
            }
        }

        function openCreateNovelModal() {
            document.getElementById('modalCreateNovel').classList.remove('hidden');
        }

        function closeCreateNovelModal() {
            document.getElementById('modalCreateNovel').classList.add('hidden');
        }

        function handleCreateNovel(e) {
            e.preventDefault();
            const title = document.getElementById('newNovelTitle').value;
            const genre = document.getElementById('newNovelGenre').value;
            const cover = document.getElementById('newNovelCover').value || 'https://images.unsplash.com/photo-1543002588-bfa74002ed7e?w=500&auto=format&fit=crop&q=80';
            const synopsis = document.getElementById('newNovelSynopsis').value;

            const newNovel = {
                id: 'novel-' + Date.now(),
                title: title,
                author: 'NusaVerse Studio',
                genre: genre,
                cover: cover,
                synopsis: synopsis,
                views: '0',
                rating: '5.0',
                bookmarks: false,
                chapters: []
            };

            dbNovels.push(newNovel);
            saveToLocalStorage();
            closeCreateNovelModal();
            renderAuthorDashboard();
            alert('Karya Novel Baru Berhasil Dibuat!');
        }

        /* =================================================================
           THEME & GENERAL UTILS
        ================================================================== */
        function toggleDarkMode() {
            document.documentElement.classList.toggle('dark');
            const icon = document.getElementById('themeIcon');
            if(document.documentElement.classList.contains('dark')) {
                icon.className = 'fa-solid fa-sun text-lg';
            } else {
                icon.className = 'fa-solid fa-moon text-lg';
            }
        }

        function toggleMobileNav() {
            document.getElementById('mobileMenu').classList.toggle('hidden');
        }

        function formatEditorText(type) {
            const textarea = document.getElementById('editorChapterBody');
            textarea.focus();
        }
    </script>
</body>
</html>
