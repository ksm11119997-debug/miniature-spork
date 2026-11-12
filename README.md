<!DOCTYPE html>
<html lang="my" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PETER GAME SHOP - MLBB Diamond Top-Up</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        cyber: {
                            bg: '#0a0d14',
                            card: '#121824',
                            cardHover: '#1a2234',
                            border: '#1f2b3e',
                            neon: '#00f0ff',
                            purple: '#8a2be2',
                            pink: '#ff007f',
                            gold: '#ffd700'
                        }
                    },
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <!-- FontAwesome & Google Fonts -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&display=swap" rel="stylesheet">
    
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #0a0d14;
            color: #e2e8f0;
            min-height: 100vh;
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #0a0d14;
        }
        ::-webkit-scrollbar-thumb {
            background: #1f2b3e;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #00f0ff;
        }

        /* Neon Border Effects */
        .neon-border {
            box-shadow: 0 0 15px rgba(0, 240, 255, 0.15);
            border: 1px solid rgba(0, 240, 255, 0.3);
        }
        .neon-border-selected {
            box-shadow: 0 0 20px rgba(0, 240, 255, 0.4);
            border: 2px solid #00f0ff;
        }

        /* Glassmorphic background */
        .glass-panel {
            background: rgba(18, 24, 36, 0.9);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.08);
        }

        /* Telegram Floating Button Glow */
        .tg-glow {
            box-shadow: 0 0 25px rgba(34, 158, 217, 0.6);
        }
        .tg-glow:hover {
            box-shadow: 0 0 35px rgba(34, 158, 217, 0.9);
        }
    </style>
