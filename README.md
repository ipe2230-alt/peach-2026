<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>大雪山紅寶石 - 精品水蜜桃預購</title>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Serif+TC:wght@700&family=Noto+Sans+TC&display=swap" rel="stylesheet">
    <style>
        :root { --primary-color: #1a3a32; --accent-color: #d4af37; }
        body {
            margin: 0; font-family: 'Noto Sans TC', sans-serif; color: white;
            background: linear-gradient(rgba(0,0,0,0.6), rgba(0,0,0,0.6)), 
                        url('DSC05348.jpg的真實網址') no-repeat center center fixed;
            background-size: cover;
        }
        h1, h2 { font-family: 'Noto Serif TC', serif; letter-spacing: 2px; }
        .container { max-width: 600px; margin: 50px auto; padding: 20px; }
        
        /* 玻璃擬態效果 */
        .glass-card {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 20px; padding: 30px;
            box-shadow: 0 8px 32px rgba(0,0,0,0.3);
        }

        .product-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-bottom: 20px; }
        .product-item { text-align: center; background: rgba(255,255,255,0.05); padding: 15px; border-radius: 15px; }
        .product-item img { width: 100%; border-radius: 10px; margin-bottom: 10px; }

        input, textarea {
            width: 100%; padding: 12px; margin: 8px 0; border-radius: 8px;
            border: 1px solid rgba(255,255,255,0.3); background: rgba(0,0,0,0.2); color: white;
        }

        .price-display { font-size: 1.2rem; color: var(--accent-color); margin: 20px 0; text-align: center; border-top: 1px solid rgba(255,255,255,0.2); pt: 15px; }

        .submit-btn {
            width: 100%; padding: 15px; background: var(--accent-color); color: #1a3a32;
            border: none; border-radius: 10px; font-weight: bold; cursor: pointer; font-size: 1.1rem;
        }
        
        .story-section { margin: 40px 0; text-align: center; }
        .story-section img { width: 100%; border-radius: 15px; margin-bottom: 10px; }
    </style>
</head>
<body>

<div class="container">
    <div class="glass-card">
        <h1 style="text-align: center;">大雪山紅寶石</h1>
        <p style="text-align: center; opacity: 0.8;">海拔 1,500m 耶穌光下的職人手摘</p>

        <form id="orderForm">
            <div class="product-grid">
                <div class="product-item">
                    <img src="DSC05394.jpg的真實網址" alt="8粒裝">
                    <h3>嚴選 8 粒裝</h3>
                    <p>$750 / 盒</p>
                    <input type="number" name="qty8" id="qty8" value="0" min="0" onchange="calculate()">
                </div>
                <div class="product-item">
                    <img src="DSC05345.jpg的真實網址" alt="6粒裝">
                    <h3>特級 6 粒裝</h3>
                    <p>$950 / 盒</p>
                    <input type="number" name="qty6" id="qty6" value="0" min="0" onchange="calculate()">
                </div>
            </div>

            <div class="story-section">
                <img src="DSC05341.jpg的真實網址" alt="果實特寫">
                <p>每一顆，都是陽光的結晶</p>
            </div>

            <div class="price-display" id="totalDisplay">總金額：$0</div>
            <input type="hidden" name="total" id="hiddenTotal" value="0">

            <input type="text" name="name" placeholder="收件人姓名" required>
            <input type="tel" name="phone" placeholder="連絡電話" required>
            <textarea name="address" placeholder="收件地址" rows="2" required></textarea>
            <input type="text" name="bank" placeholder="匯款帳號末五碼 (必填)" required>
            <textarea name="note" placeholder="備註 (如：希望到貨時段)"></textarea>

            <div style="background: rgba(0,0,0,0.3); padding: 15px; border-radius: 10px; margin: 15px 0; font-size: 0.9rem;">
                <p style="margin: 0; color: var(--accent-color);">💰 匯款資訊：</p>
                <p>銀行代碼：XXX (某某銀行)<br>帳號：XXXX-XXXX-XXXX<br>戶名：王OO</p>
                <p style="color: #ff6b6b; margin-top: 5px;">※ 請先匯款再送出表單，方便快速發貨。</p>
            </div>

            <button type="submit" class="submit-btn" id="submitBtn">確認送出訂單</button>
        </form>
    </div>
</div>

<script>
    const scriptURL = '這裡貼上你剛剛複製的GoogleAppsScript網址';
    const form = document.getElementById('orderForm');

    function calculate() {
        const q8 = parseInt(document.getElementById('qty8').value) || 0;
        const q6 = parseInt(document.getElementById('qty6').value) || 0;
        const totalQty = q8 + q6;
        
        // 邏輯：每兩盒折100
        const discount = Math.floor(totalQty / 2) * 100;
        const rawPrice = (q8 * 750) + (q6 * 950);
        const finalPrice = rawPrice - discount;

        document.getElementById('totalDisplay').innerText = `總金額：$${finalPrice} (已折抵 $${discount})`;
        document.getElementById('hiddenTotal').value = finalPrice;
    }

    form.addEventListener('submit', e => {
        e.preventDefault();
        if(document.getElementById('hiddenTotal').value == 0) return alert('請選擇訂購數量');
        
        document.getElementById('submitBtn').disabled = true;
        document.getElementById('submitBtn').innerText = '訂單傳送中...';

        fetch(scriptURL, { method: 'POST', body: new FormData(form)})
            .then(response => {
                alert('訂單已成功送出！我們將儘速與您聯繫。');
                form.reset();
                calculate();
                document.getElementById('submitBtn').disabled = false;
                document.getElementById('submitBtn').innerText = '確認送出訂單';
            })
            .catch(error => alert('送出失敗，請檢查網路或聯繫客服'));
    });
</script>

</body>
</html>
