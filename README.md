<!DOCTYPE html><html lang="cs">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Fortnite of Legends</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;800&display=swap" rel="stylesheet">
  <style>
    body { font-family: Inter, system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif; }
    .card { @apply bg-white/80 backdrop-blur shadow-md rounded-2xl p-5; }
    .btn { @apply px-4 py-2 rounded-2xl shadow hover:shadow-lg transition active:scale-[.99]; }
    .btn-primary { @apply btn bg-indigo-600 text-white disabled:opacity-50; }
    .btn-outline { @apply btn border border-gray-300 bg-white; }
    .hidden-admin { display: none; }
  </style>
</head>
<body class="min-h-screen bg-gradient-to-br from-slate-900 via-indigo-900 to-slate-800 text-slate-100">
  <header class="max-w-6xl mx-auto px-4 pt-10 pb-6">
    <div class="flex items-center justify-between">
      <h1 class="text-3xl md:text-4xl font-extrabold tracking-tight">Fortnite of Legends</h1>
      <nav class="flex gap-2 text-sm">
        <a href="#home" class="btn-outline">Domů</a>
        <a href="#clenove" class="btn-outline">Členové</a>
        <a href="#aktuality" class="btn-outline">Aktuality</a>
        <a href="#onas" class="btn-outline">O nás</a>
        <a href="#admin" class="btn-outline">Správce</a>
      </nav>
    </div>
  </header>  <main class="max-w-6xl mx-auto px-4 pb-24 space-y-8">
    <!-- Hero / Home -->
    <section id="home" class="card text-slate-900">
      <h2 class="text-2xl font-bold">Vítej v našem Fortnite esport týmu – Fortnite of Legends</h2>
      <p class="mt-2 text-slate-700">Tady najdeš info o členech, novinky, něco o nás a (pro správce) přístup k přihláškám do klubu. Obsah Členové, Aktuality a O nás může měnit pouze správce po zadání kódu.</p>
    </section><!-- Členové -->
<section id="clenove" class="card text-slate-900">
  <div class="flex items-center justify-between">
    <h2 class="text-xl font-bold">Členové týmu</h2>
    <div id="memberAdminBtns" class="hidden-admin flex gap-2">
      <button class="btn-outline" onclick="openMemberModal()">+ Přidat člena</button>
      <button class="btn-outline" onclick="clearMembers()">Smazat všechny</button>
    </div>
  </div>
  <ul id="membersList" class="mt-4 grid md:grid-cols-2 gap-3"></ul>
</section>

<!-- Aktuality -->
<section id="aktuality" class="card text-slate-900">
  <div class="flex items-center justify-between">
    <h2 class="text-xl font-bold">Aktuality</h2>
    <div id="newsAdminBtns" class="hidden-admin flex gap-2">
      <button class="btn-outline" onclick="openNewsModal()">+ Přidat novinku</button>
      <button class="btn-outline" onclick="clearNews()">Smazat všechny</button>
    </div>
  </div>
  <div id="newsList" class="mt-4 space-y-3"></div>
</section>

<!-- Přihláška -->
<section id="prihlaska" class="card text-slate-900 hidden-admin">
  <h2 class="text-xl font-bold">Přihláška do klubu (vidí jen správce)</h2>
  <form id="appForm" class="grid md:grid-cols-2 gap-3" onsubmit="submitApplication(event)">
    <div class="md:col-span-2">
      <label class="block text-sm font-semibold">Celé jméno</label>
      <input id="appName" required class="mt-1 w-full rounded-xl border border-slate-300 px-3 py-2" placeholder="Jméno a příjmení" />
    </div>
    <div>
      <label class="block text-sm font-semibold">Věk</label>
      <input id="appAge" type="number" min="9" max="14" required class="mt-1 w-full rounded-xl border border-slate-300 px-3 py-2" />
    </div>
    <div>
      <label class="block text-sm font-semibold">Kontakt (e-mail nebo telefon)</label>
      <input id="appContact" required class="mt-1 w-full rounded-xl border border-slate-300 px-3 py-2" placeholder="Zadej e-mail nebo telefon" />
    </div>
    <div class="md:col-span-2">
      <label class="block text-sm font-semibold">Komentář (libovolný)</label>
      <textarea id="appNote" class="mt-1 w-full rounded-xl border border-slate-300 px-3 py-2" rows="3"></textarea>
    </div>
    <div class="md:col-span-2 flex items-center gap-3">
      <button class="btn-primary" type="submit">Odeslat přihlášku</button>
      <span id="appMsg" class="text-sm"></span>
    </div>
  </form>
  <div class="mt-6">
    <h3 class="font-bold">Přijaté přihlášky</h3>
    <ul id="appsList" class="mt-3 space-y-2"></ul>
  </div>
</section>

