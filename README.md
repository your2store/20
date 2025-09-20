# 20
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>أداة حساب عروض الأسعار</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-color: #0056b3;
            --primary-hover: #004494;
            --success-color: #28a745;
            --success-hover: #218838;
            --danger-color: #dc3545;
            --danger-hover: #c82333;
            --secondary-color: #6c757d;
            --secondary-hover: #5a6268;
            --light-gray: #f8f9fa;
            --border-color: #dee2e6;
            --shadow: 0 4px 15px rgba(0, 0, 0, 0.07);
            --border-radius: 8px;
        }

        body {
            font-family: 'Tajawal', sans-serif;
            background-color: #f0f2f5;
            color: #333;
            margin: 0;
            line-height: 1.6;
        }

        .app-container {
            max-width: 1600px;
            margin: 0 auto;
            padding: 20px;
        }

        .app-header {
            text-align: center;
            margin-bottom: 25px;
            color: var(--primary-color);
        }

        .app-header h1 {
            margin: 0;
            font-size: 2.5em;
        }

        .app-header p {
            font-size: 1.1em;
            color: #555;
        }

        .app-layout {
            display: grid;
            grid-template-columns: 1fr;
            gap: 25px;
        }

        @media (min-width: 1024px) {
            .app-layout {
                grid-template-columns: 1fr 450px;
            }
        }

        .panel {
            background: #fff;
            padding: 25px;
            border-radius: var(--border-radius);
            box-shadow: var(--shadow);
            border: 1px solid var(--border-color);
        }
        
        .panel h2 {
            margin-top: 0;
            border-bottom: 2px solid var(--primary-color);
            padding-bottom: 10px;
            font-size: 1.5em;
            color: var(--primary-color);
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .section {
            margin-bottom: 20px;
        }
        
        .section:last-child {
            margin-bottom: 0;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 700;
            color: #495057;
            font-size: 0.95em;
        }

        input[type="number"], input[type="text"], select, textarea {
            width: 100%;
            padding: 10px 12px;
            border: 1px solid var(--border-color);
            border-radius: 5px;
            box-sizing: border-box;
            font-size: 1em;
            font-family: 'Tajawal', sans-serif;
            transition: border-color 0.2s, box-shadow 0.2s;
        }

        input:focus, select:focus, textarea:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(0, 86, 179, 0.15);
        }

        .dimensions-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
        }
         .dimensions-grid .quantity-field {
            grid-column: 1 / -1;
        }

        .action-buttons {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 10px;
            margin-top: 20px;
        }

        button {
            padding: 12px 20px;
            border: none;
            border-radius: 5px;
            color: white;
            cursor: pointer;
            font-size: 1em;
            font-weight: 700;
            transition: background-color 0.2s, transform 0.1s;
        }

        button:hover {
            transform: translateY(-2px);
        }
        
        .btn-small {
            padding: 4px 8px;
            font-size: 0.8em;
            margin-right: 5px;
        }


        .btn-primary { background-color: var(--primary-color); }
        .btn-primary:hover { background-color: var(--primary-hover); }
        .btn-success { background-color: var(--success-color); }
        .btn-success:hover { background-color: var(--success-hover); }
        .btn-danger { background-color: var(--danger-color); }
        .btn-danger:hover { background-color: var(--danger-hover); }
        .btn-secondary { background-color: var(--secondary-color); }
        .btn-secondary:hover { background-color: var(--secondary-hover); }

        .results { margin-top: 20px; }
        .results-placeholder {
            text-align: center;
            padding: 50px 20px;
            color: #777;
            border: 2px dashed var(--border-color);
            border-radius: var(--border-radius);
        }
        .results-placeholder p { font-size: 1.2em; margin: 0; }

        .result-item {
            border: 1px solid var(--border-color);
            padding: 15px;
            margin-bottom: 15px;
            border-radius: var(--border-radius);
            background: var(--light-gray);
            position: relative;
        }

        .item-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }
        .item-header h4 { margin: 0; font-size: 1.2em; color: var(--primary-color); }

        .summary {
            border: 2px solid var(--primary-color);
            padding: 20px;
            margin-top: 20px;
            border-radius: var(--border-radius);
            background-color: var(--light-gray);
        }
        .summary-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 0;
            border-bottom: 1px solid var(--border-color);
            font-size: 1.1em;
        }
        .summary-row:last-child { border-bottom: none; }
        .summary-row span:first-child { font-weight: 500; color: #555; }
        .summary-row span:last-child { font-weight: 700; }
        
        .grand-total {
            background-color: var(--primary-color);
            color: white;
            padding: 20px;
            border-radius: 5px;
            text-align: center;
            margin-top: 15px;
        }
        .grand-total span { font-size: 1.3em; display: block; }
        .grand-total div { font-size: 2.2em; font-weight: bold; display: flex; align-items: center; justify-content: center; gap: 10px; }
        
        details {
            border: 1px solid var(--border-color);
            border-radius: 5px;
            padding: 10px;
        }
        summary { cursor: pointer; font-weight: 700; color: var(--primary-color); }
        .reference-table { width: 100%; border-collapse: collapse; margin-top: 10px; font-size: 0.9em; }
        .reference-table th, .reference-table td { border: 1px solid var(--border-color); padding: 8px; text-align: right; }
        .reference-table thead { background-color: #e9ecef; }
        
    </style>
</head>
<body>

<div class="app-container">
    <header class="app-header">
        <h1>أداة حساب عروض الأسعار</h1>
        <p>قم بإنشاء وتصدير عروض أسعار احترافية بكل سهولة</p>
    </header>

    <main class="app-layout">
        <div class="panel results-panel">
            <h2><span class="icon">📊</span> معاينة عرض السعر</h2>
            <div class="results" id="results">
                <div class="results-placeholder">
                    <p>لم يتم إضافة أي أصناف بعد</p>
                </div>
            </div>
        </div>

        <div class="panel form-panel">
            <h2><span class="icon">📝</span> تفاصيل الإدخال</h2>
            
            <div class="section">
              <label for="customerName">اسم العميل (اختياري - لاسم الملف):</label>
              <input type="text" id="customerName" placeholder="مثال: مشروع فلان الفلاني">
            </div>

            <div class="section">
                <label for="bulkAddText">لصق النص هنا (كل صنف في سطر):</label>
                <textarea id="bulkAddText" placeholder="مثال: W1-1-1.5-2.2-5" rows="4"></textarea>
                <button onclick="processPastedText()" style="width: 100%; margin-top: 10px;" class="btn-success">إضافة الأصناف من النص</button>
            </div>

            <div class="section" id="referenceContainer"></div>

            <p style="text-align: center; font-weight: bold; font-size: 1.2em; margin: 20px 0; color: #777;">-- أو أضف يدوياً --</p>

            <div class="section">
              <label for="mainCategory">الفئة الرئيسية:</label>
              <select id="mainCategory" onchange="loadSubTypes()"></select>
            </div>

            <div class="section">
              <label for="subType">النوع الفرعي:</label>
              <select id="subType" onchange="renderAddons()"></select>
            </div>

            <div class="section">
                <div class="dimensions-grid">
                    <div>
                        <label for="height">الارتفاع (م):</label>
                        <input type="number" id="height" step="0.01" value="1" />
                    </div>
                    <div>
                        <label for="width">العرض (م):</label>
                        <input type="text" id="width" value="1" placeholder="مثال: 5+2.5+3"/>
                    </div>
                    <div class="quantity-field">
                        <label for="quantity">الكمية:</label>
                        <input type="number" id="quantity" value="1" />
                    </div>
                </div>
            </div>

            <div class="section" id="addonsHost"></div>

            <div class="section">
                <label for="installationCost">تكلفة التركيب (ر.ع):</label>
                <input type="number" id="installationCost" value="0" step="0.01" onchange="renderResults()" />
            </div>
            
            <div class="action-buttons">
                <button onclick="addItem()" class="btn-primary">➕ إضافة صنف</button>
                <button onclick="clearAllResults()" class="btn-danger">🗑️ مسح الكل</button>
                <button onclick="saveAsWord()" class="btn-secondary">💾 حفظ كـ Word</button>
            </div>
        </div>
    </main>
</div>


<script>
const SHIPPING_RATE = 48;
const addonPrices = { 
    curtain: 26, 
    net: { door: 39, folding: 18, sliding: 14 } 
};

const productData = {
    "Windows": {
        "Window Double Glass Double Frame Fixed": { price: 34, cbm: 0.13, method: 'per_meter', addons: 'curtain,net' },
        "Window Double Glass Double Frame 1-Way": { price: 34, fixed_component_cost: 39, cbm: 0.13, method: 'per_meter', addons: 'curtain,net' },
        "Window Double Glass Double Frame 2-Way": { price: 34, fixed_component_cost: 58, cbm: 0.13, method: 'per_meter', addons: 'curtain,net' },
        "Window Double Glass Single Frame Fixed": { price: 26, cbm: 0.07, method: 'per_meter', addons: 'curtain,net' },
        "Window Double Glass Single Frame 1-Way": { price: 26, fixed_component_cost: 20, cbm: 0.07, method: 'per_meter', addons: 'curtain,net' },
        "Window Double Glass Single Frame 2-Way": { price: 26, fixed_component_cost: 32, cbm: 0.07, method: 'per_meter', addons: 'curtain,net' },
        "Window Single Glass Single Frame Fixed": { price: 20, cbm: 0.07, method: 'per_meter', addons: 'net' },
        "Window Single Glass Single Frame 1-Way": { price: 20, fixed_component_cost: 43, cbm: 0.07, method: 'per_meter', addons: 'net' },
        "Window Single Glass Single Frame 2-Way": { price: 20, fixed_component_cost: 47, cbm: 0.07, method: 'per_meter', addons: 'net' },
        "Sliding Windows": { price: 41, fixed_component_cost: 10, cbm: 0.13, method: 'per_meter', addons: 'curtain' },
        "Electric Windows": { price: 102, cbm: 0.13, method: 'per_meter' },
        "Skylight without Motor": { price: 56, cbm: 0.13, method: 'per_meter' },
        "Skylight with Motor": { price: 145, cbm: 0.13, method: 'per_meter' },
        "Heavy Curtain Wall": { price: 56, cbm: 0.15, method: 'per_meter' },
        "Light Curtain Wall": { price: 45, cbm: 0.15, method: 'per_meter' },
    },
    "Doors": {
        "Entrance Door - Zinc": { price: 66, cbm: 0.20, method: 'per_meter', special: 'add_10' },
        "Entrance Door - Stainless Steel": { price: 120, cbm: 0.20, method: 'per_meter', special: 'add_10' },
        "Entrance Door - Cast Aluminum": { price: 168, cbm: 0.20, method: 'per_meter', special: 'add_10' },
        "WPC Door": { price: 45, cbm: 0.11, method: 'per_unit', std_h: 2.2, std_w: 1.0 },
        "WPC Door - with Wood": { price: 50, cbm: 0.11, method: 'per_unit', std_h: 2.2, std_w: 1.0 },
        "WPC Door - with Soundproof Filling": { price: 60, cbm: 0.11, method: 'per_unit', std_h: 2.2, std_w: 1.0 },
        "WPC Door - with Aluminum Frame": { price: 67, cbm: 0.11, method: 'per_unit', std_h: 2.2, std_w: 1.0 },
        "Aluminum Door": { price: 65, cbm: 0.11, method: 'per_unit', std_h: 2.2, std_w: 1.0 },
        "Aluminum Door - with Wood": { price: 75, cbm: 0.11, method: 'per_unit', std_h: 2.2, std_w: 1.0 },
        "Aluminum Door - Full": { price: 85, cbm: 0.11, method: 'per_unit', std_h: 2.2, std_w: 1.0 },
        "Aluminum Door - Hidden": { price: 110, cbm: 0.11, method: 'per_unit', std_h: 2.2, std_w: 1.0 },
        "Aluminum Door - Exterior": { price: 61, cbm: 0.11, method: 'per_unit', std_h: 2.2, std_w: 1.0 },
        "Bathroom Door - New Type": { price: 55, cbm: 0.11, method: 'per_unit', std_h: 2.2, std_w: 0.8 },
        "Bathroom Door - Old Type": { price: 45, cbm: 0.11, method: 'per_unit', std_h: 2.2, std_w: 0.8 },
        "Bathroom Door - Hidden Glass": { price: 65, cbm: 0.11, method: 'per_unit', std_h: 2.2, std_w: 0.8 },
    },
    "Sliding Doors": {
        "Interior Sliding Door - Glass": { price: 38, cbm: 0.15, method: 'per_meter', addons: 'curtain' },
        "Interior Sliding Door - Solid": { price: 41, cbm: 0.15, method: 'per_meter' },
        "Exterior Sliding Door - 1 Panel Open": { price: 55, cbm: 0.15, method: 'per_meter' },
        "Exterior Sliding Door - 2 Panels Open": { price: 58, cbm: 0.15, method: 'per_meter' },
        "WPC Sliding Door": { price: 61, cbm: 0.15, method: 'per_meter' },
    },
    "Folding Doors": {
        "Interior Folding Door": { price: 39, cbm: 0.15, method: 'per_meter' },
        "Exterior Folding Door": { price: 56, cbm: 0.15, method: 'per_meter' },
    },
    "Exterior Shutters": {
        "Rolling Shutter": { price: 28, cbm: 0.20, method: 'per_meter' },
    },
    "Garden Gates": {
        "Cast Aluminum Garden Gate": { price: 91, cbm: 0.20, method: 'per_meter' },
    },
    "Barriers": {
        "Balcony Barriers - حواجز البلكونة": { price: 33, cbm: 0.05, method: 'per_meter' },
        "Fixed Bathroom Barriers - حواجز دورات مياه ثابت": { price: 18, cbm: 0.05, method: 'per_meter' },
        "Sliding Bathroom Barriers - حواجز دورات مياه سلايد": { price: 23, cbm: 0.05, method: 'per_meter' },
        "Stainless Steel Pool Barriers - حواجز المسبح ستينلس ستيل": { price: 19, cbm: 0.05, method: 'per_meter' },
        "Stainless Steel Pool Barriers with Glass - حواجز المسبح ستينلس ستيل مع زجاج": { price: 30, cbm: 0.05, method: 'per_meter' }
    }
};

const productCodes = {
    '1': "Window Double Glass Double Frame Fixed", '2': "Window Double Glass Double Frame 1-Way", '3': "Window Double Glass Double Frame 2-Way",
    '4': "Window Double Glass Single Frame Fixed", '5': "Window Double Glass Single Frame 1-Way", '6': "Window Double Glass Single Frame 2-Way",
    '7': "Window Single Glass Single Frame Fixed", '8': "Window Single Glass Single Frame 1-Way", '9': "Window Single Glass Single Frame 2-Way",
    '10': "Sliding Windows", '11': "Electric Windows", '12': "Skylight without Motor", '13': "Skylight with Motor", '14': "Heavy Curtain Wall", '15': "Light Curtain Wall",
    'D1': "Entrance Door - Zinc", 'D2': "Entrance Door - Stainless Steel", 'D3': "Entrance Door - Cast Aluminum",
    'D4': "WPC Door", 'D5': "WPC Door - with Wood", 'D6': "WPC Door - with Soundproof Filling", 'D7': "WPC Door - with Aluminum Frame",
    'D8': "Aluminum Door", 'D9': "Aluminum Door - with Wood", 'D10': "Aluminum Door - Full", 'D11': "Aluminum Door - Hidden", 'D12': "Aluminum Door - Exterior",
    'D13': "Bathroom Door - New Type", 'D14': "Bathroom Door - Old Type", 'D15': "Bathroom Door - Hidden Glass",
    'S1': "Interior Sliding Door - Glass", 'S2': "Interior Sliding Door - Solid", 'S3': "Exterior Sliding Door - 1 Panel Open", 'S4': "Exterior Sliding Door - 2 Panels Open", 'S5': "WPC Sliding Door",
    'F1': "Interior Folding Door", 'F2': "Exterior Folding Door",
    'E1': "Rolling Shutter", 'G1': "Cast Aluminum Garden Gate",
    'B1': "Balcony Barriers - حواجز البلكونة",
    'B2': "Fixed Bathroom Barriers - حواجز دورات مياه ثابت",
    'B3': "Sliding Bathroom Barriers - حواجز دورات مياه سلايد",
    'B4': "Stainless Steel Pool Barriers - حواجز المسبح ستينلس ستيل",
    'B5': "Stainless Steel Pool Barriers with Glass - حواجز المسبح ستينلس ستيل مع زجاج"
};

let resultsList = [];
let overrideGrandTotal = null;
let isEditingGrandTotal = false;

function initializeApp() {
    const mainCat = document.getElementById("mainCategory");
    mainCat.innerHTML = `<option value="">-- اختر فئة --</option>`;
    Object.keys(productData).forEach(cat => mainCat.innerHTML += `<option value="${cat}">${cat}</option>`);
    loadSubTypes();
    renderReferenceGuide();
    loadResultsFromLocalStorage();
}

function loadSubTypes() {
    const mainCatVal = document.getElementById("mainCategory").value;
    const subType = document.getElementById("subType");
    subType.innerHTML = "";
    if (mainCatVal && productData[mainCatVal]) {
        Object.keys(productData[mainCatVal]).forEach(sub => subType.innerHTML += `<option value="${sub}">${sub}</option>`);
    }
    renderAddons();
}

function renderAddons() {
    const mainCatVal = document.getElementById("mainCategory").value;
    const subVal = document.getElementById("subType").value;
    const addonsHost = document.getElementById("addonsHost");
    addonsHost.innerHTML = "";
    
    if (mainCatVal === "Doors") {
        addonsHost.innerHTML += `
            <div class="section">
                <label for="doorOpenDirection">اتجاه الفتح (OPEN):</label>
                <input type="text" id="doorOpenDirection" placeholder="مثال: يمين / Right">
            </div>`;
    }

    const data = findProductData(subVal);
    if (data && data.addons) {
        const availableAddons = data.addons.split(',');
        if (availableAddons.includes('curtain')) {
            addonsHost.innerHTML += `<div><label><input type="checkbox" id="addon_curtain"> إضافة ستارة (+${addonPrices.curtain} ريال عماني/م²)</label></div>`;
        }
        if (availableAddons.includes('net')) {
            addonsHost.innerHTML += `<div><label for="addon_net_type">إضافة شبك:</label><select id="addon_net_type"><option value="">-- لا شيء --</option><option value="door">باب (+${addonPrices.net.door} لكل 0.5م²)</option><option value="folding">قابل للطي (+${addonPrices.net.folding} لكل 0.5م²)</option><option value="sliding">منزلق (+${addonPrices.net.sliding} لكل 0.5م²)</option></select></div>`;
        }
    }
    setDefaultDimensions();
}


function setDefaultDimensions() {
    const subVal = document.getElementById("subType").value;
    const data = findProductData(subVal);
    if (data && data.method === 'per_unit') {
        document.getElementById("height").value = data.std_h || 2.2;
        document.getElementById("width").value = data.std_w || 1.0;
    } else {
        document.getElementById("height").value = 1;
        document.getElementById("width").value = 1;
    }
}

function findProductData(productName) {
    for (const category in productData) {
        if (productData[category][productName]) {
            return productData[category][productName];
        }
    }
    return null;
}

function findProductByCode(code) {
    const upperCode = code.toUpperCase();
    const fullName = productCodes[upperCode];
    return fullName ? { name: fullName, data: findProductData(fullName) } : null;
}

function calculateItemComponents(item) {
    const data = item.data;
    if (!data) return { unitPrice: 0, totalPrice: 0, shippingCost: 0 };
    
    const widthValue = item.w.toString();
    const totalWidth = widthValue.split('+')
                               .map(part => parseFloat(part.trim()) || 0)
                               .reduce((sum, num) => sum + num, 0);

    const area = item.h * totalWidth;
    
    const basePricePerMetric = (item.overridePrice !== null && !isNaN(item.overridePrice)) ? item.overridePrice : data.price;
    
    let basePrice = 0, sizePenalty = 0, addonCost = 0;

    if (data.method === 'per_unit') {
        basePrice = basePricePerMetric || 0;
        const stdArea = (data.std_h || 0) * (data.std_w || 0);
        if (stdArea > 0 && area > stdArea) {
            sizePenalty = Math.ceil((area - stdArea) / 0.1) * 2;
        }
    } else {
        basePrice = area * (basePricePerMetric || 0);
    }
    
    if (item.selectedAddons.curtain) {
        addonCost += area * addonPrices.curtain;
    }
    
    if (item.selectedAddons.netType && addonPrices.net[item.selectedAddons.netType]) {
        const netUnits = Math.ceil(area / 0.5);
        addonCost += netUnits * addonPrices.net[item.selectedAddons.netType];
    }

    const fixedCost = data.fixed_component_cost || 0;
    const specialCost = data.special === 'add_10' ? 10 : 0;
    const shippingCost = area * (data.cbm || 0) * SHIPPING_RATE;
    const unitPrice = basePrice + sizePenalty + fixedCost + specialCost + addonCost;
    
    return { 
        unitPrice: unitPrice, 
        totalPrice: unitPrice * item.qty,
        shippingCost: shippingCost * item.qty
    };
}

function addItem(manualData = null) {
    let newItem;
    if (manualData) {
        newItem = {
            id: Date.now(),
            name: manualData.name,
            qty: manualData.qty,
            h: manualData.h,
            w: manualData.w.toString(),
            itemCodePrefix: manualData.itemCodePrefix || "",
            itemNotes: manualData.itemNotes || "",
            selectedAddons: {},
            data: manualData.data,
            isEditing: false,
            overridePrice: null,
            openDirection: ''
        };
    } else {
        const subVal = document.getElementById("subType").value;
        if (!subVal) { alert("الرجاء اختيار نوع فرعي."); return; }
        
        const height = parseFloat(document.getElementById("height").value);
        const widthStr = document.getElementById("width").value;
        const quantity = parseInt(document.getElementById("quantity").value);

        if (isNaN(height) || height <= 0) { alert("الرجاء إدخال ارتفاع صالح."); return; }
        
        const totalWidth = widthStr.split('+').map(p => parseFloat(p.trim()) || 0).reduce((s, n) => s + n, 0);
        if (totalWidth <= 0) { alert("الرجاء إدخال عرض صالح. يمكن استخدام + لجمع عدة أضلاع (مثال: 5+2.5)."); return; }
        
        if (isNaN(quantity) || quantity <= 0) { alert("الرجاء إدخال كمية صالحة."); return; }

        const data = findProductData(subVal);
        newItem = {
            id: Date.now(),
            name: subVal,
            qty: quantity,
            h: height,
            w: widthStr,
            itemCodePrefix: "",
            itemNotes: "",
            selectedAddons: {
                curtain: document.getElementById("addon_curtain")?.checked || false,
                netType: document.getElementById("addon_net_type")?.value || null
            },
            data: JSON.parse(JSON.stringify(data)),
            isEditing: false,
            overridePrice: null,
            openDirection: document.getElementById('doorOpenDirection')?.value || ''
        };
    }
    
    const prices = calculateItemComponents(newItem);
    newItem.unitPrice = prices.unitPrice;
    newItem.totalPrice = prices.totalPrice;
    newItem.shippingCost = prices.shippingCost;
    resultsList.push(newItem);
    renderResults();
}

function processPastedText() {
    const text = document.getElementById("bulkAddText").value;
    const lines = text.split('\n');
    let addedCount = 0;
    let skippedLines = [];

    lines.forEach((line, index) => {
        line = line.trim();
        if (!line) return;

        const parts = line.split('-').map(p => p.trim());
        
        if (parts.length < 5) {
            skippedLines.push(`السطر ${index + 1}: "${line}" - تنسيق غير صحيح.`);
            return;
        }

        const itemCodePrefix = parts[0];
        const typeCode = parts[1];
        const h = parseFloat(parts[2]);
        const w = parseFloat(parts[3]);
        const qty = parseInt(parts[4]);

        if (isNaN(h) || h <= 0) { skippedLines.push(`السطر ${index + 1}: "${line}" - ارتفاع غير صالح.`); return; }
        if (isNaN(w) || w <= 0) { skippedLines.push(`السطر ${index + 1}: "${line}" - عرض غير صالح.`); return; }
        if (isNaN(qty) || qty <= 0) { skippedLines.push(`السطر ${index + 1}: "${line}" - كمية غير صالحة.`); return; }

        const productInfo = findProductByCode(typeCode);
        if (productInfo) {
            addItem({ name: productInfo.name, h, w, qty, data: productInfo.data, itemCodePrefix: itemCodePrefix });
            addedCount++;
        } else {
            skippedLines.push(`السطر ${index + 1}: "${line}" - كود المنتج "${typeCode}" غير معروف.`);
        }
    });

    let alertMessage = `تمت إضافة ${addedCount} صنف بنجاح.`;
    if (skippedLines.length > 0) {
        alertMessage += `\n\nتم تخطي ${skippedLines.length} أسطر بسبب أخطاء:\n- ` + skippedLines.join('\n- ');
    }
    alert(alertMessage);
    document.getElementById("bulkAddText").value = "";
}

function deleteItem(id) {
    resultsList = resultsList.filter(item => item.id !== id);
    renderResults();
}

function clearAllResults() {
    if (confirm("هل أنت متأكد من أنك تريد مسح جميع الأصناف والبيانات المحفوظة؟")) {
        resultsList = [];
        overrideGrandTotal = null;
        isEditingGrandTotal = false;
        localStorage.removeItem('quotationData');
        localStorage.removeItem('installationCost');
        localStorage.removeItem('overrideGrandTotal');
        document.getElementById('installationCost').value = 0;
        renderResults();
    }
}

function enterEditMode(id) {
    resultsList.forEach(item => item.isEditing = (item.id === id));
    renderResults();
}

function cancelEdit(id) {
    const item = resultsList.find(i => i.id === id);
    if (item) {
        item.isEditing = false;
        renderResults();
    }
}

function findProductCategory(productName) {
    for (const category in productData) {
        if (productData[category][productName]) {
            return category;
        }
    }
    return null;
}


function saveItemEdit(id) {
    const item = resultsList.find(i => i.id === id);
    if (item) {
        const newName = document.getElementById(`edit-name-${item.id}`).value;
        const newQty = parseInt(document.getElementById(`edit-qty-${item.id}`).value);
        const newH = parseFloat(document.getElementById(`edit-h-${item.id}`).value);
        const newW = document.getElementById(`edit-w-${item.id}`).value;
        const overridePriceInput = document.getElementById(`edit-override-price-${item.id}`).value;
        const newOverridePrice = overridePriceInput === '' ? null : parseFloat(overridePriceInput);
        const newOpenDirection = document.getElementById(`edit-open-direction-${item.id}`)?.value || item.openDirection;

        if (isNaN(newH) || newH <= 0) { alert("الرجاء إدخال ارتفاع صالح."); return; }
        
        const totalWidth = newW.split('+').map(p=>parseFloat(p.trim())||0).reduce((s,n)=>s+n,0);
        if (totalWidth <= 0) { alert("الرجاء إدخال عرض صالح."); return; }

        if (isNaN(newQty) || newQty <= 0) { alert("الرجاء إدخال كمية صالحة."); return; }

        const newData = findProductData(newName);
        if (!newData) {
            alert(`اسم المنتج "${newName}" غير صالح.`);
            return;
        }
        
        item.name = newName;
        item.data = newData; 
        item.qty = newQty;
        item.h = newH;
        item.w = newW;
        item.overridePrice = newOverridePrice;
        item.openDirection = newOpenDirection;
        item.itemNotes = document.getElementById(`edit-notes-${item.id}`).value;

        const prices = calculateItemComponents(item);
        item.unitPrice = prices.unitPrice;
        item.totalPrice = prices.totalPrice;
        item.shippingCost = prices.shippingCost;

        item.isEditing = false;
    }
    renderResults();
}

function saveResultsToLocalStorage() {
    localStorage.setItem('quotationData', JSON.stringify(resultsList));
    localStorage.setItem('installationCost', document.getElementById('installationCost').value);
    localStorage.setItem('overrideGrandTotal', JSON.stringify(overrideGrandTotal));
}

function loadResultsFromLocalStorage() {
    const savedData = localStorage.getItem('quotationData');
    const savedCost = localStorage.getItem('installationCost');
    const savedOverrideTotal = localStorage.getItem('overrideGrandTotal');

    if (savedData) {
        const parsedData = JSON.parse(savedData);
        resultsList = parsedData.map(item => {
            const currentData = findProductData(item.name);
            if (currentData) { item.data = currentData; }
            return item;
        });
    }
    if (savedCost) {
        document.getElementById('installationCost').value = savedCost;
    }
    if (savedOverrideTotal) {
        overrideGrandTotal = JSON.parse(savedOverrideTotal);
    }
    renderResults();
}

function enterEditGrandTotalMode() {
    isEditingGrandTotal = true;
    renderResults();
}

function cancelGrandTotalEdit() {
    isEditingGrandTotal = false;
    overrideGrandTotal = null; // Reset on cancel
    renderResults();
}

function saveGrandTotalEdit() {
    const input = document.getElementById('grandTotalInput');
    const newValue = parseFloat(input.value);
    if (!isNaN(newValue)) {
        overrideGrandTotal = newValue;
    }
    isEditingGrandTotal = false;
    renderResults();
}


function renderResults() {
    const container = document.getElementById("results");
    container.innerHTML = "";
    if (resultsList.length === 0 && !isEditingGrandTotal) {
        container.innerHTML = `<div class="results-placeholder"><p>لم يتم إضافة أي أصناف بعد</p></div>`;
        saveResultsToLocalStorage();
        return;
    }

    let subtotal = 0;
    let totalShipping = 0;

    resultsList.forEach(item => {
        subtotal += item.totalPrice;
        totalShipping += item.shippingCost;
        
        const displayPrice = (item.overridePrice !== null && !isNaN(item.overridePrice)) ? item.overridePrice : item.data.price;

        if (item.isEditing) {
             let editFormHTML = `
                <div class="result-item">
                     <h4>تعديل الصنف: ${item.name}</h4>
                    <div class="edit-form-grid" style="grid-template-columns: 1fr 1fr; gap: 10px;">
                        <div><label>الاسم</label><input type="text" id="edit-name-${item.id}" value="${item.name}"></div>
                        <div><label>الكمية</label><input type="number" id="edit-qty-${item.id}" value="${item.qty}"></div>
                        <div><label>الارتفاع</label><input type="number" step="0.01" id="edit-h-${item.id}" value="${item.h}"></div>
                        <div><label>العرض</label><input type="text" id="edit-w-${item.id}" value="${item.w}"></div>
                        <div style="grid-column: 1 / -1;"><label>سعر المتر/الوحدة (تجاوز)</label><input type="number" step="0.01" id="edit-override-price-${item.id}" value="${item.overridePrice || ''}" placeholder="اتركه فارغاً للسعر الافتراضي"></div>
                    `;
            
            if (findProductCategory(item.name) === 'Doors') {
                editFormHTML += `<div style="grid-column: 1 / -1;"><label>اتجاه الفتح (OPEN)</label><input type="text" id="edit-open-direction-${item.id}" value="${item.openDirection || ''}"></div>`;
            }

            editFormHTML += `
                    </div>
                    <div style="margin-top: 15px;"><label>ملاحظات</label><textarea id="edit-notes-${item.id}">${item.itemNotes || ''}</textarea></div>
                    <div style="text-align: left; margin-top: 10px;">
                        <button onclick="cancelEdit(${item.id})" class="btn-secondary" style="padding: 8px 15px;">إلغاء</button>
                        <button onclick="saveItemEdit(${item.id})" class="btn-success" style="padding: 8px 15px;">حفظ</button>
                    </div>
                </div>`;
            container.innerHTML += editFormHTML;

        } else {
            container.innerHTML += `
                <div class="result-item">
                    <div class="item-header">
                        <h4>${item.itemCodePrefix ? `[${item.itemCodePrefix}] ` : ''}${item.name}</h4>
                        <div>
                           <button onclick="enterEditMode(${item.id})" class="btn-secondary" style="padding: 6px 12px; margin: 0 5px;">✏️</button>
                           <button onclick="deleteItem(${item.id})" class="btn-danger" style="padding: 6px 12px; margin: 0;">🗑️</button>
                        </div>
                    </div>
                    <p><strong>الأبعاد:</strong> ${item.h}م x ${item.w}م | <strong>الكمية:</strong> ${item.qty}</p>
                    <p><strong>السعر الأساسي:</strong> ${displayPrice.toFixed(2)} ر.ع. / ${item.data.method === 'per_unit' ? 'وحدة' : 'م²'} ${item.overridePrice !== null ? '(مُعدل)' : ''}</p>
                    <p style="font-weight: bold; font-size: 1.1em; color: #333;">
                        الإجمالي: ${item.totalPrice.toFixed(2)} ر.ع.
                    </p>
                    ${item.itemNotes ? `<p style="font-size: 0.9em; color: #555;"><strong>ملاحظات:</strong> ${item.itemNotes.replace(/\n/g, '<br>')}</p>` : ''}
                </div>`;
        }
    });

    const commission = subtotal * 0.04;
    const installationCost = parseFloat(document.getElementById('installationCost').value) || 0;
    
    const calculatedGrandTotal = subtotal + commission + totalShipping + installationCost;
    const finalGrandTotal = overrideGrandTotal !== null ? overrideGrandTotal : calculatedGrandTotal;

    let grandTotalHTML = '';
    if (isEditingGrandTotal) {
        grandTotalHTML = `
            <span>💰 المجموع الكلي</span>
            <div>
                <input type="number" id="grandTotalInput" value="${finalGrandTotal.toFixed(2)}" style="width: 150px; text-align: center; font-size: 0.8em; padding: 8px;">
                <button onclick="saveGrandTotalEdit()" class="btn-success btn-small">حفظ</button>
                <button onclick="cancelGrandTotalEdit()" class="btn-secondary btn-small">إلغاء</button>
            </div>
        `;
    } else {
         grandTotalHTML = `
            <span>💰 المجموع الكلي</span>
            <div>
                ${finalGrandTotal.toFixed(2)} ر.ع.
                <button onclick="enterEditGrandTotalMode()" class="btn-secondary btn-small">✏️</button>
            </div>
        `;
    }

    container.innerHTML += `
        <div class="summary">
            <div class="summary-row"><span>سعر الشراء من الصين:</span><span>${subtotal.toFixed(2)} ر.ع.</span></div>
            <div class="summary-row"><span>الشحن والتخليص:</span><span>${totalShipping.toFixed(2)} ر.ع.</span></div>
            <div class="summary-row"><span>عمولة المكتب (4%):</span><span>${commission.toFixed(2)} ر.ع.</span></div>
            <div class="summary-row"><span>التركيب:</span><span>${installationCost.toFixed(2)} ر.ع.</span></div>
            <div class="grand-total">
                ${grandTotalHTML}
            </div>
        </div>`;
    
    saveResultsToLocalStorage();
}

function renderReferenceGuide() {
    const container = document.getElementById('referenceContainer');
    let tableHtml = '<details><summary>اضغط هنا لرؤية أكواد المنتجات</summary><table class="reference-table"><thead><tr><th>الكود</th><th>اسم المنتج</th><th>الفئة</th></tr></thead><tbody>';
    
    const invertedCodes = {};
    for (const code in productCodes) {
        invertedCodes[productCodes[code]] = code;
    }

    for (const category in productData) {
        for (const product in productData[category]) {
            const code = invertedCodes[product] || 'N/A';
            tableHtml += `<tr><td><strong>${code}</strong></td><td>${product}</td><td>${category}</td></tr>`;
        }
    }

    tableHtml += '</tbody></table></details>';
    container.innerHTML = tableHtml;
}

function saveAsWord() {
    if (resultsList.length === 0) { alert("لا توجد نتائج لحفظها."); return; }
    
    const tableHeaderBg = '#5B9BD5'; 
    const summaryRowBg1 = '#F2F6FA'; 
    const summaryRowBg2 = '#E6EEF6';
    const totalRowBg = '#5B9BD5';
    const whiteText = '#ffffff';
    const blackBorder = '#000000';

    let subtotal = 0, totalShipping = 0, totalCBM = 0;
    resultsList.forEach(item => {
        const totalWidth = item.w.toString().split('+').map(p => parseFloat(p.trim()) || 0).reduce((s, n) => s + n, 0);
        const area = item.h * totalWidth;
        subtotal += item.totalPrice;
        totalShipping += item.shippingCost;
        totalCBM += (area * (item.data.cbm || 0) * item.qty);
    });

    const commission = subtotal * 0.04;
    const installationCost = parseFloat(document.getElementById('installationCost').value) || 0;
    
    const calculatedGrandTotal = subtotal + commission + totalShipping + installationCost;
    const finalGrandTotal = overrideGrandTotal !== null ? overrideGrandTotal : calculatedGrandTotal;

    let tableRows = '';
    resultsList.forEach((item, index) => {
        const totalWidthCalc = item.w.toString().split('+').map(p=>parseFloat(p.trim())||0).reduce((s,n)=>s+n,0);
        const displayArea = item.h * totalWidthCalc;

        let styleContent = item.itemCodePrefix || '';
        if (item.openDirection) {
            styleContent += ` - ${item.openDirection}`;
        }

        tableRows += `
            <tr style="page-break-inside: avoid; height: 30px; font-weight: bold;">
                <td style="border: 1px solid ${blackBorder}; padding: 5px; text-align: center; vertical-align: middle;">${index + 1}</td>
                <td style="border: 1px solid ${blackBorder}; padding: 5px; text-align: center; vertical-align: middle;">${item.h}</td>
                <td style="border: 1px solid ${blackBorder}; padding: 5px; text-align: center; vertical-align: middle;">${item.w}</td>
                <td style="border: 1px solid ${blackBorder}; padding: 5px; text-align: center; vertical-align: middle;">${displayArea.toFixed(2)}</td>
                <td style="border: 1px solid ${blackBorder}; padding: 5px; text-align: center; vertical-align: middle;">${item.qty}</td>
                <td style="border: 1px solid ${blackBorder}; padding: 5px; text-align: center; vertical-align: middle;">${styleContent}</td>
                <td style="border: 1px solid ${blackBorder}; padding: 5px; text-align: center; vertical-align: middle;">${(item.totalPrice / item.qty).toFixed(2)}</td>
                <td style="border: 1px solid ${blackBorder}; padding: 5px; text-align: center; vertical-align: middle;">${item.totalPrice.toFixed(2)}</td>
                <td style="border: 1px solid ${blackBorder}; padding: 5px; text-align: right; vertical-align: middle;">${item.name}${item.itemNotes ? `<br><small style="color: #555; font-weight: normal;">${item.itemNotes.replace(/\n/g, '<br>')}</small>`: ''}</td>
            </tr>`;
    });
    
    for (let i = resultsList.length; i < 10; i++) {
        tableRows += `<tr style="height: 30px;"><td style="border: 1px solid ${blackBorder};"></td><td style="border: 1px solid ${blackBorder};"></td><td style="border: 1px solid ${blackBorder};"></td><td style="border: 1px solid ${blackBorder};"></td><td style="border: 1px solid ${blackBorder};"></td><td style="border: 1px solid ${blackBorder};"></td><td style="border: 1px solid ${blackBorder};"></td><td style="border: 1px solid ${blackBorder};"></td><td style="border: 1px solid ${blackBorder};"></td></tr>`;
    }

    let content = `
        <html xmlns:w="urn:schemas-microsoft-com-office:word">
        <head><meta charset='utf-8'><title>Quotation</title></head>
        <body style="font-family: Arial, sans-serif; direction: ltr; font-size: 12pt;">
            
            <table style="width: 100%; border-collapse: collapse; font-family: Arial, sans-serif;">
                <tr>
                    <td colspan="3" style="background-color: ${tableHeaderBg}; padding: 10px; text-align: center;">
                        <span style="font-size: 20pt; font-weight: bold; color: #ffffff; letter-spacing: 2px;">BLUE WAVES SERVICES LLC</span>
                    </td>
                </tr>
                <tr style="color: #333333;">
                    <td style="padding: 8px 5px; text-align: left; width: 33%; font-size: 11pt;">
                        <strong>OMAN - MUSCAT</strong>
                    </td>
                    <td style="padding: 8px 5px; text-align: center; width: 34%; font-size: 11pt;">
                        <strong>SR. NO. :</strong> 1595256
                    </td>
                    <td style="padding: 8px 5px; text-align: right; width: 33%; font-size: 10pt;">
                        <strong>TEL: 77 22 45 11 - 90 99 88 10</strong>
                    </td>
                </tr>
                <tr><td colspan="3" style="border-bottom: 2px solid ${tableHeaderBg};"></td></tr>
            </table>

            <br/>

            <table style="width: 100%; border-collapse: collapse; font-size: 12pt; border: 1px solid ${blackBorder};">
                <thead>
                    <tr style="background-color: ${tableHeaderBg}; color: ${whiteText};">
                        <th style="border: 1px solid ${blackBorder}; padding: 8px; width: 4%;">NO</th><th style="border: 1px solid ${blackBorder}; padding: 8px; width: 4%;">H</th>
                        <th style="border: 1px solid ${blackBorder}; padding: 8px; width: 4%;">W</th><th style="border: 1px solid ${blackBorder}; padding: 8px; width: 4%;">m²</th>
                        <th style="border: 1px solid ${blackBorder}; padding: 8px; width: 4%;">Q</th><th style="border: 1px solid ${blackBorder}; padding: 8px; width: 15%;">STYLE</th>
                        <th style="border: 1px solid ${blackBorder}; padding: 8px; width: 8%;">PRICE</th><th style="border: 1px solid ${blackBorder}; padding: 8px; width: 8%;">TOTAL</th>
                        <th style="border: 1px solid ${blackBorder}; padding: 8px;">DESCRITION</th>
                    </tr>
                </thead>
                <tbody>${tableRows}</tbody>
            </table>
            
            <table style="width: 100%; border-collapse: collapse; font-size: 12pt; border: 1px solid ${blackBorder};">
                 <tr style="page-break-inside: avoid; font-weight: bold;">
                    <td style="border: 1px solid ${blackBorder}; background-color: ${summaryRowBg1}; padding: 5px; text-align: right; direction: rtl; width: 75%;">سعر الشراء من الصين</td>
                    <td style="border: 1px solid ${blackBorder}; padding: 5px; text-align: center;">${subtotal.toFixed(2)}</td>
                    <td style="border: 1px solid ${blackBorder}; padding: 5px; text-align: center; background-color: ${summaryRowBg1};">TOTAL CBM</td>
                 </tr>
                 <tr style="page-break-inside: avoid; font-weight: bold;">
                    <td style="border: 1px solid ${blackBorder}; background-color: ${summaryRowBg2}; padding: 5px; text-align: right; direction: rtl;">عمولة المكتب 4 %</td>
                    <td style="border: 1px solid ${blackBorder}; padding: 5px; text-align: center;">${commission.toFixed(2)}</td>
                    <td style="border: 1px solid ${blackBorder}; padding: 5px; text-align: center;">${totalCBM.toFixed(3)}</td>
                </tr>
                 <tr style="page-break-inside: avoid; font-weight: bold;">
                    <td style="border: 1px solid ${blackBorder}; background-color: ${summaryRowBg1}; padding: 5px; text-align: right; direction: rtl;">الشحن والتخليص الجمركي</td>
                    <td style="border: 1px solid ${blackBorder}; padding: 5px; text-align: center;">${totalShipping.toFixed(2)}</td>
                    <td style="border: 1px solid ${blackBorder}; padding: 5px; text-align: right; direction: rtl; background-color: ${summaryRowBg1};">سعر الشحن الحالي</td>
                </tr>
                <tr style="page-break-inside: avoid; font-weight: bold;">
                    <td style="border: 1px solid ${blackBorder}; background-color: ${summaryRowBg2}; padding: 5px; text-align: right; direction: rtl;">التركيب</td>
                    <td style="border: 1px solid ${blackBorder}; padding: 5px; text-align: center;">${installationCost.toFixed(2)}</td>
                    <td style="border: 1px solid ${blackBorder}; padding: 5px; text-align: center;">${SHIPPING_RATE}</td>
                </tr>
                 <tr style="page-break-inside: avoid; font-weight: bold;">
                    <td style="border: 1px solid ${blackBorder}; background-color: ${totalRowBg}; color:${whiteText}; padding: 5px; text-align: right; direction: rtl;">الإجمالي</td>
                    <td style="border: 1px solid ${blackBorder}; padding: 5px; text-align: center;">${finalGrandTotal.toFixed(2)}</td>
                    <td style="border: 1px solid ${blackBorder};"></td>
                </tr>
            </table>
        </body>
        </html>
    `;
    
    const blob = new Blob(['\ufeff', content], { type: 'application/msword' });
    const link = document.createElement("a");
    link.href = URL.createObjectURL(blob);
    link.download = `Quotation-${document.getElementById('customerName').value || 'General'}.doc`;
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
}

document.addEventListener('DOMContentLoaded', initializeApp);

</script>
</body>
</html>
