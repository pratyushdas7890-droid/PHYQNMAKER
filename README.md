
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

    /* ১. গ্লাস টপ হেডার বার */
    .top-bar {
      background: var(--panel-bg);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      border-bottom: 1px solid var(--glass-border);
      padding: 10px 16px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      flex-shrink: 0;
      z-index: 20;
      box-shadow: 0 4px 25px rgba(0, 0, 0, 0.4);
    }

    .brand-title {
      font-size: 1.05rem;
      font-weight: 700;
      display: flex;
      align-items: center;
      gap: 8px;
      background: linear-gradient(135deg, #38bdf8, #818cf8);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      white-space: nowrap;
    }

    .brand-icon {
      font-size: 1.25rem;
      -webkit-text-fill-color: initial;
      filter: drop-shadow(0 0 8px rgba(56, 189, 248, 0.5));
    }

    .action-group {
      display: flex;
      gap: 8px;
      align-items: center;
    }

    .action-btn {
      font-family: inherit;
      border: none;
      outline: none;
      font-size: 0.82rem;
      font-weight: 600;
      padding: 7px 14px;
      border-radius: 8px;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      gap: 6px;
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

    /* ২. ওয়ার্কস্পেস */
    .workspace {
      flex: 1;
      display: grid;
      grid-template-columns: 1fr 410px;
      gap: 12px;
      padding: 12px;
      overflow: hidden;
    }

    @media (max-width: 920px) {
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
      border-radius: 14px;
      display: flex;
      flex-direction: column;
      overflow: hidden;
      box-shadow: 0 8px 32px rgba(0, 0, 0, 0.4);
      transition: border-color 0.2s;
    }

    .editor-card:focus-within {
      border-color: var(--glass-border-focus);
      box-shadow: 0 8px 32px rgba(0, 0, 0, 0.4), 0 0 15px rgba(56, 189, 248, 0.15);
    }

    textarea {
      flex: 1;
      width: 100%;
      background: transparent;
      color: #f8fafc;
      border: none;
      outline: none;
      padding: 18px;
      font-size: 1.15rem;
      line-height: 1.85;
      font-family: 'Noto Sans Bengali', 'Cambria Math', 'Fira Code', sans-serif;
      resize: none;
    }

    textarea::placeholder { color: #475569; }

    .editor-status {
      background: rgba(10, 15, 29, 0.8);
      border-top: 1px solid var(--glass-border);
      padding: 8px 14px;
      font-size: 0.78rem;
      color: var(--text-muted);
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .auto-save-pill {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      color: #34d399;
    }
    .pulse-dot {
      width: 7px;
      height: 7px;
      background: #10b981;
      border-radius: 50%;
      box-shadow: 0 0 8px #10b981;
    }

    /* ৪. সাইন্টিফিক সিম্বল ম্যাট্রিক্স কিপ্যাড */
    .keypad-card {
      background: var(--panel-bg);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      border: 1px solid var(--glass-border);
      border-radius: 14px;
      display: flex;
      flex-direction: column;
      padding: 12px;
      gap: 10px;
      box-shadow: 0 8px 32px rgba(0, 0, 0, 0.4);
    }

    .cat-selector {
      display: grid;
      grid-template-columns: repeat(5, 1fr);
      gap: 5px;
    }

    .cat-btn {
      background: var(--card-bg);
      border: 1px solid var(--glass-border);
      color: var(--text-muted);
      padding: 7px 4px;
      font-size: 0.74rem;
      font-weight: 600;
      border-radius: 8px;
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

    .symbol-matrix {
      flex: 1;
      display: grid;
      grid-template-columns: repeat(6, 1fr);
      grid-auto-rows: 46px;
      gap: 6px;
      background: rgba(10, 15, 29, 0.7);
      padding: 10px;
      border-radius: 10px;
      border: 1px solid var(--glass-border);
      align-content: start;
      max-height: 290px;
      overflow-y: auto;
    }

    @media (min-width: 921px) {
      .symbol-matrix {
        max-height: none;
        grid-template-columns: repeat(5, 1fr);
        grid-auto-rows: 50px;
      }
    }

    .matrix-key {
      background: var(--key-bg);
      border: 1px solid var(--glass-border);
      color: #fff;
      font-size: 1.18rem;
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

    /* ৫. প্রিমিয়াম গ্লাস পপআপ / টোস্ট নোটিফিকেশন */
    .toast-container {
      position: fixed;
      top: 75px;
      left: 50%;
      transform: translateX(-50%) translateY(-20px);
      background: rgba(15, 23, 42, 0.92);
      backdrop-filter: blur(18px);
      -webkit-backdrop-filter: blur(18px);
      border: 1px solid var(--glass-border);
      padding: 10px 20px;
      border-radius: 999px;
      box-shadow: 0 15px 35px rgba(0, 0, 0, 0.6), 0 0 20px rgba(56, 189, 248, 0.2);
      display: flex;
      align-items: center;
      gap: 10px;
      z-index: 1000;
      pointer-events: none;
      opacity: 0;
      visibility: hidden;
      transition: all 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
    }

    .toast-container.show {
      opacity: 1;
      visibility: visible;
      transform: translateX(-50%) translateY(0);
    }

    .toast-icon {
      font-size: 1.2rem;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .toast-message {
      font-size: 0.9rem;
      font-weight: 600;
      color: #f8fafc;
      white-space: nowrap;
    }

    /* কাস্টম কনফার্মেশন মোডাল */
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
      padding: 22px;
      max-width: 360px;
      width: 100%;
      text-align: center;
      box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.8), 0 0 25px rgba(244, 63, 94, 0.15);
      transform: scale(0.9);
      transition: transform 0.25s cubic-bezier(0.34, 1.56, 0.64, 1);
    }

    .modal-overlay.open .modal-box { transform: scale(1); }

    .modal-icon { font-size: 2.2rem; margin-bottom: 8px; }
    .modal-title { font-size: 1.1rem; font-weight: 700; color: #fff; margin-bottom: 6px; }
    .modal-desc { font-size: 0.86rem; color: var(--text-muted); margin-bottom: 18px; line-height: 1.5; }
    
    .modal-actions {
      display: flex;
      gap: 8px;
      justify-content: center;
    }
    .modal-btn {
      flex: 1;
      padding: 9px;
      border-radius: 8px;
      border: none;
      font-size: 0.88rem;
      font-weight: 600;
      cursor: pointer;
      font-family: inherit;
      transition: opacity 0.15s;
    }
    .modal-btn.cancel { background: #334155; color: #fff; }
    .modal-btn.danger { background: #e11d48; color: #fff; }
    .modal-btn:hover { opacity: 0.9; }
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

  <!-- মূল ওয়ার্কস্পেস -->
  <main class="workspace">
    
    <!-- ডিজিটাল খাতা (Editor) -->
    <section class="editor-card">
      <textarea id="editor" placeholder="Type question"></textarea>
      
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

    // ম্যাট্রিক্স রেন্ডার করা
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

    // কীবোর্ড বজায় রেখে সিম্বল বসানো
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

    // কীবোর্ড বজায় রেখে ট্যাব বদলানো
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

    // MCQ ব্লক তৈরি করা
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

    // মোডাল হ্যান্ডলার
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
