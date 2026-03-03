<html>
<html lang="ar" dir="rtl" id="main-html">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PharmaLink-SUDAN</title>
    <style>
        :root { --primary: #0056b3; --secondary: #28a745; --light: #f4f7f6; }
        body { font-family: 'Segoe UI', sans-serif; margin: 0; background: var(--light); text-align: center; }
        header { background: var(--primary); color: white; padding: 40px 20px; box-shadow: 0 4px 12px rgba(0,0,0,0.1); }
        .search-container { margin: -25px auto 30px; max-width: 500px; padding: 0 20px; }
        input { width: 100%; padding: 15px; border-radius: 30px; border: 1px solid #ddd; box-shadow: 0 4px 6px rgba(0,0,0,0.1); font-size: 16px; }
        .results { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; padding: 20px 5%; }
        .card { background: white; padding: 20px; border-radius: 12px; box-shadow: 0 2px 8px rgba(0,0,0,0.05); }
        .lang-btn { background: var(--secondary); color: white; border: none; padding: 10px 20px; border-radius: 20px; cursor: pointer; position: absolute; top: 20px; left: 20px; }
        .en-mode { direction: ltr; }
        .en-mode .lang-btn { left: auto; right: 20px; }
    </style>
</head>
<body id="body-tag">

    <button class="lang-btn" onclick="toggleLang()">English / عربي</button>

    <header>
        <h1 id="title">فارمالينك السودان</h1>
        <p id="subtitle">نظام إدارة المخزون والبحث عن الأدوية</p>
    </header>

    <div class="search-container">
        <input type="text" id="searchInput" onkeyup="searchMedicine()" placeholder="ابحث عن دواء... / Search medicine...">
    </div>

    <div class="results" id="medicineList">
        </div>

    <script>
        // قاعدة بيانات تجريبية للأدوية
        const medicines = [
            { ar: "باندول", en: "Panadol", stock: 50, price: "1500 SDG" },
            { ar: "أموكسيسيلين", en: "Amoxicillin", stock: 12, price: "3000 SDG" },
            { ar: "أنسولين", en: "Insulin", stock: 5, price: "8000 SDG" },
            { ar: "فيتامين سي", en: "Vitamin C", stock: 100, price: "500 SDG" }
        ];

        let currentLang = 'ar';

        function displayMedicines(data) {
            const list = document.getElementById('medicineList');
            list.innerHTML = data.map(med => `
                <div class="card">
                    <h3>${currentLang === 'ar' ? med.ar : med.en}</h3>
                    <p>${currentLang === 'ar' ? 'المخزون' : 'Stock'}: ${med.stock}</p>
                    <p style="color: var(--primary); font-weight: bold;">${med.price}</p>
                </div>
            `).join('');
        }

        function searchMedicine() {
            const term = document.getElementById('searchInput').value.toLowerCase();
            const filtered = medicines.filter(med => 
                med.ar.includes(term) || med.en.toLowerCase().includes(term)
            );
            displayMedicines(filtered);
        }

        function toggleLang() {
            currentLang = currentLang === 'ar' ? 'en' : 'ar';
            const body = document.getElementById('body-tag');
            const html = document.getElementById('main-html');
            
            if(currentLang === 'en') {
                body.classList.add('en-mode');
                html.dir = "ltr";
                document.getElementById('title').innerText = "PharmaLink Sudan";
                document.getElementById('subtitle').innerText = "Inventory & Medicine Search System";
            } else {
                body.classList.remove('en-mode');
                html.dir = "rtl";
                document.getElementById('title').innerText = "فارمالينك السودان";
                document.getElementById('subtitle').innerText = "نظام إدارة المخزون والبحث عن الأدوية";
            }
            displayMedicines(medicines);
        }

        // عرض الأدوية عند تحميل الصفحة لأول مرة
        displayMedicines(medicines);
    </script>
</body>
</html>
