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
        
        .currency-table {
            width: 100%;
            border-collapse: collapse;
            margin: 1.5rem 0;
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
            width: 20%;
        }
        
        .amount-column {
            text-align: right;
            font-family: 'Courier New', monospace;
            font-weight: bold;
            color: #2c3e50;
            width: 35%;
            padding: 12px;
            background: #f8f9fa;
            border-radius: 6px;
        }
        
        .currency-column {
            font-weight: bold;
            color: #2c3e50;
            width: 45%;
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
            }
            
            .usdt-input {
                width: 100%;
            }
            
            .currency-table {
                display: block;
                overflow-x: auto;
            }
            
            .usdt-column,
            .amount-column,
            .currency-column {
                white-space: nowrap;
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
                    <input type="number" class="usdt-input" id="usdt-input" placeholder="Enter USDT amount" value="1">
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
                        <td class="amount-column" id="php-amount">61.12</td>
                        <td class="currency-column">
                            Philippine Peso <span class="currency-symbol">(PHP)</span>
                            <div class="rate-info">Rate: 61.12 PHP per USDT</div>
                        </td>
                    </tr>
                    <tr>
                        <td class="usdt-column">1.00</td>
                        <td class="amount-column" id="thb-amount">39.28</td>
                        <td class="currency-column">
                            Thai Baht <span class="currency-symbol">(THB)</span>
                            <div class="rate-info">Rate: 39.28 THB per USDT</div>
                        </td>
                    </tr>
                    <tr>
                        <td class="usdt-column">1.00</td>
                        <td class="amount-column" id="vnd-amount">28,571.42</td>
                        <td class="currency-column">
                            Vietnamese Dong <span class="currency-symbol">(VND)</span>
                            <div class="rate-info">Rate: 28,571.42 VND per USDT</div>
                        </td>
                    </tr>
                    <tr>
                        <td class="usdt-column">1.00</td>
                        <td class="amount-column" id="myr-amount">5.19</td>
                        <td class="currency-column">
                            Malaysian Ringgit <span class="currency-symbol">(MYR)</span>
                            <div class="rate-info">Rate: 5.19 MYR per USDT</div>
                        </td>
                    </tr>
                    <tr>
                        <td class="usdt-column">1.00</td>
                        <td class="amount-column" id="idr-amount">17,031.25</td>
                        <td class="currency-column">
                            Indonesian Rupiah <span class="currency-symbol">(IDR)</span>
                            <div class="rate-info">Rate: 17,031.25 IDR per USDT</div>
                        </td>
                    </tr>
                </tbody>
            </table>
            
            <div class="note">
                <p><strong>Note:</strong> Exchange rates may change at any time. Please refer to the latest exchange rate during actual transactions.</p>
            </div>
            
            <div class="contact">
                <h3>Contact Us</h3>
                <p>If you have any questions or need help, please feel free to contact us</p>
                <p>TG: @FindJunS</p>
            </div>
        </div>
        
        <div class="footer">
            <p>&copy; USDT Converter. </p>
        </div>
    </div>

    <script>
        // 基础汇率数据（基于USDT的汇率）
        const baseExchangeRates = {
            'PHP': 55.56,   // 1 USDT = 55.56 PHP
            'THB': 35.71,   // 1 USDT = 35.71 THB
            'VND': 23809.52, // 1 USDT = 23,809.52 VND
            'MYR': 4.76,    // 1 USDT = 4.76 MYR
            'IDR': 15625    // 1 USDT = 15,625 IDR
        };

        // 倍率调整系数
        const multipliers = {
            'PHP': 1.10,    // 菲律宾 +10%
            'THB': 1.10,    // 泰国 +10%
            'VND': 1.20,    // 越南 +20%
            'MYR': 1.09,    // 马来西亚 +9%
            'IDR': 1.09     // 印尼 +9%
        };

        // 计算调整后的汇率
        const adjustedExchangeRates = {};
        for (const currency in baseExchangeRates) {
            adjustedExchangeRates[currency] = baseExchangeRates[currency] * multipliers[currency];
        }

        // 更新UTC时间
        function updateUTCTime() {
            const now = new Date();
            const utcTime = now.toUTCString().replace('GMT', 'UTC+00:00');
            document.getElementById('utc-time').textContent = utcTime;
        }
        
        // 计算转换后的金额
        function calculateConversion(usdtAmount, currency) {
            if (!usdtAmount || usdtAmount <= 0) return 0;
            
            const rate = adjustedExchangeRates[currency];
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
            
            // 更新USDT列
            document.querySelectorAll('.usdt-column').forEach(cell => {
                cell.textContent = usdtAmount.toFixed(2);
            });
            
            // 更新各货币金额
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
        });
    </script>
</body>
</html>
