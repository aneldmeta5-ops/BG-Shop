# BG-Shop
Blockman GO Shop.
```html
<!DOCTYPE html>
<html lang="en" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Blockman Go & Discord Marketplace</title>

    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        cyber: {
                            bg: '#08090d',
                            card: '#11131c',
                            border: '#1e2333',
                            purple: '#a855f7',
                            cyan: '#06b6d4',
                            pink: '#ec4899',
                            gold: '#f59e0b',
                            green: '#10b981'
                        }
                    },
                    fontFamily: {
                        sans: ['Inter', 'sans-serif']
                    }
                }
            }
        }
    </script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #08090d;
            color: #f3f4f6;
            overflow-x: hidden;
        }
        .glass-panel {
            background: rgba(17, 19, 28, 0.85);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.08);
        }
        .glow-purple {
            box-shadow: 0 0 20px rgba(168, 85, 247, 0.25);
        }
        .glow-cyan {
            box-shadow: 0 0 20px rgba(6, 182, 212, 0.25);
        }
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: #08090d; }
        ::-webkit-scrollbar-thumb { background: #1e2333; border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: #a855f7; }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between selection:bg-cyber-purple selection:text-white">

    <nav class="sticky top-0 z-40 glass-panel border-b border-cyber-border">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-20">
                <div class="flex items-center space-x-3 cursor-pointer" onclick="setCategory('All')">
                    <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-cyber-purple to-cyber-cyan flex items-center justify-center text-black font-black text-2xl shadow-lg shadow-cyber-purple/30">
                        B
                    </div>
                    <span class="text-xl sm:text-2xl font-black tracking-wider bg-gradient-to-r from-white via-gray-200 to-cyber-cyan bg-clip-text text-transparent">
                        BMG<span class="text-cyber-purple">&</span>DISCORD<span class="text-xs ml-1 text-cyber-cyan uppercase font-mono">STORE</span>
                    </span>
                </div>

                <!-- Desktop Navigation Tabs -->
                <div class="hidden lg:flex items-center space-x-1 bg-cyber-card border border-cyber-border p-1.5 rounded-2xl text-xs font-bold">
                    <button onclick="setCategory('Discord')" class="px-3.5 py-2 rounded-xl text-gray-300 hover:text-white hover:bg-white/5 transition flex items-center gap-1.5">
                        <i class="fa-brands fa-discord text-cyber-purple"></i> Discord
                    </button>
                    <button onclick="setCategory('Accounts')" class="px-3.5 py-2 rounded-xl text-gray-300 hover:text-white hover:bg-white/5 transition flex items-center gap-1.5">
                        <i class="fa-solid fa-user-shield text-cyber-cyan"></i> Accounts
                    </button>
                    <button onclick="setCategory('Clans')" class="px-3.5 py-2 rounded-xl text-gray-300 hover:text-white hover:bg-white/5 transition flex items-center gap-1.5">
                        <i class="fa-solid fa-shield-halved text-cyber-gold"></i> Clans
                    </button>
                    <button onclick="setCategory('Items')" class="px-3.5 py-2 rounded-xl text-gray-300 hover:text-white hover:bg-white/5 transition flex items-center gap-1.5">
                        <i class="fa-solid fa-gem text-cyber-pink"></i> Items
                    </button>
                    <button onclick="setCategory('YouTube')" class="px-3.5 py-2 rounded-xl text-gray-300 hover:text-white hover:bg-white/5 transition flex items-center gap-1.5">
                        <i class="fa-brands fa-youtube text-red-500"></i> YouTube
                    </button>
                </div>

                <!-- Right Header Actions -->
                <div class="flex items-center space-x-3">
                    <button onclick="openVercelGuide()" class="bg-gradient-to-r from-cyber-purple/20 to-cyber-cyan/20 border border-cyber-cyan/40 hover:border-cyber-cyan text-cyber-cyan hover:text-white px-3.5 py-2 rounded-xl text-xs font-bold transition flex items-center gap-2">
                        <i class="fa-solid fa-cloud-arrow-up text-cyber-cyan"></i>
                        <span class="hidden sm:inline">Host Free on Vercel</span>
                    </button>
                    <button onclick="toggleCart()" class="relative p-2.5 bg-cyber-card hover:bg-cyber-border border border-cyber-border rounded-xl transition text-gray-200">
                        <i class="fa-solid fa-bag-shopping text-lg"></i>
                        <span id="cart-count" class="absolute -top-1.5 -right-1.5 bg-cyber-purple text-white text-[10px] font-black w-5 h-5 rounded-full flex items-center justify-center shadow-lg shadow-cyber-purple/50">0</span>
                    </button>
                </div>
            </div>
        </div>
    </nav>

    <section class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 mt-6">
        <div class="relative rounded-3xl overflow-hidden glass-panel border border-cyber-border p-6 sm:p-10 bg-gradient-to-r from-cyber-card via-cyber-bg to-cyber-card">
            <div class="max-w-3xl">
                <span class="inline-flex items-center gap-2 px-3 py-1 bg-cyber-purple/20 border border-cyber-purple/40 text-cyber-purple font-bold text-xs rounded-full mb-3">
                    <span class="w-2 h-2 rounded-full bg-cyber-purple animate-pulse"></span>
                    VERIFIED ASSETS STORE
                </span>
                <h1 class="text-3xl sm:text-5xl font-black text-white leading-tight mb-3">
                    Blockman Go & Discord <span class="bg-gradient-to-r from-cyber-cyan via-cyber-purple to-cyber-pink bg-clip-text text-transparent">Marketplace</span>
                </h1>
                <p class="text-xs sm:text-sm text-gray-400 mb-6 max-w-xl">
                    Buy OG Blockman Go accounts, Level 4/6 clans, Discord community servers & ranking bots, or rare in-game items with coins!
                </p>
                <div class="flex flex-wrap gap-3">
                    <button onclick="setCategory('Accounts')" class="px-5 py-2.5 bg-gradient-to-r from-cyber-purple to-cyber-cyan text-black font-extrabold rounded-xl hover:opacity-90 transition text-xs sm:text-sm shadow-lg shadow-cyber-purple/20">
                        Browse OG Accounts
                    </button>
                    <button onclick="setCategory('Items')" class="px-5 py-2.5 glass-panel hover:bg-white/10 text-white font-bold rounded-xl transition text-xs sm:text-sm border border-white/20">
                        In-Game Items (Coins)
                    </button>
                </div>
            </div>
        </div>
    </section>

    <main id="store" class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8 flex-grow">
        <!-- Filter Tabs & Search Bar -->
        <div class="flex flex-col lg:flex-row items-center justify-between gap-4 mb-8">
            <div class="flex items-center gap-2 overflow-x-auto w-full lg:w-auto pb-2 lg:pb-0 scrollbar-none" id="category-filters">
                <!-- Filters injected dynamically -->
            </div>
            <div class="relative w-full lg:w-80">
                <i class="fa-solid fa-magnifying-glass absolute left-4 top-1/2 -translate-y-1/2 text-gray-500 text-xs"></i>
                <input type="text" id="search-input" oninput="filterProducts()" placeholder="Search accounts, clans, bots..." class="w-full bg-cyber-card border border-cyber-border rounded-xl py-2.5 pl-10 pr-4 text-xs text-gray-200 placeholder-gray-500 focus:outline-none focus:border-cyber-cyan transition">
            </div>
        </div>

        <!-- Section Title Header -->
        <div class="flex items-center justify-between mb-6">
            <h2 class="text-xl sm:text-2xl font-extrabold tracking-tight text-white flex items-center gap-2.5" id="section-title-heading">
                <span class="w-2.5 h-6 bg-cyber-purple rounded-full inline-block"></span>
                <span>All Offers</span>
            </h2>
            <span id="product-count" class="text-xs text-gray-400 font-medium bg-cyber-card px-3 py-1 rounded-lg border border-cyber-border">Showing 0 offers</span>
        </div>

        <!-- Product Cards Grid -->
        <div id="product-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
            <!-- Product cards injected dynamically via JavaScript -->
        </div>

        <!-- Empty State Search Result -->
        <div id="no-results" class="hidden text-center py-16">
            <i class="fa-solid fa-ghost text-5xl text-gray-600 mb-4"></i>
            <h3 class="text-xl font-bold text-gray-400">No offers found</h3>
            <p class="text-sm text-gray-600 mt-1">Try changing your category tab or search phrase.</p>
        </div>
    </main>

    <div id="cart-overlay" onclick="toggleCart()" class="fixed inset-0 bg-black/80 backdrop-blur-sm z-50 opacity-0 pointer-events-none transition-opacity duration-300"></div>
    <div id="cart-drawer" class="fixed top-0 right-0 w-full max-w-md h-full glass-panel z-50 border-l border-cyber-border transform translate-x-full transition-transform duration-300 flex flex-col justify-between">
        <div class="p-6 border-b border-cyber-border flex items-center justify-between">
            <div class="flex items-center space-x-2.5">
                <i class="fa-solid fa-bag-shopping text-cyber-cyan text-xl"></i>
                <h3 class="text-lg font-bold text-white">Your Shopping Cart</h3>
            </div>
            <button onclick="toggleCart()" class="p-2 text-gray-400 hover:text-white">
                <i class="fa-solid fa-xmark text-xl"></i>
            </button>
        </div>

        <div id="cart-items" class="p-6 overflow-y-auto flex-grow space-y-4">
            <!-- Items injected by JavaScript -->
        </div>

        <div class="p-6 border-t border-cyber-border bg-cyber-card/90 space-y-4">
            <div class="space-y-2 text-xs font-semibold">
                <div class="flex justify-between text-gray-400">
                    <span>Total USD ($)</span>
                    <span id="cart-usd-total" class="text-cyber-cyan font-bold text-sm">$0.00</span>
                </div>
                <div class="flex justify-between text-gray-400">
                    <span>Total In-Game Coins</span>
                    <span id="cart-coins-total" class="text-cyber-gold font-bold text-sm">0 Coins</span>
                </div>
            </div>
            <button onclick="checkout()" class="w-full py-3.5 bg-gradient-to-r from-cyber-purple to-cyber-cyan hover:opacity-90 text-black font-extrabold rounded-xl shadow-lg shadow-cyber-purple/20 transition text-xs uppercase tracking-wider">
                Submit Order Request
            </button>
        </div>
    </div>

    <div id="image-modal" class="fixed inset-0 bg-black/90 backdrop-blur-md z-50 hidden flex items-center justify-center p-4" onclick="closeImageModal()">
        <div class="max-w-3xl w-full p-2 relative" onclick="event.stopPropagation()">
            <button onclick="closeImageModal()" class="absolute -top-10 right-0 text-white text-2xl hover:text-cyber-pink">
                <i class="fa-solid fa-xmark"></i>
            </button>
            <img id="modal-img-target" src="" class="w-full h-auto max-h-[80vh] object-contain rounded-2xl border border-cyber-border shadow-2xl">
        </div>
    </div>

    <div id="vercel-modal" class="fixed inset-0 bg-black/85 backdrop-blur-md z-50 hidden flex items-center justify-center p-4">
        <div class="bg-cyber-card border border-cyber-border rounded-3xl max-w-2xl w-full max-h-[85vh] flex flex-col overflow-hidden shadow-2xl">
            <div class="p-6 border-b border-cyber-border flex items-center justify-between bg-cyber-bg/60">
                <div class="flex items-center space-x-3">
                    <div class="w-9 h-9 rounded-xl bg-white text-black flex items-center justify-center font-black">▲</div>
                    <div>
                        <h3 class="text-base font-bold text-white">Deploy Store for Free on Vercel</h3>
                        <p class="text-xs text-gray-400">Put your website online live in 3 steps</p>
                    </div>
                </div>
                <button onclick="closeVercelGuide()" class="p-2 text-gray-400 hover:text-white">
                    <i class="fa-solid fa-xmark text-xl"></i>
                </button>
            </div>
            <div class="p-6 overflow-y-auto space-y-5 text-xs sm:text-sm text-gray-300">
                <div class="flex gap-4">
                    <div class="w-8 h-8 rounded-full bg-cyber-purple/20 text-cyber-purple border border-cyber-purple/40 font-bold flex items-center justify-center flex-shrink-0">1</div>
                    <div>
                        <h4 class="font-bold text-white">Save code as index.html</h4>
                        <p class="text-gray-400 mt-1">Copy this complete HTML file onto your PC as <code class="bg-black px-2 py-0.5 rounded text-cyber-cyan border border-cyber-border">index.html</code>.</p>
                    </div>
                </div>
                <div class="flex gap-4">
                    <div class="w-8 h-8 rounded-full bg-cyber-cyan/20 text-cyber-cyan border border-cyber-cyan/40 font-bold flex items-center justify-center flex-shrink-0">2</div>
                    <div>
                        <h4 class="font-bold text-white">Upload to GitHub</h4>
                        <p class="text-gray-400 mt-1">Create a free repository at <a href="https://github.com" target="_blank" class="text-cyber-cyan underline">GitHub.com</a> and upload your <code class="bg-black px-2 py-0.5 rounded text-cyber-cyan border border-cyber-border">index.html</code> file.</p>
                    </div>
                </div>
                <div class="flex gap-4">
                    <div class="w-8 h-8 rounded-full bg-cyber-green/20 text-cyber-green border border-cyber-green/40 font-bold flex items-center justify-center flex-shrink-0">3</div>
                    <div>
                        <h4 class="font-bold text-white">Import into Vercel</h4>
                        <p class="text-gray-400 mt-1">Sign up at <a href="https://vercel.com" target="_blank" class="text-cyber-cyan underline">Vercel.com</a>, click <strong>"Import Project"</strong>, select your repository, and click <strong>Deploy</strong>!</p>
                    </div>
                </div>
            </div>
            <div class="p-4 border-t border-cyber-border bg-cyber-bg/60 flex justify-end">
                <button onclick="closeVercelGuide()" class="px-5 py-2 bg-cyber-purple text-white font-bold rounded-xl text-xs hover:bg-cyber-purple/80 transition">Got It</button>
            </div>
        </div>
    </div>

    <footer class="border-t border-cyber-border glass-panel mt-16">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
            <div class="flex flex-col md:flex-row items-center justify-between gap-4">
                <div class="flex items-center space-x-3">
                    <div class="w-7 h-7 rounded-lg bg-gradient-to-tr from-cyber-purple to-cyber-cyan flex items-center justify-center text-black font-black text-sm">B</div>
                    <span class="text-sm font-black tracking-wider text-white">BMG<span class="text-cyber-purple">&</span>DISCORD STORE</span>
                </div>
                <div class="text-xs text-gray-500">&copy; Blockman Go & Discord Digital Asset Store. All rights reserved.</div>
            </div>
        </div>
    </footer>

    <script>
        // SVG Data Generators for realistic crisp cards matching provided images
        function createDiscordServerSVG() {
            const svg = `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 600 350" width="100%" height="100%">
                <rect width="600" height="350" fill="#2b2d31"/>
                <rect x="20" y="20" width="560" height="60" rx="12" fill="#1e1f22"/>
                <text x="40" y="55" fill="#f2f3f5" font-family="sans-serif" font-weight="bold" font-size="20">🏠 Community Server</text>
                <circle cx="280" cy="50" r="6" fill="#23a55a"/>
                <text x="295" y="55" fill="#dbdee1" font-family="sans-serif" font-size="16">10 Online</text>
                <circle cx="410" cy="50" r="6" fill="#80848e"/>
                <text x="425" y="55" fill="#dbdee1" font-family="sans-serif" font-size="16">73 Members</text>
                <rect x="40" y="100" width="110" height="90" rx="16" fill="#313338"/>
                <text x="95" y="150" text-anchor="middle" fill="#f47fff" font-size="32">💎</text>
                <text x="95" y="180" text-anchor="middle" fill="#dbdee1" font-family="sans-serif" font-size="14">Boost</text>
                <rect x="175" y="100" width="110" height="90" rx="16" fill="#313338"/>
                <text x="230" y="150" text-anchor="middle" fill="#ffffff" font-size="32">👥</text>
                <text x="230" y="180" text-anchor="middle" fill="#dbdee1" font-family="sans-serif" font-size="14">Invite</text>
                <rect x="310" y="100" width="110" height="90" rx="16" fill="#313338"/>
                <text x="365" y="150" text-anchor="middle" fill="#ffffff" font-size="32">🔔</text>
                <text x="365" y="180" text-anchor="middle" fill="#dbdee1" font-family="sans-serif" font-size="14">Notifications</text>
                <rect x="445" y="100" width="110" height="90" rx="16" fill="#313338"/>
                <text x="500" y="150" text-anchor="middle" fill="#ffffff" font-size="32">⚙️</text>
                <text x="500" y="180" text-anchor="middle" fill="#dbdee1" font-family="sans-serif" font-size="14">Settings</text>
                <rect x="20" y="210" width="560" height="110" rx="16" fill="#1e1f22"/>
                <text x="40" y="250" fill="#949ba4" font-family="sans-serif" font-weight="bold" font-size="18">Mark As Read</text>
                <line x1="40" y1="270" x2="560" y2="270" stroke="#35363c" stroke-width="2"/>
                <text x="40" y="300" fill="#f2f3f5" font-family="sans-serif" font-weight="bold" font-size="18">Browse Channels</text>
                <rect x="500" y="282" width="45" height="24" rx="6" fill="#5865f2"/>
                <text x="522" y="299" text-anchor="middle" fill="#ffffff" font-family="sans-serif" font-weight="bold" font-size="12">NEW</text>
            </svg>`;
            return 'data:image/svg+xml;utf8,' + encodeURIComponent(svg);
        }

        function createDiscordBotSVG() {
            const svg = `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 600 350" width="100%" height="100%">
                <rect width="600" height="350" fill="#111214"/>
                <rect x="0" y="0" width="600" height="140" fill="#2d488a"/>
           
