
<html lang="bn">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Physics Exam Question Maker</title>
  <!-- Google Fonts for Bengali & Symbols -->
  <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+Bengali:wght@400;600;700&family=JetBrains+Mono:wght@400;600&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg: #0b1120;
      --card: #1e293b;
      --card-border: #334155;
      --accent: #38bdf8;
      --accent-hover: #0ea5e9;
      --text: #f8fafc;
      --text-muted: #94a3b8;
      --btn-bg: #334155;
      --btn-hover: #475569;
      --save-btn: #10b981;
      --save-btn-hover: #059669;
      --danger-btn: #ef4444;
      --danger-hover: #dc2626;
    }
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: 'Noto Sans Bengali', 'Segoe UI', sans-serif;
      background-color: var(--bg);
      color: var(--text);
      padding: 16px;
      min-height: 100vh;
    }
    .container {
      max-width: 1300px;
      margin: 0 auto;
      display: grid;
      grid-template-columns: 1fr 380px;
      gap: 16px;
    }
    @media (max-width: 960px) {
      .container { grid-template-columns: 1fr; }
    }
    .card {
      background: var(--card);
      border: 1px solid var(--card-border);
      border-radius: 12px;
      padding: 16px;
      display: flex;
      flex-direction: column;
      gap: 12px;
      box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.3);
    }
    .header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 10px;
    }
    h1 { font-size: 1.25rem; color: var(--accent); display: flex; align-items: center; gap: 8px; }
    .toolbar {
      display: flex;
      gap: 8px;
      flex-wrap: wrap;
    }
    .action-btn {
      background: var(--accent);
      color: #0f172a;
      border: none;
      padding: 8px 14px;
      border-radius: 6px;
      font-weight: 600;
      cursor: pointer;
      font-size: 0.88rem;
      transition: all 0.2s;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      user-select: none;
    }
    .action-btn:hover { background: var(--accent-hover); transform: translateY(-1px); }
    .action-btn:active { transform: translateY(0); }
    .action-btn.secondary {
      background: var(--btn-bg);
      color: var(--text);
    }
    .action-btn.secondary:hover { background: var(--btn-hover); }
    .action-btn.save-btn {
      background: var(--save-btn);
      color: #ffffff;
    }
    .action-btn.save-btn:hover { background: var(--save-btn-hover); }
    .action-btn.danger-btn:hover { background: var(--danger-hover); color: #fff; }

    textarea {
      width: 100%;
      height: 520px;
      background: #070d17;
      color: #f1f5f9;
      border: 1px solid var(--card-border);
      border-radius: 8px;
      padding: 14px;
      font-size: 1.1rem;
      line-height: 1.75;
      font-family: 'Noto Sans Bengali', 'Cambria Math', 'Segoe UI Symbol', monospace;
      resize: vertical;
      outline: none;
      transition: border-color 0.2s;
    }
    textarea:focus { border-color: var(--accent); box-shadow: 0 0 0 2px rgba(56, 189, 248, 0.2); }

    .status-bar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 0.82rem;
      color: var(--text-muted);
      padding: 4px 2px;
    }

    .tabs {
      display: flex;
      gap: 4px;
      overflow-x: auto;
      padding-bottom: 6px;
      border-bottom: 1px solid var(--card-border);
    }
    .tabs::-webkit-scrollbar { height: 4px; }
    .tabs::-webkit-scrollbar-thumb { background: var(--card-border); border-radius: 4px; }

    .tab-btn {
      background: transparent;
      border: none;
      color: var(--text-muted);
      padding: 6px 12px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 0.85rem;
      font-weight: 600;
      white-space: nowrap;
      transition: all 0.2s;
    }
    .tab-btn:hover { color: var(--text); background: rgba(255, 255, 255, 0.05); }
    .tab-btn.active {
      background: var(--btn-bg);
      color: var(--accent);
      border-bottom: 2px solid var(--accent);
    }
    .symbol-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(48px, 1fr));
      gap: 6px;
      max-height: 470px;
      overflow-y: auto;
      padding: 4px 2px;
    }
    .symbol-grid::-webkit-scrollbar { width: 6px; }
    .symbol-grid::-webkit-scrollbar-thumb { background: var(--card-border); border-radius: 4px; }

    .sym-btn {
      background: var(--btn-bg);
      border: 1px solid rgba(255,255,255,0.05);
      color: #fff;
      font-size: 1.15rem;
      padding: 8px 4px;
      border-radius: 6px;
      cursor: pointer;
      font-family: 'Cambria Math', 'Segoe UI Symbol', 'Noto Sans Bengali', sans-serif;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: all 0.15s ease;
      user-select: none;
    }
    .sym-btn:hover {
      background: var(--accent);
      color: #0f172a;
      transform: scale(1.05);
    }
    .sym-btn:active {
      transform: scale(0.95);
    }
  </style>
</head>
<body>

