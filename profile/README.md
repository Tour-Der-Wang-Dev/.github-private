<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Neon Portal v3.0</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;500;700;900&family=Rajdhani:wght@400;500;600;700&display=swap');
        
        :root {
            --neon-blue: #05d9e8;
            --neon-pink: #ff2a6d;
            --neon-purple: #d300c5;
            --neon-green: #00ff9d;
            --dark-bg: #05010e;
            --darker-bg: #0d0221;
            --nav-dark: #12092a;
            --matrix-green: #00ff41;
        }
        
        body {
            font-family: 'Rajdhani', 'Orbitron', sans-serif;
            background-color: var(--dark-bg);
            color: white;
            min-height: 100vh;
            background-image: var(--bg-image, none);
            background-size: cover;
            background-attachment: fixed;
            background-position: center;
            overflow-x: hidden;
        }
        
        .glitch-effect {
            position: relative;
            color: white;
        }
        
        .glitch-effect::before, .glitch-effect::after {
            content: attr(data-text);
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            opacity: 0.8;
        }
        
        .glitch-effect::before {
            color: var(--neon-blue);
            z-index: -1;
            animation: glitch-effect 3s infinite;
        }
        
        .glitch-effect::after {
            color: var(--neon-pink);
            z-index: -2;
            animation: glitch-effect 2s infinite reverse;
        }
        
        @keyframes glitch-effect {
            0% { transform: translate(0); }
            20% { transform: translate(-3px, 3px); }
            40% { transform: translate(-3px, -3px); }
            60% { transform: translate(3px, 3px); }
            80% { transform: translate(3px, -3px); }
            100% { transform: translate(0); }
        }
        
        .neon-text-blue {
            color: var(--neon-blue);
            text-shadow: 0 0 5px var(--neon-blue), 0 0 10px var(--neon-blue), 0 0 20px var(--neon-blue);
        }
        
        .neon-text-pink {
            color: var(--neon-pink);
            text-shadow: 0 0 5px var(--neon-pink), 0 0 10px var(--neon-pink), 0 0 20px var(--neon-pink);
        }
        
        .neon-text-purple {
            color: var(--neon-purple);
            text-shadow: 0 0 5px var(--neon-purple), 0 0 10px var(--neon-purple), 0 0 20px var(--neon-purple);
        }
        
        .neon-text-green {
            color: var(--neon-green);
            text-shadow: 0 0 5px var(--neon-green), 0 0 10px var(--neon-green), 0 0 20px var(--neon-green);
        }
        
        .neon-border-blue {
            border: 1px solid var(--neon-blue);
            box-shadow: 0 0 5px var(--neon-blue), inset 0 0 5px var(--neon-blue), 0 0 20px var(--neon-blue);
        }
        
        .neon-border-pink {
            border: 1px solid var(--neon-pink);
            box-shadow: 0 0 5px var(--neon-pink), inset 0 0 5px var(--neon-pink), 0 0 20px var(--neon-pink);
        }
        
        .neon-border-green {
            border: 1px solid var(--neon-green);
            box-shadow: 0 0 5px var(--neon-green), inset 0 0 5px var(--neon-green), 0 0 20px var(--neon-green);
        }
        
        .neon-hover:hover {
            text-shadow: 0 0 10px currentColor, 0 0 20px currentColor, 0 0 30px currentColor;
            transition: text-shadow 0.3s ease;
        }
        
        .nav-item:hover {
            transform: translateY(-2px);
            transition: transform 0.3s ease;
        }
        
        .dropdown {
            display: none;
            background: var(--nav-dark);
            border: 1px solid var(--neon-blue);
            box-shadow: 0 0 20px var(--neon-blue);
            transition: all 0.3s ease;
            z-index: 100;
        }
        
        .group:hover .dropdown {
            display: block;
        }
        
        .portal-card {
            transition: all 0.3s ease;
            backdrop-filter: blur(10px);
            perspective: 1000px;
            transform-style: preserve-3d;
        }
        
        .portal-card:hover {
            transform: translateY(-5px) scale(1.05);
            box-shadow: 0 0 20px currentColor;
        }
        
        .portal-card-inner {
            transition: transform 0.6s;
            transform-style: preserve-3d;
        }
        
        .portal-card:hover .portal-card-inner {
            transform: rotateY(15deg) rotateX(10deg);
        }
        
        .modal-overlay {
            background: rgba(5, 1, 14, 0.9);
            backdrop-filter: blur(5px);
            animation: fadeIn 0.3s ease;
        }
        
        .modal-content {
            animation: slideIn 0.3s ease;
            background: var(--darker-bg);
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        @keyframes slideIn {
            from { transform: translateY(-50px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }
        
        .color-option {
            width: 30px;
            height: 30px;
            border-radius: 50%;
            display: inline-block;
            margin: 5px;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
        }
        
        .color-option:hover {
            transform: scale(1.1);
        }
        
        .color-option.selected::after {
            content: "✓";
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            color: white;
            font-weight: bold;
        }
        
        .custom-color-toggle {
            padding: 8px;
            cursor: pointer;
            border-radius: 5px;
            margin-top: 10px;
            text-align: center;
            border: 1px dashed var(--neon-blue);
        }
        
        .custom-color-toggle:hover {
            background: rgba(5, 217, 232, 0.1);
        }
        
        .custom-color-input {
            width: 100%;
            height: 30px;
            border: none;
            background: transparent;
            cursor: pointer;
            margin-top: 10px;
        }
        
        .bg-preview, .icon-preview {
            max-width: 100%;
            height: auto;
            margin-top: 10px;
            border-radius: 5px;
            display: none;
        }
        
        .grid-lines {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: linear-gradient(to right, rgba(5, 217, 232, 0.05) 1px, transparent 1px),
                              linear-gradient(to bottom, rgba(5, 217, 232, 0.05) 1px, transparent 1px);
            background-size: 30px 30px;
            z-index: -1;
            pointer-events: none;
        }
        
        .neon-underline {
            position: relative;
            display: inline-block;
        }
        
        .neon-underline::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 100%;
            height: 2px;
            background: linear-gradient(to right, var(--neon-blue), var(--neon-pink));
            transform: scaleX(0);
            transform-origin: bottom right;
            transition: transform 0.5s ease-out;
        }
        
        .neon-underline:hover::after {
            transform: scaleX(1);
            transform-origin: bottom left;
        }
        
        /* Holographic effect */
        .holographic-effect {
            position: relative;
            overflow: hidden;
        }
        
        .holographic-effect::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(
                to bottom right,
                rgba(255, 255, 255, 0) 45%,
                rgba(5, 217, 232, 0.2) 50%,
                rgba(255, 255, 255, 0) 55%
            );
            transform: rotate(30deg);
            animation: holographic 6s linear infinite;
        }
        
        @keyframes holographic {
            0% { transform: translateY(-100%) rotate(30deg); }
            100% { transform: translateY(100%) rotate(30deg); }
        }
        
        /* Matrix rain effect */
        .matrix-rain {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            opacity: 0.05;
            pointer-events: none;
        }
        
        /* Search bar */
        .search-container {
            transition: all 0.3s ease;
        }
        
        .search-container.focused {
            box-shadow: 0 0 15px var(--neon-blue), 0 0 30px var(--neon-blue);
        }
        
        /* Weather widget */
        .weather-icon {
            font-size: 2rem;
            margin-bottom: 0.5rem;
        }
        
        /* Quick actions */
        .quick-action {
            transition: all 0.3s ease;
        }
        
        .quick-action:hover {
            transform: scale(1.1);
        }
        
        /* Notification badge */
        .notification-badge {
            position: absolute;
            top: -5px;
            right: -5px;
            width: 18px;
            height: 18px;
            background-color: var(--neon-pink);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 10px;
            font-weight: bold;
            box-shadow: 0 0 5px var(--neon-pink);
        }
        
        /* Draggable portal */
        .draggable-portal {
            cursor: grab;
            user-select: none;
        }
        
        .draggable-portal:active {
            cursor: grabbing;
        }
        
        /* Loading spinner */
        .loading-spinner {
            border: 3px solid rgba(5, 217, 232, 0.3);
            border-radius: 50%;
            border-top: 3px solid var(--neon-blue);
            width: 30px;
            height: 30px;
            animation: spin 1s linear infinite;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        /* Terminal effect */
        .terminal-cursor {
            animation: blink 1s infinite;
        }
        
        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0; }
        }
        
        /* Responsive adjustments */
        @media (max-width: 768px) {
            .portal-card {
                perspective: none;
            }
            
            .portal-card:hover .portal-card-inner {
                transform: none;
            }
        }
    </style>