</head>
<body class="flex flex-col min-h-screen selection:bg-cyan-500 selection:text-black relative pb-32">

    <!-- TOP ANNOUNCEMENT BAR -->
    <div class="bg-gradient-to-r from-purple-950 via-cyan-950 to-purple-950 text-xs py-2 px-4 text-center font-medium text-cyan-200 tracking-wide border-b border-cyan-500/20 flex flex-wrap items-center justify-between gap-2">
        <div class="hidden sm:flex items-center gap-2">
            <span class="inline-block w-2.5 h-2.5 rounded-full bg-emerald-400 animate-ping"></span>
            <span class="text-[11px]">Status: <strong class="text-emerald-400">ONLINE 24/7 AUTO TOPUP</strong></span>
        </div>
        <div class="mx-auto sm:mx-0 flex items-center gap-2 text-[11px]">
            <i class="fa-solid fa-bolt text-yellow-400"></i>
            <span>Welcome to <strong class="text-white font-bold">PETER GAME SHOP</strong></span>
        </div>
        <!-- Admin Toggle Switch -->
        <div class="flex items-center gap-2 bg-black/50 px-2.5 py-1 rounded-full border border-cyan-500/30 ml-auto sm:ml-0">
            <span class="text-[10px] uppercase font-bold text-gray-300">Admin Mode</span>
            <button id="adminToggleBtn" onclick="toggleAdminView()" class="w-8 h-4 bg-gray-700 rounded-full p-0.5 transition-colors relative focus:outline-none">
                <div id="adminToggleDot" class="w-3 h-3 bg-white rounded-full transition-transform"></div>
            </button>
        </div>
    </div>

    <!-- MAIN NAVIGATION -->
    <header class="sticky top-0 z-40 glass-panel border-b border-slate-800">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-3 flex items-center justify-between gap-2">
            <!-- Brand Logo with Stacked Title (PETER / GAME SHOP) -->
            <div class="flex items-center gap-3 cursor-pointer shrink-0" onclick="window.scrollTo({top: 0, behavior: 'smooth'})">
                <div class="w-10 h-10 sm:w-11 sm:h-11 rounded-xl bg-gradient-to-tr from-cyan-500 to-purple-600 flex items-center justify-center p-0.5 shadow-lg shadow-cyan-500/20 shrink-0">
                    <div class="w-full h-full bg-cyber-bg rounded-[10px] flex items-center justify-center">
                        <i class="fa-solid fa-gamepad text-lg sm:text-xl text-cyan-400"></i>
                    </div>
                </div>
                <div class="flex flex-col justify-center leading-none">
                    <span class="text-base sm:text-lg font-black tracking-wider text-white uppercase italic">PETER</span>
                    <span class="text-xs sm:text-sm font-extrabold tracking-wider text-cyan-400 uppercase italic mt-0.5">GAME SHOP</span>
                </div>
            </div>

            <!-- Wallet & Actions -->
            <div class="flex items-center gap-2 sm:gap-3">
                <!-- Wallet Balance Widget -->
                <div class="flex items-center bg-cyber-card border border-slate-700/80 rounded-xl p-1.5 pl-2.5 sm:pl-3 gap-2 sm:gap-3 shadow-inner">
                    <div class="flex flex-col">
                        <span class="text-[9px] font-semibold text-gray-400 uppercase leading-none">Wallet</span>
                        <span class="text-xs sm:text-sm font-black text-cyan-400 leading-tight"><span id="userWalletBalance">0</span> MMK</span>
                    </div>
                    <button onclick="openDepositModal()" class="bg-gradient-to-r from-cyan-500 to-blue-600 hover:from-cyan-400 hover:to-blue-500 text-black font-bold px-2.5 py-1.5 rounded-lg text-[11px] sm:text-xs flex items-center gap-1 transition-all shadow-md shadow-cyan-500/20 active:scale-95 shrink-0">
                        <i class="fa-solid fa-wallet text-[10px]"></i>
                        <span>+ Deposit</span>
                    </button>
                </div>

                <!-- History Button -->
                <button onclick="openHistoryModal()" class="w-9 h-9 sm:w-10 sm:h-10 rounded-xl bg-cyber-card border border-slate-700 flex items-center justify-center text-gray-300 hover:text-cyan-400 hover:border-cyan-500/50 transition-all relative shrink-0">
                    <i class="fa-solid fa-clock-rotate-left text-xs sm:text-sm"></i>
                    <span id="historyBadge" class="hidden absolute -top-1 -right-1 w-4 h-4 bg-purple-600 text-white text-[10px] font-bold rounded-full flex items-center justify-center">0</span>
                </button>
            </div>
        </div>
    </header>

    <!-- ADMIN PANEL OVERLAY (Hidden by default) -->
    <div id="adminPanel" class="hidden bg-slate-900 border-b-2 border-purple-500 p-4 sm:p-6 mb-6">
        <div class="max-w-7xl mx-auto">
            <div class="flex justify-between items-center mb-4">
                <h2 class="text-lg font-bold text-purple-400 flex items-center gap-2">
                    <i class="fa-solid fa-user-shield"></i> Admin Dashboard & Orders Control
                </h2>
                <span class="text-xs bg-purple-950 text-purple-300 px-3 py-1 rounded-full border border-purple-700">Administrator View</span>
            </div>

            <!-- Tabs -->
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <!-- Pending Deposits -->
                <div class="bg-cyber-card border border-slate-800 rounded-xl p-4">
                    <h3 class="text-sm font-bold text-cyan-400 mb-3 flex items-center justify-between">
                        <span><i class="fa-solid fa-hand-holding-dollar mr-1"></i> Pending Deposit Requests</span>
                        <span id="depositCountBadge" class="text-xs bg-cyan-950 text-cyan-400 px-2 py-0.5 rounded-full">0</span>
                    </h3>
                    <div id="adminDepositList" class="space-y-3 max-h-60 overflow-y-auto pr-1">
                        <p class="text-xs text-gray-500 italic">မရှိသေးပါ။</p>
                    </div>
                </div>

                <!-- Pending Diamond Orders -->
                <div class="bg-cyber-card border border-slate-800 rounded-xl p-4">
                    <h3 class="text-sm font-bold text-purple-400 mb-3 flex items-center justify-between">
                        <span><i class="fa-solid fa-cart-shopping mr-1"></i> Diamond Orders</span>
                        <span id="orderCountBadge" class="text-xs bg-purple-950 text-purple-400 px-2 py-0.5 rounded-full">0</span>
                    </h3>
                    <div id="adminOrderList" class="space-y-3 max-h-60 overflow-y-auto pr-1">
                        <p class="text-xs text-gray-500 italic">မရှိသေးပါ။</p>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- MAIN APP CONTENT CONTAINER -->
    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 pt-4 flex-grow w-full">
        
        <!-- HERO BANNER WITH USER PROVIDED ARTWORK -->
        <div class="relative overflow-hidden rounded-2xl border border-purple-500/40 mb-8 shadow-2xl shadow-purple-900/30 group">
            <img src="https://lh3.googleusercontent.com/gg/AEmxVGdQW94kE_tK6-GjZ4Jb5p9X-Z5b-J7T5g1Z" 
                 alt="PETER GAME SHOP BANNER" 
                 onerror="this.onerror=null; this.src='https://placehold.co/1200x500/0a0d14/00f0ff?text=PETER+GAME+SHOP';"
                 class="w-full h-auto max-h-[360px] object-cover object-center transform group-hover:scale-105 transition-transform duration-500">
            <div class="absolute inset-0 bg-gradient-to-t from-cyber-bg via-transparent to-transparent opacity-80"></div>
            <div class="absolute bottom-3 left-4 right-4 flex items-center justify-between text-xs text-gray-300">
                <span class="bg-black/60 backdrop-blur-md px-3 py-1 rounded-full border border-cyan-500/30 font-bold text-cyan-400">
                    <i class="fa-solid fa-shield-halved mr-1"></i> Official Top-Up Shop
                </span>
                <span class="hidden sm:inline-block bg-black/60 backdrop-blur-md px-3 py-1 rounded-full border border-purple-500/30 text-purple-300">
                    Mobile Legends: Bang Bang
                </span>
            </div>
        </div>

        <!-- MAIN TOP-UP FORM & PACKAGES GRID -->
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            
            <!-- LEFT PANEL: USER ID INPUT & PAYMENT METHOD -->
            <div class="lg:col-span-1 space-y-6">
                
                <!-- STEP 1: USER ID & ZONE ID -->
                <div class="bg-cyber-card border border-slate-800 rounded-2xl p-5 shadow-lg relative overflow-hidden">
                    <div class="flex items-center gap-3 mb-4">
                        <div class="w-8 h-8 rounded-lg bg-cyan-500/20 text-cyan-400 font-bold flex items-center justify-center text-sm border border-cyan-500/30">1</div>
                        <h3 class="font-bold text-white text-base">Account Information</h3>
                    </div>

                    <div class="space-y-4">
                        <div>
                            <label class="block text-xs font-semibold text-gray-400 mb-1.5">User ID</label>
                            <input type="number" id="userIdInput" placeholder="e.g. 12345678" 
                                class="w-full bg-slate-900/90 border border-slate-700 focus:border-cyan-400 rounded-xl px-3.5 py-2.5 text-sm font-mono text-white placeholder-gray-600 focus:outline-none transition-all">
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-gray-400 mb-1.5">Zone ID</label>
                            <input type="number" id="zoneIdInput" placeholder="e.g. 1234" 
                                class="w-full bg-slate-900/90 border border-slate-700 focus:border-cyan-400 rounded-xl px-3.5 py-2.5 text-sm font-mono text-white placeholder-gray-600 focus:outline-none transition-all">
                        </div>
                    </div>
                    <p class="text-[11px] text-gray-500 mt-3 flex items-center gap-1.5">
                        <i class="fa-solid fa-circle-info text-cyan-400"></i> MLBB Profile အောက်ရှိ User ID နှင့် Zone ID ကို မှန်ကန်စွာ ဖြည့်သွင်းပါ။
                    </p>
                </div>

                <!-- STEP 3: PAYMENT METHOD SELECTION -->
                <div class="bg-cyber-card border border-slate-800 rounded-2xl p-5 shadow-lg">
                    <div class="flex items-center gap-3 mb-4">
                        <div class="w-8 h-8 rounded-lg bg-cyan-500/20 text-cyan-400 font-bold flex items-center justify-center text-sm border border-cyan-500/30">3</div>
                        <h3 class="font-bold text-white text-base">Select Payment Method</h3>
                    </div>

                    <div class="space-y-3" id="paymentMethods">
                        <!-- Direct KPay -->
                        <div onclick="selectPayment('kpay')" id="pay-kpay" class="payment-card border border-slate-700 bg-slate-900/60 hover:border-blue-500 p-3.5 rounded-xl cursor-pointer transition-all flex items-center justify-between">
                            <div class="flex items-center gap-3">
                                <div class="w-9 h-9 rounded-lg bg-blue-600 text-white font-black flex items-center justify-center text-xs">KPay</div>
                                <div>
                                    <p class="text-xs font-bold text-white">KBZPay (Direct)</p>
                                    <p class="text-[10px] text-gray-400">Instant Slip Verification</p>
                                </div>
                            </div>
                            <div class="radio-indicator w-4 h-4 rounded-full border border-slate-600 flex items-center justify-center">
                                <div class="w-2 h-2 rounded-full bg-cyan-400 hidden"></div>
                            </div>
                        </div>

                        <!-- Direct WavePay -->
                        <div onclick="selectPayment('wavepay')" id="pay-wavepay" class="payment-card border border-slate-700 bg-slate-900/60 hover:border-yellow-500 p-3.5 rounded-xl cursor-pointer transition-all flex items-center justify-between">
                            <div class="flex items-center gap-3">
                                <div class="w-9 h-9 rounded-lg bg-yellow-500 text-black font-black flex items-center justify-center text-xs">Wave</div>
                                <div>
                                    <p class="text-xs font-bold text-white">WavePay (Direct)</p>
                                    <p class="text-[10px] text-gray-400">Instant Txn ID Entry</p>
                                </div>
                            </div>
                            <div class="radio-indicator w-4 h-4 rounded-full border border-slate-600 flex items-center justify-center">
                                <div class="w-2 h-2 rounded-full bg-cyan-400 hidden"></div>
                            </div>
                        </div>

                        <!-- In-App Wallet -->
                        <div onclick="selectPayment('wallet')" id="pay-wallet" class="payment-card border border-slate-700 bg-slate-900/60 hover:border-cyan-500 p-3.5 rounded-xl cursor-pointer transition-all flex items-center justify-between">
                            <div class="flex items-center gap-3">
                                <div class="w-9 h-9 rounded-lg bg-purple-600 text-white font-black flex items-center justify-center text-xs"><i class="fa-solid fa-wallet"></i></div>
                                <div>
                                    <p class="text-xs font-bold text-white">PETER Wallet</p>
                                    <p class="text-[10px] text-gray-400">Fast Auto Checkout</p>
                                </div>
                            </div>
                            <div class="radio-indicator w-4 h-4 rounded-full border border-slate-600 flex items-center justify-center">
                                <div class="w-2 h-2 rounded-full bg-cyan-400 hidden"></div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- SUBMIT ORDER BUTTON -->
                <button onclick="processOrderCheckout()" class="w-full py-4 bg-gradient-to-r from-cyan-500 via-blue-600 to-purple-600 hover:from-cyan-400 hover:to-purple-500 text-black font-black text-sm uppercase tracking-wider rounded-2xl shadow-xl shadow-cyan-500/20 active:scale-[0.98] transition-all flex items-center justify-center gap-2 border border-cyan-300/40">
                    <i class="fa-solid fa-cart-check text-base"></i>
                    <span>Buy Now / ဝယ်ယူမည်</span>
                </button>

            </div>

            <!-- RIGHT PANEL: STEP 2 - DIAMOND PACKAGES SELECTOR -->
            <div class="lg:col-span-2">
                <div class="bg-cyber-card border border-slate-800 rounded-2xl p-5 shadow-lg">
                    <div class="flex items-center justify-between mb-5">
                        <div class="flex items-center gap-3">
                            <div class="w-8 h-8 rounded-lg bg-cyan-500/20 text-cyan-400 font-bold flex items-center justify-center text-sm border border-cyan-500/30">2</div>
                            <h3 class="font-bold text-white text-base">Select Diamond Package</h3>
                        </div>
                        <span class="text-xs text-gray-400">အလိုရှိသော ပက်ကေ့ချ်ကို နှိပ်ပါ</span>
                    </div>

                    <!-- PACKAGES GRID -->
                    <div class="grid grid-cols-2 sm:grid-cols-3 gap-3.5" id="packageGrid">
                        <!-- Dynamic packages rendered via Javascript -->
                    </div>
                </div>
            </div>

        </div>

    </main>

    <!-- FLOATING TELEGRAM SUPPORT BUTTON (DIRECT LINK TO @k3p_sanji007) -->
    <a href="https://t.me/k3p_sanji007" target="_blank" rel="noopener noreferrer" 
       class="fixed bottom-6 right-6 z-50 flex items-center gap-2 bg-gradient-to-r from-sky-500 to-blue-600 hover:from-sky-400 hover:to-blue-500 text-white font-bold px-4 py-3 rounded-full tg-glow transition-all duration-300 hover:scale-105 group border border-sky-300/30">
        <i class="fa-brands fa-telegram text-2xl group-hover:rotate-12 transition-transform"></i>
        <span class="text-xs font-extrabold pr-1 tracking-wide">Customer Support</span>
    </a>

    <!-- CHECKOUT MODAL (PAYMENT CONFIRMATION) -->
    <div id="checkoutModal" class="fixed inset-0 bg-black/80 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4 overflow-y-auto">
        <div class="bg-cyber-card border border-slate-700 rounded-2xl max-w-md w-full p-6 shadow-2xl relative">
            <button onclick="closeCheckoutModal()" class="absolute top-4 right-4 text-gray-400 hover:text-white text-lg">
                <i class="fa-solid fa-xmark"></i>
            </button>

            <h3 class="text-lg font-bold text-white mb-1 flex items-center gap-2">
                <i class="fa-solid fa-receipt text-cyan-400"></i> Order Summary & Payment
            </h3>
            <p class="text-xs text-gray-400 mb-4">အောက်ပါ အချက်အလက်များကို စစ်ဆေး၍ ငွေလ