<div class="container">
  <!-- Left Side: Editor Area -->
  <div class="card">
    <div class="header">
      <h1>⚛️ পদার্থবিজ্ঞান প্রশ্নপত্র সম্পাদক</h1>
      <div class="toolbar">
        <button type="button" class="action-btn secondary" onclick="insertMCQ()">+ MCQ</button>
        <button type="button" class="action-btn save-btn" onclick="saveToDevice()">💾 সেভ (Ctrl+S)</button>
        <button type="button" class="action-btn" onclick="copyText()">📋 কপি</button>
        <button type="button" class="action-btn secondary danger-btn" onclick="clearText()">মুছুন</button>
      </div>
    </div>
    
    <textarea id="editor" placeholder="এখানে সরাসরি প্রশ্ন টাইপ করুন..."></textarea>
    
    <div class="status-bar">
      <span id="saveStatus">🟢 অটো-সেভ সক্রিয়</span>
      <span id="charStats">লাইন: 0 | শব্দ: 0</span>
    </div>
  </div>

  <!-- Right Side: Physics Symbols -->
  <div class="card">
    <div class="tabs">
      <button type="button" class="tab-btn active" onclick="switchTab('greek', this)">Greek</button>
      <button type="button" class="tab-btn" onclick="switchTab('phys', this)">Physics / Vector</button>
      <button type="button" class="tab-btn" onclick="switchTab('math', this)">Math / Calculus</button>
      <button type="button" class="tab-btn" onclick="switchTab('script', this)">Power / Base</button>
      <button type="button" class="tab-btn" onclick="switchTab('markers', this)">চিহ্ন / দাগ</button>
    </div>

    <div id="symbol-grid" class="symbol-grid"></div>
  </div>
</div>

