# americaffeyalegria
<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Plataforma - Colegio América B Fe y Alegría</title>
  <style>
    :root{--accent:#0b76ef;--bg:#f6f8fb;--card:#fff;--muted:#6b7280}
    *{box-sizing:border-box;font-family:Inter, system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial}
    body{margin:0;background:linear-gradient(180deg,#eef4ff 0%,var(--bg)100%);color:#0f172a}
    header{display:flex;align-items:center;gap:16px;padding:18px 24px;background:var(--card);box-shadow:0 1px 6px rgba(12,20,40,0.06)}
    .logo{width:56px;height:56px;border-radius:8px;object-fit:cover;background:#e6eefc;border:1px solid #dbeafe}
    .title{font-size:18px;font-weight:700}
    .subtitle{font-size:12px;color:var(--muted)}
    main{max-width:1000px;margin:24px auto;padding:0 16px}
    .hero{display:grid;grid-template-columns:1fr 320px;gap:20px;align-items:start}
    .card{background:var(--card);padding:16px;border-radius:12px;box-shadow:0 6px 18px rgba(11,36,71,0.06)}
    .login{display:flex;flex-direction:column;gap:8px}
    input[type=text],textarea,select{width:100%;padding:10px;border-radius:8px;border:1px solid #e6eef7}
    button{background:var(--accent);color:#fff;padding:10px 12px;border:0;border-radius:10px;cursor:pointer}
    .muted{color:var(--muted);font-size:13px}
    .posts{margin-top:18px;display:grid;gap:12px}
    .post{padding:12px;border-radius:10px;background:linear-gradient(180deg,#fff,#fbfdff);border:1px solid #eef3ff}
    .post h3{margin:0 0 6px 0}
    .meta{font-size:12px;color:var(--muted);display:flex;gap:12px;align-items:center}
    .post img{max-width:100%;border-radius:8px;margin-top:8px}
    .actions{display:flex;gap:8px;margin-top:8px}
    .ghost{background:transparent;border:1px solid #e6eef7;color:var(--muted);padding:8px;border-radius:8px;cursor:pointer}
    .toast{position:fixed;right:18px;bottom:18px;background:#111;color:#fff;padding:12px 16px;border-radius:8px;box-shadow:0 8px 30px rgba(2,6,23,0.4)}
    footer{max-width:1000px;margin:32px auto;color:var(--muted);text-align:center}
    @media(max-width:880px){.hero{grid-template-columns:1fr;}.logo{width:48px;height:48px}}
  </style>
</head>
<body>
  <header>
    <!-- Aquí puedes poner tu logo real -->
    <img id="logoImg" class="logo" src="logo_colegio.jpg" alt="Logo Colegio América B Fe y Alegría" />
    <div>
      <div class="title">Colegio América B — Fe y Alegría</div>
      <div class="subtitle">Plataforma Escolar — Lectura pública / Edición con código</div>
    </div>
  </header>

  <main>
    <section class="hero">
      <div class="card">
        <div id="authArea">
          <!-- Zona de acceso -->
          <h2 id="welcome">Bienvenido</h2>
          <p id="introMsg" class="muted">Introduce el código para editar. Si no tienes código, entra como visitante y podrás leer la información.</p>

          <div class="login" id="loginBox">
            <input id="accessCode" type="text" placeholder="Ingresa el código" />
            <div style="display:flex;gap:8px">
              <button id="enterBtn">Entrar como editor</button>
              <button id="visitorBtn" class="ghost">Entrar como visitante</button>
            </div>
            <div style="margin-top:8px;display:flex;gap:8px;align-items:center">
              <label class="muted">Número de editores permitidos:</label>
              <select id="numEditorsSelect" title="Cambiar cantidad de códigos" aria-label="editores">
                <option value="1">Solo 1</option>
                <option value="2">Hasta 2</option>
              </select>
            </div>
          </div>

          <div id="editorInfo" style="display:none;margin-top:12px">
            <div class="muted">Has entrado como <strong id="whoName">Editor</strong>.</div>
            <div style="margin-top:8px;display:flex;gap:8px">
              <button id="logoutBtn" class="ghost">Salir</button>
              <button id="uploadLogoBtn" class="ghost">Cambiar logo</button>
              <button id="uploadHeroBtn" class="ghost">Cambiar imagen principal</button>
            </div>
          </div>
        </div>

        <div id="editorPanel" style="display:none;margin-top:18px">
          <h3>Crear publicación / archivo</h3>
          <input id="postTitle" placeholder="Título (opcional)" />
          <textarea id="postBody" rows="4" placeholder="Escribe aquí..."></textarea>
          <div style="display:flex;gap:8px;margin-top:8px;align-items:center">
            <input id="postImage" type="file" accept="image/*" />
            <select id="expireSelect" title="Duración">
              <option value="0">No expira</option>
              <option value="3600">1 hora</option>
              <option value="86400">1 día</option>
              <option value="604800">7 días</option>
            </select>
            <button id="addPostBtn">Subir</button>
          </div>
          <div class="muted" style="margin-top:8px">Las publicaciones se almacenan localmente en el navegador (localStorage). Esta versión funciona sin servidor (ideal para pruebas/labs).</div>
        </div>

        <div style="margin-top:18px">
          <h3>Mensajes / Anuncios</h3>
          <div id="posts" class="posts"></div>
        </div>
      </div>

      <aside class="card">
        <div style="text-align:center">
          <img id="heroImg" src="https://via.placeholder.com/300x180?text=Imagen+principal" alt="Imagen principal" style="width:100%;height:auto;border-radius:10px;object-fit:cover" />
          <h4 style="margin:12px 0 6px 0">Plantilla principal</h4>
          <p class="muted">Esta imagen y el logo se pueden reemplazar desde el botón "Cambiar logo" o "Cambiar imagen principal" (sólo editores).</p>
        </div>
      </aside>
    </section>

    <footer>
      <small>Nota: la protección por código es local (lado cliente). No es adecuada para información sensible.</small>
    </footer>
  </main>

  <!-- Hidden file inputs -->
  <input id="hiddenLogo" type="file" accept="image/*" style="display:none" />
  <input id="hiddenHero" type="file" accept="image/*" style="display:none" />

  <div id="toast" class="toast" style="display:none"></div>

  <script>
    /***** CONFIGURACIÓN (personalizada) *****/
    const CONFIG = {
      editorCodes: ['AmericaFeYAlegria'], // Nuevo código único
      allowTwoEditorsDefault: false,
      expiryMessage: 'Esta publicación ha expirado y fue eliminada',
    };
    /***** FIN DE CONFIGURACIÓN *****/

    const $ = id => document.getElementById(id);
    const toast = msg => {
      const t = $('toast'); t.textContent = msg; t.style.display='block';
      setTimeout(()=>t.style.display='none', 4000);
    }

    const LS_POSTS='site_posts_v1', LS_LOGO='site_logo_v1', LS_HERO='site_hero_v1', LS_CODES='site_codes_v1';
    let currentEditor=null;

    function ensureCodes(){const saved=JSON.parse(localStorage.getItem(LS_CODES)||'null');if(!saved)localStorage.setItem(LS_CODES,JSON.stringify(CONFIG.editorCodes));}
    function loadCodes(){try{return JSON.parse(localStorage.getItem(LS_CODES)||'[]');}catch(e){return[]}}
    function loadPosts(){try{const arr=JSON.parse(localStorage.getItem(LS_POSTS)||'[]');return Array.isArray(arr)?arr:[]}catch(e){return[]}}
    function savePosts(posts){localStorage.setItem(LS_POSTS,JSON.stringify(posts));}
    function addPost(post){const posts=loadPosts();posts.unshift(post);savePosts(posts);renderPosts();}
    function deletePost(id){let posts=loadPosts();posts=posts.filter(p=>p.id!==id);savePosts(posts);renderPosts();}
    function escapeHtml(s){if(!s)return'';return s.replace(/[&<>"]/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;","\"":"&quot;"}[c]||c));}
    function formatBody(text){if(!text)return'';return `<div>${escapeHtml(text).replace(/\n/g,'<br>')}</div>`}
    function uid(){return Date.now().toString(36)+'-'+Math.random().toString(36).slice(2,9);}
    function enterWithCode(code){const codes=loadCodes();if(codes.includes(code)){currentEditor=code;onEnterEditor();localStorage.setItem('current_editor_code',code);return true;}return false;}
    function leaveEditor(){currentEditor=null;localStorage.removeItem('current_editor_code');onLeaveEditor();}

    function onEnterEditor(){
      $('loginBox').style.display='none';
      $('editorInfo').style.display='block';
      $('editorPanel').style.display='block';
      $('welcome').style.display='none';
      $('introMsg').style.display='none';
      toast('Modo editor activado');
      renderPosts();
    }

    function onLeaveEditor(){
      $('loginBox').style.display='flex';
      $('editorInfo').style.display='none';
      $('editorPanel').style.display='none';
      $('welcome').style.display='none';
      $('introMsg').style.display='none';
      toast('Has salido');
      renderPosts();
    }

    function tryRestoreSession(){const code=localStorage.getItem('current_editor_code');if(code&&loadCodes().includes(code)){currentEditor=code;onEnterEditor();}}

    async function fileToDataUrl(file){return new Promise((res,rej)=>{const r=new FileReader();r.onload=()=>res(r.result);r.onerror=rej;r.readAsDataURL(file);})}
    async function handleReplaceLogo(file){if(!file)return;const data=await fileToDataUrl(file);localStorage.setItem(LS_LOGO,data);loadAssets();toast('Logo actualizado');}
    async function handleReplaceHero(file){if(!file)return;const data=await fileToDataUrl(file);localStorage.setItem(LS_HERO,data);loadAssets();toast('Imagen principal actualizada');}
    function loadAssets(){const logo=localStorage.getItem(LS_LOGO);if(logo)$('logoImg').src=logo;const hero=localStorage.getItem(LS_HERO);if(hero)$('heroImg').src=hero;}

    function renderPosts(){
      const c=$('posts');c.innerHTML='';
      let posts=loadPosts(),now=Date.now(),changed=false;
      posts=posts.filter(p=>{if(p.expiresAt&&p.expiresAt<=now){changed=true;return false;}return true;});
      if(changed){savePosts(posts);toast(CONFIG.expiryMessage);}
      if(posts.length===0){c.innerHTML='<div class="muted">No hay publicaciones todavía.</div>';return;}
      posts.forEach(p=>{
        const el=document.createElement('div');el.className='post';
        const title=p.title?`<h3>${escapeHtml(p.title)}</h3>`:'';const when=new Date(p.createdAt).toLocaleString();const exp=p.expiresAt?(' • expira: '+new Date(p.expiresAt).toLocaleString()):'';
        el.innerHTML=`${title}<div class="meta">Por: <strong>${escapeHtml(p.authorName||'Editor')}</strong> • ${when}${exp}</div><div style="margin-top:8px">${formatBody(p.body)}</div>`;
        if(p.imageData){const img=document.createElement('img');img.src=p.imageData;el.appendChild(img);}
        const actions=document.createElement('div');actions.className='actions';
        if(currentEditor){const del=document.createElement('button');del.textContent='Eliminar';del.className='ghost';del.onclick=()=>{if(confirm('Eliminar publicación?'))deletePost(p.id);};actions.appendChild(del);}
        el.appendChild(actions);c.appendChild(el);
      });
    }

    (function init(){
      // === CONFIGURACIÓN DE BLOQUEO ===
  const LS_ATTEMPTS = 'login_attempts';
  const LS_BLOCKED_UNTIL = 'blocked_until';
  const MAX_ATTEMPTS = 3;
  const BLOCK_DURATION = 60 * 60 * 1000; // 1 hora
  let countdownTimer = null;

  // Crear un temporizador visible
  const timerEl = document.createElement('div');
  timerEl.id = 'blockTimer';
  timerEl.style.color = 'crimson';
  timerEl.style.fontWeight = '600';
  timerEl.style.marginTop = '10px';
  $('loginBox').appendChild(timerEl);

  // Función para comprobar si hay bloqueo
  function isBlocked() {
    const until = parseInt(localStorage.getItem(LS_BLOCKED_UNTIL) || '0', 10);
    if (!until) return false;
    const now = Date.now();
    if (now >= until) {
      localStorage.removeItem(LS_BLOCKED_UNTIL);
      localStorage.removeItem(LS_ATTEMPTS);
      timerEl.textContent = '';
      return false;
    }
    return true;
  }

  // Desactivar botones
  function disableAccessButtons() {
    $('enterBtn').disabled = true;
    $('visitorBtn').disabled = true;
    $('accessCode').disabled = true;
    $('enterBtn').style.opacity = '0.5';
    $('visitorBtn').style.opacity = '0.5';
  }

  // Activar botones
  function enableAccessButtons() {
    $('enterBtn').disabled = false;
    $('visitorBtn').disabled = false;
    $('accessCode').disabled = false;
    $('enterBtn').style.opacity = '1';
    $('visitorBtn').style.opacity = '1';
  }

  // Mostrar cuenta regresiva
  function startCountdown() {
    clearInterval(countdownTimer);
    countdownTimer = setInterval(() => {
      const until = parseInt(localStorage.getItem(LS_BLOCKED_UNTIL) || '0', 10);
      if (!until) {
        timerEl.textContent = '';
        clearInterval(countdownTimer);
        enableAccessButtons();
        return;
      }
      const remaining = until - Date.now();
      if (remaining <= 0) {
        timerEl.textContent = '';
        clearInterval(countdownTimer);
        enableAccessButtons();
        localStorage.removeItem(LS_BLOCKED_UNTIL);
        localStorage.removeItem(LS_ATTEMPTS);
        toast('Bloqueo finalizado. Puedes volver a intentar.');
        return;
      }
      const mins = Math.floor(remaining / 60000);
      const secs = Math.floor((remaining % 60000) / 1000);
      timerEl.textContent = `⏳ Bloqueado: faltan ${mins} min ${secs < 10 ? '0'+secs : secs} s`;
    }, 1000);
  }

  // Si ya está bloqueado al cargar
  if (isBlocked()) {
    disableAccessButtons();
    startCountdown();
  } else {
    enableAccessButtons();
  }

  // === EVENTOS ===
  $('enterBtn').addEventListener('click', () => {
    if (isBlocked()) {
      toast('Acceso bloqueado temporalmente.');
      disableAccessButtons();
      startCountdown();
      return;
    }

    const code = $('accessCode').value.trim();
    if (!code) { toast('Ingresa un código'); return; }

    if (enterWithCode(code)) {
      localStorage.removeItem(LS_ATTEMPTS);
      localStorage.removeItem(LS_BLOCKED_UNTIL);
      timerEl.textContent = '';
      const s = $('numEditorsSelect');
      s.value = loadCodes().length > 1 ? '2' : '1';
    } else {
      let attempts = parseInt(localStorage.getItem(LS_ATTEMPTS) || '0', 10);
      attempts++;
      localStorage.setItem(LS_ATTEMPTS, attempts);

      if (attempts >= MAX_ATTEMPTS) {
        const blockUntil = Date.now() + BLOCK_DURATION;
        localStorage.setItem(LS_BLOCKED_UNTIL, blockUntil);
        alert("Has superado el número máximo de intentos. Se notificará al administrador.");
        disableAccessButtons();
        startCountdown();
      } else {
        toast(`Código incorrecto. Intento ${attempts} de ${MAX_ATTEMPTS}`);
      }
    }


  $('visitorBtn').addEventListener('click', () => {
    if (isBlocked()) {
      toast('Acceso bloqueado temporalmente.');
      disableAccessButtons();
      startCountdown();
      return;
    }
    leaveEditor();
    $('loginBox').style.display = 'none';
    $('editorInfo').style.display = 'none';
    $('editorPanel').style.display = 'none';
    $('welcome').style.display = 'none';
    $('introMsg').style.display = 'none';
    toast('Modo visitante');
    renderPosts();
  });

  $('logoutBtn').addEventListener('click', () => leaveEditor());

  $('addPostBtn').addEventListener('click', async () => {
    if (!currentEditor) { toast('Necesitas entrar con código para subir'); return; }
    const title = $('postTitle').value.trim(), body = $('postBody').value.trim();
    let imgData = null; const f = $('postImage').files[0];
    if (f) imgData = await fileToDataUrl(f);
    const expSec = parseInt($('expireSelect').value, 10), now = Date.now(), expAt = expSec > 0 ? now + expSec * 1000 : null;
    const post = { id: uid(), title, body, imageData: imgData, createdAt: now, expiresAt: expAt, authorCode: currentEditor, authorName: 'Editor' };
    addPost(post);
    $('postTitle').value = ''; $('postBody').value = ''; $('postImage').value = '';
    toast('Subido');
  });

  $('uploadLogoBtn').addEventListener('click', () => { if (!currentEditor) { toast('Solo editores'); return; } $('hiddenLogo').click(); });
  $('hiddenLogo').addEventListener('change', e => { const f = e.target.files[0]; if (f) handleReplaceLogo(f); });
  $('uploadHeroBtn').addEventListener('click', () => { if (!currentEditor) { toast('Solo editores'); return; } $('hiddenHero').click(); });
  $('hiddenHero').addEventListener('change', e => { const f = e.target.files[0]; if (f) handleReplaceHero(f); });
  $('numEditorsSelect').addEventListener('change', e => {
    let codes = loadCodes();
    if (e.target.value === '1') { codes = [codes[0] || 'AmericaFeYAlegria']; }
    else { if (codes.length === 1) codes.push('prof456'); }
    localStorage.setItem(LS_CODES, JSON.stringify(codes));
    toast('Configuración actualizada (número de códigos)');
  });
  $('accessCode').addEventListener('keydown', e => { if (e.key === 'Enter') $('enterBtn').click(); });
  setInterval(() => renderPosts(), 10000);
})();    
      ensureCodes();loadAssets();renderPosts();tryRestoreSession();
      $('enterBtn').addEventListener('click',()=>{
        const code=$('accessCode').value.trim();
        if(!code){toast('Ingresa un código');return;}
        if(enterWithCode(code)){
          const s=$('numEditorsSelect');s.value=loadCodes().length>1?'2':'1';
        }else{alert('Código incorrecto. Entra como visitante o pide el código al administrador.');}
      });
      $('visitorBtn').addEventListener('click',()=>{
        leaveEditor();
        $('loginBox').style.display='none';
        $('editorInfo').style.display='none';
        $('editorPanel').style.display='none';
        $('welcome').style.display='none';
        $('introMsg').style.display='none';
        toast('Modo visitante');
        renderPosts();
      });
      $('logoutBtn').addEventListener('click',()=>leaveEditor());
      $('addPostBtn').addEventListener('click',async()=>{
        if(!currentEditor){toast('Necesitas entrar con código para subir');return;}
        const title=$('postTitle').value.trim(),body=$('postBody').value.trim();
        let imgData=null;const f=$('postImage').files[0];if(f)imgData=await fileToDataUrl(f);
        const expSec=parseInt($('expireSelect').value,10),now=Date.now(),expAt=expSec>0?now+expSec*1000:null;
        const post={id:uid(),title,body,imageData:imgData,createdAt:now,expiresAt:expAt,authorCode:currentEditor,authorName:'Editor'};
        addPost(post);$('postTitle').value='';$('postBody').value='';$('postImage').value='';toast('Subido');
      });
      $('uploadLogoBtn').addEventListener('click',()=>{if(!currentEditor){toast('Solo editores');return;}$('hiddenLogo').click();});
      $('hiddenLogo').addEventListener('change',e=>{const f=e.target.files[0];if(f)handleReplaceLogo(f);});
      $('uploadHeroBtn').addEventListener('click',()=>{if(!currentEditor){toast('Solo editores');return;}$('hiddenHero').click();});
      $('hiddenHero').addEventListener('change',e=>{const f=e.target.files[0];if(f)handleReplaceHero(f);});
      $('numEditorsSelect').addEventListener('change',e=>{
        let codes=loadCodes();
        if(e.target.value==='1'){codes=[codes[0]||'AmericaFeYAlegria'];}
        else{if(codes.length===1)codes.push('prof456');}
        localStorage.setItem(LS_CODES,JSON.stringify(codes));
        toast('Configuración actualizada (número de códigos)');
      });
      $('accessCode').addEventListener('keydown',e=>{if(e.key==='Enter')$('enterBtn').click();});
      setInterval(()=>renderPosts(),10000);
    })();
  </script>
</body>
</html>
