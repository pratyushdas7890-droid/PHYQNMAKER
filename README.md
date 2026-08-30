
<html lang="bn">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, interactive-widget=resizes-content">
  <title>Physics Exam Paper Studio Pro</title>
  
  <!-- Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@500;600&family=Noto+Sans+Bengali:wght@400;500;600;700&display=swap" rel="stylesheet">
  
  <style>
    :root {
      --bg-gradient: radial-gradient(circle at 50% 0%, #172554 0%, #090d16 60%, #030712 100%);
      --panel-bg: rgba(15, 23, 42, 0.75);
      --glass-border: rgba(255, 255, 255, 0.08);
      --glass-border-focus: rgba(56, 189, 248, 0.4);
      --card-bg: rgba(30, 41, 59, 0.5);
      --key-bg: #1e293b;
      --key-hover: #334155;
      
      --cyan-glow: #38bdf8;
      --emerald-glow: #10b981;
      --indigo-glow: #6366f1;
      --rose-glow: #f43f5e;
      --amber-glow: #f59e0b;

      --text-main: #f8fafc;
      --text-sub: #cbd5e1;
      --text-muted: #94a3b8;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      -webkit-tap-highlight-color: transparent;
    }

    body {
      font-family: 'Noto Sans Bengali', system-ui, sans-serif;
      background: var(--bg-gradient);
      color: var(--text-main);
      height: 100dvh;
      display: flex;
      flex-direction: column;
      overflow: hidden;
      position: relative;
    }

    /* ১. অটো-অ্যাডাপ্টিভ শীর্ষ কমান্ড বার */
    .top-bar {
      background: var(--panel-bg);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      border-bottom: 1px solid var(--glass-border);
      padding: clamp(6px, 1.2vh, 12px) clamp(10px, 2vw, 24px);
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: clamp(6px, 1.5vw, 14px);
      flex-shrink: 0;
      z-index: 20;
      box-shadow: 0 4px 25px rgba(0, 0, 0, 0.4);
    }

    .brand-title {
      font-size: clamp(0.85rem, 1.4vw + 0.4rem, 1.15rem);
      font-weight: 700;
      display: flex;
      align-items: center;
      gap: 6px;
      background: linear-gradient(135deg, #38bdf8, #818cf8);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      white-space: nowrap;
    }

    .brand-icon {
      font-size: clamp(1rem, 1.6vw, 1.35rem);
      -webkit-text-fill-color: initial;
      filter: drop-shadow(0 0 8px rgba(56, 189, 248, 0.5));
    }

    .action-group {
      display: flex;
      gap: clamp(4px, 0.8vw, 10px);
      align-items: center;
      overflow-x: auto;
      scrollbar-width: none;
    }
    .action-group::-webkit-scrollbar { display: none; }

    .action-btn {
      font-family: inherit;
      border: none;
      outline: none;
      font-size: clamp(0.72rem, 0.9vw + 0.3rem, 0.88rem);
      font-weight: 600;
      padding: clamp(5px, 0.9vh, 9px) clamp(8px, 1.2vw, 16px);
      border-radius: 8px;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      gap: 5px;
      white-space: nowrap;
      transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.25);
    }
    .action-btn:active { transform: scale(0.94); }

    .btn-mcq { background: linear-gradient(135deg, #4f46e5, #6366f1); color: #fff; }
    .btn-mcq:hover { box-shadow: 0 0 15px rgba(99, 102, 241, 0.4); }

    .btn-save { background: linear-gradient(135deg, #059669, #10b981); color: #022c1e; font-weight: 700; }
    .btn-save:hover { box-shadow: 0 0 15px rgba(16, 185, 129, 0.4); }

    .btn-copy { background: #1e293b; color: #f8fafc; border: 1px solid var(--glass-border); }
    .btn-copy:hover { background: #334155; }

    .btn-clear { background: rgba(244, 63, 94, 0.12); color: #fb7185; border: 1px solid rgba(244, 63, 94, 0.25); }
    .btn-clear:hover { background: rgba(244, 63, 94, 0.25); color: #fff; }

    /* ২. ইউনিভার্সাল ফ্লুইড ওয়ার্কস্পেস */
    .workspace {
      flex: 1;
      display: grid;
      padding: clamp(6px, 1.2vw, 16px);
      gap: clamp(6px, 1.2vw, 16px);
      overflow: hidden;
      max-width: 1800px;
      width: 100%;
      margin: 0 auto;
    }

    /* স্ক্রিন সাইজ অনুযায়ী গ্রিড অ্যাডজাস্টমেন্ট */
    /* ট্যাবলেট ল্যান্ডস্কেপ ও পিসি/ল্যাপটপ (> 850px) */
    @media (min-width: 851px) {
      .workspace {
        grid-template-columns: 1fr clamp(320px, 34vw, 480px);
        grid-template-rows: 1fr;
      }
    }

    /* মোবাইল ও পোর্ট্রেট ট্যাবলেট (<= 850px) */
    @media (max-width: 850px) {
      .workspace {
        grid-template-columns: 1fr;
        grid-template-rows: 1fr auto;
      }
    }

    /* ৩. ডিজিটাল খাতা (Editor Panel) */
    .editor-card {
      background: var(--panel-bg);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      border: 1px solid var(--glass-border);
      border-radius: clamp(10px, 1.5vw, 16px);
      display: flex;
      flex-direction: column;
      overflow: hidden;
      box-shadow: 0 8px 32px rgba(0, 0, 0, 0.4);
      transition: border-color 0.2s;
      min-height: 0;
    }

    .editor-card:focus-within {
      border-color: var(--glass-border-focus);
      box-shadow: 0 8px 32px rgba(0, 0, 0, 0.4), 0 0 15px rgba(56, 189, 248, 0.15);
    }

    textarea {
      flex: 1;
      width: 100%;
      height: 100%;
      background: transparent;
      color: #f8fafc;
      border: none;
      outline: none;
      padding: clamp(10px, 1.8vw, 22px);
      font-size: clamp(0.95rem, 1.1vw + 0.4rem, 1.22rem);
      line-height: 1.8;
      font-family: 'Noto Sans Bengali', 'Cambria Math', 'Fira Code', sans-serif;
      resize: none;
      overflow-y: auto;
    }

    textarea::placeholder { color: #475569; }

    .editor-status {
      background: rgba(10, 15, 29, 0.85);
      border-top: 1px solid var(--glass-border);
      padding: clamp(5px, 0.8vh, 10px) clamp(10px, 1.5vw, 18px);
      font-size: clamp(0.7rem, 0.8vw + 0.2rem, 0.84rem);
      color: var(--text-muted);
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-shrink: 0;
    }

    .auto-save-pill {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      color: #34d399;
    }
    .pulse-dot {
      width: clamp(6px, 0.8vw, 8px);
      height: clamp(6px, 0.8vw, 8px);
      background: #10b981;
      border-radius: 50%;
      box-shadow: 0 0 8px #10b981;
    }

    /* ৪. ফ্লুইড সাইন্টিফিক কিপ্যাড */
    .keypad-card {
      background: var(--panel-bg);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      border: 1px solid var(--glass-border);
      border-radius: clamp(10px, 1.5vw, 16px);
      display: flex;
      flex-direction: column;
      padding: clamp(8px, 1.2vw, 14px);
      gap: clamp(6px, 1vh, 10px);
      box-shadow: 0 8px 32px rgba(0, 0, 0, 0.4);
      min-height: 0;
    }

    .cat-selector {
      display: grid;
      grid-template-columns: repeat(5, 1fr);
      gap: clamp(3px, 0.6vw, 6px);
      flex-shrink: 0;
    }

    .cat-btn {
      background: var(--card-bg);
      border: 1px solid var(--glass-border);
      color: var(--text-muted);
      padding: clamp(5px, 0.9vh, 8px) 2px;
      font-size: clamp(0.65rem, 0.8vw + 0.15rem, 0.82rem);
      font-weight: 600;
      border-radius: 6px;
      cursor: pointer;
      text-align: center;
      transition: all 0.2s ease;
      user-select: none;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }
    .cat-btn:hover { color: #fff; background: rgba(255, 255, 255, 0.08); }
    .cat-btn.active {
      background: linear-gradient(135deg, rgba(56, 189, 248, 0.2), rgba(99, 102, 241, 0.2));
      color: var(--cyan-glow);
      font-weight: 700;
      border-color: var(--cyan-glow);
      box-shadow: 0 0 10px rgba(56, 189, 248, 0.2);
    }

    /* স্বয়ংক্রিয় অ্যাডাপ্টিভ সিম্বল ম্যাট্রিক্স */
    .symbol-matrix {
      flex: 1;
      display: grid;
      /* স্ক্রিনের জায়গা বুঝে বাটন নিজে থেকে বড়/ছোট ও সংখ্যা ঠিক করে নেবে */
      grid-template-columns: repeat(auto-fill, minmax(clamp(40px, 6.2vw, 56px), 1fr));
      grid-auto-rows: clamp(38px, 5.2vh, 52px);
      gap: clamp(4px, 0.8vw, 8px);
      background: rgba(10, 15, 29, 0.7);
      padding: clamp(6px, 1vw, 12px);
      border-radius: 10px;
      border: 1px solid var(--glass-border);
      align-content: start;
      overflow-y: auto;
      scrollbar-width: thin;
    }

    @media (max-width: 850px) {
      .symbol-matrix {
        max-height: clamp(170px, 32vh, 260px);
      }
    }

    .symbol-matrix::-webkit-scrollbar { width: 4px; }
    .symbol-matrix::-webkit-scrollbar-thumb { background: var(--key-hover); border-radius: 4px; }

    .matrix-key {
      background: var(--key-bg);
      border: 1px solid var(--glass-border);
      color: #fff;
      font-size: clamp(1rem, 1.3vw + 0.4rem, 1.28rem);
      border-radius: 8px;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      font-family: 'Cambria Math', 'Segoe UI Symbol', 'Noto Sans Bengali', sans-serif;
      transition: all 0.12s ease;
      user-select: none;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
    }

    .matrix-key:hover {
      background: var(--key-hover);
      border-color: rgba(56, 189, 248, 0.4);
      transform: translateY(-2px);
    }
    .matrix-key:active {
      background: var(--cyan-glow);
      color: #041226;
      font-weight: 700;
      transform: scale(0.92);
      box-shadow: 0 0 12px var(--cyan-glow);
    }

    /* ৫. রেসপনসিভ টোস্ট পপআপ */
    .toast-container {
      position: fixed;
      top: clamp(55px, 9vh, 85px);
      left: 50%;
      transform: translateX(-50%) translateY(-20px);
      background: rgba(15, 23, 42, 0.94);
      backdrop-filter: blur(18px);
      -webkit-backdrop-filter: blur(18px);
      border: 1px solid var(--glass-border);
      padding: clamp(6px, 1.2vh, 12px) clamp(14px, 2.5vw, 24px);
      border-radius: 999px;
      box-shadow: 0 15px 35px rgba(0, 0, 0, 0.6), 0 0 20px rgba(56, 189, 248, 0.2);
      display: flex;
      align-items: center;
      gap: 8px;
      z-index: 1000;
      pointer-events: none;
      opacity: 0;
      visibility: hidden;
      max-width: 90vw;
      transition: all 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
    }

    .toast-container.show {
      opacity: 1;
      visibility: visible;
      transform: translateX(-50%) translateY(0);
    }

    .toast-icon {
      font-size: clamp(1rem, 1.4vw, 1.3rem);
      display: flex;
      align-items: center;
    }

    .toast-message {
      font-size: clamp(0.78rem, 1vw + 0.2rem, 0.95rem);
      font-weight: 600;
      color: #f8fafc;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }

    /* কনফার্মেশন মোডাল */
    .modal-overlay {
      position: fixed;
      inset: 0;
      background: rgba(3, 7, 18, 0.7);
      backdrop-filter: blur(8px);
      -webkit-backdrop-filter: blur(8px);
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 2000;
      opacity: 0;
      visibility: hidden;
      transition: all 0.25s ease;
      padding: 16px;
    }

    .modal-overlay.open {
      opacity: 1;
      visibility: visible;
    }

    .modal-box {
      background: #0f172a;
      border: 1px solid var(--glass-border);
      border-radius: 16px;
      padding: clamp(16px, 2.5vw, 24px);
      max-width: min(380px, 90vw);
      width: 100%;
      text-align: center;
      box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.8), 0 0 25px rgba(244, 63, 94, 0.15);
      transform: scale(0.9);
      transition: transform 0.25s cubic-bezier(0.34, 1.56, 0.64, 1);
    }

    .modal-overlay.open .modal-box { transform: scale(1); }
    .modal-icon { font-size: clamp(1.8rem, 3vw, 2.4rem); margin-bottom: 8px; }
    .modal-title { font-size: clamp(0.95rem, 1.4vw, 1.15rem); font-weight: 700; color: #fff; margin-bottom: 6px; }
    .modal-desc { font-size: clamp(0.78rem, 1vw, 0.88rem); color: var(--text-muted); margin-bottom: 18px; line-height: 1.5; }
    
    .modal-actions {
      display: flex;
      gap: 8px;
      justify-content: center;
    }
    .modal-btn {
      flex: 1;
      padding: clamp(7px, 1.2vh, 10px);
      border-radius: 8px;
      border: none;
      font-size: clamp(0.78rem, 1vw, 0.9rem);
      font-weight: 600;
      cursor: pointer;
      font-family: inherit;
    }
    .modal-btn.cancel { background: #334155; color: #fff; }
    .modal-btn.danger { background: #e11d48; color: #fff; }
  </style>
</head>
<body>

  <!-- পপআপ টোস্ট নোটিফিকেশন বার -->
  <div id="toast" class="toast-container">
    <div id="toastIcon" class="toast-icon">✨</div>
    <div id="toastMsg" class="toast-message">অপারেশন সফল হয়েছে!</div>
  </div>

  <!-- ক্লিয়ার কনফার্মেশন মোডাল -->
  <div id="clearModal" class="modal-overlay">
    <div class="modal-box">
      <div class="modal-icon">🗑️</div>
      <h3 class="modal-title">সব লেখা মুছে ফেলবেন?</h3>
      <p class="modal-desc">মুছে ফেললে পূর্বের ড্রাফট আর ফিরিয়ে আনা সম্ভব হবে না।</p>
      <div class="modal-actions">
        <button class="modal-btn cancel" onclick="closeClearModal()">না, থাক</button>
        <button class="modal-btn danger" onclick="confirmClearText()">হ্যাঁ, মুছুন</button>
      </div>
    </div>
  </div>

  <!-- শীর্ষ কমান্ড বার -->
  <header class="top-bar">
    <div class="brand-title">
      <span class="brand-icon">⚛️</span>
      <span>ফিজিক্স পেপার স্টুডিও</span>
    </div>
    
    <div class="action-group">
      <button class="action-btn btn-mcq" onpointerdown="preventBlurAndRun(event, insertMCQ)">➕ MCQ</button>
      <button class="action-btn btn-save" onpointerdown="preventBlurAndRun(event, saveToDevice)">💾 সেভ</button>
      <button class="action-btn btn-copy" onpointerdown="preventBlurAndRun(event, copyText)">📋 কপি</button>
      <button class="action-btn btn-clear" onpointerdown="preventBlurAndRun(event, openClearModal)">মুছুন</button>
    </div>
  </header>

  <!-- ইউনিভার্সাল ফ্লুইড ওয়ার্কস্পেস -->
  <main class="workspace">
    
    <!-- ডিজিটাল খাতা (Editor) -->
    <section class="editor-card">
      <textarea id="editor" placeholder="এখানে সরাসরি প্রশ্নপত্র লিখুন... কিপ্যাডের বাটনে ক্লিক করলে কীবোর্ড সক্রিয় রেখেই সিম্বল বসে যাবে।"></textarea>
      
      <div class="editor-status">
        <div class="auto-save-pill">
          <span class="pulse-dot"></span>
          <span id="saveStatus">ড্রাফট অটো-সেভ আছে</span>
        </div>
        <span id="statCount">লাইন: 1 | অক্ষর: 0</span>
      </div>
    </section>

    <!-- সাইন্টিফিক কিপ্যাড ম্যাট্রিক্স -->
    <section class="keypad-card">
      <div class="cat-selector">
        <button class="cat-btn active" onpointerdown="preventBlurAndSwitch(event, 'greek')">Greek</button>
        <button class="cat-btn" onpointerdown="preventBlurAndSwitch(event, 'phys')">Vector</button>
        <button class="cat-btn" onpointerdown="preventBlurAndSwitch(event, 'math')">Calculus</button>
        <button class="cat-btn" onpointerdown="preventBlurAndSwitch(event, 'script')">Power</button>
        <button class="cat-btn" onpointerdown="preventBlurAndSwitch(event, 'markers')">দাগ</button>
      </div>

      <div id="symbol-matrix" class="symbol-matrix"></div>
    </section>

  </main>

  <script>
    const symbolSets = {
      greek: [
        'α', 'β', 'γ', 'δ', 'ε', 'θ', 'λ', 'μ', 'π', 'ρ', 'σ', 'τ', 'φ', 'ψ', 'ω',
        'Δ', 'Γ', 'Θ', 'Λ', 'Σ', 'Φ', 'Ψ', 'Ω', 'η', 'κ', 'ν', 'ξ', 'ζ', 'χ'
      ],
      phys: [
        'î', 'ĵ', 'k̂', 'F⃗', 'v⃗', 'a⃗', 'r⃗', 'E⃗', 'B⃗', 'p⃗', 'ħ', 'Å', '℃', '℉', 'Ω',
        'μF', 'pF', 'μm', 'nm', 'm/s²', 'N', 'J', 'W', 'Pa', 'T', 'Wb', 'H', 'eV', 'C'
      ],
      math: [
        '±', '∓', '×', '÷', '·', '√', '∛', '∝', '≈', '≠', '≡', '≤', '≥', '∫', '∬',
        '∮', '∂', '∇', '∑', '∏', '∞', '→', '⇒', '⇌', '∠', '⊥', '°', '′', '″'
      ],
      script: [
        '⁰', '¹', '²', '³', '⁴', '⁵', '⁶', '⁷', '⁸', '⁹', '⁺', '⁻', 'ⁿ',
        '₀', '₁', '₂', '₃', '₄', '₅', '₆', '₇', '₈', '₉', '₊', '₋', 'ᵢ', 'ⱼ', 'ₖ'
      ],
      markers: [
        '(A)', '(B)', '(C)', '(D)', '(a)', '(b)', '(c)', '(d)',
        '(i)', '(ii)', '(iii)', '(iv)', '(v)',
        '[1]', '[2]', '[3]', '[4]', '[5]', 'Ans:', 'Q.'
      ]
    };

    const editor = document.getElementById('editor');
    const matrix = document.getElementById('symbol-matrix');
    const saveStatus = document.getElementById('saveStatus');
    const statCount = document.getElementById('statCount');
    const toast = document.getElementById('toast');
    const toastMsg = document.getElementById('toastMsg');
    const toastIcon = document.getElementById('toastIcon');
    const clearModal = document.getElementById('clearModal');
    let toastTimer = null;

    window.onload = () => {
      const saved = localStorage.getItem('physics_draft_text');
      if (saved) {
        editor.value = saved;
        updateCounts();
      }
      renderMatrix('greek');
    };

    editor.addEventListener('input', () => {
      localStorage.setItem('physics_draft_text', editor.value);
      saveStatus.innerText = 'ড্রাফট অটো-সেভ আছে';
      updateCounts();
    });

    function updateCounts() {
      const val = editor.value;
      const lines = val ? val.split('\n').length : 1;
      statCount.innerText = `লাইন: ${lines} | অক্ষর: ${val.length}`;
    }

    // পপআপ নোটিফিকেশন
    function showToast(message, icon = '✨', borderColor = 'var(--cyan-glow)') {
      toastMsg.innerText = message;
      toastIcon.innerText = icon;
      toast.style.borderColor = borderColor;
      toast.classList.add('show');

      clearTimeout(toastTimer);
      toastTimer = setTimeout(() => {
        toast.classList.remove('show');
      }, 2400);
    }

    // ম্যাট্রিক্স রেন্ডার করা (অটো-ফিট গ্রিড)
    function renderMatrix(cat) {
      matrix.innerHTML = '';
      symbolSets[cat].forEach(sym => {
        const btn = document.createElement('button');
        btn.className = 'matrix-key';
        btn.innerText = sym;
        btn.addEventListener('pointerdown', (e) => preventBlurAndInsert(e, sym));
        matrix.appendChild(btn);
      });
    }

    // কীবোর্ড ওপেন রেখে ইনসার্ট
    function preventBlurAndInsert(e, sym) {
      e.preventDefault();
      if (document.activeElement !== editor) {
        editor.focus();
      }
      const start = editor.selectionStart;
      const end = editor.selectionEnd;
      editor.setRangeText(sym, start, end, 'end');
      editor.dispatchEvent(new Event('input'));
    }

    // কীবোর্ড বজায় রেখে ট্যাব পরিবর্তন
    function preventBlurAndSwitch(e, cat) {
      e.preventDefault();
      document.querySelectorAll('.cat-btn').forEach(b => b.classList.remove('active'));
      e.currentTarget.classList.add('active');
      renderMatrix(cat);
    }

    // কীবোর্ড বজায় রেখে অ্যাকশন চালানো
    function preventBlurAndRun(e, fn) {
      e.preventDefault();
      fn();
    }

    function getNextQuestionNumber(text) {
      if (!text) return 1;
      const matches = [...text.matchAll(/(?:^|\n)\s*(\d+)\./g)];
      if (matches.length === 0) return 1;
      const nums = matches.map(m => parseInt(m[1], 10)).filter(n => !isNaN(n));
      return nums.length > 0 ? Math.max(...nums) + 1 : 1;
    }

    // MCQ ব্লক তৈরি
    function insertMCQ() {
      const currentText = editor.value.trimEnd();
      const nextNum = getNextQuestionNumber(currentText);
      
      const prefix = currentText.length > 0 ? '\n\n' : '';
      const questionHead = `${prefix}${nextNum}. `;
      const optionsBlock = `\n   (A)                 (B) \n   (C)                 (D) `;
      
      const newBlock = questionHead + optionsBlock;
      editor.value = currentText + newBlock;
      
      const targetCursorPos = currentText.length + questionHead.length;
      editor.selectionStart = editor.selectionEnd = targetCursorPos;
      editor.focus();
      editor.scrollTop = editor.scrollHeight;

      editor.dispatchEvent(new Event('input'));
      showToast(`প্রশ্ন নং ${nextNum} যুক্ত হয়েছে!`, '📝', 'var(--indigo-glow)');
    }

    // ডিভাইসে ফাইল সেভ করা
    async function saveToDevice() {
      const text = editor.value;
      if (!text.trim()) {
        showToast('সেভ করার মতো কোনো লেখা নেই!', '⚠️', 'var(--amber-glow)');
        return;
      }

      if ('showSaveFilePicker' in window) {
        try {
          const handle = await window.showSaveFilePicker({
            suggestedName: 'Physics_Question_Paper.txt',
            types: [{
              description: 'Text File',
              accept: { 'text/plain': ['.txt'] }
            }]
          });
          const writable = await handle.createWritable();
          await writable.write(text);
          await writable.close();
          showToast('ডিভাইসে ফাইল সেভ সম্পন্ন হয়েছে!', '💾', 'var(--emerald-glow)');
          return;
        } catch (err) {
          if (err.name === 'AbortError') return;
        }
      }

      const blob = new Blob(['\ufeff' + text], { type: 'text/plain;charset=utf-8' });
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = 'Physics_Question_Paper.txt';
      document.body.appendChild(a);
      a.click();
      document.body.removeChild(a);
      URL.revokeObjectURL(url);
      showToast('ফাইল ডাউনলোড সফল হয়েছে!', '💾', 'var(--emerald-glow)');
    }

    // ক্লিপবোর্ডে টেক্সট কপি করা
    function copyText() {
      if (!editor.value.trim()) {
        showToast('কপি করার মতো কিছু নেই!', '⚠️', 'var(--amber-glow)');
        return;
      }
      navigator.clipboard.writeText(editor.value).then(() => {
        showToast('ক্লিপবোর্ডে কপি সম্পন্ন হয়েছে!', '📋', 'var(--cyan-glow)');
      });
    }

    // ক্লিয়ার মোডাল ওপেন/ক্লোজ
    function openClearModal() {
      if (!editor.value.trim()) {
        showToast('খাতা ইতিমধ্যে খালি আছে!', 'ℹ️', 'var(--cyan-glow)');
        return;
      }
      clearModal.classList.add('open');
    }

    function closeClearModal() {
      clearModal.classList.remove('open');
    }

    function confirmClearText() {
      closeClearModal();
      editor.value = '';
      localStorage.removeItem('physics_draft_text');
      editor.dispatchEvent(new Event('input'));
      showToast('সব লেখা মুছে ফেলা হয়েছে!', '🗑️', 'var(--rose-glow)');
      editor.focus();
    }
  </script>
</body>