<script>
  const symbolSets = {
    greek: [
      'α', 'β', 'γ', 'δ', 'ε', 'θ', 'λ', 'μ', 'π', 'ρ', 'σ', 'τ', 'φ', 'ψ', 'ω',
      'Δ', 'Γ', 'Θ', 'Λ', 'Σ', 'Φ', 'Ψ', 'Ω', 'η', 'κ', 'ν', 'ξ', 'ζ', 'χ', 'ε₀', 'μ₀'
    ],
    phys: [
      'î', 'ĵ', 'k̂', 'F⃗', 'v⃗', 'a⃗', 'r⃗', 'E⃗', 'B⃗', 'p⃗', 'ħ', 'Å', '℃', '℉', 'Ω',
      'μF', 'pF', 'μm', 'nm', 'm/s', 'm/s²', 'N', 'J', 'W', 'Pa', 'T', 'Wb', 'H', 'eV', 'C', 'kg'
    ],
    math: [
      '±', '∓', '×', '÷', '·', '√', '∛', '∝', '≈', '≠', '≡', '≤', '≥', '∫', '∬',
      '∮', '∂', '∇', '∑', '∏', '∞', '→', '⇒', '⇌', '∠', '⊥', '°', '′', '″', '∆'
    ],
    script: [
      '⁰', '¹', '²', '³', '⁴', '⁵', '⁶', '⁷', '⁸', '⁹', '⁺', '⁻', 'ⁿ', 'ˣ', 'ʸ',
      '₀', '₁', '₂', '₃', '₄', '₅', '₆', '₇', '₈', '₉', '₊', '₋', 'ᵢ', 'ⱼ', 'ₖ', 'ₓ', 'ᵧ'
    ],
    markers: [
      '(A)', '(B)', '(C)', '(D)', '(ক)', '(খ)', '(গ)', '(ঘ)',
      '(i)', '(ii)', '(iii)', '(iv)', '(v)',
      '[1]', '[2]', '[3]', '[4]', '[5]', 'Ans:', 'Q.'
    ]
  };

  const editor = document.getElementById('editor');
  const grid = document.getElementById('symbol-grid');
  const saveStatus = document.getElementById('saveStatus');
  const charStats = document.getElementById('charStats');

  // বাংলা ও ইংরেজি উভয় সংখ্যা থেকে কনভার্সন
  const banglaDigits = {'০':'0', '১':'1', '২':'2', '৩':'3', '৪':'4', '৫':'5', '৬':'6', '৭':'7', '৮':'8', '৯':'9'};
  
  function toEngDigit(str) {
    return str.replace(/[০-৯]/g, d => banglaDigits[d]);
  }

  window.addEventListener('DOMContentLoaded', () => {
    try {
      const saved = localStorage.getItem('physics_draft_text');
      if (saved) {
        editor.value = saved;
      }
    } catch (e) {
      console.warn('LocalStorage access issue:', e);
    }
    renderSymbols('greek');
    updateStats();
  });

  function updateStats() {
    const text = editor.value;
    const lines = text ? text.split('\n').length : 0;
    const words = text.trim() ? text.trim().split(/\s+/).length : 0;
    charStats.innerText = `লাইন: ${lines} | শব্দ: ${words}`;
  }

  editor.addEventListener('input', () => {
    try {
      localStorage.setItem('physics_draft_text', editor.value);
      saveStatus.innerText = '🟢 ড্রাফট সেভ করা আছে';
    } catch (e) {}
    updateStats();
  });

  // কীবোর্ড শর্টকাট (Ctrl + S)
  window.addEventListener('keydown', (e) => {
    if ((e.ctrlKey || e.metaKey) && e.key === 's') {
      e.preventDefault();
      saveToDevice();
    }
  });

  function renderSymbols(cat) {
    grid.innerHTML = '';
    const fragment = document.createDocumentFragment();
    symbolSets[cat].forEach(sym => {
      const btn = document.createElement('button');
      btn.type = 'button';
      btn.className = 'sym-btn';
      btn.innerText = sym;
      
      // Focus লস হওয়া বন্ধ করতে onmousedown এ preventDefault
      btn.onmousedown = (e) => {
        e.preventDefault();
        insertSymbol(sym);
      };
      
      fragment.appendChild(btn);
    });
    grid.appendChild(fragment);
  }

  function switchTab(cat, btn) {
    document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    renderSymbols(cat);
  }

  // Undo/Redo (Ctrl+Z) যাতে না ভাঙে সেজন্য setRangeText ব্যবহার
  function insertSymbol(sym) {
    const start = editor.selectionStart;
    const end = editor.selectionEnd;
    
    editor.focus();
    if (document.queryCommandSupported && document.queryCommandSupported('insertText')) {
      document.execCommand('insertText', false, sym);
    } else {
      editor.setRangeText(sym, start, end, 'end');
      editor.dispatchEvent(new Event('input', { bubbles: true }));
    }
  }

  // পরবর্তী ক্রমিক নম্বর গোনার ফাংশন (ইংরেজি ও বাংলা উভয় সংখ্যা হ্যান্ডেল করে)
  function getNextQuestionNumber(text) {
    if (!text) return 1;
    const matches = [...text.matchAll(/(?:^|\n)\s*([0-9০-৯]+)\./g)];
    if (matches.length === 0) return 1;
    
    const nums = matches.map(m => parseInt(toEngDigit(m[1]), 10)).filter(n => !isNaN(n));
    return nums.length > 0 ? Math.max(...nums) + 1 : 1;
  }

  function insertMCQ() {
    const currentText = editor.value.trimEnd();
    const nextNum = getNextQuestionNumber(currentText);
    
    const prefix = currentText.length > 0 ? '\n\n' : '';
    const questionHead = `${prefix}${nextNum}. `;
    const optionsBlock = `\n   (A)                 (B) \n   (C)                 (D) `;
    
    editor.value = currentText + questionHead + optionsBlock;
    
    // কার্সর নতুন প্রশ্নের নম্বরের ঠিক পাশে নিয়ে যাওয়া
    const targetCursorPos = currentText.length + questionHead.length;
    editor.focus();
    editor.setSelectionRange(targetCursorPos, targetCursorPos);
    
    editor.scrollTop = editor.scrollHeight;
    editor.dispatchEvent(new Event('input', { bubbles: true }));
  }

  // Safe Save To Device with UTF-8 BOM
  async function saveToDevice() {
    const text = editor.value;
    if (!text.trim()) {
      alert('সেভ করার জন্য কোনো লেখা নেই!');
      return;
    }

    const bomText = '\ufeff' + text; // বাংলা ফন্ট উইন্ডোজ নোটপ্যাডে যেন না ভাঙে

    if ('showSaveFilePicker' in window) {
      try {
        const handle = await window.showSaveFilePicker({
          suggestedName: 'Physics_Question_Paper.txt',
          types: [{
            description: 'Text Document (*.txt)',
            accept: { 'text/plain': ['.txt'] }
          }]
        });
        const writable = await handle.createWritable();
        await writable.write(bomText);
        await writable.close();
        saveStatus.innerText = '✅ ডিভাইসে সেভ হয়েছে!';
        return;
      } catch (err) {
        if (err.name === 'AbortError') return;
      }
    }

    // Fallback Download
    const blob = new Blob([bomText], { type: 'text/plain;charset=utf-8' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = 'Physics_Question_Paper.txt';
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    URL.revokeObjectURL(url);
    saveStatus.innerText = '✅ ডাউনলোড সম্পন্ন!';
  }

  async function copyText() {
    if (!editor.value.trim()) {
      alert('কপি করার মতো কোনো লেখা নেই!');
      return;
    }
    try {
      await navigator.clipboard.writeText(editor.value);
      saveStatus.innerText = '📋 ক্লিপবোর্ডে কপি হয়েছে!';
    } catch (e) {
      editor.select();
      document.execCommand('copy');
      saveStatus.innerText = '📋 ক্লিপবোর্ডে কপি হয়েছে!';
    }
  }

  function clearText() {
    if (confirm('আপনি কি নিশ্চিত যে সব লেখা মুছে ফেলতে চান?')) {
      editor.value = '';
      try {
        localStorage.removeItem('physics_draft_text');
      } catch (e) {}
      saveStatus.innerText = '🗑️ খালি করা হয়েছে';
      updateStats();
      editor.focus();
    }
  }
</script>
</body>
