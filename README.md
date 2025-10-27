<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>USDT Currency Converter</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: #333;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
        }
        
        header {
            background-color: rgba(44, 62, 80, 0.95);
            color: white;
            padding: 1rem 0;
            box-shadow: 0 2px 15px rgba(0,0,0,0.2);
            backdrop-filter: blur(10px);
        }
        
        .container {
            width: 90%;
            max-width: 1200px;
            margin: 0 auto;
        }
        
        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .logo {
            font-size: 1.5rem;
            font-weight: bold;
            color: #3498db;
        }
        
        .nav-links {
            display: flex;
            list-style: none;
        }
        
        .nav-links li {
            margin-left: 1.5rem;
        }
        
        .nav-links a {
            color: white;
            text-decoration: none;
            transition: color 0.3s;
            padding: 5px 10px;
            border-radius: 4px;
        }
        
        .nav-links a:hover {
            color: #3498db;
            background: rgba(255,255,255,0.1);
        }
        
        main {
            padding: 2rem 0;
        }
        
        .hero {
            background: rgba(255, 255, 255, 0.1);
            color: white;
            padding: 3rem 0;
            text-align: center;
            border-radius: 15px;
            margin-bottom: 2rem;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255,255,255,0.2);
        }
        
        .hero h1 {
            font-size: 2.5rem;
            margin-bottom: 1rem;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }
        
        .hero p {
            font-size: 1.2rem;
            max-width: 600px;
            margin: 0 auto;
            opacity: 0.9;
        }
        
        .content-section {
            background: rgba(255, 255, 255, 0.95);
            padding: 2rem;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            margin-bottom: 2rem;
            backdrop-filter: blur(10px);
        }
        
        .content-section h2 {
            color: #2c3e50;
            margin-bottom: 1rem;
            padding-bottom: 0.5rem;
            border-bottom: 2px solid #3498db;
        }
        
        .usdt-input-section {
            background: linear-gradient(135deg, #e8f4fd, #d4e6f1);
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 1.5rem;
            border-left: 4px solid #3498db;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .usdt-input-container {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .usdt-label {
            font-weight: bold;
            color: #2c3e50;
            font-size: 1.1rem;
            white-space: nowrap;
        }
        
        .usdt-input {
            flex: 1;
            padding: 12px 15px;
            border: 2px solid #3498db;
            border-radius: 8px;
            font-size: 1.1rem;
            transition: all 0.3s ease;
            background-color: #f0f8ff;
            box-shadow: inset 0 2px 4px rgba(0,0,0,0.1);
        }
        
        .usdt-input:focus {
            outline: none;
            border-color: #2980b9;
            box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.3);
            transform: scale(1.02);
        }
        
        .currency-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 1.5rem;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            border-radius: 10px;
            overflow: hidden;
        }
        
        .currency-table th {
            background: linear-gradient(135deg, #3498db, #2980b9);
            color: white;
            padding: 15px;
            text-align: left;
            font-weight: 600;
        }
        
        .currency-table td {
            padding: 15px;
            border-bottom: 1px solid #e0e0e0;
        }
        
        .currency-table tr:nth-child(even) {
            background-color: #f8f9fa;
        }
        
        .currency-table tr:hover {
            background-color: #e3f2fd;
            transform: translateY(-2px);
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .currency-table .currency-code {
            font-weight: bold;
            color: #2c3e50;
            width: 30%;
        }
        
        .currency-table .currency-amount {
            text-align: right;
            font-family: 'Courier New', monospace;
            width: 35%;
            font-weight: bold;
            color: #2c3e50;
        }
        
        .currency-table .currency-symbol {
            text-align: left;
            width: 35%;
            color: #7f8c8d;
        }
        
        .time-display {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
            padding: 15px;
            background: linear-gradient(135deg, #e8f4fd, #d4e6f1);
            border-radius: 10px;
            border-left: 4px solid #3498db;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .time-label {
            font-weight: bold;
            color: #2c3e50;
            font-size: 1.1rem;
        }
        
        .utc-time {
            font-family: 'Courier New', monospace;
            font-weight: bold;
            color: #e74c3c;
            background-color: #fff;
            padding: 8px 15px;
            border-radius: 8px;
            border: 1px solid #3498db;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        
        .info-note {
            margin-top: 1.5rem;
            padding: 15px;
            background: linear-gradient(135deg, #e8f4fd, #d4e6f1);
            border-left: 4px solid #3498db;
            border-radius: 8px;
            font-size: 0.9rem;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
        }
        
        footer {
            background-color: rgba(44, 62, 80, 0.95);
            color: white;
            text-align: center;
            padding: 1.5rem 0;
            margin-top: 2rem;
            backdrop-filter: blur(10px);
        }
        
        @media (max-width: 768px) {
            .nav-links {
                flex-direction: column;
                position: absolute;
                top: 70px;
                left: 0;
                width: 100%;
                background-color: rgba(44, 62, 80, 0.98);
                display: none;
                z-index: 1000;
            }
            
            .nav-links.active {
                display: flex;
            }
            
            .nav-links li {
                margin: 0;
                text-align: center;
                padding: 1rem;
                border-top: 1px solid rgba(255,255,255,0.1);
            }
            
            .menu-toggle {
                display: block;
                cursor: pointer;
                font-size: 1.5rem;
            }
            
            .hero h1 {
                font-size: 2rem;
            }
            
            .currency-table {
                display: block;
                overflow-x: auto;
            }
            
            .time-display {
                flex-direction: column;
                align-items: flex-start;
                gap: 10px;
            }
            
            .usdt-input-container {
                flex-direction: column;
                align-items: flex-start;
            }
            
            .usdt-input {
                width: 100%;
            }
            
            .container {
                width: 95%;
            }
        }
        
        .menu-toggle {
            display: none;
            color: white;
            font-size: 1.5rem;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .content-section {
            animation: fadeIn 0.8s ease-out;
        }
        
        .hero {
            animation: fadeIn 0.6s ease-out;
        }
    </style>
</head>
<body>
    <header>
        <div class="container">
            <nav>
                <div class="logo">USDT Converter</div>
                <div class="menu-toggle">☰</div>
                <ul class="nav-links">
                    <li><a href="#home">Home</a></li>
                    <li><a href="#services">Converter</a></li>
                    <li><a href="#contact">Contact</a></li>
                </ul>
            </nav>
        </div>
    </header>

    <main class="container">
        <section id="home" class="hero">
            <h1>USDT Currency Converter</h1>
            <p>Convert USDT to various currencies in real-time</p>
        </section>
        
        <section id="services" class="content-section">
            <h2>Currency Conversion Table</h2>
            <p>Enter USDT amount to convert to various currencies</p>
            
            <div class="time-display">
                <span class="time-label">Current Time (UTC+00:00):</span>
                <span class="utc-time" id="utc-time">Loading...</span>
            </div>
            
            <div class="usdt-input-section">
                <div class="usdt-input-container">
                    <span class="usdt-label">Enter USDT Amount:</span>
                    <input type="number" class="usdt-input" id="usdt-input" placeholder="Enter USDT amount" value="1">
                </div>
            </div>
            
            <table class="currency-table">
                <thead>
                    <tr>
                        <th>Currency</th>
                        <th>Amount</th>
                        <th>Symbol</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td class="currency-code">Philippine Peso (PHP)</td>
                        <td class="currency-amount" id="php-amount">0.00</td>
                        <td class="currency-symbol">₱</td>
                    </tr>
                    <tr>
                        <td class="currency-code">Thai Baht (THB)</td>
                        <td class="currency-amount" id="thb-amount">0.00</td>
                        <td class="currency-symbol">฿</td>
                    </tr>
                    <tr>
                        <td class="currency-code">Vietnamese Dong (VND)</td>
                        <td class="currency-amount" id="vnd-amount">0.00</td>
                        <td class="currency-symbol">₫</td>
                    </tr>
                    <tr>
                        <td class="currency-code">Malaysian Ringgit (MYR)</td>
                        <td class="currency-amount" id="myr-amount">0.00</td>
                        <td class="currency-symbol">RM</td>
                    </tr>
                    <tr>
                        <td class="currency-code">Indonesian Rupiah (IDR)</td>
                        <td class="currency-amount" id="idr-amount">0.00</td>
                        <td class="currency-symbol">Rp</td>
                    </tr>
                </tbody>
            </table>
            
            <div class="info-note">
                <p><strong>Note:</strong> Exchange rates may change at any time. Please refer to the latest exchange rate during actual transactions.</p>
            </div>
        </section>
        
        <section id="contact" class="content-section">
            <h2>Contact Us</h2>
            <p>If you have any questions or need help, please feel free to contact us</p>
            <p>TG: @FindJunS</p>
        </section>
    </main>

    <footer>
        <div class="container">
            <p>&copy; 2023 USDT Converter. All rights reserved.</p>
        </div>
    </footer>

    <script>
        // 汇率数据（基于USDT的汇率）
        const exchangeRates = {
            'PHP': 55.56,  // 1 USDT = 55.56 PHP
            'THB': 35.71,  // 1 USDT = 35.71 THB
            'VND': 23809.52, // 1 USDT = 23,809.52 VND
            'MYR': 4.76,   // 1 USDT = 4.76 MYR
            'IDR': 15625   // 1 USDT = 15,625 IDR
        };
        
        // 更新UTC时间
        function updateUTCTime() {
            const now = new Date();
            const utcTime = now.toUTCString().replace('GMT', 'UTC+00:00');
            document.getElementById('utc-time').textContent = utcTime;
        }
        
        // 计算转换后的金额
        function calculateConversion(usdtAmount, currency) {
            if (!usdtAmount || usdtAmount <= 0) return 0;
            
            const rate = exchangeRates[currency];
            if (!rate) return 0;
            
            // 根据不同货币格式化显示
            if (currency === 'VND' || currency === 'IDR') {
                return (usdtAmount * rate).toLocaleString('en-US', {
                    minimumFractionDigits: 0,
                    maximumFractionDigits: 0
                });
            } else {
                return (usdtAmount * rate).toLocaleString('en-US', {
                    minimumFractionDigits: 2,
                    maximumFractionDigits: 2
                });
            }
        }
        
        // 更新所有货币的显示结果
        function updateAllConversions() {
            const usdtAmount = parseFloat(document.getElementById('usdt-input').value) || 0;
            
            document.getElementById('php-amount').textContent = calculateConversion(usdtAmount, 'PHP');
            document.getElementById('thb-amount').textContent = calculateConversion(usdtAmount, 'THB');
            document.getElementById('vnd-amount').textContent = calculateConversion(usdtAmount, 'VND');
            document.getElementById('myr-amount').textContent = calculateConversion(usdtAmount, 'MYR');
            document.getElementById('idr-amount').textContent = calculateConversion(usdtAmount, 'IDR');
        }
        
        document.addEventListener('DOMContentLoaded', function() {
            // 初始化UTC时间
            updateUTCTime();
            setInterval(updateUTCTime, 1000);
            
            // 初始化转换结果
            updateAllConversions();
            
            // 为USDT输入框添加事件监听
            document.getElementById('usdt-input').addEventListener('input', updateAllConversions);
            
            // 移动端菜单切换
            const menuToggle = document.querySelector('.menu-toggle');
            const navLinks = document.querySelector('.nav-links');
            
            if (menuToggle) {
                menuToggle.addEventListener('click', function() {
                    navLinks.classList.toggle('active');
                });
            }
            
            // 平滑滚动
            document.querySelectorAll('a[href^="#"]').forEach(anchor => {
                anchor.addEventListener('click', function(e) {
                    e.preventDefault();
                    
                    const targetId = this.getAttribute('href');
                    const targetElement = document.querySelector(targetId);
                    
                    if (targetElement) {
                        window.scrollTo({
                            top: targetElement.offsetTop - 70,
                            behavior: 'smooth'
                        });
                        
                        if (window.innerWidth <= 768) {
                            navLinks.classList.remove('active');
                        }
                    }
                });
            });
        });
    </script>
</body>
</html>
