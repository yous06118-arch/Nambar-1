<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Nambar 1 - Software by M/Youssef Mohammed</title>
    
    <link rel="apple-touch-icon" href="https://via.placeholder.com/192/00d2d3/000000?text=N1">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">

    <style>
        @import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap');
        :root { --main: #00d2d3; --bg: #0a0e12; --card: #161d24; --text: #ffffff; --danger: #ff4757; --success: #05c46b; --info: #3498db; }
        body { font-family: 'Cairo', sans-serif; background-color: var(--bg); color: var(--text); margin: 0; padding-bottom: 100px; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }
        
        #splash-screen { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: #000; display: flex; flex-direction: column; justify-content: center; align-items: center; z-index: 10000; transition: 0.6s ease-in-out; }
        .splash-logo { font-size: 3.5rem; color: var(--main); font-weight: bold; letter-spacing: 3px; text-shadow: 0 0 20px rgba(0, 210, 211, 0.5); animation: pulse 1.5s infinite; }
        .loader { width: 45px; height: 45px; border: 4px solid #111; border-top: 4px solid var(--main); border-radius: 50%; margin-top: 30px; animation: spin 1s linear infinite; }
        
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
        @keyframes pulse { 0% { transform: scale(0.95); opacity: 0.7; } 50% { transform: scale(1); opacity: 1; } 100% { transform: scale(0.95); opacity: 0.7; } }
        
        header { background: var(--card); padding: 20px; text-align: center; border-bottom: 3px solid var(--main); box-shadow: 0 4px 15px rgba(0,0,0,0.5); }
        .stats-bar { background: #1e272e; padding: 15px; text-align: center; color: var(--main); display: flex; justify-content: space-around; font-weight: bold; font-size: 13px; border-bottom: 1px solid #333; }
        
        .profit-box { background: var(--card); margin: 10px 15px; padding: 15px; border-radius: 12px; border: 2px solid var(--main); display: flex; flex-direction: column; align-items: center; gap: 10px; }
        .profit-header { width: 100%; display: flex; justify-content: space-between; align-items: center; }
        
        .tabs { display: flex; gap: 5px; padding: 10px; flex-wrap: wrap; }
        .tab-btn { flex: 1; min-width: 90px; padding: 10px; border: none; background: #222; color: white; border-radius: 10px; cursor: pointer; font-weight: bold; font-family: 'Cairo'; font-size: 12px; transition: 0.3s; }
        .tab-btn.active { background: var(--main); color: #000; box-shadow: 0 0 10px var(--main); }
        
        .container { padding: 0 15px; }
        .content { display: none; }
        .content.active { display: block; animation: fadeIn 0.5s ease; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        
        .input-card { background: var(--card); padding: 20px; border-radius: 15px; margin-bottom: 20px; border: 1px solid #333; }
        input { width: 100%; padding: 12px; margin: 8px 0; background: #2d3436; border: 1px solid #444; color: white; border-radius: 8px; box-sizing: border-box; font-family: 'Cairo'; outline: none; }
        
        .add-btn { width: 100%; padding: 15px; background: var(--main); border: none; border-radius: 8px; font-weight: bold; cursor: pointer; color: #000; font-size: 16px; margin-top: 10px; font-family: 'Cairo'; }
        
        .table-container { background: var(--card); border-radius: 12px; overflow-x: auto; border: 1px solid #333; }
        table { width: 100%; border-collapse: collapse; min-width: 400px; }
        th { background: #222; padding: 12px; text-align: right; color: var(--main); font-size: 12px; }
        td { padding: 12px; border-bottom: 1px solid #333; font-size: 13px; }
        
        .date-small { color: #888; font-size: 10px; display: block; margin-top: 4px; }
        .status { cursor: pointer; padding: 5px 8px; border-radius: 6px; font-size: 10px; background: #333; font-weight: bold; }
        .done { background: var(--success); color: white; }
        .delete-btn { background: none; border: none; color: var(--danger); cursor: pointer; font-size: 18px; }
        
        footer { position: fixed; bottom: 0; width: 100%; background: #161d24; color: #777; text-align: center; padding: 15px 0; border-top: 1px solid #333; font-size: 14px; z-index: 100; }
        .dev-name { color: var(--main); font-weight: bold; display: block; }
        .dev-phone { color: #888; font-size: 12px; margin-top: 3px; display: block; text-decoration: none; }
    </style>
</head>
<body onload="initApp()">

<div id="splash-screen">
    <div class="splash-logo">NAMBAR 1</div>
    <div style="color:#555; font-weight: bold; letter-spacing: 1px;">DESIGNED BY M/Youssef Mohammed</div>
    <div style="color:var(--main); font-size: 14px; margin-top: 5px;">01018240374</div>
    <div class="loader"></div>
</div>

<header>
    <h2 style="margin:0; color:var(--main);">NAMBAR 1</h2>
    <div style="font-size: 12px; color: #888;">أصل الصيانة - م/ وليد فضيل</div>
</header>

<div class="stats-bar">
    <div>إجمالي البيع: <span id="totalSales" style="color:var(--info)">0</span></div>
    <div>العمليات: <span id="totalOps">0</span></div>
</div>

<div class="profit-box">
    <div class="profit-header">
        <span style="font-weight: bold;">صافي أرباح المحل الكلية 💸</span>
        <button onclick="toggleProfit()" id="profitBtn" style="background:var(--success); border:none; color:white; padding:6px 15px; border-radius:8px; font-family:'Cairo'; font-weight:bold; cursor:pointer;">عرض</button>
    </div>
    <div id="totalProfitValue" style="display:none; font-size: 24px; color: var(--success); font-weight: bold;">0 ج.م</div>
</div>

<div class="tabs">
    <button class="tab-btn active" onclick="switchTab(event, 'mTab')">صيانة</button>
    <button class="tab-btn" onclick="switchTab(event, 'sTab')">سوفت وير</button>
    <button class="tab-btn" onclick="switchTab(event, 'aTab')">اكسسوارات</button>
</div>

<div class="container">
    <div id="mTab" class="content active">
        <div class="input-card">
            <input type="text" id="mCust" placeholder="اسم العميل">
            <input type="text" id="mDev" placeholder="الجهاز والعطل">
            <input type="number" id="mCost" placeholder="تكلفة قطع الغيار">
            <input type="number" id="mPrice" placeholder="سعر الصيانة النهائي">
            <button class="add-btn" onclick="saveData('m')">حفظ صيانة ✅</button>
        </div>
        <div class="table-container">
            <table id="mTable">
                <thead><tr><th>العميل/التاريخ</th><th>الجهاز</th><th>السعر</th><th>الحالة</th><th>🗑️</th></tr></thead>
                <tbody></tbody>
            </table>
        </div>
    </div>

    <div id="sTab" class="content">
        <div class="input-card">
            <input type="text" id="sCust" placeholder="اسم العميل">
            <input type="text" id="sDev" placeholder="نوع الجهاز">
            <input type="text" id="sOp" placeholder="العملية (سوفت، فك شفرة...)">
            <input type="number" id="sPrice" placeholder="سعر الخدمة">
            <button class="add-btn" style="background:#3498db" onclick="saveData('s')">حفظ سوفت وير 💻</button>
        </div>
        <div class="table-container">
            <table id="sTable">
                <thead><tr><th>العميل/التاريخ</th><th>الخدمة</th><th>السعر</th><th>الحالة</th><th>🗑️</th></tr></thead>
                <tbody></tbody>
            </table>
        </div>
    </div>

    <div id="aTab" class="content">
        <div class="input-card">
            <input type="text" id="aItem" placeholder="الصنف">
            <input type="number" id="aCost" placeholder="سعر الجملة">
            <input type="number" id="aPrice" placeholder="سعر البيع">
            <button class="add-btn" style="background:#05c46b" onclick="saveData('a')">تسجيل بيع 💰</button>
        </div>
        <div class="table-container">
            <table id="aTable">
                <thead><tr><th>الصنف/التاريخ</th><th>السعر</th><th>الوقت</th><th>🗑️</th></tr></thead>
                <tbody></tbody>
            </table>
        </div>
    </div>
</div>

<footer>
    Designed & Developed by <span class="dev-name">M/Youssef Mohammed</span>
    <a href="tel:01018240374" class="dev-phone">01018240374</a>
</footer>

<script>
    function initApp() { loadData(); setTimeout(() => { document.getElementById('splash-screen').style.display = 'none'; }, 2500); }

    function toggleProfit() {
        const p = document.getElementById('totalProfitValue');
        const b = document.getElementById('profitBtn');
        if(p.style.display === 'none') { p.style.display = 'block'; b.innerText = 'إخفاء'; } 
        else { p.style.display = 'none'; b.innerText = 'عرض'; }
    }

    function switchTab(evt, name) {
        document.querySelectorAll(".content").forEach(c => c.classList.remove("active"));
        document.querySelectorAll(".tab-btn").forEach(b => b.classList.remove("active"));
        document.getElementById(name).classList.add("active");
        evt.currentTarget.classList.add("active");
    }

    function saveData(type) {
        let db = JSON.parse(localStorage.getItem('nambar1_yousef_v4')) || { m: [], s: [], a: [] };
        const now = new Date();
        const dateStr = now.toLocaleDateString('ar-EG');
        const timeStr = now.toLocaleTimeString('ar-EG', {hour:'2-digit', minute:'2-digit'});

        if(type === 'm') {
            const p = parseFloat(document.getElementById('mPrice').value) || 0;
            const c = parseFloat(document.getElementById('mCost').value) || 0;
            if(!p) return alert("ادخل السعر");
            db.m.push({ name: document.getElementById('mCust').value, dev: document.getElementById('mDev').value, fullPrice: p, profit: p-c, status: 'قيد التصليح ⏳', date: dateStr });
        } else if(type === 's') {
            const p = parseFloat(document.getElementById('sPrice').value) || 0;
            if(!p) return alert("ادخل السعر");
            db.s.push({ name: document.getElementById('sCust').value, dev: document.getElementById('sDev').value, op: document.getElementById('sOp').value, fullPrice: p, profit: p, status: 'تم بنجاح ✅', date: dateStr });
        } else {
            const p = parseFloat(document.getElementById('aPrice').value) || 0;
            const c = parseFloat(document.getElementById('aCost').value) || 0;
            if(!p) return alert("ادخل السعر");
            db.a.push({ item: document.getElementById('aItem').value, fullPrice: p, profit: p-c, time: timeStr, date: dateStr });
        }

        localStorage.setItem('nambar1_yousef_v4', JSON.stringify(db));
        loadData();
        document.querySelectorAll('input').forEach(i => i.value = '');
    }

    function loadData() {
        let db = JSON.parse(localStorage.getItem('nambar1_yousef_v4')) || { m: [], s: [], a: [] };
        let sales = 0, profit = 0;

        let mBody = document.querySelector("#mTable tbody"); mBody.innerHTML = '';
        db.m.forEach((i, idx) => {
            mBody.innerHTML += `<tr><td>${i.name}<span class="date-small">${i.date}</span></td><td>${i.dev}</td><td style="color:var(--main)">${i.fullPrice} ج.م</td><td><span class="status ${i.status.includes('تم')?'done':''}" onclick="toggleStatus('m',${idx})">${i.status}</span></td><td><button class="delete-btn" onclick="deleteItem('m',${idx})">🗑️</button></td></tr>`;
            sales += i.fullPrice; profit += i.profit;
        });

        let sBody = document.querySelector("#sTable tbody"); sBody.innerHTML = '';
        db.s.forEach((i, idx) => {
            sBody.innerHTML += `<tr><td>${i.name}<span class="date-small">${i.date}</span></td><td>${i.op}</td><td style="color:var(--main)">${i.fullPrice} ج.م</td><td><span class="status done">${i.status}</span></td><td><button class="delete-btn" onclick="deleteItem('s',${idx})">🗑️</button></td></tr>`;
            sales += i.fullPrice; profit += i.profit;
        });

        let aBody = document.querySelector("#aTable tbody"); aBody.innerHTML = '';
        db.a.forEach((i, idx) => {
            aBody.innerHTML += `<tr><td>${i.item}<span class="date-small">${i.date}</span></td><td style="color:var(--main)">${i.fullPrice} ج.م</td><td>${i.time}</td><td><button class="delete-btn" onclick="deleteItem('a',${idx})">🗑️</button></td></tr>`;
            sales += i.fullPrice; profit += i.profit;
        });

        document.getElementById('totalSales').innerText = sales.toLocaleString() + " ج.م";
        document.getElementById('totalProfitValue').innerText = profit.toLocaleString() + " ج.م";
        document.getElementById('totalOps').innerText = db.m.length + db.s.length + db.a.length;
    }

    function toggleStatus(type, idx) {
        let db = JSON.parse(localStorage.getItem('nambar1_yousef_v4'));
        db[type][idx].status = db[type][idx].status.includes('تم') ? 'قيد التصليح ⏳' : 'تم التسليم ✅';
        localStorage.setItem('nambar1_yousef_v4', JSON.stringify(db));
        loadData();
    }

    function deleteItem(type, index) {
        if(confirm("حذف العملية؟")) {
            let db = JSON.parse(localStorage.getItem('nambar1_yousef_v4'));
            db[type].splice(index, 1);
            localStorage.setItem('nambar1_yousef_v4', JSON.stringify(db));
            loadData();
        }
    }
</script>
</body>
</html>
