# Abboud-Cart-
شحن برامج والعاب
<!doctype html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>متجر الشحن الرقمي — شحن ألعاب وسوشال</title>
  <style>
    /* --- Reset بسيط --- */
    * { box-sizing: border-box; margin: 0; padding: 0; }
    html,body { height:100%; font-family: "Tajawal", "Tahoma", sans-serif; background:#f5f7fb; color:#111; }
    a { text-decoration:none; color:inherit; }

    /* --- واجهة عامة --- */
    header {
      background: linear-gradient(90deg,#0f172a 0%, #0b3a6b 100%);
      color: #fff;
      padding:18px 20px;
      display:flex;
      align-items:center;
      justify-content:space-between;
      gap:12px;
    }
    .logo { display:flex; align-items:center; gap:12px; }
    .logo img { width:46px; height:46px; border-radius:8px; object-fit:cover; }
    .brand { font-weight:700; font-size:18px; letter-spacing:0.4px; }
    .search { flex:1; margin:0 18px; max-width:640px; }
    .search input {
      width:100%; padding:10px 14px; border-radius:10px; border:0; outline:none;
      box-shadow: 0 2px 6px rgba(11, 26, 46, 0.15);
    }
    nav { display:flex; gap:12px; align-items:center; }

    /* --- زر الشراء/أيقونة السلة --- */
    .btn {
      background:#06b6d4; color:#042028; padding:10px 14px; border-radius:10px; font-weight:700;
      box-shadow: 0 4px 10px rgba(6,182,212,0.15);
    }
    .btn.ghost { background:transparent; color:#fff; border:1px solid rgba(255,255,255,0.12); box-shadow:none; }

    /* --- محتوى الصفحات --- */
    .container { max-width:1150px; margin:22px auto; padding:0 20px; }
    .hero {
      background:linear-gradient(90deg,#eef7fb, #ffffff);
      padding:20px; border-radius:12px; display:flex; gap:20px; align-items:center;
      box-shadow:0 6px 18px rgba(12,32,64,0.06);
    }
    .hero .left { flex:1; }
    .hero h1 { font-size:22px; margin-bottom:8px; }
    .hero p { color:#41536b; margin-bottom:12px; line-height:1.5; }
    .quick-links { display:flex; gap:10px; flex-wrap:wrap; }
    .chip { padding:10px 12px; background:white; border-radius:8px; box-shadow:0 4px 12px rgba(12,32,64,0.05); font-weight:600; }

    /* --- أقسام المنتجات --- */
    .grid { display:grid; grid-template-columns: repeat(auto-fit,minmax(220px,1fr)); gap:14px; margin-top:18px; }
    .card {
      background:#fff; border-radius:12px; padding:14px; box-shadow:0 8px 20px rgba(12,32,64,0.06);
      display:flex; flex-direction:column; gap:10px;
    }
    .card .title { font-weight:700; font-size:15px; }
    .card .desc { color:#5b6b7a; font-size:13px; min-height:36px; }
    .price-row { display:flex; justify-content:space-between; align-items:center; gap:8px; margin-top:auto; }
    .price { font-weight:800; color:#0b3a6b; }
    .small { font-size:12px; color:#74808d; }

    /* --- سلة الشراء (شريط جانبي/مودال) --- */
    .cart-btn { position:relative; }
    .cart-count { position:absolute; top:-8px; left:-8px; background:#ff5252; color:#fff; border-radius:50%; width:20px; height:20px; display:flex; align-items:center; justify-content:center; font-size:12px; font-weight:700; }

    /* --- Footer --- */
    footer { margin-top:26px; padding:20px 0; text-align:center; color:#6b7684; font-size:13px; }

    /* --- Modal بسيط --- */
    .modal-backdrop { position:fixed; inset:0; background:rgba(2,6,23,0.45); display:none; align-items:center; justify-content:center; z-index:80; padding:18px; }
    .modal { width:100%; max-width:520px; background:#fff; border-radius:12px; padding:18px; box-shadow:0 20px 40px rgba(2,6,23,0.35); }
    .modal h3 { margin-bottom:8px; }
    .form-row { display:flex; gap:8px; margin-top:10px; }
    .form-row input, .form-row select { flex:1; padding:10px 12px; border-radius:8px; border:1px solid #e6eef7; outline:none; }

    /* --- Responsive small --- */
    @media (max-width:720px){
      .hero { flex-direction:column; align-items:flex-start; }
      .search { display:none; }
      header { padding:12px; }
    }

  </style>
</head>
<body>

  <header>
    <div class="logo">
      <img src="https://via.placeholder.com/80x80.png?text=Logo" alt="logo">
      <div>
        <div class="brand">شحننا — المتجر الرقمي</div>
        <div class="small">شحن ألعاب، أرصدة، باقات، وجوائز</div>
      </div>
    </div>

    <div class="search">
      <input id="searchInput" placeholder="ابحث عن لعبة / برنامج / باقة (مثال: شدات ببجي)" />
    </div>

    <nav>
      <button class="btn ghost" onclick="openLogin()">تسجيل / دخول</button>
      <div class="cart-btn">
        <button class="btn" onclick="openCart()">سلة الشراء</button>
        <div class="cart-count" id="cartCount" style="display:none">0</div>
      </div>
    </nav>
  </header>

  <main class="container">
    <section class="hero" aria-label="مقدمة">
      <div class="left">
        <h1>اشحن ألعابك وحساباتك بسرعة وأمان</h1>
        <p>اختر الخدمة، أدخل بيانات الحساب/اليوزر، وأكمل الدفع. دعم فوري للـ PUBG, Free Fire, Google Play, Spotify, واشتراكات السوشال.</p>
        <div class="quick-links" id="quickLinks">
          <span class="chip">شدات PUBG</span>
          <span class="chip">جواهر Free Fire</span>
          <span class="chip">قيمة Google Play</span>
          <span class="chip">اشتراك Spotify</span>
        </div>
      </div>
      <div class="right">
        <!-- مكان لإضافة صورة / رسومات -->
        <img src="https://via.placeholder.com/220x160.png?text=Top+Up" alt="illustration" style="border-radius:10px;">
      </div>
    </section>

    <!-- --- قسم المنتجات / الخدمات --- -->
    <section style="margin-top:18px;">
      <h2 style="font-size:18px; margin-bottom:8px;">الخدمات الشهيرة</h2>
      <div class="grid" id="productsGrid">
        <!-- عناصر تُحقن عبر الجافاسكربت -->
      </div>
    </section>

    <!-- --- تعليمات / خطوات --- -->
    <section style="margin-top:18px;">
      <div style="display:flex; gap:12px; flex-wrap:wrap;">
        <div class="card" style="flex:1; min-width:240px;">
          <div class="title">كيف تشتري؟</div>
          <div class="desc">اختر الخدمة → أدخل بيانات الحساب → أضف للسلة → أدخل معلومات الدفع → استلم الشحن فورًا.</div>
        </div>
        <div class="card" style="flex:1; min-width:240px;">
          <div class="title">طرق الدفع</div>
          <div class="desc">قبول بطاقات فيزا/ماستركارد (عن طريق بوابة)، رصيد محفظة، أو تحويل بنكي. ربط بوابة الدفع عبر الـ API سهل.</div>
        </div>
        <div class="card" style="flex:1; min-width:240px;">
          <div class="title">دعم فني</div>
          <div class="desc">دعم عبر تيليجرام / واتساب متاح 24/7. أضف رقم الدعم وروابط القناة هنا.</div>
        </div>
      </div>
    </section>

  </main>

  <!-- --- Footer --- -->
  <footer>
    © <span id="year"></span> شحننا — جميع الحقوق محفوظة. تصميم وواجهة جاهزة للاندماج مع الخادم.
  </footer>

  <!-- --- مودال السلة / الشراء --- -->
  <div class="modal-backdrop" id="cartModal" role="dialog" aria-hidden="true">
    <div class="modal" role="document">
      <h3>سلة الشراء</h3>
      <div id="cartItems" style="max-height:320px; overflow:auto; margin-top:10px;"></div>

      <div style="display:flex; justify-content:space-between; align-items:center; margin-top:14px;">
        <div>
          <div class="small">المجموع:</div>
          <div style="font-weight:800; font-size:18px;" id="cartTotal">0 د.ع</div>
        </div>
        <div style="display:flex; gap:8px;">
          <button class="btn ghost" onclick="closeCart()">متابعة تسوق</button>
          <button class="btn" onclick="checkout()">الدفع الآن</button>
        </div>
      </div>
    </div>
  </div>

  <!-- --- مودال تسجيل/دخول بسيط --- -->
  <div class="modal-backdrop" id="loginModal" role="dialog" aria-hidden="true">
    <div class="modal">
      <h3>تسجيل / دخول</h3>
      <p class="small">يمكنك ربط هذا النموذج بنظام المصادقة الخاص بك عبر API (Token أو session).</p>

      <div style="margin-top:8px;">
        <input id="username" placeholder="اسم المستخدم أو البريد" style="width:100%; padding:10px; border-radius:8px; border:1px solid #e9f0f6;" />
      </div>
      <div style="margin-top:8px;">
        <input id="password" placeholder="كلمة المرور" type="password" style="width:100%; padding:10px; border-radius:8px; border:1px solid #e9f0f6;" />
      </div>

      <div style="display:flex; gap:8px; justify-content:flex-end; margin-top:12px;">
        <button class="btn ghost" onclick="closeLogin()">إغلاق</button>
        <button class="btn" onclick="doLogin()">دخول</button>
      </div>
    </div>
  </div>

<script>
  // --- بيانات تجريبية للمنتجات (استبدلها بداتا من الخادم لاحقًا) ---
  const products = [
    { id: 'pubg-uc-60', title: 'شدات PUBG - 60 UC', desc: 'شحن مباشر داخل اللعبة', price: 3.5, category: 'ببجي' },
    { id: 'pubg-uc-300', title: 'شدات PUBG - 300 UC', desc: 'بأفضل سعر', price: 15.0, category: 'ببجي' },
    { id: 'ff-diamond-50', title: 'جواهر FreeFire - 50', desc: 'شحن فوري', price: 2.0, category: 'فري فاير' },
    { id: 'googleplay-10', title: 'رصيد Google Play - 10$', desc: 'قيمة رمز شحن', price: 9.8, category: 'متجر' },
    { id: 'spotify-month', title: 'Spotify Premium - شهر', desc: 'اشتراك شهري', price: 4.9, category: 'سوشال' },
    { id: 'steam-5', title: 'كود Steam - 5$', desc: 'كود إلكتروني مفعل', price: 4.7, category: 'متجر' }
  ];

  // مكونات الواجهة
  const grid = document.getElementById('productsGrid');
  const cartCountEl = document.getElementById('cartCount');
  const cartItemsEl = document.getElementById('cartItems');
  const cartTotalEl = document.getElementById('cartTotal');
  const cartModal = document.getElementById('cartModal');
  const loginModal = document.getElementById('loginModal');

  // عربة مشتريات محلية (يمكن استبدال بالتخزين في backend)
  let cart = [];

  // زر إضافة إلى السلة
  function addToCart(prodId){
    const p = products.find(x=>x.id===prodId);
    if(!p) return;
    const existing = cart.find(i=>i.id===prodId);
    if(existing) existing.qty++;
    else cart.push({ ...p, qty:1 });
    renderCartCount();
  }

  function renderProducts(list = products){
    grid.innerHTML = '';
    list.forEach(p=>{
      const card = document.createElement('div');
      card.className = 'card';
      card.innerHTML = `
        <div style="display:flex; gap:10px; align-items:center;">
          <div style="width:56px;height:56px;border-radius:8px;background:linear-gradient(90deg,#eef,#def);display:flex;align-items:center;justify-content:center;font-weight:700;">${p.category.slice(0,2)}</div>
          <div style="flex:1;">
            <div class="title">${p.title}</div>
            <div class="desc">${p.desc}</div>
          </div>
        </div>
        <div class="price-row">
          <div>
            <div class="price">${p.price} $</div>
            <div class="small">سعر تقريبي بالدولار</div>
          </div>
          <div style="display:flex; gap:8px;">
            <button class="btn ghost" onclick="quickBuy('${p.id}')">شراء سريع</button>
            <button class="btn" onclick="addToCart('${p.id}')">أضف للسلة</button>
          </div>
        </div>
      `;
      grid.appendChild(card);
    });
  }

  function renderCartCount(){
    const totalQty = cart.reduce((s,i)=>s+i.qty,0);
    if(totalQty>0){ cartCountEl.style.display='flex'; cartCountEl.textContent = totalQty; }
    else cartCountEl.style.display='none';
  }

  function openCart(){
    renderCartItems();
    cartModal.style.display='flex';
    cartModal.setAttribute('aria-hidden','false');
  }
  function closeCart(){
    cartModal.style.display='none';
    cartModal.setAttribute('aria-hidden','true');
  }

  function renderCartItems(){
    if(cart.length===0){ cartItemsEl.innerHTML = '<div class="small">السلة فارغة</div>'; cartTotalEl.textContent = '0 $'; return; }
    cartItemsEl.innerHTML = '';
    let sum = 0;
    cart.forEach(item=>{
      const row = document.createElement('div');
      row.style.display='flex'; row.style.justifyContent='space-between'; row.style.alignItems='center';
      row.style.padding='8px 0'; row.style.borderBottom='1px solid #f0f4f8';
      row.innerHTML = `
        <div style="flex:1;">
          <div style="font-weight:700">${item.title}</div>
          <div class="small">كمية: <strong>${item.qty}</strong></div>
        </div>
        <div style="text-align:left; min-width:120px;">
          <div style="font-weight:800;">${(item.price * item.qty).toFixed(2)} $</div>
          <div style="margin-top:6px; display:flex; gap:6px; justify-content:flex-end;">
            <button class="btn ghost" onclick="decreaseQty('${item.id}')">-</button>
            <button class="btn ghost" onclick="increaseQty('${item.id}')">+</button>
            <button class="btn" onclick="removeFromCart('${item.id}')">حذف</button>
          </div>
        </div>
      `;
      cartItemsEl.appendChild(row);
      sum += item.price * item.qty;
    });
    cartTotalEl.textContent = sum.toFixed(2) + ' $';
  }

  function increaseQty(id){ const it = cart.find(c=>c.id===id); if(it){ it.qty++; renderCartItems(); renderCartCount(); } }
  function decreaseQty(id){ const it = cart.find(c=>c.id===id); if(it){ it.qty = Math.max(1,it.qty-1); renderCartItems(); renderCartCount(); } }
  function removeFromCart(id){ cart = cart.filter(c=>c.id!==id); renderCartItems(); renderCartCount(); }

  // شراء سريع يفتح مودال الدفع (هنا نبقيه يضيف للسلة ويُفتَح)
  function quickBuy(id){
    addToCart(id);
    openCart();
  }

  // إجراء تسجيل دخول (نموذج تجريبي — ربط للـ API لاحقًا)
  function openLogin(){ loginModal.style.display='flex'; loginModal.setAttribute('aria-hidden','false'); }
  function closeLogin(){ loginModal.style.display='none'; loginModal.setAttribute('aria-hidden','true'); }

  function doLogin(){
    const u = document.getElementById('username').value.trim();
    const p = document.getElementById('password').value.trim();
    if(!u || !p){ alert('يرجى إدخال اسم المستخدم وكلمة المرور'); return; }
    // TODO: استبدل بالـ API: مثال fetch('/api/login', {method:'POST', body: JSON.stringify({u,p})})
    alert('تم تسجيل الدخول تجريبياً كـ: ' + u);
    closeLogin();
  }

  // الدفع — هنا نعرض نموذج تجريبي ثم "محاكاة" استدعاء بوابة الدفع
  function checkout(){
    if(cart.length===0){ alert('السلة فارغة'); return; }
    // مثال: إرسال بيانات الطلب إلى الخادم لإنشاء فاتورة، ثم توجيه المستخدم لبوابة دفع
    const order = {
      items: cart.map(i=>({id:i.id, qty:i.qty, price:i.price})),
      total: cart.reduce((s,i)=>s+i.price*i.qty,0),
      currency: 'USD',
      createdAt: new Date().toISOString()
    };
    console.log('Create order (send to server):', order);

    // TODO: استبدل هذا الجزء بطلب fetch إلى سيرفرك لإنشاء جلسة دفع
    alert('تم إنشاء الطلب محليًا (محاكاة). إجمالي: ' + order.total.toFixed(2) + ' $.\nفي نسخة الإنتاج: أرسل الطلب للسيرفر وابدأ بوابة الدفع.');

    // مسح السلة بعد الشراء (في تطبيق حقيقي انتظر تأكيد الدفع قبل التفريغ)
    cart = [];
    renderCartItems();
    renderCartCount();
    closeCart();
  }

  // تهيئة الواجهة
  document.getElementById('year').textContent = new Date().getFullYear();
  renderProducts();

  // بحث بسيط على المنتجات
  document.getElementById('searchInput').addEventListener('input', function(e){
    const q = e.target.value.trim().toLowerCase();
    if(!q) return renderProducts();
    const filtered = products.filter(p => (p.title + ' ' + p.desc + ' ' + p.category).toLowerCase().includes(q));
    renderProducts(filtered);
  });

  // نصائح للتكامل (التعليقات للمطور):
  /*
    - ربط المنتجات بقاعدة بيانات: استبدل المصفوفة `products` باستجابة fetch('/api/products').
    - تسجيل الطلبات: عند checkout استدعي endpoint مثل POST /api/orders مع بيانات العميل والعناصر.
    - بوابة الدفع: يمكن استخدام Stripe/PayPal/Paymob أو بوابة محلية. أنشئ جلسة دفع على السيرفر ثم أعد توجيه المستخدم.
    - حماية: احفظ بيانات المستخدم بجلسة server-side، ولا تحفظ بيانات الدفع على المتصفح.
    - واجهة الإدارة: أنشئ صفحة منفصلة لإضافة/تعديل المنتجات، عرض الطلبات، وإدارة الشحنات.
    - ترجمة: الملف معد للـ RTL والعربية؛ غير النصوص حسب السوق والعملة (أضف تحويل العملات إن لزم).
  */
</script>

</body>
</html>
