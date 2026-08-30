
<html lang="bn">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Physics Exam Question Maker</title>
  <!-- Google Fonts for Bengali & Symbols -->
  <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+Bengali:wght@400;600;700&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg: #0f172a;
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
      max-width: 1250px;
      margin: 0 auto;
      display: grid;
      grid-template-columns: 1fr 350px;
      gap: 16px;
    }
    @media (max-width: 900px) {
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
    }
    .header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 10px;
    }
    h1 { font-size: 1.2rem; color: var(--accent); }
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
      gap: 4px;
    }
    .action-btn:hover { background: var(--accent-hover); }
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

    textarea {
      width: 100%;
      height: 490px;
      background: #090d16;
      color: #f1f5f9;
      border: 1px solid var(--card-border);
      border-radius: 8px;
      padding: 14px;
      font-size: 1.1rem;
      line-height: 1.7;
      font-family: 'Noto Sans Bengali', 'Cambria Math', 'Segoe UI Symbol', sans-serif;
      resize: vertical;
      outline: none;
    }
    textarea:focus { border-color: var(--accent); }

    .status-bar {
      display: flex;
      justify-content: space-between;
      font-size: 0.8rem;
      color: var(--text-muted);
    }

    .tabs {
      display: flex;
      gap: 4px;
      overflow-x: auto;
      padding-bottom: 6px;
      border-bottom: 1px solid var(--card-border);
    }
    .tab-btn {
      background: transparent;
      border: none;
      color: var(--text-muted);
      padding: 6px 10px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 0.85rem;
      font-weight: 600;
      white-space: nowrap;
    }
    .tab-btn.active {
      background: var(--btn-bg);
      color: var(--accent);
    }
    .symbol-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(46px, 1fr));
      gap: 6px;
      max-height: 450px;
      overflow-y: auto;
      padding: 4px 2px;
    }
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
    }
    .sym-btn:hover {
      background: var(--accent);
      color: #000;
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
        <button class="action-btn secondary" onclick="insertMCQ()">+ MCQ</button>
        <button class="action-btn save-btn" onclick="saveToDevice()">💾 সেভ করুন</button>
        <button class="action-btn" onclick="copyText()">📋 কপি</button>
        <button class="action-btn secondary" onclick="clearText()">মুছুন</button>
      </div>
    </div>
    
    <textarea id="editor" placeholder="এখানে সরাসরি প্রশ্ন টাইপ করুন..."></textarea>
    
    <div class="status-bar">
      <span id="saveStatus">🟢 অটো-সেভ সক্রিয়</span>
      <span>কার্সরের স্থানে সিম্বল ইনসার্ট হবে</span>
    </div>
  </div>

  <!-- Right Side: Physics Symbols -->
  <div class="card">
    <div class="tabs">
      <button class="tab-btn active" onclick="switchTab('greek', this)">Greek</button>
      <button class="tab-btn" onclick="switchTab('phys', this)">Physics / Vector</button>
      <button class="tab-btn" onclick="switchTab('math', this)">Math / Calculus</button>
      <button class="tab-btn" onclick="switchTab('script', this)">Power / Base</button>
      <button class="tab-btn" onclick="switchTab('markers', this)">চিহ্ন / দাগ</button>
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
    saveStatus.innerText = '🟢 ড্রাফট সেভ করা আছে';
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

  // কার্সর পয়েন্টে সিম্বল বসানো
  function insertSymbol(sym) {
    const start = editor.selectionStart;
    const end = editor.selectionEnd;
    const text = editor.value;
    editor.value = text.substring(0, start) + sym + text.substring(end);
    editor.selectionStart = editor.selectionEnd = start + sym.length;
    editor.focus();
    localStorage.setItem('physics_draft_text', editor.value);
  }

  // পরবর্তী ক্রমিক নম্বর গোনার ফাংশন
  function getNextQuestionNumber(text) {
    if (!text) return 1;
    const matches = [...text.matchAll(/(?:^|\n)\s*(\d+)\./g)];
    if (matches.length === 0) return 1;
    const nums = matches.map(m => parseInt(m[1], 10)).filter(n => !isNaN(n));
    return nums.length > 0 ? Math.max(...nums) + 1 : 1;
  }

  // ফিক্সড: সবসময় ডকুমেন্টের একদম নিচে নতুন প্রশ্ন যোগ হবে
  function insertMCQ() {
    const currentText = editor.value.trimEnd();
    const nextNum = getNextQuestionNumber(currentText);
    
    // আগের লেখার সাথে পরিষ্কার ব্যবধান (spacing) রাখা
    const prefix = currentText.length > 0 ? '\n\n' : '';
    const questionHead = `${prefix}${nextNum}. `;
    const optionsBlock = `\n   (A)                 (B) \n   (C)                 (D) `;
    
    // নতুন ব্লক তৈরি এবং নিচে যুক্ত করা
    const newBlock = questionHead + optionsBlock;
    editor.value = currentText + newBlock;
    
    // কার্সর সরাসরি নতুন প্রশ্নের নম্বরের ঠিক পাশে নিয়ে যাওয়া
    const targetCursorPos = currentText.length + questionHead.length;
    editor.selectionStart = editor.selectionEnd = targetCursorPos;
    editor.focus();

    // অটো-স্ক্রোল করে নিচে নিয়ে আসা
    editor.scrollTop = editor.scrollHeight;

    localStorage.setItem('physics_draft_text', editor.value);
    saveStatus.innerText = '🟢 ড্রাফট সেভ করা আছে';
  }

  // Internal Storage Save
  async function saveToDevice() {
    const text = editor.value;
    if (!text.trim()) return alert('সেভ করার জন্য কোনো লেখা নেই!');

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
        saveStatus.innerText = '✅ স্টোরেজে সেভ সম্পন্ন!';
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
    saveStatus.innerText = '✅ Downloaded!';
  }

  function copyText() {
    if (!editor.value) return;
    navigator.clipboard.writeText(editor.value).then(() => alert('ক্লিপবোর্ডে কপি হয়েছে!'));
  }

  function clearText() {
    if (confirm('সব লেখা মুছে ফেলতে চান?')) {
      editor.value = '';
      localStorage.removeItem('physics_draft_text');
      saveStatus.innerText = '🗑️ খালি করা হয়েছে';
      editor.focus();
    }
  }
</script>
</body>