</head>
<body class="min-h-screen relative">
    <!-- Grid lines effect -->
    <div class="grid-lines"></div>
    
    <!-- Matrix rain effect (will be initialized by JS) -->
    <canvas id="matrix-rain" class="matrix-rain"></canvas>

    <!-- Navbar -->
    <nav class="navbar fixed top-0 left-0 right-0 z-50 bg-[#05010e]/90 backdrop-blur-md border-b border-[#12092a]">
        <div class="container mx-auto px-4">
            <div class="flex justify-between items-center h-16">
                <!-- Logo -->
                <div class="flex items-center">
                    <div class="neon-border-pink rounded-full p-2">
                        <i class="fas fa-terminal text-xl neon-text-pink"></i>
                    </div>
                    <span class="ml-3 font-bold text-xl neon-text-blue">NEON PORTAL v3.0</span>
                </div>

                <!-- Search bar -->
                <div class="hidden md:flex items-center mx-4 flex-1 max-w-xl">
                    <div class="search-container relative w-full neon-border-blue rounded-lg transition-all">
                        <input type="text" id="search-input" placeholder="Search portals..." 
                            class="w-full bg-transparent p-2 pl-10 pr-4 focus:outline-none">
                        <i class="fas fa-search absolute left-3 top-3 text-[#05d9e8]"></i>
                        <div id="search-results" class="absolute left-0 right-0 top-full mt-1 bg-[#0d0221] rounded-lg shadow-lg hidden z-50 max-h-80 overflow-y-auto">
                            <!-- Search results will be populated here -->
                        </div>
                    </div>
                </div>

                <!-- Nav Items -->
                <div class="hidden md:flex items-center space-x-6">
                    <div class="nav-item relative group">
                        <button class="flex items-center space-x-1 neon-text-blue neon-underline">
                            <i class="fas fa-cog"></i>
                            <span>Settings</span>
                            <i class="fas fa-chevron-down text-xs"></i>
                        </button>
                        <div class="dropdown absolute right-0 mt-2 w-80 rounded-lg dropdown-content p-4">
                            <h3 class="text-sm neon-text-pink mb-3 uppercase tracking-wider">Portal Management</h3>
                            <button onclick="showAddLinkModal()"
                                class="w-full py-2 neon-border-blue rounded flex items-center justify-center mb-3 hover:bg-[#05d9e8] hover:text-[#0d0221] transition-all">
                                <i class="fas fa-plus mr-2"></i>Add New Portal
                            </button>
                            
                            <button onclick="showImportExportModal()"
                                class="w-full py-2 neon-border-green rounded flex items-center justify-center mb-3 hover:bg-[#00ff9d] hover:text-[#0d0221] transition-all">
                                <i class="fas fa-file-import mr-2"></i>Import/Export
                            </button>

                            <h3 class="text-sm neon-text-blue mt-4 mb-3 uppercase tracking-wider">Customization</h3>
                            <div class="space-y-4">
                                <div>
                                    <label for="bg-image" class="block mb-2 text-xs uppercase tracking-wider">Background Image URL</label>
                                    <div class="flex">
                                        <input type="url" id="bg-image" class="flex-grow p-2 rounded-l-lg bg-[#12092a]"
                                            placeholder="https://example.com/image.jpg">
                                        <button onclick="setBackgroundImage()"
                                            class="px-3 py-2 bg-[#05d9e8] text-[#0d0221] rounded-r-lg hover:bg-[#00c4d2] transition-all">
                                            <i class="fas fa-check"></i>
                                        </button>
                                    </div>
                                    <div class="bg-upload-container">
                                        <label class="block mt-2 text-xs uppercase tracking-wider">Upload Background</label>
                                        <input type="file" id="bg-upload" class="w-full mt-1" accept="image/*">
                                        <img id="bg-preview" class="bg-preview" src="#" alt="Background Preview">
                                        <button onclick="applyUploadedBackground()"
                                            class="mt-2 px-3 py-1 rounded border border-[#ff2a6d] hover:bg-[#ff2a6d]/20 transition-all text-xs">
                                            Apply Uploaded Image
                                        </button>
                                    </div>
                                    <button onclick="resetBackgroundImage()"
                                        class="mt-2 text-xs px-3 py-1 rounded border border-[#ff2a6d] hover:bg-[#ff2a6d]/20 transition-all">
                                        Reset Background
                                    </button>
                                </div>

                                <div>
                                    <label class="block mb-2 text-xs uppercase tracking-wider">Theme Color</label>
                                    <div class="color-picker-container neon-border-blue rounded-lg p-4">
                                        <div class="color-option selected" style="background-color: #05d9e8;"
                                            onclick="selectThemeColor('#05d9e8', this)"></div>
                                        <div class="color-option" style="background-color: #ff2a6d;"
                                            onclick="selectThemeColor('#ff2a6d', this)"></div>
                                        <div class="color-option" style="background-color: #d300c5;"
                                            onclick="selectThemeColor('#d300c5', this)"></div>
                                        <div class="color-option" style="background-color: #00ff9d;"
                                            onclick="selectThemeColor('#00ff9d', this)"></div>
                                        <div class="color-option" style="background-color: #ffcc00;"
                                            onclick="selectThemeColor('#ffcc00', this)"></div>
                                        <div class="color-option" style="background-color: #ff3333;"
                                            onclick="selectThemeColor('#ff3333', this)"></div>
                                        <div class="color-option" style="background-color: #4267B2;"
                                            onclick="selectThemeColor('#4267B2', this)"></div>
                                        <div class="color-option" style="background-color: #9147ff;"
                                            onclick="selectThemeColor('#9147ff', this)"></div>
                                        <div class="color-option" style="background-color: #25F4EE;"
                                            onclick="selectThemeColor('#25F4EE', this)"></div>
                                        <div class="custom-color-toggle w-full" onclick="toggleCustomColorInput()">
                                            Custom Color
                                        </div>
                                        <div id="custom-color-wrapper" class="custom-color-option" style="display: none;">
                                            <input type="color" id="custom-color" class="custom-color-input">
                                            <button class="custom-color-confirm mt-2 px-3 py-1 rounded border border-[#05d9e8] hover:bg-[#05d9e8]/20 transition-all" onclick="confirmCustomColor()">OK</button>
                                        </div>
                                    </div>
                                </div>
                                
                                <div>
                                    <label class="block mb-2 text-xs uppercase tracking-wider">Effects</label>
                                    <div class="flex items-center justify-between">
                                        <span>Matrix Rain</span>
                                        <label class="relative inline-flex items-center cursor-pointer">
                                            <input type="checkbox" id="matrix-toggle" class="sr-only peer" checked>
                                            <div class="w-11 h-6 bg-gray-700 peer-focus:outline-none rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-[#05d9e8]"></div>
                                        </label>
                                    </div>
                                </div>
                            </div>

                            <h3 class="text-sm neon-text-blue mt-4 mb-3 uppercase tracking-wider">System Info</h3>
                            <div class="text-xs space-y-2">
                                <div class="flex justify-between">
                                    <span>Version</span>
                                    <span class="text-[#05d9e8]">v3.0.0</span>
                                </div>
                                <div class="flex justify-between">
                                    <span>Portals</span>
                                    <span id="portal-count" class="text-[#ff2a6d]">0</span>
                                </div>
                                <div class="flex justify-between">
                                    <span>Memory</span>
                                    <span id="memory-usage" class="text-[#00ff9d]">Loading...</span>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="nav-item relative group">
                        <button class="flex items-center space-x-1 neon-text-blue neon-underline">
                            <i class="fas fa-address-card"></i>
                            <span>Contact</span>
                            <i class="fas fa-chevron-down text-xs"></i>
                        </button>
                        <div class="dropdown absolute right-0 mt-2 w-72 rounded-lg dropdown-content p-4">
                            <h3 class="text-sm neon-text-pink mb-3 uppercase tracking-wider">Connection Channels</h3>
                            <div class="space-y-3">
                                <div class="contact-card p-3 rounded border border-[#05d9e8] hover:bg-[#05d9e8]/10 transition-all">
                                    <div class="flex items-center">
                                        <i class="fas fa-envelope text-lg text-[#05d9e8] mr-3"></i>
                                        <div>
                                            <h4 class="font-bold">Encrypted Mail</h4>
                                            <a href="mailto:contact@neonportal.dev"
                                                class="text-sm hover:underline block">contact@neonportal.dev</a>
                                        </div>
                                    </div>
                                </div>
                                
                                <div class="contact-card p-3 rounded border border-[#ff2a6d] hover:bg-[#ff2a6d]/10 transition-all">
                                    <div class="flex items-center">
                                        <i class="fab fa-discord text-lg text-[#5865F2] mr-3"></i>
                                        <div>
                                            <h4 class="font-bold">Discord</h4>
                                            <span class="text-sm">NeonPortal#0001</span>
                                        </div>
                                    </div>
                                </div>
                                
                                <div class="contact-card p-3 rounded border border-[#25F4EE] hover:bg-[#25F4EE]/10 transition-all">
                                    <div class="flex items-center">
                                        <i class="fab fa-twitter text-lg text-[#1DA1F2] mr-3"></i>
                                        <div>
                                            <h4 class="font-bold">Twitter</h4>
                                            <a href="https://twitter.com/neonportal" target="_blank" class="text-sm hover:underline block">@neonportal</a>
                                        </div>
                                    </div>
                                </div>
                                
                                <div class="contact-card p-3 rounded border border-[#9147ff] hover:bg-[#9147ff]/10 transition-all">
                                    <div class="flex items-center">
                                        <i class="fab fa-patreon text-lg text-[#FF424D] mr-3"></i>
                                        <div>
                                            <h4 class="font-bold">Support</h4>
                                            <a href="https://patreon.com/neonportal" target="_blank" class="text-sm hover:underline block">Patreon</a>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Weather widget -->
                    <div class="nav-item relative group">
                        <button class="flex items-center space-x-1 neon-text-green neon-underline" id="weather-btn">
                            <i class="fas fa-cloud-sun"></i>
                            <span id="weather-temp">--°C</span>
                        </button>
                        <div class="dropdown absolute right-0 mt-2 w-48 rounded-lg dropdown-content p-4">
                            <div class="text-center">
                                <div id="weather-icon" class="weather-icon">
                                    <i class="fas fa-question"></i>
                                </div>
                                <div id="weather-description" class="text-sm uppercase">Loading...</div>
                                <div id="weather-location" class="text-xs mt-1 neon-text-blue">Unknown</div>
                                <div class="flex justify-between mt-3 text-xs">
                                    <div>
                                        <i class="fas fa-wind mr-1"></i>
                                        <span id="weather-wind">-- km/h</span>
                                    </div>
                                    <div>
                                        <i class="fas fa-tint mr-1"></i>
                                        <span id="weather-humidity">--%</span>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Notifications -->
                    <div class="nav-item relative">
                        <button class="flex items-center space-x-1 neon-text-purple neon-underline" onclick="showNotifications()">
                            <i class="fas fa-bell"></i>
                            <span>Alerts</span>
                            <div id="notification-count" class="notification-badge hidden">0</div>
                        </button>
                    </div>
                </div>

                <!-- Mobile menu button -->
                <div class="md:hidden">
                    <button id="mobile-menu-button" class="neon-text-pink text-2xl focus:outline-none">
                        <i class="fas fa-bars"></i>
                    </button>
                </div>
            </div>
        </div>

        <!-- Mobile menu -->
        <div id="mobile-menu" class="md:hidden hidden bg-[#05010e] border-t border-[#ff2a6d]">
            <div class="px-2 py-3 space-y-1">
                <!-- Mobile search -->
                <div class="search-container relative w-full neon-border-blue rounded-lg transition-all mx-2 mb-3">
                    <input type="text" id="search-input-mobile" placeholder="Search portals..." 
                        class="w-full bg-transparent p-2 pl-10 pr-4 focus:outline-none">
                    <i class="fas fa-search absolute left-3 top-3 text-[#05d9e8]"></i>
                </div>
                
                <button onclick="showAddLinkModal()" class="block px-3 py-2 rounded-md neon-text-blue w-full text-left hover:bg-[#05d9e8]/20">
                    <i class="fas fa-plus mr-2"></i>Add New Portal
                </button>
                
                <button onclick="showImportExportModal()" class="block px-3 py-2 rounded-md neon-text-green w-full text-left hover:bg-[#00ff9d]/20">
                    <i class="fas fa-file-import mr-2"></i>Import/Export
                </button>
                
                <button class="block px-3 py-2 rounded-md neon-text-blue w-full text-left hover:bg-[#05d9e8]/20">
                    <i class="fas fa-cog mr-2"></i>Settings
                </button>
                
                <button class="block px-3 py-2 rounded-md neon-text-blue w-full text-left hover:bg-[#05d9e8]/20">
                    <i class="fas fa-address-card mr-2"></i>Contact
                </button>
                
                <button class="block px-3 py-2 rounded-md neon-text-green w-full text-left hover:bg-[#00ff9d]/20" id="weather-btn-mobile">
                    <i class="fas fa-cloud-sun mr-2"></i>Weather
                </button>
                
                <button class="block px-3 py-2 rounded-md neon-text-purple w-full text-left hover:bg-[#d300c5]/20" onclick="showNotifications()">
                    <i class="fas fa-bell mr-2"></i>Alerts
                    <div id="notification-count-mobile" class="notification-badge hidden">0</div>
                </button>
                
                <div class="px-3 py-2">
                    <label class="block text-xs neon-text-blue mb-1">Background Image</label>
                    <div class="flex mb-2">
                        <input type="url" id="bg-image-mobile" class="flex-grow p-2 rounded-l-lg bg-[#12092a]"
                            placeholder="Image URL">
                        <button onclick="setBackgroundImage()"
                            class="px-3 py-2 bg-[#05d9e8] text-[#0d0221] rounded-r-lg hover:bg-[#00c4d2] transition-all">
                            <i class="fas fa-check"></i>
                        </button>
                    </div>
                    <button onclick="resetBackgroundImage()"
                        class="w-full px-3 py-1.5 text-xs rounded border border-[#ff2a6d] hover:bg-[#ff2a6d]/20 transition-all">
                        Reset Background
                    </button>
                </div>
            </div>
        </div>
    </nav>

    <!-- Main container -->
    <div class="container mx-auto px-4 py-8 relative z-10 mt-20">
        <!-- Header -->
        <header class="text-center mb-12">
            <div class="relative inline-block">
                <h1 class="glitch-effect text-5xl md:text-7xl font-bold mb-4" data-text="NEON PORTAL v3.0">NEON PORTAL v3.0</h1>
                <span
                    class="absolute -bottom-3 left-1/2 transform -translate-x-1/2 w-48 h-1 bg-gradient-to-r from-transparent via-[#05d9e8] to-transparent"></span>
                <span
                    class="absolute -bottom-5 left-1/2 transform -translate-x-1/2 w-32 h-1 bg-gradient-to-r from-transparent via-[#ff2a6d] to-transparent"></span>
            </div>
            <p class="text-xl neon-text-purple uppercase tracking-wider mt-8">Your gateway to the digital neonverse</p>
            
            <!-- Quick actions -->
            <div class="flex justify-center mt-8 space-x-4">
                <button class="quick-action neon-border-blue rounded-full p-3 hover:bg-[#05d9e8]/20" title="Terminal" onclick="showTerminal()">
                    <i class="fas fa-terminal text-xl neon-text-blue"></i>
                </button>
                <button class="quick-action neon-border-pink rounded-full p-3 hover:bg-[#ff2a6d]/20" title="Music Player" onclick="showMusicPlayer()">
                    <i class="fas fa-music text-xl neon-text-pink"></i>
                </button>
                <button class="quick-action neon-border-green rounded-full p-3 hover:bg-[#00ff9d]/20" title="System Monitor" onclick="showSystemMonitor()">
                    <i class="fas fa-chart-line text-xl neon-text-green"></i>
                </button>
                <button class="quick-action neon-border-purple rounded-full p-3 hover:bg-[#d300c5]/20" title="Quick Notes" onclick="showQuickNotes()">
                    <i class="fas fa-sticky-note text-xl neon-text-purple"></i>
                </button>
            </div>
        </header>

        <!-- Time and date display -->
        <div class="flex justify-center mb-12">
            <div class="neon-border-blue rounded-lg p-4 text-center backdrop-blur-sm bg-[#0d0221]/50 holographic-effect">
                <div id="time" class="text-3xl font-bold neon-text-blue">00:00:00</div>
                <div id="date" class="text-lg uppercase tracking-wider mt-1">Loading...</div>
                <div id="terminal-output" class="text-xs mt-2 font-mono hidden">
                    <div class="text-left">
                        <div class="text-[#00ff9d]">user@neonportal:~$ <span class="terminal-cursor">_</span></div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Portals grid -->
        <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 gap-6 mb-12" id="portals-grid">
            <!-- Default portals will be added here by JavaScript -->
        </div>
        
        <!-- Loading state -->
        <div id="loading-state" class="text-center py-12 hidden">
            <div class="loading-spinner mx-auto mb-4"></div>
            <p class="neon-text-blue">Initializing system...</p>
        </div>
    </div>

    <!-- Add Portal Modal -->
    <div id="add-portal-modal" class="fixed inset-0 flex items-center justify-center z-50 hidden modal-overlay">
        <div class="modal-content neon-border-blue rounded-xl p-8 max-w-md w-full mx-4 relative">
            <button id="close-portal-modal"
                class="absolute top-4 right-4 text-xl hover:text-[#ff2a6d] transition-all">×</button>
            <h2 class="text-2xl neon-text-pink mb-6 uppercase tracking-wider">Create New Portal</h2>

            <form id="portal-form" class="space-y-6">
                <div>
                    <label for="portal-name" class="block mb-2 neon-text-blue uppercase text-sm tracking-wider">Portal Name</label>
                    <input type="text" id="portal-name" class="w-full p-3 rounded-lg bg-[#12092a] focus:outline-none focus:border focus:border-[#05d9e8]" required>
                </div>

                <div>
                    <label for="portal-url"
                        class="block mb-2 neon-text-blue uppercase text-sm tracking-wider">Destination URL</label>
                    <input type="url" id="portal-url" class="w-full p-3 rounded-lg bg-[#12092a] focus:outline-none focus:border focus:border-[#05d9e8]" placeholder="https://"
                        required>
                </div>

                <div>
                    <label class="block mb-2 neon-text-blue uppercase text-sm tracking-wider">Icon</label>
                    <select id="portal-icon" class="w-full p-3 rounded-lg bg-[#0d0221] border border-[#05d9e8] focus:outline-none focus:border focus:border-[#ff2a6d]">
                        <option value="fab fa-youtube">YouTube</option>
                        <option value="fab fa-twitter">Twitter</option>
                        <option value="fab fa-github">GitHub</option>
                        <option value="fab fa-reddit">Reddit</option>
                        <option value="fab fa-discord">Discord</option>
                        <option value="fab fa-facebook">Facebook</option>
                        <option value="fab fa-google-drive">Drive</option>
                        <option value="fas fa-envelope">Mail</option>
                        <option value="fas fa-music">Music</option>
                        <option value="fas fa-gamepad">Games</option>
                        <option value="fas fa-film">Movies</option>
                        <option value="fas fa-newspaper">News</option>
                        <option value="fas fa-shopping-cart">Shop</option>
                        <option value="custom-icon">Custom Icon</option>
                    </select>

                    <div id="custom-icon-options" class="custom-icon-option mt-3" style="display: none;">
                        <div class="flex space-x-4">
                            <div class="flex-1">
                                <label class="block mb-2 text-xs uppercase tracking-wider">Upload Icon</label>
                                <input type="file" id="icon-upload" class="w-full" accept="image/*">
                            </div>
                            <div class="flex-1">
                                <label class="block mb-2 text-xs uppercase tracking-wider">Icon URL</label>
                                <input type="url" id="icon-url" class="w-full p-2 rounded bg-[#0d0221]"
                                    placeholder="https://example.com/icon.png">
                            </div>
                        </div>
                        <img id="icon-preview" class="icon-preview" src="#" alt="Icon Preview">
                    </div>
                </div>

                <div>
                    <label class="block mb-2 neon-text-blue uppercase text-sm tracking-wider">Color</label>
                    <div class="color-picker-container neon-border-blue rounded-lg p-4">
                        <div class="color-option" style="background-color: #ff2a6d;"
                            onclick="selectPortalColor('#ff2a6d', this)"></div>
                        <div class="color-option selected" style="background-color: #05d9e8;"
                            onclick="selectPortalColor('#05d9e8', this)"></div>
                        <div class="color-option" style="background-color: #d300c5;"
                            onclick="selectPortalColor('#d300c5', this)"></div>
                        <div class="color-option" style="background-color: #00ff9d;"
                            onclick="selectPortalColor('#00ff9d', this)"></div>
                        <div class="color-option" style="background-color: #ffcc00;"
                            onclick="selectPortalColor('#ffcc00', this)"></div>
                        <div class="color-option" style="background-color: #ffffff;"
                            onclick="selectPortalColor('#ffffff', this)"></div>
                        <div class="color-option" style="background-color: #4267B2;"
                            onclick="selectPortalColor('#4267B2', this)"></div>
                        <div class="color-option" style="background-color: #9147ff;"
                            onclick="selectPortalColor('#9147ff', this)"></div>
                        <div class="custom-color-toggle w-full" onclick="togglePortalCustomColorInput()">
                            Custom Color
                        </div>
                        <input type="color" id="portal-custom-color" class="custom-color-input"
                            onchange="applyCustomPortalColor(this.value)">
                    </div>
                    <input type="hidden" id="portal-color" value="#05d9e8">
                </div>

                <div class="flex justify-end space-x-3">
                    <button type="button" onclick="document.getElementById('add-portal-modal').classList.add('hidden')"
                        class="px-4 py-2 rounded-lg border border-[#ff2a6d] hover:bg-[#ff2a6d] hover:text-white transition-all">
                        Cancel
                    </button>
                    <button type="submit"
                        class="px-6 py-2 neon-border-blue rounded-lg hover:bg-[#05d9e8] hover:text-[#0d0221] transition-all font-bold">
                        Create Portal
                    </button>
                </div>
            </form>
        </div>
    </div>
    
    <!-- Import/Export Modal -->
    <div id="import-export-modal" class="fixed inset-0 flex items-center justify-center z-50 hidden modal-overlay">
        <div class="modal-content neon-border-green rounded-xl p-8 max-w-md w-full mx-4 relative">
            <button onclick="document.getElementById('import-export-modal').classList.add('hidden')"
                class="absolute top-4 right-4 text-xl hover:text-[#ff2a6d] transition-all">×</button>
            <h2 class="text-2xl neon-text-green mb-6 uppercase tracking-wider">Import/Export Portals</h2>
            
            <div class="space-y-6">
                <div>
                    <h3 class="text-lg neon-text-blue mb-3">Export Portals</h3>
                    <textarea id="export-data" class="w-full h-32 p-3 rounded-lg bg-[#12092a] font-mono text-xs" readonly></textarea>
                    <button onclick="copyExportData()"
                        class="mt-2 px-4 py-2 neon-border-blue rounded-lg hover:bg-[#05d9e8] hover:text-[#0d0221] transition-all">
                        <i class="fas fa-copy mr-2"></i>Copy to Clipboard
                    </button>
                    <button onclick="downloadExportData()"
                        class="mt-2 px-4 py-2 neon-border-green rounded-lg hover:bg-[#00ff9d] hover:text-[#0d0221] transition-all">
                        <i class="fas fa-download mr-2"></i>Download JSON
                    </button>
                </div>
                
                <div>
                    <h3 class="text-lg neon-text-pink mb-3">Import Portals</h3>
                    <textarea id="import-data" class="w-full h-32 p-3 rounded-lg bg-[#12092a] font-mono text-xs" placeholder="Paste your portal data here..."></textarea>
                    <div class="flex space-x-3 mt-2">
                        <button onclick="importPortals()"
                            class="px-4 py-2 neon-border-pink rounded-lg hover:bg-[#ff2a6d] hover:text-white transition-all">
                            <i class="fas fa-file-import mr-2"></i>Import
                        </button>
                        <button onclick="document.getElementById('import-file').click()"
                            class="px-4 py-2 neon-border-purple rounded-lg hover:bg-[#d300c5] hover:text-white transition-all">
                            <i class="fas fa-upload mr-2"></i>Upload File
                        </button>
                        <input type="file" id="import-file" class="hidden" accept=".json">
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Terminal Modal -->
    <div id="terminal-modal" class="fixed inset-0 flex items-center justify-center z-50 hidden modal-overlay">
        <div class="modal-content neon-border-blue rounded-xl p-6 max-w-2xl w-full mx-4 relative h-96">
            <button onclick="document.getElementById('terminal-modal').classList.add('hidden')"
                class="absolute top-4 right-4 text-xl hover:text-[#ff2a6d] transition-all">×</button>
            <h2 class="text-xl neon-text-blue mb-4 uppercase tracking-wider">System Terminal</h2>
            
            <div id="terminal-container" class="h-full bg-black/80 rounded-lg p-4 overflow-y-auto font-mono text-sm">
                <div class="text-[#00ff9d]">Neon Portal Terminal v3.0</div>
                <div class="text-[#00ff9d]">Type 'help' for available commands</div>
                <div class="terminal-line mt-4">
                    <span class="text-[#00ff9d]">user@neonportal:~$ </span>
                    <span id="terminal-input" class="terminal-input" contenteditable="true"></span>
                    <span class="terminal-cursor">_</span>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Music Player Modal -->
    <div id="music-player-modal" class="fixed inset-0 flex items-center justify-center z-50 hidden modal-overlay">
        <div class="modal-content neon-border-pink rounded-xl p-6 max-w-md w-full mx-4 relative">
            <button onclick="document.getElementById('music-player-modal').classList.add('hidden')"
                class="absolute top-4 right-4 text-xl hover:text-[#ff2a6d] transition-all">×</button>
            <h2 class="text-xl neon-text-pink mb-4 uppercase tracking-wider">Neon Music Player</h2>
            
            <div class="text-center">
                <div id="music-cover" class="w-48 h-48 mx-auto mb-4 bg-[#12092a] rounded-lg flex items-center justify-center">
                    <i class="fas fa-music text-4xl text-[#ff2a6d]"></i>
                </div>
                
                <div id="music-info" class="mb-4">
                    <h3 id="music-title" class="text-lg font-bold neon-text-pink">No track selected</h3>
                    <p id="music-artist" class="text-sm">Unknown artist</p>
                </div>
                
                <div class="flex items-center justify-center mb-4">
                    <button id="prev-btn" class="mx-2 text-xl neon-text-pink hover:text-[#ff2a6d]">
                        <i class="fas fa-step-backward"></i>
                    </button>
                    <button id="play-btn" class="mx-2 text-3xl neon-text-pink hover:text-[#ff2a6d]">
                        <i class="fas fa-play"></i>
                    </button>
                    <button id="next-btn" class="mx-2 text-xl neon-text-pink hover:text-[#ff2a6d]">
                        <i class="fas fa-step-forward"></i>
                    </button>
                </div>
                
                <div class="mb-4">
                    <input type="range" id="progress-bar" class="w-full h-1 bg-[#12092a] rounded-lg appearance-none" min="0" max="100" value="0">
                    <div class="flex justify-between text-xs mt-1">
                        <span id="current-time">0:00</span>
                        <span id="duration">0:00</span>
                    </div>
                </div>
                
                <div class="flex justify-center space-x-4">
                    <button id="upload-music-btn" class="px-4 py-2 neon-border-pink rounded-lg hover:bg-[#ff2a6d] hover:text-white transition-all">
                        <i class="fas fa-upload mr-2"></i>Upload
                    </button>
                    <input type="file" id="music-upload" class="hidden" accept="audio/*">
                    
                    <button id="playlist-btn" class="px-4 py-2 neon-border-purple rounded-lg hover:bg-[#d300c5] hover:text-white transition-all">
                        <i class="fas fa-list mr-2"></i>Playlist
                    </button>
                </div>
            </div>
        </div>
    </div>
    
    <!-- System Monitor Modal -->
    <div id="system-monitor-modal" class="fixed inset-0 flex items-center justify-center z-50 hidden modal-overlay">
        <div class="modal-content neon-border-green rounded-xl p-6 max-w-md w-full mx-4 relative">
            <button onclick="document.getElementById('system-monitor-modal').classList.add('hidden')"
                class="absolute top-4 right-4 text-xl hover:text-[#ff2a6d] transition-all">×</button>
            <h2 class="text-xl neon-text-green mb-4 uppercase tracking-wider">System Monitor</h2>
            
            <div class="space-y-4">
                <div class="bg-[#12092a] rounded-lg p-4">
                    <h3 class="text-sm neon-text-blue mb-2 uppercase tracking-wider">CPU Usage</h3>
                    <div class="h-4 bg-[#0d0221] rounded-full overflow-hidden">
                        <div id="cpu-usage-bar" class="h-full bg-gradient-to-r from-[#05d9e8] to-[#00ff9d] rounded-full" style="width: 0%"></div>
                    </div>
                    <div class="flex justify-between text-xs mt-1">
                        <span>0%</span>
                        <span id="cpu-usage-text">0%</span>
                        <span>100%</span>
                    </div>
                </div>
                
                <div class="bg-[#12092a] rounded-lg p-4">
                    <h3 class="text-sm neon-text-pink mb-2 uppercase tracking-wider">Memory Usage</h3>
                    <div class="h-4 bg-[#0d0221] rounded-full overflow-hidden">
                        <div id="memory-usage-bar" class="h-full bg-gradient-to-r from-[#ff2a6d] to-[#d300c5] rounded-full" style="width: 0%"></div>
                    </div>
                    <div class="flex justify-between text-xs mt-1">
                        <span>0%</span>
                        <span id="memory-usage-text">0%</span>
                        <span>100%</span>
                    </div>
                </div>
                
                <div class="bg-[#12092a] rounded-lg p-4">
                    <h3 class="text-sm neon-text-purple mb-2 uppercase tracking-wider">Network Activity</h3>
                    <div class="flex justify-between text-xs mb-1">
                        <span><i class="fas fa-arrow-down text-[#05d9e8]"></i> <span id="network-down">0 KB/s</span></span>
                        <span><i class="fas fa-arrow-up text-[#ff2a6d]"></i> <span id="network-up">0 KB/s</span></span>
                    </div>
                </div>
                
                <div class="bg-[#12092a] rounded-lg p-4">
                    <h3 class="text-sm neon-text-blue mb-2 uppercase tracking-wider">System Info</h3>
                    <div class="grid grid-cols-2 gap-2 text-xs">
                        <div>
                            <span class="text-[#05d9e8]">Browser:</span> <span id="browser-info">Unknown</span>
                        </div>
                        <div>
                            <span class="text-[#ff2a6d]">OS:</span> <span id="os-info">Unknown</span>
                        </div>
                        <div>
                            <span class="text-[#00ff9d]">Screen:</span> <span id="screen-info">Unknown</span>
                        </div>
                        <div>
                            <span class="text-[#d300c5]">Online:</span> <span id="online-status">Unknown</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Quick Notes Modal -->
    <div id="quick-notes-modal" class="fixed inset-0 flex items-center justify-center z-50 hidden modal-overlay">
        <div class="modal-content neon-border-purple rounded-xl p-6 max-w-md w-full mx-4 relative h-96">
            <button onclick="document.getElementById('quick-notes-modal').classList.add('hidden')"
                class="absolute top-4 right-4 text-xl hover:text-[#ff2a6d] transition-all">×</button>
            <h2 class="text-xl neon-text-purple mb-4 uppercase tracking-wider">Quick Notes</h2>
            
            <div class="h-full flex flex-col">
                <div class="flex justify-between mb-2">
                    <select id="notes-select" class="bg-[#12092a] border border-[#d300c5] rounded px-2 py-1 text-sm">
                        <option value="new">New Note</option>
                    </select>
                    <button id="new-note-btn" class="px-3 py-1 neon-border-purple rounded hover:bg-[#d300c5] hover:text-white transition-all text-sm">
                        <i class="fas fa-plus mr-1"></i>New
                    </button>
                </div>
                
                <input type="text" id="note-title" class="w-full p-2 mb-2 bg-[#12092a] rounded border border-[#d300c5]" placeholder="Note title">
                
                <textarea id="note-content" class="flex-grow w-full p-3 bg-[#12092a] rounded border border-[#d300c5]" placeholder="Write your note here..."></textarea>
                
                <div class="flex justify-between mt-2">
                    <button id="delete-note-btn" class="px-3 py-1 border border-[#ff2a6d] rounded hover:bg-[#ff2a6d] hover:text-white transition-all text-sm">
                        <i class="fas fa-trash mr-1"></i>Delete
                    </button>
                    <button id="save-note-btn" class="px-3 py-1 neon-border-purple rounded hover:bg-[#d300c5] hover:text-white transition-all text-sm">
                        <i class="fas fa-save mr-1"></i>Save
                    </button>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Notifications Panel -->
    <div id="notifications-panel" class="fixed top-16 right-4 w-80 bg-[#0d0221] rounded-lg shadow-lg z-50 hidden neon-border-pink">
        <div class="p-4">
            <div class="flex justify-between items-center mb-3">
                <h3 class="text-lg neon-text-pink">Notifications</h3>
                <button onclick="clearNotifications()" class="text-xs hover:text-[#ff2a6d]">Clear All</button>
            </div>
            
            <div id="notifications-list" class="space-y-2 max-h-80 overflow-y-auto">
                <!-- Notifications will be added here -->
                <div class="text-center py-8 text-sm text-gray-400">
                    No new notifications
                </div>
            </div>
        </div>
    </div>

    <script>
        // Initialize default portals
        const defaultPortals = [
            { name: 'YouTube', url: 'https://youtube.com', icon: 'fab fa-youtube', color: '#ff0000' },
            { name: 'Twitter', url: 'https://twitter.com', icon: 'fab fa-twitter', color: '#1DA1F2' },
            { name: 'GitHub', url: 'https://github.com', icon: 'fab fa-github', color: '#ffffff' },
            { name: 'Reddit', url: 'https://reddit.com', icon: 'fab fa-reddit', color: '#FF5700' },
            { name: 'Discord', url: 'https://discord.com', icon: 'fab fa-discord', color: '#5865F2' },
            { name: 'Google Drive', url: 'https://drive.google.com', icon: 'fab fa-google-drive', color: '#34A853' },
            { name: 'Gmail', url: 'https://mail.google.com', icon: 'fas fa-envelope', color: '#EA4335' },
            { name: 'Spotify', url: 'https://open.spotify.com', icon: 'fas fa-music', color: '#1DB954' }
        ];

        // DOM elements
        const portalsGrid = document.getElementById('portals-grid');
        const portalForm = document.getElementById('portal-form');
        const portalCount = document.getElementById('portal-count');
        const mobileMenuButton = document.getElementById('mobile-menu-button');
        const mobileMenu = document.getElementById('mobile-menu');
        const timeDisplay = document.getElementById('time');
        const dateDisplay = document.getElementById('date');
        const portalIconSelect = document.getElementById('portal-icon');
        const customIconOptions = document.getElementById('custom-icon-options');
        const bgUpload = document.getElementById('bg-upload');
        const bgPreview = document.getElementById('bg-preview');
        const iconUpload = document.getElementById('icon-upload');
        const iconPreview = document.getElementById('icon-preview');
        const searchInput = document.getElementById('search-input');
        const searchResults = document.getElementById('search-results');
        const weatherBtn = document.getElementById('weather-btn');
        const weatherTemp = document.getElementById('weather-temp');
        const weatherIcon = document.getElementById('weather-icon');
        const weatherDescription = document.getElementById('weather-description');
        const weatherLocation = document.getElementById('weather-location');
        const weatherWind = document.getElementById('weather-wind');
        const weatherHumidity = document.getElementById('weather-humidity');
        const notificationCount = document.getElementById('notification-count');
        const notificationCountMobile = document.getElementById('notification-count-mobile');
        const notificationsPanel = document.getElementById('notifications-panel');
        const notificationsList = document.getElementById('notifications-list');
        const terminalModal = document.getElementById('terminal-modal');
        const terminalInput = document.getElementById('terminal-input');
        const terminalContainer = document.getElementById('terminal-container');
        const musicPlayerModal = document.getElementById('music-player-modal');
        const systemMonitorModal = document.getElementById('system-monitor-modal');
        const quickNotesModal = document.getElementById('quick-notes-modal');
        const loadingState = document.getElementById('loading-state');
        
        // Current state
        let portals = JSON.parse(localStorage.getItem('portals')) || defaultPortals;
        let currentThemeColor = '#05d9e8'; // Default neon blue
        let currentBgImage = localStorage.getItem('bgImage') || '';
        let notifications = JSON.parse(localStorage.getItem('notifications')) || [];
        let notes = JSON.parse(localStorage.getItem('notes')) || [];
        let currentNoteId = null;
        let audioContext = null;
        let audioElement = null;
        let isPlaying = false;
        let currentTrackIndex = 0;
        let tracks = [];
        let networkDownSpeed = 0;
        let networkUpSpeed = 0;
        let lastNetworkDown = 0;
        let lastNetworkUp = 0;
        let lastNetworkTime = 0;
        
        // Initialize the app
        document.addEventListener('DOMContentLoaded', function() {
            // Show loading state
            loadingState.classList.remove('hidden');
            
            // Initialize after a short delay to allow animations
            setTimeout(() => {
                renderPortals();
                updateTime();
                setInterval(updateTime, 1000);
                loadBackgroundImage();
                initMatrixRain();
                initSearch();
                loadWeather();
                updateNotifications();
                initSystemMonitor();
                loadNotes();
                
                // Hide loading state
                loadingState.classList.add('hidden');
            }, 1000);
            
            // Mobile menu toggle
            mobileMenuButton.addEventListener('click', function() {
                mobileMenu.classList.toggle('hidden');
            });
            
            // Event listeners for form
            portalForm.addEventListener('submit', handlePortalFormSubmit);
            
            // Show custom icon options when custom icon is selected
            portalIconSelect.addEventListener('change', function() {
                if (this.value === 'custom-icon') {
                    customIconOptions.style.display = 'block';
                } else {
                    customIconOptions.style.display = 'none';
                }
            });
            
            // Image preview for background upload
            bgUpload.addEventListener('change', function(e) {
                const file = e.target.files[0];
                if (file) {
                    const reader = new FileReader();
                    reader.onload = function(event) {
                        bgPreview.src = event.target.result;
                        bgPreview.style.display = 'block';
                    };
                    reader.readAsDataURL(file);
                }
            });
            
            // Image preview for custom icon upload
            iconUpload.addEventListener('change', function(e) {
                const file = e.target.files[0];
                if (file) {
                    const reader = new FileReader();
                    reader.onload = function(event) {
                        iconPreview.src = event.target.result;
                        iconPreview.style.display = 'block';
                    };
                    reader.readAsDataURL(file);
                }
            });
            
            // Close modals when clicking outside
            document.addEventListener('click', function(e) {
                if (e.target.classList.contains('modal-overlay')) {
                    e.target.classList.add('hidden');
                }
            });
            
            // Matrix rain toggle
            document.getElementById('matrix-toggle').addEventListener('change', function() {
                const matrixRain = document.getElementById('matrix-rain');
                if (this.checked) {
                    matrixRain.style.display = 'block';
                    initMatrixRain();
                } else {
                    matrixRain.style.display = 'none';
                }
            });
            
            // Terminal input handling
            terminalInput.addEventListener('keydown', function(e) {
                if (e.key === 'Enter') {
                    e.preventDefault();
                    const command = this.textContent.trim();
                    executeCommand(command);
                    this.textContent = '';
                }
            });
            
            // Music player controls
            document.getElementById('play-btn').addEventListener('click', togglePlay);
            document.getElementById('prev-btn').addEventListener('click', prevTrack);
            document.getElementById('next-btn').addEventListener('click', nextTrack);
            document.getElementById('progress-bar').addEventListener('input', seekAudio);
            document.getElementById('upload-music-btn').addEventListener('click', function() {
                document.getElementById('music-upload').click();
            });
            document.getElementById('music-upload').addEventListener('change', handleMusicUpload);
            document.getElementById('playlist-btn').addEventListener('click', showPlaylist);
            
            // Notes controls
            document.getElementById('new-note-btn').addEventListener('click', createNewNote);
            document.getElementById('save-note-btn').addEventListener('click', saveNote);
            document.getElementById('delete-note-btn').addEventListener('click', deleteNote);
            document.getElementById('notes-select').addEventListener('change', loadSelectedNote);
            
            // Import file handling
            document.getElementById('import-file').addEventListener('change', function(e) {
                const file = e.target.files[0];
                if (file) {
                    const reader = new FileReader();
                    reader.onload = function(event) {
                        document.getElementById('import-data').value = event.target.result;
                    };
                    reader.readAsText(file);
                }
            });
            
            // Add test notification
            addNotification('System', 'Neon Portal v3.0 initialized successfully', 'info');
        });
        
        // Render all portals
        function renderPortals() {
            portalsGrid.innerHTML = '';
            
            portals.forEach((portal, index) => {
                const portalElement = document.createElement('div');
                
                // Apply the portal's color for text and border glow
                const textColorStyle = `color: ${portal.color}; text-shadow: 0 0 5px ${portal.color}, 0 0 10px ${portal.color};`;
                const borderStyle = `border: 1px solid ${portal.color}; box-shadow: 0 0 5px ${portal.color}, inset 0 0 5px ${portal.color}, 0 0 20px ${portal.color};`;
                
                portalElement.innerHTML = `
                    <div class="portal-card h-full draggable-portal" draggable="true" data-index="${index}" style="${borderStyle}">
                        <a href="${portal.url}" target="_blank" class="block h-full p-6 rounded-lg text-center relative overflow-hidden backdrop-blur-sm bg-[#0d0221]/50 transition-all duration-300">
                            <div class="portal-card-inner">
                                ${portal.icon.startsWith('http') ? 
                                    `<img src="${portal.icon}" class="mx-auto h-12 w-12 mb-4" alt="${portal.name} icon">` : 
                                    `<i class="${portal.icon} text-4xl mb-4" style="${textColorStyle}"></i>`}
                                <h3 class="font-bold uppercase tracking-wider" style="${textColorStyle}">${portal.name}</h3>
                            </div>
                            <button onclick="deletePortal(${index}); event.preventDefault();" 
                                class="absolute top-1 right-1 text-xs text-red-500 hover:text-red-400">
                                <i class="fas fa-times"></i>
                            </button>
                        </a>
                    </div>
                `;
                
                portalsGrid.appendChild(portalElement);
            });
            
            // Update portal count
            portalCount.textContent = portals.length;
            
            // Make portals draggable
            initDragAndDrop();
        }
        
        // Initialize drag and drop for portals
        function initDragAndDrop() {
            const draggables = document.querySelectorAll('.draggable-portal');
            
            draggables.forEach(draggable => {
                draggable.addEventListener('dragstart', () => {
                    draggable.classList.add('dragging');
                });
                
                draggable.addEventListener('dragend', () => {
                    draggable.classList.remove('dragging');
                });
            });
            
            portalsGrid.addEventListener('dragover', e => {
                e.preventDefault();
                const afterElement = getDragAfterElement(portalsGrid, e.clientY);
                const draggable = document.querySelector('.dragging');
                if (draggable) {
                    if (afterElement == null) {
                        portalsGrid.appendChild(draggable);
                    } else {
                        portalsGrid.insertBefore(draggable, afterElement);
                    }
                }
            });
            
            // Save new order after drop
            portalsGrid.addEventListener('dragend', () => {
                const newOrder = Array.from(portalsGrid.children).map(el => {
                    return portals[parseInt(el.dataset.index)];
                });
                portals = newOrder;
                savePortals();
                
                // Update indices
                Array.from(portalsGrid.children).forEach((el, index) => {
                    el.dataset.index = index;
                });
            });
        }
        
        function getDragAfterElement(container, y) {
            const draggableElements = [...container.querySelectorAll('.draggable-portal:not(.dragging)')];
            
            return draggableElements.reduce((closest, child) => {
                const box = child.getBoundingClientRect();
                const offset = y - box.top - box.height / 2;
                if (offset < 0 && offset > closest.offset) {
                    return { offset: offset, element: child };
                } else {
                    return closest;
                }
            }, { offset: Number.NEGATIVE_INFINITY }).element;
        }
        
        // Handle form submission
        function handlePortalFormSubmit(e) {
            e.preventDefault();
            
            const name = document.getElementById('portal-name').value;
            const url = document.getElementById('portal-url').value;
            let icon = document.getElementById('portal-icon').value;
            const color = document.getElementById('portal-color').value;
            
            // Handle custom icon
            if (icon === 'custom-icon') {
                const iconUrl = document.getElementById('icon-url').value;
                const iconFile = document.getElementById('icon-upload').files[0];
                
                if (iconUrl) {
                    icon = iconUrl;
                } else if (iconFile) {
                    const reader = new FileReader();
                    reader.onload = function(e) {
                        // Convert image to base64 to store in local storage
                        icon = e.target.result;
                        addPortalToArray(name, url, icon, color);
                    };
                    reader.readAsDataURL(iconFile);
                    return; // Exit early as we'll call addPortalToArray in the callback
                } else {
                    addNotification('Error', 'Please provide an icon URL or upload an icon', 'error');
                    return;
                }
            }
            
            addPortalToArray(name, url, icon, color);
        }
        
        // Add a new portal to the array and update UI
        function addPortalToArray(name, url, icon, color) {
            const newPortal = {
                name: name,
                url: url,
                icon: icon,
                color: color
            };
            
            portals.push(newPortal);
            savePortals();
            renderPortals();
            document.getElementById('add-portal-modal').classList.add('hidden');
            resetPortalForm();
            
            addNotification('Portal Added', `Created new portal: ${name}`, 'success');
        }
        
        // Delete a portal
        function deletePortal(index) {
            if (confirm('Are you sure you want to delete this portal?')) {
                const portalName = portals[index].name;
                portals.splice(index, 1);
                savePortals();
                renderPortals();
                
                addNotification('Portal Deleted', `Removed portal: ${portalName}`, 'warning');
            }
        }
        
        // Reset portal form
        function resetPortalForm() {
            document.getElementById('portal-form').reset();
            customIconOptions.style.display = 'none';
            iconPreview.style.display = 'none';
            document.getElementById('portal-color').value = '#05d9e8';
        }
        
        // Save portals to localStorage
        function savePortals() {
            localStorage.setItem('portals', JSON.stringify(portals));
        }
        
        // Show add portal modal
        function showAddLinkModal() {
            document.getElementById('add-portal-modal').classList.remove('hidden');
            mobileMenu.classList.add('hidden');
        }
        
        // Show import/export modal
        function showImportExportModal() {
            document.getElementById('import-export-modal').classList.remove('hidden');
            document.getElementById('export-data').value = JSON.stringify(portals, null, 2);
            mobileMenu.classList.add('hidden');
        }
        
        // Copy export data to clipboard
        function copyExportData() {
            const exportData = document.getElementById('export-data');
            exportData.select();
            document.execCommand('copy');
            
            addNotification('Copied', 'Portal data copied to clipboard', 'info');
        }
        
        // Download export data as JSON file
        function downloadExportData() {
            const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(portals, null, 2));
            const downloadAnchor = document.createElement('a');
            downloadAnchor.setAttribute('href', dataStr);
            downloadAnchor.setAttribute('download', 'neon-portals.json');
            document.body.appendChild(downloadAnchor);
            downloadAnchor.click();
            document.body.removeChild(downloadAnchor);
            
            addNotification('Downloaded', 'Portal data exported to JSON file', 'success');
        }
        
        // Import portals from JSON
        function importPortals() {
            const importData = document.getElementById('import-data').value;
            
            try {
                const importedPortals = JSON.parse(importData);
                if (Array.isArray(importedPortals) && importedPortals.length > 0) {
                    if (confirm(`Import ${importedPortals.length} portals? This will replace your current portals.`)) {
                        portals = importedPortals;
                        savePortals();
                        renderPortals();
                        
                        addNotification('Imported', `Successfully imported ${importedPortals.length} portals`, 'success');
                        document.getElementById('import-export-modal').classList.add('hidden');
                    }
                } else {
                    throw new Error('Invalid portal data');
                }
            } catch (e) {
                addNotification('Import Error', 'Failed to parse portal data. Please check the format.', 'error');
                console.error('Import error:', e);
            }
        }
        
        // Update time display
        function updateTime() {
            const now = new Date();
            const timeString = now.toLocaleTimeString();
            const dateString = now.toLocaleDateString(undefined, { 
                weekday:
</html>
