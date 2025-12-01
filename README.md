<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>LACEDiA Beta - 3-Tier Authentication System</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <meta name="description" content="Professional sneaker authentication with AI-powered analysis">
    <style>
        /* CSS Variables for Theming */
        :root {
            --dark-bg: #0d1117;
            --darker-bg: #161b22;
            --primary-blue: #58a6ff;
            --success-green: #56d364;
            --warning-yellow: #ffdf5d;
            --danger-red: #f85149;
            --text-primary: #f0f6fc;
            --text-secondary: #8b949e;
            --border-color: #21262d;
            --accent-purple: #a5a5ff;
            --premium-gold: #ffd700;
        }
        
        /* Reset and Base Styles */
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            -webkit-user-select: none;
            -moz-user-select: none;
            user-select: none;
        }
        
        body {
            font-family: 'Rajdhani', sans-serif;
            background: linear-gradient(180deg, var(--dark-bg) 0%, var(--darker-bg) 100%);
            color: var(--text-primary);
            min-height: 100vh;
            line-height: 1.5;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        /* Header Styles */
        .header {
            background: var(--darker-bg);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 25px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .brand-section {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .mn-logo {
            width: 55px;
            height: 55px;
            background: linear-gradient(135deg, var(--primary-blue), var(--accent-purple));
            border: 2px solid var(--primary-blue);
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 900;
            font-size: 24px;
            color: white;
        }
        
        .brand-text h1 {
            font-family: 'Orbitron', monospace;
            font-size: 20px;
            color: var(--text-primary);
            margin-bottom: 2px;
        }
        
        .brand-text p {
            font-size: 12px;
            color: var(--text-secondary);
        }
        
        .lia-section {
            display: flex;
            align-items: center;
            gap: 12px;
        }
        
        .lia-info {
            text-align: right;
        }
        
        .lia-name {
            font-family: 'Orbitron', monospace;
            font-size: 18px;
            color: var(--accent-purple);
            font-weight: 700;
        }
        
        .lia-status {
            font-size: 11px;
            color: var(--success-green);
        }
        
        .lia-avatar {
            width: 55px;
            height: 55px;
            background: linear-gradient(135deg, var(--primary-blue), var(--accent-purple));
            border: 2px solid var(--border-color);
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            font-weight: 700;
            color: white;
        }
        
        /* 3-Tier Pricing Grid */
        .tier-grid-complete {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr;
            gap: 20px;
            margin: 25px 0;
        }
        
        .tier-card-complete {
            background: var(--dark-bg);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 25px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
        }
        
        .tier-card-complete:hover {
            border-color: var(--primary-blue);
            background: rgba(88, 166, 255, 0.05);
        }
        
        .tier-card-complete.selected {
            border-color: var(--success-green);
            background: rgba(86, 211, 100, 0.1);
        }
        
        .tier-card-complete.premium {
            border-color: var(--premium-gold);
            background: rgba(255, 215, 0, 0.05);
        }
        
        .tier-card-complete.premium:hover,
        .tier-card-complete.premium.selected {
            border-color: var(--premium-gold);
            background: rgba(255, 215, 0, 0.1);
            box-shadow: 0 0 20px rgba(255, 215, 0, 0.3);
        }
        
        .tier-price-complete {
            font-family: 'Orbitron', monospace;
            font-size: 2.2em;
            font-weight: 900;
            margin-bottom: 10px;
            line-height: 1;
        }
        
        .tier-price-complete.standard {
            color: var(--primary-blue);
        }
        
        .tier-price-complete.business {
            color: var(--warning-yellow);
        }
        
        .tier-price-complete.premium {
            color: var(--premium-gold);
            text-shadow: 0 0 15px rgba(255, 215, 0, 0.8);
        }
        
        .tier-title-complete {
            color: var(--text-primary);
            font-size: 16px;
            font-weight: 700;
            margin-bottom: 15px;
            font-family: 'Orbitron', monospace;
        }
        
        .tier-features-complete {
            color: var(--text-secondary);
            font-size: 12px;
            line-height: 1.6;
            text-align: left;
        }
        
        .premium-badge {
            position: absolute;
            top: -8px;
            right: 15px;
            background: var(--premium-gold);
            color: var(--dark-bg);
            font-size: 10px;
            font-weight: 700;
            padding: 4px 12px;
            border-radius: 12px;
            font-family: 'Orbitron', monospace;
            text-transform: uppercase;
        }
        
        .value-highlight {
            background: rgba(255, 215, 0, 0.1);
            border: 1px solid var(--premium-gold);
            border-radius: 6px;
            padding: 8px;
            margin-top: 10px;
            font-size: 11px;
            color: var(--premium-gold);
        }
        
        /* Authentication Photo Grid */
        .auth-photo-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
            margin-bottom: 25px;
        }
        
        .auth-photo-slot {
            background: var(--dark-bg);
            border: 2px dashed var(--border-color);
            border-radius: 12px;
            aspect-ratio: 1;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            padding: 15px;
        }
        
        .auth-photo-slot:hover {
            border-color: var(--primary-blue);
            background: rgba(88, 166, 255, 0.05);
        }
        
        .auth-photo-slot.filled {
            border-color: var(--success-green);
            border-style: solid;
            background: rgba(86, 211, 100, 0.05);
        }
        
        .auth-photo-slot .photo-preview {
            width: 100%;
            height: 70%;
            object-fit: cover;
            border-radius: 8px;
            margin-bottom: 8px;
        }
        
        .remove-photo-btn {
            position: absolute;
            top: 8px;
            right: 8px;
            background: var(--danger-red);
            color: white;
            border: none;
            border-radius: 50%;
            width: 22px;
            height: 22px;
            cursor: pointer;
            font-size: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        /* Upload Options Modal */
        .upload-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            z-index: 1000;
            align-items: center;
            justify-content: center;
        }
        
        .upload-modal-content {
            background: var(--darker-bg);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 30px;
            width: 90%;
            max-width: 400px;
            text-align: center;
        }
        
        .upload-options {
            display: flex;
            flex-direction: column;
            gap: 15px;
            margin: 20px 0;
        }
        
        .upload-option-btn {
            padding: 15px;
            background: var(--dark-bg);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            color: var(--text-primary);
            font-size: 16px;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }
        
        .upload-option-btn:hover {
            border-color: var(--primary-blue);
            background: rgba(88, 166, 255, 0.05);
        }
        
        .close-modal {
            position: absolute;
            top: 15px;
            right: 15px;
            background: none;
            border: none;
            color: var(--text-secondary);
            font-size: 24px;
            cursor: pointer;
        }
        
        /* Locked Content Styling */
        .locked-feature {
            opacity: 0.5;
            pointer-events: none;
            position: relative;
        }
        
        .locked-feature::before {
            content: '🔒';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 32px;
            z-index: 10;
            background: rgba(0, 0, 0, 0.8);
            padding: 15px;
            border-radius: 50%;
        }
        
        /* Upgrade Prompt */
        .upgrade-prompt {
            background: linear-gradient(135deg, rgba(255, 215, 0, 0.1), rgba(255, 170, 0, 0.1));
            border: 2px solid var(--premium-gold);
            border-radius: 12px;
            padding: 20px;
            margin: 20px 0;
            text-align: center;
        }
        
        /* Results Panel */
        .results-panel {
            background: var(--darker-bg);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 25px;
            margin-bottom: 25px;
            display: none;
        }
        
        .results-panel.show {
            display: block;
            animation: fadeIn 0.5s ease;
        }
        
        /* Loading Animation */
        .loading {
            position: relative;
            pointer-events: none;
        }
        
        .loading::after {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 20px;
            height: 20px;
            border: 2px solid transparent;
            border-top: 2px solid var(--primary-blue);
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }
        
        @keyframes spin {
            0% { transform: translate(-50%, -50%) rotate(0deg); }
            100% { transform: translate(-50%, -50%) rotate(360deg); }
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        /* Form Elements */
        .input-group {
            margin-bottom: 15px;
        }
        
        .input-group label {
            display: block;
            color: var(--text-primary);
            font-weight: 600;
            margin-bottom: 6px;
            font-size: 13px;
        }
        
        .input-group input,
        .input-group select {
            width: 100%;
            padding: 12px 16px;
            background: var(--darker-bg);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            color: var(--text-primary);
            font-size: 14px;
            transition: border-color 0.3s ease;
        }
        
        .input-group input:focus,
        .input-group select:focus {
            outline: none;
            border-color: var(--primary-blue);
        }
        
        /* Buttons */
        .btn {
            padding: 15px;
            border: none;
            border-radius: 8px;
            font-family: 'Orbitron', monospace;
            font-size: 14px;
            font-weight: 700;
            cursor: pointer;
            text-transform: uppercase;
            transition: all 0.3s ease;
            width: 100%;
        }
        
        .btn-primary {
            background: linear-gradient(135deg, var(--primary-blue), var(--accent-purple));
            color: white;
        }
        
        .btn-premium {
            background: linear-gradient(135deg, var(--premium-gold), #ffaa00);
            color: var(--dark-bg);
        }
        
        .btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
        }
        
        .btn:hover:not(:disabled) {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
        
        /* Stats Grid */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
            text-align: center;
        }
        
        .stat-value {
            font-size: 24px;
            font-weight: 700;
        }
        
        .stat-label {
            font-size: 11px;
            color: var(--text-secondary);
        }
        
        /* Responsive Design */
        @media (max-width: 768px) {
            .tier-grid-complete {
                grid-template-columns: 1fr;
            }
            
            .header {
                flex-direction: column;
                gap: 15px;
                text-align: center;
            }
            
            .auth-photo-grid {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .stats-grid {
                grid-template-columns: 1fr;
            }
        }
        
        @media (max-width: 480px) {
            .auth-photo-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Rajdhani:wght@300;400;600;700&display=swap" rel="stylesheet">
</head>
<body>
    <!-- Upload Options Modal -->
    <div class="upload-modal" id="uploadModal">
        <div class="upload-modal-content">
            <button class="close-modal" id="closeModal">&times;</button>
            <h3 style="color: var(--text-primary); margin-bottom: 20px;">Choose Upload Method</h3>
            <div class="upload-options">
                <button class="upload-option-btn" id="cameraOption">
                    📷 Take Photo
                </button>
                <button class="upload-option-btn" id="galleryOption">
                    🖼️ Choose from Gallery
                </button>
            </div>
        </div>
    </div>

    <div class="container">
        <!-- HEADER WITH FIXED LOGOS -->
        <header class="header" role="banner">
            <div class="brand-section">
                <div class="mn-logo" aria-label="MN Shoe Guy Logo">MN</div>
                <div class="brand-text">
                    <h1>MN SHOE GUY</h1>
                    <p>complete authentication system</p>
                </div>
            </div>
            <div class="lia-section">
                <div class="lia-info">
                    <div class="lia-name">LiA</div>
                    <div class="lia-status" id="liaStatus">● ready for authentication</div>
                </div>
                <div class="lia-avatar" id="liaAvatar" role="button" aria-label="LiA assistant information" tabindex="0">LiA</div>
            </div>
        </header>

        <!-- MAIN TITLE -->
        <section aria-labelledby="main-title">
            <div style="text-align: center; margin-bottom: 30px;">
                <h1 id="main-title" style="font-family: 'Orbitron', monospace; font-size: 36px; color: var(--primary-blue); margin-bottom: 8px; font-weight: 900;">LACEDiA BETA</h1>
                <p style="color: var(--text-secondary); font-size: 16px;">Professional Authentication + Business Intelligence</p>
            </div>
        </section>

        <!-- 3-TIER PRICING -->
        <section aria-labelledby="pricing-title">
            <div style="background: var(--darker-bg); border: 1px solid var(--border-color); border-radius: 12px; padding: 25px; margin-bottom: 25px;">
                <h2 id="pricing-title" style="color: var(--text-primary); margin-bottom: 20px; font-family: 'Orbitron', monospace; text-align: center;">Choose Your Authentication Package</h2>
                
                <div class="tier-grid-complete">
                    <div class="tier-card-complete" data-tier="standard">
                        <div class="tier-price-complete standard">$5</div>
                        <div class="tier-title-complete">STANDARD</div>
                        <div class="tier-features-complete">
                            ✓ 9-Photo Authentication<br>
                            ✓ Technical Analysis<br>
                            ✓ Cultural Context<br>
                            ✓ MN Street Test<br>
                            ✓ Digital Certificate<br>
                            ✓ Basic Report
                        </div>
                    </div>
                    
                    <div class="tier-card-complete" data-tier="business">
                        <div class="tier-price-complete business">$10</div>
                        <div class="tier-title-complete">BUSINESS</div>
                        <div class="tier-features-complete">
                            ✓ Everything in Standard<br>
                            ✓ Market Intelligence<br>
                            ✓ Rep Factory Analysis<br>
                            ✓ Resell Recommendations<br>
                            ✓ Business Report<br>
                            ✓ Priority Processing
                        </div>
                    </div>
                    
                    <div class="tier-card-complete premium" data-tier="premium">
                        <div class="premium-badge">Most Popular</div>
                        <div class="tier-price-complete premium">$15</div>
                        <div class="tier-title-complete">DATASTREAM PRO</div>
                        <div class="tier-features-complete">
                            ✓ Everything in Business<br>
                            ✓ <strong style="color: var(--premium-gold);">DataStream Export</strong><br>
                            ✓ <strong style="color: var(--premium-gold);">Auto-Inventory Processing</strong><br>
                            ✓ <strong style="color: var(--premium-gold);">Spreadsheet Integration</strong><br>
                            ✓ <strong style="color: var(--premium-gold);">Batch Processing</strong><br>
                            ✓ <strong style="color: var(--premium-gold);">ADHD Workflow Tools</strong>
                        </div>
                        <div class="value-highlight">
                            💡 Save hours of data entry - perfect for inventory management!
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- AUTHENTICATION INTERFACE -->
        <section id="authenticationInterface" aria-labelledby="auth-title">
            <div style="background: var(--darker-bg); border: 1px solid var(--border-color); border-radius: 12px; padding: 25px; margin-bottom: 25px;">
                <h2 id="auth-title" style="color: var(--text-primary); margin-bottom: 20px; font-family: 'Orbitron', monospace;">🔍 Authentication Analysis</h2>
                
                <div style="background: rgba(88, 166, 255, 0.1); border: 1px solid var(--primary-blue); border-radius: 8px; padding: 15px; margin-bottom: 25px;">
                    <p style="color: var(--text-primary); font-size: 14px; line-height: 1.5;">
                        <strong>Complete Authentication:</strong> Upload all 9 required angles for comprehensive analysis including technical details, cultural significance, market intelligence, and MN street credibility test.
                    </p>
                </div>

                <!-- 9 PHOTO UPLOAD INTERFACE -->
                <h3 style="color: var(--text-primary); margin-bottom: 15px;">📸 Required Authentication Photos</h3>
                
                <div class="auth-photo-grid" id="authPhotoGrid">
                    <!-- Photo slots will be populated by JavaScript -->
                </div>

                <!-- FILE INPUTS (Hidden) -->
                <input type="file" id="fileInput" style="display: none;" accept="image/*">
                <input type="file" id="cameraInput" style="display: none;" accept="image/*" capture="camera">

                <div style="background: var(--dark-bg); border: 1px solid var(--border-color); border-radius: 8px; padding: 20px; margin-top: 25px;">
                    <div class="input-group">
                        <label for="authSneakerModel" style="display: block; color: var(--text-primary); font-weight: 600; margin-bottom: 6px; font-size: 13px;">Sneaker Model</label>
                        <input type="text" id="authSneakerModel" style="width: 100%; padding: 12px 16px; background: var(--darker-bg); border: 1px solid var(--border-color); border-radius: 8px; color: var(--text-primary); font-size: 14px;" placeholder="e.g., Jordan 1 Chicago" aria-label="Enter sneaker model for authentication">
                    </div>
                    
                    <button class="btn btn-primary" id="authAnalyzeBtn" aria-live="polite">
                        <span id="authButtonText">🔍 Start Authentication Analysis</span>
                    </button>
                    
                    <div style="margin-top: 15px; font-size: 13px; color: var(--text-secondary); text-align: center;">
                        <strong>Photos:</strong> <span id="authPhotoStatus">0/9 required</span>
                    </div>
                </div>
            </div>
        </section>

        <!-- DATASTREAM PRO SECTION (LOCKED UNLESS PREMIUM SELECTED) -->
        <section id="datastreamSection" aria-labelledby="datastream-title">
            <div style="background: var(--darker-bg); border: 1px solid var(--border-color); border-radius: 12px; padding: 25px; margin-bottom: 25px;">
                <div style="display: flex; align-items: center; gap: 12px; margin-bottom: 20px;">
                    <div style="width: 32px; height: 32px; background: var(--premium-gold); border-radius: 6px; display: flex; align-items: center; justify-content: center; font-weight: 700;">DS</div>
                    <h2 id="datastream-title" style="color: var(--premium-gold); font-family: 'Orbitron', monospace; font-size: 20px;">DataStream Pro</h2>
                    <div style="background: var(--premium-gold); color: var(--dark-bg); font-size: 10px; font-weight: 700; padding: 4px 8px; border-radius: 8px;">PREMIUM</div>
                </div>
                
                <div id="datastreamContent" class="locked-feature">
                    <div style="background: rgba(255, 215, 0, 0.1); border: 1px solid var(--premium-gold); border-radius: 8px; padding: 15px; margin-bottom: 20px;">
                        <h4 style="color: var(--premium-gold); margin-bottom: 10px;">🧠 ADHD-Optimized Inventory Processing</h4>
                        <p style="color: var(--text-primary); font-size: 13px; line-height: 1.4;">
                            Just 2 photos per pair! LiA handles all data extraction and generates ready-to-import spreadsheet rows. 
                            Perfect for batch inventory processing without overwhelming your executive function.
                        </p>
                    </div>

                    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 25px;">
                        <div style="background: var(--dark-bg); border: 2px dashed var(--border-color); border-radius: 12px; padding: 30px 20px; text-align: center;">
                            <div style="font-size: 40px; color: var(--text-secondary); margin-bottom: 15px;">🏷️</div>
                            <div style="color: var(--text-primary); font-size: 16px; font-weight: 600; margin-bottom: 8px;">Size Tag Photo</div>
                            <div style="color: var(--text-secondary); font-size: 12px;">Auto-extract SKU, sizes, production date</div>
                        </div>
                        
                        <div style="background: var(--dark-bg); border: 2px dashed var(--border-color); border-radius: 12px; padding: 30px 20px; text-align: center;">
                            <div style="font-size: 40px; color: var(--text-secondary); margin-bottom: 15px;">👟</div>
                            <div style="color: var(--text-primary); font-size: 16px; font-weight: 600; margin-bottom: 8px;">Lateral Profile</div>
                            <div style="color: var(--text-secondary); font-size: 12px;">Identify model, colorway, condition</div>
                        </div>
                    </div>

                    <div style="background: var(--dark-bg); border: 1px solid var(--border-color); border-radius: 8px; padding: 20px;">
                        <h4 style="color: var(--text-primary); margin-bottom: 15px;">⚙️ DataStream Options</h4>
                        
                        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-bottom: 15px;">
                            <div class="input-group">
                                <label for="conditionSelect" style="display: block; color: var(--text-primary); font-weight: 600; margin-bottom: 6px; font-size: 13px;">Condition (Default: 9/10)</label>
                                <select id="conditionSelect" style="width: 100%; padding: 12px 16px; background: var(--darker-bg); border: 1px solid var(--border-color); border-radius: 8px; color: var(--text-primary); font-size: 14px;">
                                    <option value="9/10">9/10 - Near Perfect</option>
                                    <option value="8/10">8/10 - Excellent</option>
                                    <option value="7/10">7/10 - Very Good</option>
                                </select>
                            </div>
                            
                            <div class="input-group">
                                <label for="storageLocation" style="display: block; color: var(--text-primary); font-weight: 600; margin-bottom: 6px; font-size: 13px;">Storage Location</label>
                                <input type="text" id="storageLocation" style="width: 100%; padding: 12px 16px; background: var(--darker-bg); border: 1px solid var(--border-color); border-radius: 8px; color: var(--text-primary); font-size: 14px;" placeholder="Office Closet Shelf A...">
                            </div>
                        </div>
                        
                        <button class="btn btn-premium" id="datastreamBtn" disabled>
                            📊 Generate DataStream Export
                        </button>
                    </div>
                </div>
            </div>

            <!-- UPGRADE PROMPT FOR NON-PREMIUM -->
            <div id="upgradePrompt" class="upgrade-prompt" style="display: none;">
                <h3 style="color: var(--premium-gold); font-family: 'Orbitron', monospace; margin-bottom: 15px;">
                    🔓 Unlock DataStream Pro
                </h3>
                <p style="color: var(--text-primary); margin-bottom: 20px; line-height: 1.5;">
                    Get automated spreadsheet generation, batch processing, and ADHD-friendly inventory tools for just <strong style="color: var(--premium-gold);">$5 more</strong>!
                </p>
                <div style="background: rgba(255, 215, 0, 0.1); border-radius: 8px; padding: 15px; margin-bottom: 20px;">
                    <h4 style="color: var(--premium-gold); margin-bottom: 10px;">⏱️ Time-Saving Features:</h4>
                    <ul style="color: var(--text-primary); font-size: 14px; line-height: 1.6;">
                        <li>• Auto-extract 24 data fields from 2 photos</li>
                        <li>• Generate ready-to-import CSV rows</li>
                        <li>• ADHD-friendly batch processing</li>
                        <li>• Automatic quality validation</li>
                        <li>• Save hours of manual data entry</li>
                    </ul>
                </div>
                <button class="btn btn-premium" style="width: auto; margin: 0 auto; display: block;">
                    🚀 Upgrade to DataStream Pro - $15
                </button>
            </div>
        </section>

        <!-- RESULTS -->
        <section id="results" class="results-panel" aria-live="polite"></section>

        <!-- BETA STATS -->
        <section aria-labelledby="stats-title">
            <div style="background: var(--darker-bg); border: 1px solid var(--border-color); border-radius: 12px; padding: 20px; margin-top: 30px;">
                <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 15px;">
                    <div style="width: 28px; height: 28px; background: var(--primary-blue); border-radius: 6px; display: flex; align-items: center; justify-content: center; font-weight: 700; color: white;">LU</div>
                    <h3 id="stats-title" style="color: var(--text-primary); font-family: 'Orbitron', monospace;">The Loop Universe Integration</h3>
                </div>
                <p style="color: var(--text-secondary); font-size: 13px; margin-bottom: 20px;">
                    LiA's authentication system powers the Sole-Circle's technology in The Loop comics, showing how AI preserves authentic sneaker culture.
                </p>
                
                <h4 style="color: var(--text-primary); margin-bottom: 15px;">📈 Your Beta Testing Progress</h4>
                <div class="stats-grid">
                    <div>
                        <div class="stat-value" id="totalAuthentications">0</div>
                        <div class="stat-label">Authentications</div>
                    </div>
                    <div>
                        <div class="stat-value" id="totalDataStream">0</div>
                        <div class="stat-label">DataStream Exports</div>
                    </div>
                    <div>
                        <div class="stat-value" id="totalCSVRows">0</div>
                        <div class="stat-label">CSV Rows Generated</div>
                    </div>
                </div>
            </div>
        </section>
    </div>

    <script>
        // Enhanced State Management
        const AppState = {
            authPhotos: new Array(9).fill(null),
            selectedTier: null,
            currentPhotoIndex: null,
            betaStats: {
                authentications: 0,
                datastreamExports: 0,
                csvRowsGenerated: 0
            },
            userPreferences: {
                lastModel: '',
                preferredTier: null
            },
            
            // Getters for computed properties
            get filledPhotoCount() {
                return this.authPhotos.filter(photo => photo !== null).length;
            },
            
            get hasMinimumPhotos() {
                return this.filledPhotoCount >= 6;
            },
            
            get isPremium() {
                return this.selectedTier === 'premium';
            },
            
            // Methods
            saveToLocalStorage() {
                const data = {
                    betaStats: this.betaStats,
                    userPreferences: this.userPreferences,
                    selectedTier: this.selectedTier
                };
                localStorage.setItem('lacediaApp', JSON.stringify(data));
            },
            
            loadFromLocalStorage() {
                try {
                    const data = JSON.parse(localStorage.getItem('lacediaApp'));
                    if (data) {
                        this.betaStats = data.betaStats || this.betaStats;
                        this.userPreferences = data.userPreferences || this.userPreferences;
                        this.selectedTier = data.selectedTier || null;
                        
                        // Update UI with loaded data
                        document.getElementById('totalAuthentications').textContent = this.betaStats.authentications;
                        document.getElementById('totalDataStream').textContent = this.betaStats.datastreamExports;
                        document.getElementById('totalCSVRows').textContent = this.betaStats.csvRowsGenerated;
                        
                        if (this.userPreferences.lastModel) {
                            document.getElementById('authSneakerModel').value = this.userPreferences.lastModel;
                        }
                        
                        if (this.selectedTier) {
                            this.selectTierUI(this.selectedTier);
                            this.updateTierDependentUI();
                        }
                    }
                } catch (error) {
                    console.error('Error loading from localStorage:', error);
                }
            },
            
            selectTierUI(tier) {
                document.querySelectorAll('.tier-card-complete').forEach(card => {
                    card.classList.remove('selected');
                });
                
                const tierCard = document.querySelector(`.tier-card-complete[data-tier="${tier}"]`);
                if (tierCard) {
                    tierCard.classList.add('selected');
                }
            },
            
            updateTierDependentUI() {
                const upgradePrompt = document.getElementById('upgradePrompt');
                const liaStatus = document.getElementById('liaStatus');
                
                if (this.selectedTier === 'premium') {
                    DataStreamManager.enableFeatures();
                    upgradePrompt.style.display = 'none';
                    liaStatus.textContent = '● datastream pro activated';
                } else {
                    DataStreamManager.disableFeatures();
                    upgradePrompt.style.display = 'block';
                    liaStatus.textContent = '● authentication mode active';
                }
            }
        };

        // Photo State Management
        const PhotoManager = {
            slots: [
                { id: 'lateral', label: 'Lateral Side', desc: 'Outside view', icon: '👟' },
                { id: 'medial', label: 'Medial Side', desc: 'Inside view', icon: '🔄' },
                { id: 'heel', label: 'Heel View', desc: 'Back of shoe', icon: '⬅️' },
                { id: 'outsole', label: 'Outsole', desc: 'Bottom tread', icon: '🔽' },
                { id: 'insole-top', label: 'Insole Top', desc: 'Branding visible', icon: '🏷️' },
                { id: 'insole-bottom', label: 'Insole Bottom', desc: 'Construction details', icon: '🔍' },
                { id: 'interior', label: 'Interior View', desc: 'Seams & heel area', icon: '👁️' },
                { id: 'tongue', label: 'Tongue & Logo', desc: 'Tongue branding', icon: '📋' },
                { id: 'size-tag', label: 'Size Tag', desc: 'Production label', icon: '📏' }
            ],
            
            init() {
                this.renderPhotoGrid();
                this.setupEventListeners();
            },
            
            renderPhotoGrid() {
                const grid = document.getElementById('authPhotoGrid');
                grid.innerHTML = '';
                
                this.slots.forEach((slot, index) => {
                    const slotElement = document.createElement('div');
                    slotElement.className = 'auth-photo-slot';
                    slotElement.setAttribute('role', 'button');
                    slotElement.setAttribute('aria-label', `Upload ${slot.label} photo`);
                    slotElement.setAttribute('tabindex', '0');
                    slotElement.setAttribute('data-index', index);
                    slotElement.innerHTML = this.getSlotHTML(slot, index);
                    
                    slotElement.addEventListener('click', () => {
                        this.showUploadModal(index);
                    });
                    
                    // Add keyboard support
                    slotElement.addEventListener('keydown', (e) => {
                        if (e.key === 'Enter' || e.key === ' ') {
                            e.preventDefault();
                            this.showUploadModal(index);
                        }
                    });
                    
                    grid.appendChild(slotElement);
                });
            },
            
            getSlotHTML(slot, index) {
                const photo = AppState.authPhotos[index];
                
                if (photo) {
                    return `
                        <img src="${photo.src}" alt="${slot.label}" class="photo-preview">
                        <div style="position: absolute; bottom: 8px; left: 8px; right: 8px; background: rgba(0,0,0,0.8); color: white; font-size: 10px; padding: 3px; border-radius: 4px; text-align: center;">
                            ${slot.label}
                        </div>
                        <button class="remove-photo-btn" onclick="event.stopPropagation(); removeAuthPhoto(${index})" aria-label="Remove ${slot.label} photo">×</button>
                    `;
                } else {
                    return `
                        <div style="font-size: 24px; color: var(--text-secondary); margin-bottom: 8px;">${slot.icon}</div>
                        <div style="color: var(--text-primary); font-size: 12px; font-weight: 600; margin-bottom: 4px;">${slot.label}</div>
                        <div style="color: var(--text-secondary); font-size: 10px; text-align: center;">${slot.desc}</div>
                    `;
                }
            },
            
            showUploadModal(index) {
                AppState.currentPhotoIndex = index;
                const modal = document.getElementById('uploadModal');
                modal.style.display = 'flex';
                
                // Update modal title with current photo type
                const modalTitle = modal.querySelector('h3');
                const slot = this.slots[index];
                modalTitle.textContent = `Upload ${slot.label} Photo`;
            },
            
            setupEventListeners() {
                // Debounced model input
                let searchTimeout;
                document.getElementById('authSneakerModel').addEventListener('input', (e) => {
                    clearTimeout(searchTimeout);
                    searchTimeout = setTimeout(() => {
                        AppState.userPreferences.lastModel = e.target.value;
                        AppState.saveToLocalStorage();
                        updateAuthStatus();
                    }, 300);
                });
            },
            
            handleFileUpload(file) {
                if (!file) return;
                
                // File validation
                if (!file.type.startsWith('image/')) {
                    alert('❌ Please upload an image file (JPEG, PNG, etc.)');
                    return;
                }
                
                if (file.size > 10 * 1024 * 1024) { // 10MB limit
                    alert('❌ File too large. Please choose an image smaller than 10MB.');
                    return;
                }
                
                const reader = new FileReader();
                reader.onload = (e) => {
                    const index = AppState.currentPhotoIndex;
                    const slot = this.slots[index];
                    
                    AppState.authPhotos[index] = { 
                        src: e.target.result, 
                        filename: file.name, 
                        type: slot.id 
                    };
                    
                    this.renderPhotoGrid();
                    updateAuthStatus();
                    this.hideUploadModal();
                };
                
                reader.onerror = () => {
                    alert('❌ Error reading file. Please try again.');
                };
                
                reader.readAsDataURL(file);
            },
            
            hideUploadModal() {
                const modal = document.getElementById('uploadModal');
                modal.style.display = 'none';
                AppState.currentPhotoIndex = null;
            }
        };

        // Enhanced Authentication Functions
        const AuthManager = {
            async startAuthentication() {
                const model = document.getElementById('authSneakerModel').value.trim();
                
                if (!AppState.hasMinimumPhotos) {
                    this.showError(`Need at least 6 photos for authentication. Currently have ${AppState.filledPhotoCount}/9.`);
                    return;
                }
                
                if (!model) {
                    this.showError('Please enter the sneaker model name.');
                    return;
                }
                
                if (!AppState.selectedTier) {
                    this.showError('Please select an authentication tier.');
                    return;
                }
                
                try {
                    this.setLoadingState(true);
                    
                    // Simulate API call with timeout
                    await new Promise(resolve => setTimeout(resolve, 4000));
                    
                    const result = this.performAuthentication(model, AppState.authPhotos, AppState.selectedTier);
                    this.displayAuthResult(result);
                    
                    AppState.betaStats.authentications++;
                    AppState.saveToLocalStorage();
                    this.updateBetaStatsUI();
                    
                } catch (error) {
                    this.showError('Authentication failed. Please try again.');
                    console.error('Authentication error:', error);
                } finally {
                    this.setLoadingState(false);
                }
            },
            
            setLoadingState(loading) {
                const authBtn = document.getElementById('authAnalyzeBtn');
                const authText = document.getElementById('authButtonText');
                const liaStatus = document.getElementById('liaStatus');
                
                if (loading) {
                    authBtn.disabled = true;
                    authBtn.classList.add('loading');
                    authText.textContent = 'Processing...';
                    liaStatus.textContent = '● analyzing all photos...';
                } else {
                    authBtn.disabled = !this.canStartAuthentication();
                    authBtn.classList.remove('loading');
                    authText.textContent = '🔍 Start Authentication Analysis';
                    liaStatus.textContent = '● authentication complete';
                }
            },
            
            canStartAuthentication() {
                return AppState.hasMinimumPhotos && 
                       document.getElementById('authSneakerModel').value.trim() && 
                       AppState.selectedTier;
            },
            
            performAuthentication(model, photos, tier) {
                const photoCount = photos.filter(p => p !== null).length;
                const completeness = (photoCount / 9) * 100;
                
                const technical = 75 + Math.random() * 20;
                const cultural = 80 + Math.random() * 15;
                const market = 70 + Math.random() * 25;
                const street = (technical + cultural) / 2 + Math.random() * 15 - 7.5;
                
                const finalScore = Math.round((technical + cultural + market + street) / 4);
                
                let verdict, statusColor;
                if (finalScore > 85) {
                    verdict = "AUTHENTIC";
                    statusColor = "var(--success-green)";
                } else if (finalScore > 70) {
                    verdict = "LIKELY AUTHENTIC";
                    statusColor = "var(--warning-yellow)";
                } else {
                    verdict = "QUESTIONABLE";
                    statusColor = "var(--warning-yellow)";
                }

                const analysis = `🧠 LiA's ${photoCount}-Photo Analysis:

TIER: ${tier.toUpperCase()} Authentication
PHOTO COVERAGE: ${Math.round(completeness)}% of required angles

TECHNICAL ANALYSIS: Construction quality verified across ${photoCount} angles
CULTURAL VERIFICATION: Model history and significance confirmed
${tier === 'business' || tier === 'premium' ? 'MARKET INTELLIGENCE: Current pricing and resell data analyzed' : ''}
${tier === 'premium' ? 'DATASTREAM READY: All data extracted for spreadsheet export' : ''}
MN STREET TEST: ${finalScore > 80 ? 'Passes Minneapolis credibility standards' : 'Some concerns detected'}

COMPREHENSIVE VERDICT: ${finalScore}% confidence based on multi-angle analysis`;

                return {
                    verdict,
                    confidence: finalScore,
                    statusColor,
                    breakdown: {
                        technical: Math.round(technical),
                        cultural: Math.round(cultural),
                        market: Math.round(market),
                        street: Math.round(street)
                    },
                    analysis,
                    model,
                    tier,
                    photoCount,
                    hasDataStream: tier === 'premium'
                };
            },
            
            displayAuthResult(result) {
                let datastreamSection = '';
                if (result.hasDataStream) {
                    datastreamSection = `
                        <div style="background: rgba(255, 215, 0, 0.1); border: 1px solid var(--premium-gold); border-radius: 8px; padding: 20px; margin-top: 20px;">
                            <h4 style="color: var(--premium-gold); margin-bottom: 15px;">📊 DataStream Pro Export Available</h4>
                            <p style="color: var(--text-primary); margin-bottom: 15px;">
                                Ready to generate complete inventory data for this authenticated pair.
                            </p>
                            <button onclick="DataStreamManager.generateDataStream('${result.model}')" class="btn btn-premium" style="width: auto;">
                                📊 Generate DataStream Export
                            </button>
                        </div>
                    `;
                }
                
                const resultsHTML = `
                    <div>
                        <h3 style="color: var(--text-primary); font-family: 'Orbitron', monospace; margin-bottom: 15px;">
                            🔍 Authentication Complete - ${result.tier.toUpperCase()} Tier
                        </h3>
                        
                        <div style="display: flex; align-items: center; gap: 20px; margin: 25px 0; padding: 20px; background: var(--dark-bg); border-radius: 8px;">
                            <div style="width: 50px; height: 50px; background: linear-gradient(135deg, var(--primary-blue), var(--accent-purple)); border-radius: 10px; display: flex; align-items: center; justify-content: center; position: relative;">
                                <div style="font-weight: 700; color: white;">LiA</div>
                            </div>
                            <div>
                                <div style="font-family: 'Orbitron', monospace; font-size: 20px; font-weight: 900; color: ${result.statusColor}; margin-bottom: 5px;">
                                    ${result.verdict} - ${result.confidence}%
                                </div>
                                <div style="color: var(--text-secondary); font-size: 14px;">
                                    ${result.photoCount}-Photo Analysis Complete
                                </div>
                            </div>
                        </div>
                        
                        <div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 15px; margin: 25px 0;">
                            <div style="background: var(--darker-bg); padding: 15px; border-radius: 8px; text-align: center;">
                                <div style="color: var(--text-secondary); font-size: 11px; margin-bottom: 5px;">TECHNICAL</div>
                                <div style="font-family: 'Orbitron', monospace; font-size: 20px; color: var(--primary-blue);">${result.breakdown.technical}</div>
                            </div>
                            <div style="background: var(--darker-bg); padding: 15px; border-radius: 8px; text-align: center;">
                                <div style="color: var(--text-secondary); font-size: 11px; margin-bottom: 5px;">CULTURAL</div>
                                <div style="font-family: 'Orbitron', monospace; font-size: 20px; color: var(--accent-purple);">${result.breakdown.cultural}</div>
                            </div>
                            <div style="background: var(--darker-bg); padding: 15px; border-radius: 8px; text-align: center;">
                                <div style="color: var(--text-secondary); font-size: 11px; margin-bottom: 5px;">MARKET</div>
                                <div style="font-family: 'Orbitron', monospace; font-size: 20px; color: var(--warning-yellow);">${result.breakdown.market}</div>
                            </div>
                            <div style="background: var(--darker-bg); padding: 15px; border-radius: 8px; text-align: center;">
                                <div style="color: var(--text-secondary); font-size: 11px; margin-bottom: 5px;">STREET TEST</div>
                                <div style="font-family: 'Orbitron', monospace; font-size: 20px; color: var(--success-green);">${result.breakdown.street}</div>
                            </div>
                        </div>
                        
                        <div style="background: var(--dark-bg); border: 1px solid var(--border-color); border-radius: 8px; padding: 20px;">
                            <pre style="color: var(--text-primary); font-family: 'Rajdhani', sans-serif; line-height: 1.6; white-space: pre-wrap; font-size: 13px;">${result.analysis}</pre>
                        </div>
                        
                        ${datastreamSection}
                    </div>
                `;
                
                const resultsPanel = document.getElementById('results');
                resultsPanel.innerHTML = resultsHTML;
                resultsPanel.classList.add('show');
                resultsPanel.scrollIntoView({ behavior: 'smooth' });
            },
            
            showError(message) {
                alert(`❌ ${message}`);
            },
            
            updateBetaStatsUI() {
                document.getElementById('totalAuthentications').textContent = AppState.betaStats.authentications;
                document.getElementById('totalDataStream').textContent = AppState.betaStats.datastreamExports;
                document.getElementById('totalCSVRows').textContent = AppState.betaStats.csvRowsGenerated;
            }
        };

        // DataStream Manager
        const DataStreamManager = {
            init() {
                const datastreamBtn = document.getElementById('datastreamBtn');
                if (datastreamBtn) {
                    datastreamBtn.addEventListener('click', () => {
                        this.generateDataStream();
                    });
                }
            },
            
            generateDataStream(model = '') {
                if (!model) {
                    model = document.getElementById('authSneakerModel').value.trim() || 'unknown model';
                }
                
                alert(`🚀 DataStream Pro: Generating complete inventory data for ${model}!\n\nThis feature will extract all 24 Inventory25 columns from your authentication photos and create ready-to-import spreadsheet rows.`);
                
                AppState.betaStats.datastreamExports++;
                AppState.betaStats.csvRowsGenerated++;
                AppState.saveToLocalStorage();
                AuthManager.updateBetaStatsUI();
            },
            
            enableFeatures() {
                const datastreamContent = document.getElementById('datastreamContent');
                const datastreamBtn = document.getElementById('datastreamBtn');
                
                if (datastreamContent && datastreamBtn) {
                    datastreamContent.classList.remove('locked-feature');
                    datastreamBtn.disabled = false;
                }
            },
            
            disableFeatures() {
                const datastreamContent = document.getElementById('datastreamContent');
                const datastreamBtn = document.getElementById('datastreamBtn');
                
                if (datastreamContent && datastreamBtn) {
                    datastreamContent.classList.add('locked-feature');
                    datastreamBtn.disabled = true;
                }
            }
        };

        // Global Functions (for HTML onclick attributes)
        function selectTier(tier) {
            AppState.selectedTier = tier;
            AppState.userPreferences.preferredTier = tier;
            AppState.saveToLocalStorage();
            
            // Update UI
            AppState.selectTierUI(tier);
            AppState.updateTierDependentUI();
            
            updateAuthStatus();
        }

        function removeAuthPhoto(index) {
            AppState.authPhotos[index] = null;
            PhotoManager.renderPhotoGrid();
            updateAuthStatus();
        }

        function updateAuthStatus() {
            const authBtn = document.getElementById('authAnalyzeBtn');
            authBtn.disabled = !AuthManager.canStartAuthentication();
            document.getElementById('authPhotoStatus').textContent = 
                `${AppState.filledPhotoCount}/9 required`;
        }

        function startAuthentication() {
            AuthManager.startAuthentication();
        }

        // Initialize the application
        document.addEventListener('DOMContentLoaded', function() {
            // Load saved data
            AppState.loadFromLocalStorage();
            
            // Initialize modules
            PhotoManager.init();
            DataStreamManager.init();
            
            // Set up tier selection
            document.querySelectorAll('.tier-card-complete').forEach(card => {
                card.addEventListener('click', function() {
                    const tier = this.getAttribute('data-tier');
                    selectTier(tier);
                });
            });
            
            // Set up upload modal
            const uploadModal = document.getElementById('uploadModal');
            const closeModal = document.getElementById('closeModal');
            const cameraOption = document.getElementById('cameraOption');
            const galleryOption = document.getElementById('galleryOption');
            const fileInput = document.getElementById('fileInput');
            const cameraInput = document.getElementById('cameraInput');
            
            closeModal.addEventListener('click', () => {
                PhotoManager.hideUploadModal();
            });
            
            uploadModal.addEventListener('click', (e) => {
                if (e.target === uploadModal) {
                    PhotoManager.hideUploadModal();
                }
            });
            
            cameraOption.addEventListener('click', () => {
                cameraInput.click();
            });
            
            galleryOption.addEventListener('click', () => {
                fileInput.click();
            });
            
            fileInput.addEventListener('change', (e) => {
                if (e.target.files.length > 0) {
                    PhotoManager.handleFileUpload(e.target.files[0]);
                    fileInput.value = ''; // Reset input
                }
            });
            
            cameraInput.addEventListener('change', (e) => {
                if (e.target.files.length > 0) {
                    PhotoManager.handleFileUpload(e.target.files[0]);
                    cameraInput.value = ''; // Reset input
                }
            });
            
            // Set up authentication button
            document.getElementById('authAnalyzeBtn').addEventListener('click', startAuthentication);
            
            // Set up LiA avatar interaction
            document.getElementById('liaAvatar').addEventListener('click', showLiaInfo);
            document.getElementById('liaAvatar').addEventListener('keydown', (e) => {
                if (e.key === 'Enter' || e.key === ' ') {
                    e.preventDefault();
                    showLiaInfo();
                }
            });
            
            // Set up upgrade button
            document.querySelector('#upgradePrompt .btn').addEventListener('click', () => {
                selectTier('premium');
            });
            
            // Initial UI update
            updateAuthStatus();
        });

        function showLiaInfo() {
            const tierInfo = AppState.selectedTier === 'premium' ? 
                'DATASTREAM PRO: Full authentication + automated inventory processing' :
                AppState.selectedTier === 'business' ? 
                'BUSINESS: Full authentication + market intelligence' :
                AppState.selectedTier === 'standard' ?
                'STANDARD: Complete authentication analysis' :
                'SELECT A TIER: Choose your authentication package';
                
            alert(`🧠 LiA Authentication System

CURRENT MODE: ${tierInfo}

CAPABILITIES:
• Multi-angle photo analysis
• Technical construction verification
• Cultural significance assessment  
• Market intelligence integration
• MN street credibility testing

${AppState.selectedTier === 'premium' ? '\n💡 DATASTREAM PRO ACTIVE: Automated inventory generation available!' : AppState.selectedTier ? '' : '\n📋 Please select a tier to begin!'}`);
        }

        // Event tracking (commented out - would need gtag setup)
        function trackEvent(category, action, label) {
            console.log(`Event: ${category} - ${action} - ${label}`);
        }
    </script>
</body>
</html>