<!-- O nás -->
<section id="onas" class="card text-slate-900">
  <div class="flex items-center justify-between">
    <h2 class="text-xl font-bold">O nás</h2>
    <div id="aboutAdminBtns" class="hidden-admin">
      <button class="btn-outline" onclick="editAbout()">Upravit</button>
    </div>
  </div>
  <div id="aboutContent" class="mt-4 text-slate-700">Zatím žádné informace.</div>
  <div id="socialLinks" class="mt-4 space-y-2"></div>
</section>

<!-- Admin -->
<section id="admin" class="card text-slate-900">
  <h2 class="text-xl font-bold">Správcovský panel</h2>
  <p class="text-slate-700">Zadej kód správce pro odemčení úprav a zobrazení přihlášky. (Kód je „1235“.)</p>
  <div class="mt-3 flex flex-col md:flex-row gap-3 md:items-end">
    <div class="flex-1">
      <label class="block text-sm font-semibold">Kód správce</label>
      <input id="adminCodeInput" type="password" class="mt-1 w-full rounded-xl border border-slate-300 px-3 py-2" placeholder="••••" />
    </div>
    <div class="flex gap-2">
      <button class="btn-primary" onclick="enterAdmin()">Přihlásit se</button>
      <button class="btn-outline" onclick="logoutAdmin()">Odhlásit</button>
    </div>
  </div>
  <p id="adminStatus" class="mt-2 text-sm font-semibold"></p>
</section>

  </main>  <footer class="max-w-6xl mx-auto px-4 pb-16 text-center text-slate-300 text-sm">
    © <span id="year"></span> Fortnite of Legends • Vytvořeno pro tým
  </footer>  <script>
    const ADMIN_CODE = "1235";
    const store = {
      get(key, fallback) { try { return JSON.parse(localStorage.getItem(key)) ?? fallback; } catch { return fallback; }},
      set(key, value) { localStorage.setItem(key, JSON.stringify(value)); }
    };
    let isAdmin = store.get('isAdmin', false);

    function applyAdminUI() {
      document.querySelectorAll('.hidden-admin').forEach(el => el.style.display = isAdmin ? '' : 'none');
      document.getElementById('adminStatus').textContent = isAdmin ? '✅ Správcovský režim aktivní.' : '🔒 Režim zamčený.';
    }
    function enterAdmin() {
      if (document.getElementById('adminCodeInput').value.trim() === ADMIN_CODE) {
        isAdmin = true; store.set('isAdmin', true); applyAdminUI(); alert('Vítej, správce!');
      } else { alert('Špatný kód.'); }
    }
    function logoutAdmin(){ isAdmin=false; store.set('isAdmin',false); applyAdminUI(); }

    function submitApplication(ev){
      ev.preventDefault();
      const name=document.getElementById('appName').value.trim();
      const age=parseInt(document.getElementById('appAge').value,10);
      const contact=document.getElementById('appContact').value.trim();
      const note=document.getElementById('appNote').value.trim();
      const msg=document.getElementById('appMsg');
      if(!(age>=9&&age<=14)){ msg.textContent='❌ Věk musí být 9–14.'; msg.className='text-red-600'; return; }
      if(!contact){ msg.textContent='❌ Zadej kontakt (e-mail nebo telefon).'; msg.className='text-red-600'; return; }
      const apps=store.get('applications',[]);
      apps.push({name,age,contact,note,ts:Date.now()});
      store.set('applications',apps);
      document.getElementById('appForm').reset();
      msg.textContent='✅ Přihláška uložena.'; msg.className='text-green-600';
      renderApplications();
    }
    function renderApplications(){
      const ul=document.getElementById('appsList');
      const apps=store.get('applications',[]);
      ul.innerHTML='';
      if(!apps.length){ ul.innerHTML='<li>Žádné přihlášky.</li>'; return; }
      apps.forEach(a=>{
        const li=document.createElement('li');
        li.className='p-3 rounded-xl bg-white border border-slate-200';
        li.innerHTML=`<div><strong>${a.name}</strong> • ${a.age} let<br>Kontakt: ${a.contact}<br>${a.note||''}</div>`;
        ul.appendChild(li);
      });
    }

    function editAbout(){
      const text=prompt('Uprav text O nás:', store.get('aboutText',''));
      if(text!==null){ store.set('aboutText',text); renderAbout(); }
      const links=prompt('Zadej odkazy na sociální sítě (oddělené čárkou):', store.get('socialLinks',''));
      if(links!==null){ store.set('socialLinks',links); renderAbout(); }
    }
    function renderAbout(){
      document.getElementById('aboutContent').textContent=store.get('aboutText','Zatím žádné informace.');
      const wrap=document.getElementById('socialLinks'); wrap.innerHTML='';
      const links=(store.get('socialLinks','')).split(',').map(l=>l.trim()).filter(Boolean);
      links.forEach(l=>{ const a=document.createElement('a'); a.href=l; a.textContent=l; a.className='block text-indigo-600 underline'; wrap.appendChild(a); });
    }

    function init(){
      document.getElementById('year').textContent=new Date().getFullYear();
      applyAdminUI(); renderApplications(); renderAbout();
    }
    window.addEventListener('DOMContentLoaded',init);
  </script></body>
</html>
