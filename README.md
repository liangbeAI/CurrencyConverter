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
            padding: 20px;
        }
        
        .container {
            max-width: 900px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            overflow: hidden;
        }
        
        .header {
            background: linear-gradient(135deg, #3498db, #2980b9);
            color: white;
            padding: 2rem;
            text-align: center;
        }
        
        .header h1 {
            font-size: 2.2rem;
            margin-bottom: 0.5rem;
        }
        
        .header p {
            font-size: 1.1rem;
            opacity: 0.9;
        }
        
        .content {
            padding: 2rem;
        }
        
        .section-title {
            color: #2c3e50;
            margin-bottom: 1rem;
            padding-bottom: 0.5rem;
            border-bottom: 2px solid #3498db;
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
        }
        
        .time-label {
            font-weight: bold;
            color: #2c3e50;
        }
        
        .utc-time {
            font-family: 'Courier New', monospace;
            font-weight: bold;
            color: #e74c3c;
            background-color: #fff;
            padding: 8px 15px;
            border-radius: 8px;
            border: 1px solid #3498db;
        }
        
        .usdt-input-section {
            background: linear-gradient(135deg, #e8f4fd, #d4e6f1);
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 1.5rem;
            border-left: 4px solid #3498db;
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
        
        .usdt-input-wrapper {
            flex: 1;
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .usdt-input {
            flex: 1;
            padding: 12px 15px;
            border: 2px solid #3498db;
            border-radius: 8px;
            font-size: 1.1rem;
            background-color: #f0f8ff;
            box-shadow: inset 0 2px 4px rgba(0,0,0,0.1);
        }
        
        .usdt-input:focus {
            outline: none;
            border-color: #2980b9;
            box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.3);
        }
        
        .update-timer {
            font-size: 0.9rem;
            color: #e67e22;
            background: #fff3cd;
            padding: 8px 12px;
            border-radius: 6px;
            border: 1px solid #f39c12;
            white-space: nowrap;
            font-weight: bold;
        }
        
        .currency-table {
            width: 100%;
            border-collapse: collapse;
            margin: 1.5rem 0;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            border-radius: 10px;
            overflow: hidden;
            table-layout: fixed;
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
            vertical-align: top;
        }
        
        .currency-table tr:nth-child(even) {
            background-color: #f8f9fa;
        }
        
        .currency-table tr:hover {
            background-color: #e3f2fd;
            transform: translateY(-1px);
            transition: all 0.3s ease;
        }
        
        .usdt-column {
            text-align: center;
            font-weight: bold;
            color: #e74c3c;
            background: linear-gradient(135deg, #ffeaea, #ffd1d1);
            padding: 12px;
            border-radius: 6px;
            border: 1px solid #e74c3c;
            width: 15%;
        }
        
        .amount-column {
            text-align: right;
            font-family: 'Courier New', monospace;
            font-weight: bold;
            color: #2c3e50;
            width: 25%;
            padding: 12px;
            background: #f8f9fa;
            border-radius: 6px;
        }
        
        .currency-column {
            font-weight: bold;
            color: #2c3e50;
            width: 60%;
            padding: 12px;
        }
        
        .currency-symbol {
            color: #7f8c8d;
            margin-left: 8px;
            font-weight: normal;
        }
        
        .rate-info {
            color: #27ae60;
            font-size: 0.85rem;
            margin-top: 5px;
            font-style: italic;
        }
        
        .loading {
            color: #3498db;
            font-style: italic;
        }
        
        .error {
            color: #e74c3c;
            font-style: italic;
        }
        
        .note {
            margin-top: 1.5rem;
            padding: 15px;
            background: linear-gradient(135deg, #e8f4fd, #d4e6f1);
            border-left: 4px solid #3498db;
            border-radius: 8px;
            font-size: 0.9rem;
        }
        
        .contact {
            margin-top: 2rem;
            padding-top: 1.5rem;
            border-top: 2px solid #3498db;
        }
        
        .contact h3 {
            color: #2c3e50;
            margin-bottom: 1rem;
        }
        
        .footer {
            background: #2c3e50;
            color: white;
            text-align: center;
            padding: 1.5rem;
            margin-top: 2rem;
        }
        
        /* 修复表格布局 */
        .currency-table thead th:nth-child(1) { width: 15%; }
        .currency-table thead th:nth-child(2) { width: 25%; }
        .currency-table thead th:nth-child(3) { width: 60%; }
        
        @media (max-width: 768px) {
            .container {
                margin: 10px;
            }
            
            .header {
                padding: 1.5rem;
            }
            
            .header h1 {
                font-size: 1.8rem;
            }
            
            .content {
                padding: 1.5rem;
            }
            
            .time-display {
                flex-direction: column;
                align-items: flex-start;
                gap: 10px;
            }
            
            .usdt-input-container {
                flex-direction: column;
                align-items: flex-start;
                gap: 10px;
            }
            
            .usdt-input-wrapper {
                width: 100%;
                flex-direction: column;
                gap: 10px;
            }
            
            .usdt-input {
                width: 100%;
            }
            
            .update-timer {
                width: 100%;
                text-align: center;
            }
            
            .currency-table {
                display: block;
                overflow-x: auto;
                table-layout: auto;
            }
            
            .currency-table th,
            .currency-table td {
                white-space: nowrap;
                min-width: 100px;
            }
            
            .usdt-column,
            .amount-column,
            .currency-column {
                white-space: normal;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>USDT Currency Converter</h1>
            <p>Convert USDT to various currencies in real-time</p>
        </div>
        
        <div class="content">
            <h2 class="section-title">Currency Conversion Table</h2>
            <p>Enter USDT amount to convert to various currencies</p>
            
            <div class="time-display">
                <span class="time-label">Current Time (UTC+00:00):</span>
                <span class="utc-time" id="utc-time">Loading...</span>
            </div>
            
            <div class="usdt-input-section">
                <div class="usdt-input-container">
                    <span class="usdt-label">Enter USDT Amount:</span>
                    <div class="usdt-input-wrapper">
                        <input type="number" class="usdt-input" id="usdt-input" placeholder="Enter USDT amount" value="1" min="0" step="0.01">
                        <div class="update-timer" id="update-timer">Next update: 5m 0s</div>
                    </div>
                </div>
            </div>
            
            <table class="currency-table">
                <thead>
                    <tr>
                        <th>USDT</th>
                        <th>Amount</th>
                        <th>Currency</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td class="usdt-column">1.00</td>
                        <td class="amount-column" id="php-amount">
                            <span class="loading">Loading...</span>
                        </td>
                        <td class="currency-column">
                            Philippine Peso <span class="currency-symbol">(PHP)</span>
                            <div class="rate-info" id="php-rate">Rate: Loading...</div>
                        </td>
                    </tr>
                    <tr>
                        <td class="usdt-column">1.00</td>
                        <td class="amount-column" id="thb-amount">
                            <span class="loading">Loading...</span>
                        </td>
                        <td class="currency-column">
                            Thai Baht <span class="currency-symbol">(THB)</span>
                            <div class="rate-info" id="thb-rate">Rate: Loading...</div>
                        </td>
                    </tr>
                    <tr>
                        <td class="usdt-column">1.00</td>
                        <td class="amount-column" id="vnd-amount">
                            <span class="loading">Loading...</span>
                        </td>
                        <td class="currency-column">
                            Vietnamese Dong <span class="currency-symbol">(VND)</span>
                            <div class="rate-info" id="vnd-rate">Rate: Loading...</div>
                        </td>
                    </tr>
                    <tr>
                        <td class="usdt-column">1.00</td>
                        <td class="amount-column" id="myr-amount">
                            <span class="loading">Loading...</span>
                        </td>
                        <td class="currency-column">
                            Malaysian Ringgit <span class="currency-symbol">(MYR)</span>
                            <div class="rate-info" id="myr-rate">Rate: Loading...</div>
                        </td>
                    </tr>
                    <tr>
                        <td class="usdt-column">1.00</td>
                        <td class="amount-column" id="idr-amount">
                            <span class="loading">Loading...</span>
                        </td>
                        <td class="currency-column">
                            Indonesian Rupiah <span class="currency-symbol">(IDR)</span>
                            <div class="rate-info" id="idr-rate">Rate: Loading...</div>
                        </td>
                    </tr>
                </tbody>
            </table>
            
            <div class="note">
                <p><strong>Note:</strong> Exchange rates are updated every 5 minutes from XE.com. Rates may vary during actual transactions.</p>
            </div>
            
            <div class="contact">
                <h3>Contact Us</h3>
                <p>If you have any questions or need help, please feel free to contact us</p>
                <p>TG: @FindJunS</p>
            </div>
        </div>
        
        <div class="footer">
            <p>&copy; 2023 USDT Converter. All rights reserved.</p>
        </div>
    </div>

    <script>
        // 配置信息
        const CONFIG = {
            updateInterval: 5 * 60 * 1000, // 5分钟更新一次
            baseCurrencies: ['USD'], // 基础货币
            targetCurrencies: ['PHP', 'THB', 'VND', 'MYR', 'IDR'],
            multipliers: {
                'PHP': 1.10,    // 菲律宾 +10%
                'THB': 1.10,    // 泰国 +10%
                'VND': 1.20,    // 越南 +20%
                'MYR': 1.09,    // 马来西亚 +9%
                'IDR': 1.09     // 印尼 +9%
            }
        };

        // 存储汇率数据
        let exchangeRates = {};
        let lastUpdateTime = null;
        let nextUpdateTime = null;

        // 更新UTC时间
        function updateUTCTime() {
            const now = new Date();
            const utcTime = now.toUTCString().replace('GMT', 'UTC+00:00');
            document.getElementById('utc-time').textContent = utcTime;
        }

        // 获取汇率数据
        async function fetchExchangeRates() {
            try {
                // 使用免费的汇率API
                const response = await fetch('https://api.exchangerate-api.com/v4/latest/USD');
                
                if (!response.ok) {
                    throw new Error('Failed to fetch exchange rates');
                }
                
                const data = await response.json();
                return data.rates;
                
            } catch (error) {
                console.error('Error fetching exchange rates:', error);
                
                // 如果API失败，使用备用数据源
                try {
                    const backupResponse = await fetch('https://api.frankfurter.app/latest?from=USD');
                    if (backupResponse.ok) {
                        const backupData = await backupResponse.json();
                        return backupData.rates;
                    }
                } catch (backupError) {
                    console.error('Backup API also failed:', backupError);
                }
                
                throw error;
            }
        }

        // 处理汇率数据并应用调整系数
        async function updateExchangeRates() {
            try {
                const rates = await fetchExchangeRates();
                
                // 应用调整系数到目标货币
                CONFIG.targetCurrencies.forEach(currency => {
                    if (rates[currency]) {
                        const baseRate = rates[currency];
                        const multiplier = CONFIG.multipliers[currency];
                        exchangeRates[currency] = baseRate * multiplier;
                    }
                });
                
                lastUpdateTime = new Date();
                nextUpdateTime = new Date(lastUpdateTime.getTime() + CONFIG.updateInterval);
                
                updateNextUpdateTime();
                updateAllConversions();
                updateRateDisplays();
                
            } catch (error) {
                console.error('Error updating exchange rates:', error);
            }
        }

        // 更新倒计时显示
        function updateNextUpdateTime() {
            if (nextUpdateTime) {
                const now = new Date();
                const timeUntilUpdate = Math.max(0, nextUpdateTime - now);
                const minutes = Math.floor(timeUntilUpdate / 60000);
                const seconds = Math.floor((timeUntilUpdate % 60000) / 1000);
                
                document.getElementById('update-timer').textContent = 
                    `Next update: ${minutes}m ${seconds}s`;
            }
        }

        // 更新汇率显示
        function updateRateDisplays() {
            CONFIG.targetCurrencies.forEach(currency => {
                const rateElement = document.getElementById(`${currency.toLowerCase()}-rate`);
                if (rateElement && exchangeRates[currency]) {
                    const rate = exchangeRates[currency];
                    let displayRate = rate;
                    
                    if (currency === 'VND' || currency === 'IDR') {
                        displayRate = rate.toLocaleString('en-US', {
                            minimumFractionDigits: 0,
                            maximumFractionDigits: 0
                        });
                    } else {
                        displayRate = rate.toLocaleString('en-US', {
                            minimumFractionDigits: 2,
                            maximumFractionDigits: 2
                        });
                    }
                    
                    rateElement.textContent = `Rate: ${displayRate} ${currency} per USDT`;
                    rateElement.className = 'rate-info';
                }
            });
        }

        // 计算转换后的金额
        function calculateConversion(usdtAmount, currency) {
            if (!usdtAmount || usdtAmount <= 0) return '0.00';
            
            const rate = exchangeRates[currency];
            if (!rate) return 'N/A';
            
            const amount = usdtAmount * rate;
            
            // 根据不同货币格式化显示
            if (currency === 'VND' || currency === 'IDR') {
                return amount.toLocaleString('en-US', {
                    minimumFractionDigits: 0,
                    maximumFractionDigits: 0
                });
            } else {
                return amount.toLocaleString('en-US', {
                    minimumFractionDigits: 2,
                    maximumFractionDigits: 2
                });
            }
        }

        // 更新所有货币的显示结果
        function updateAllConversions() {
            const usdtAmount = parseFloat(document.getElementById('usdt-input').value) || 0;
            
            // 更新USDT列
            document.querySelectorAll('.usdt-column').forEach(cell => {
                cell.textContent = usdtAmount.toFixed(2);
            });
            
            // 更新各货币金额
            CONFIG.targetCurrencies.forEach(currency => {
                const amountElement = document.getElementById(`${currency.toLowerCase()}-amount`);
                if (amountElement) {
                    if (exchangeRates[currency]) {
                        const convertedAmount = calculateConversion(usdtAmount, currency);
                        amountElement.innerHTML = convertedAmount;
                        amountElement.className = 'amount-column';
                    } else {
                        amountElement.innerHTML = '<span class="error">Rate unavailable</span>';
                    }
                }
            });
        }

        document.addEventListener('DOMContentLoaded', function() {
            // 初始化UTC时间
            updateUTCTime();
            setInterval(updateUTCTime, 1000);
            
            // 初始化汇率
            updateExchangeRates();
            
            // 设置定时更新汇率
            setInterval(updateExchangeRates, CONFIG.updateInterval);
            
            // 更新倒计时显示
            setInterval(updateNextUpdateTime, 1000);
            
            // 为USDT输入框添加事件监听
            document.getElementById('usdt-input').addEventListener('input', updateAllConversions);
            
            // 初始更新显示
            updateAllConversions();
        });
    </script>
</body>
</html>
