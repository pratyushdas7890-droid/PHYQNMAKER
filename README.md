
<html lang="bn">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Physics Exam Question Maker</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Noto+Sans+Bengali:wght@400;500;600;700&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg-main: #090d16;
      --panel-bg: rgba(18, 24, 38, 0.9);
      --card-border: rgba(255, 255, 255, 0.08);
      --primary: #38bdf8;
      --primary-hover: #0ea5e9;
      --primary-glow: rgba(56, 189, 248, 0.15);
      --success: #10b981;
      --text-main: #f1f5f9;
      --text-muted: #94a3b8;
      --btn-secondary: rgba(255, 255, 255, 0.06);
      --btn-secondary-hover: rgba(255, 255, 255, 0.12);
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    html, body {
      width: 100%;
      min-height: 100vh;
      background-color: var(--bg-main);
      color: var(--text-main);
      font-family: 'Inter', 'Noto Sans Bengali', 'Segoe UI', sans-serif;
      overflow-x: hidden;
    }

    body {
      padding: 16px;
      display: flex;
      justify-content: center;
      align-items: flex-start;
      background-image: 
        radial-gradient(circle at 15% 15%, rgba(56, 189, 248, 0.05) 0%, transparent 40%),
        radial-gradient(circle at 85% 85%, rgba(16, 185, 129, 0.04) 0%, transparent 40%);
    }

    /* Fixed 2-Column Balanced Grid Layout */
    .container {
      width: 100%;
      max-width: 1400px;
      margin: 0 auto;
      display: grid;
      grid-template-columns: minmax(0, 1fr) 380px;
      gap: 16px;
      align-items: stretch;
    }

    /* Mobile / Small Portrait Layout */
    @media (max-width: 850px) {
      .container {
        grid-template-columns: 1fr;
      }
      body {
        padding: 10px;
      }
    }

    /* Glass Panels */
    .glass-panel {
      background: var(--panel-bg);
      backdrop-filter: blur(12px);
      -webkit-backdrop-filter: blur(12px);
      border: 1px solid var(--card-border);
      border-radius: 16px;
      padding: 16px;
      box-shadow: 0 10px 30px -10px rgba(0, 0, 0, 0.5);
      display: flex;
      flex-direction: column;
      gap: 12px;
      min-width: 0; /* Prevents overflow */
    }

    /* Header */
    .header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 10px;
      padding-bottom: 8px;
      border-bottom: 1px solid var(--card-border);
    }

    .logo-badge {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .logo-icon {
      width: 34px;
      height: 34px;
      background: linear-gradient(135deg, #38bdf8 0%, #6366f1 100%);
      border-radius: 8px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1.1rem;
      box-shadow: 0 4px 12px rgba(56, 189, 248, 0.3);
    }

    h1 {
      font-size: 1.1rem;
      font-weight: 700;
      color: #fff;
    }

    .toolbar {
      display: flex;
      gap: 6px;
      flex-wrap: wrap;
    }

    /* Modern Buttons */
    .btn {
      font-family: inherit;
      border: none;
      padding: 7px 12px;
      border-radius: 8px;
      font-weight: 600;
      cursor: pointer;
      font-size: 0.84rem;
      transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
      display: inline-flex;
      align-items: center;
      gap: 5px;
    }

    .btn:active {
      transform: scale(0.97);
    }

    .btn-mcq {
      background: linear-gradient(135deg, #0284c7 0%, #0369a1 100%);
      color: #ffffff;
      border: 1px solid rgba(255, 255, 255, 0.15);
    }
    .btn-mcq:hover {
      background: linear-gradient(135deg, #0369a1 0%, #075985 100%);
    }

    .btn-save {
      background: linear-gradient(135deg, #10b981 0%, #059669 100%);
      color: #ffffff;
      border: 1px solid rgba(255, 255, 255, 0.15);
    }
    .btn-save:hover {
      background: linear-gradient(135deg, #059669 0%, #047857 100%);
    }

    .btn-secondary {
      background: var(--btn-secondary);
      color: var(--text-main);
      border: 1px solid var(--card-border);
    }
    .btn-secondary:hover {
      background: var(--btn-secondary-hover);
    }

    .btn-danger-hover:hover {
      background: rgba(239, 68, 68, 0.15);
      color: #f87171;
      border-color: rgba(239, 68, 68, 0.3);
    }

    /* Editor Box */
    .editor-wrapper {
      width: 100%;
      flex: 1;
      display: flex;
    }

    textarea {
      width: 100%;
      height: 520px;
      background: #060911;
      color: #f8fafc;
      border: 1px solid var(--card-border);
      border-radius: 12px;
      padding: 16px;
      font-size: 1.08rem;
      line-height: 1.75;
      font-family: 'Inter', 'Noto Sans Bengali', 'Cambria Math', 'Segoe UI Symbol', sans-serif;
      resize: vertical;
      outline: none;
      transition: border-color 0.2s, box-shadow 0.2s;
    }

    textarea:focus {
      border-color: var(--primary);
      box-shadow: 0 0 0 3px var(--primary-glow);
    }

    textarea::placeholder {
      color: #475569;
    }

    /* Custom Scrollbars */
    textarea::-webkit-scrollbar, .symbol-grid::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    textarea::-webkit-scrollbar-thumb, .symbol-grid::-webkit-scrollbar-thumb {
      background: rgba(255, 255, 255, 0.15);
      border-radius: 10px;
    }

    /* Status Bar */
    .status-bar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 0.82rem;
      color: var(--text-muted);
    }

    .status-pill {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      background: rgba(16, 185, 129, 0.1);
      color: #34d399;
      padding: 4px 10px;
      border-radius: 20px;
      border: 1px solid rgba(16, 185, 129, 0.2);
    }

    .dot {
      width: 6px;
      height: 6px;
      background: #10b981;
      border-radius: 50%;
    }

    /* Tabs */
    .tabs {
      display: flex;
      gap: 4px;
      background: rgba(0, 0, 0, 0.3);
      padding: 4px;
      border-radius: 10px;
      border: 1px solid var(--card-border);
      overflow-x: auto;
    }

    .tab-btn {
      flex: 1;
      background: transparent;
      border: none;
      color: var(--text-muted);
      padding: 7px 8px;
      border-radius: 7px;
      cursor: pointer;
      font-size: 0.82rem;
      font-weight: 600;
      white-space: nowrap;
      transition: all 0.2s ease;
      text-align: center;
    }

    .tab-btn:hover {
      color: #fff;
    }

    .tab-btn.active {
      background: rgba(255, 255, 255, 0.1);
      color: var(--primary);
    }

    /* Symbol Grid */
    .symbol-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(46px, 1fr));
      gap: 6px;
      height: 480px;
      overflow-y: auto;
      padding-right: 2px;
    }

    .sym-btn {
      background: rgba(255, 255, 255, 0.04);
      border: 1px solid rgba(255, 255, 255, 0.06);
      color: #e2e8f0;
      font-size: 1.15rem;
      padding: 10px 4px;
      border-radius: 8px;
      cursor: pointer;
      font-family: 'Cambria Math', 'Segoe UI Symbol', 'Noto Sans Bengali', sans-serif;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: all 0.15s ease;
    }

    .sym-btn:hover {
      background: var(--primary);
      color: #090d16;
      border-color: var(--primary);
      transform: translateY(-2px);
      font-weight: bold;
    }

    .sym-btn:active {
      transform: scale(0.94);
    }
  </style>
</head>
<body>

<div class="container">
  <!-- Left Side: Editor -->
  <div class="glass-panel">
    <div class="header">
      <div class="logo-badge">
        <div class="logo-icon">⚛</div>
        <h1>Physics Question Maker</h1>
      </div>
      <div class="toolbar">
        <button class="btn btn-mcq" onclick="insertMCQ()">
          <span>➕</span> MCQ
        </button>
        <button class="btn btn-save" onclick="saveToDevice()">
          <span>💾</span> SAVE
        </button>
        <button class="btn btn-secondary" onclick="copyText()">
          <span>📋</span> COPY
        </button>
        <button class="btn btn-secondary btn-danger-hover" onclick="clearText()">
          <span>🗑️</span> DELETE ALL
        </button>
      </div>
    </div>
    
    <div class="editor-wrapper">
      <textarea id="editor" placeholder="এখানে সরাসরি প্রশ্ন টাইপ করুন এবং পাশের কীবোর্ড থেকে চিহ্ন যোগ করুন..."></textarea>
    </div>
    
    <div class="status-bar">
      <div class="status-pill">
        <div class="dot"></div>
        <span id="saveStatus">অটো-সেভ সক্রিয়</span>
      </div>
    </div>
  </div>

  <!-- Right Side: Symbols Keyboard -->
  <div class="glass-panel">
    <div class="tabs">
      <button class="tab-btn active" onclick="switchTab('greek', this)">Greek</button>
      <button class="tab-btn" onclick="switchTab('phys', this)">Physics</button>
      <button class="tab-btn" onclick="switchTab('math', this)">Math</button>
      <button class="tab-btn" onclick="switchTab('script', this)">x² / x₁</button>
      <button class="tab-btn" onclick="switchTab('markers', this)">চিহ্ন</button>
    </div>

    <div id="symbol-grid" class="symbol-grid"></div>
  </div>
</div>

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
  const grid = document.getElementById('symbol-grid');
  const saveStatus = document.getElementById('saveStatus');

  window.onload = () => {
    const saved = localStorage.getItem('physics_draft_text');
    if (saved) editor.value = saved;
    renderSymbols('greek');
  };

  editor.addEventListener('input', () => {
    localStorage.setItem('physics_draft_text', editor.value);
    saveStatus.innerText = 'ড্রাফট সেভ আছে';
  });

  function renderSymbols(cat) {
    grid.innerHTML = '';
    symbolSets[cat].forEach(sym => {
      const btn = document.createElement('button');
      btn.className = 'sym-btn';
      btn.innerText = sym;
      btn.onclick = () => insertSymbol(sym);
      grid.appendChild(btn);
    });
  }

  function switchTab(cat, btn) {
    document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    renderSymbols(cat);
  }

  function insertSymbol(sym) {
    const start = editor.selectionStart;
    const end = editor.selectionEnd;
    const text = editor.value;
    editor.value = text.substring(0, start) + sym + text.substring(end);
    editor.selectionStart = editor.selectionEnd = start + sym.length;
    editor.focus();
    localStorage.setItem('physics_draft_text', editor.value);
  }

  function getNextQuestionNumber(text) {
    if (!text) return 1;
    const matches = [...text.matchAll(/(?:^|\n)\s*(\d+)\./g)];
    if (matches.length === 0) return 1;
    const nums = matches.map(m => parseInt(m[1], 10)).filter(n => !isNaN(n));
    return nums.length > 0 ? Math.max(...nums) + 1 : 1;
  }

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

    localStorage.setItem('physics_draft_text', editor.value);
    saveStatus.innerText = 'ড্রাফট সেভ আছে';
  }

  // Internal Storage Save
  async function saveToDevice() {
    const text = editor.value;
    if (!text.trim()) return alert('সেভ করার জন্য কোনো লেখা নেই!');

    if (window.showSaveFilePicker) {
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
        saveStatus.innerText = 'স্টোরেজে সেভ সম্পন্ন!';
        return;
      } catch (err) {
        if (err.name === 'AbortError') return;
      }
    }

    const file = new File(['\ufeff' + text], 'Physics_Question_Paper.txt', { type: 'text/plain;charset=utf-8' });
    if (navigator.canShare && navigator.canShare({ files: [file] })) {
      try {
        await navigator.share({
          files: [file],
          title: 'Physics Question Paper',
          text: 'Physics Question Paper'
        });
        saveStatus.innerText = 'স্টোরেজে সেভ সম্পন্ন!';
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
    saveStatus.innerText = 'Downloaded!';
  }

  function copyText() {
    if (!editor.value) return;
    navigator.clipboard.writeText(editor.value).then(() => alert('ক্লিপবোর্ডে কপি হয়েছে!'));
  }

  function clearText() {
    if (confirm('সব লেখা মুছে ফেলতে চান?')) {
      editor.value = '';
      localStorage.removeItem('physics_draft_text');
      saveStatus.innerText = 'খালি করা হয়েছে';
      editor.focus();
    }
  }
</script>
</body>
