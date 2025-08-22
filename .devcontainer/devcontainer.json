<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>AI Research & Writing Assistant</title>
  <!-- Tailwind -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Marked (Markdown → HTML) -->
  $1<script src="https://unpkg.com/papaparse@5.4.1/papaparse.min.js"></script>
  <script src="https://unpkg.com/xlsx@0.18.5/dist/xlsx.full.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
  $2
  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            primary: '#5D5CDE',
            'primary-dark': '#4A49C2'
          }
        }
      }
    };
  </script>
  <style>
    /* smoother modal scroll */
    .scroll-smooth { scroll-behavior: smooth; }
    /* prose tweaks */
    .prose pre { white-space: pre-wrap; word-wrap: break-word; }
  </style>
</head>
<body class="bg-white dark:bg-gray-900 text-gray-900 dark:text-gray-100 min-h-screen transition-colors duration-300 scroll-smooth">
  <!-- Auto dark-mode based on system preference -->
  <script>
    const root = document.documentElement;
    const setDark = (on) => root.classList[on ? 'add' : 'remove']('dark');
    const mm = window.matchMedia('(prefers-color-scheme: dark)');
    setDark(mm.matches);
    mm.addEventListener('change', (e) => setDark(e.matches));
  </script>

  <div class="container mx-auto px-4 py-8 max-w-7xl">
    <!-- Header -->
    <header class="text-center mb-8">
      <h1 class="text-4xl font-bold text-primary mb-3">
        <i class="fas fa-flask-vial mr-3"></i>
        AI Research & Writing Assistant
      </h1>
      <p class="text-lg md:text-xl text-gray-600 dark:text-gray-400">Comprehensive research, literature search, and academic writing toolkit</p>
    </header>

    <!-- Smart Defaults / Profile -->
    <section class="mb-6 p-4 md:p-6 bg-gray-50 dark:bg-gray-800 rounded-lg">
      <div class="grid gap-4 md:grid-cols-4">
        <div>
          <label class="block text-sm font-medium mb-1">Your Name</label>
          <input id="author" class="w-full px-3 py-2 rounded-lg border border-gray-300 dark:border-gray-700 bg-white dark:bg-gray-900" placeholder="e.g., A. Researcher" />
        </div>
        <div>
          <label class="block text-sm font-medium mb-1">Degree</label>
          <input id="degree" class="w-full px-3 py-2 rounded-lg border border-gray-300 dark:border-gray-700 bg-white dark:bg-gray-900" value="Master of Science" />
        </div>
        <div>
          <label class="block text-sm font-medium mb-1">Institution</label>
          <input id="institution" class="w-full px-3 py-2 rounded-lg border border-gray-300 dark:border-gray-700 bg-white dark:bg-gray-900" placeholder="Your University" />
        </div>
        <div>
          <label class="block text-sm font-medium mb-1">Year</label>
          <input id="year" type="number" class="w-full px-3 py-2 rounded-lg border border-gray-300 dark:border-gray-700 bg-white dark:bg-gray-900" value="2025" />
        </div>
      </div>
      <div class="grid gap-4 md:grid-cols-4 mt-4">
        <div>
          <label class="block text-sm font-medium mb-1">Citation Style</label>
          <select id="citation-style" class="w-full px-3 py-2 rounded-lg border border-gray-300 dark:border-gray-700 bg-white dark:bg-gray-900">
            <option selected>APA 7th</option>
            <option>Vancouver</option>
            <option>Harvard</option>
          </select>
        </div>
        <div>
          <label class="block text-sm font-medium mb-1">Ref. year range</label>
          <input id="ref-range" class="w-full px-3 py-2 rounded-lg border border-gray-300 dark:border-gray-700 bg-white dark:bg-gray-900" value="2019–2025" />
        </div>
        <div class="flex items-center">
          <label class="inline-flex items-center mt-6">
            <input id="numeric-cites" type="checkbox" class="mr-2" checked />
            <span class="text-sm">Use numeric in‑text citations [1–N]</span>
          </label>
        </div>
        <div class="flex items-center">
          <label class="inline-flex items-center mt-6">
            <input id="smart-doi" type="checkbox" class="mr-2" checked />
            <span class="text-sm">Smart DOI / hyperlink policy</span>
          </label>
        </div>
      </div>
    </section>

    <!-- Topic & Actions -->
    <!-- Writing Tools -->
    <section class="mb-8 p-6 bg-gradient-to-r from-yemen/10 to-primary/10 dark:from-yemen/20 dark:to-primary/20 rounded-lg">
      <h2 class="text-2xl font-semibold mb-4"><i class="fas fa-tools mr-2"></i>AI Writing Tools</h2>
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
        <button onclick="openWritingTool('plagiarism')" class="writing-tool-btn p-4 bg-white dark:bg-gray-700 rounded-lg shadow hover:shadow-lg transition-all border-2 border-transparent hover:border-primary">
          <i class="fas fa-search text-2xl text-primary mb-2"></i>
          <h3 class="font-semibold">Plagiarism Check</h3>
          <p class="text-sm text-gray-600 dark:text-gray-400">Similarity & overlap</p>
        </button>
        <button onclick="openWritingTool('grammar')" class="writing-tool-btn p-4 bg-white dark:bg-gray-700 rounded-lg shadow hover:shadow-lg transition-all border-2 border-transparent hover:border-primary">
          <i class="fas fa-spell-check text-2xl text-primary mb-2"></i>
          <h3 class="font-semibold">Grammar Check</h3>
          <p class="text-sm text-gray-600 dark:text-gray-400">Clarity & style fixes</p>
        </button>
        <button onclick="openWritingTool('citation')" class="writing-tool-btn p-4 bg-white dark:bg-gray-700 rounded-lg shadow hover:shadow-lg transition-all border-2 border-transparent hover:border-primary">
          <i class="fas fa-quote-left text-2xl text-primary mb-2"></i>
          <h3 class="font-semibold">Citation Generator</h3>
          <p class="text-sm text-gray-600 dark:text-gray-400">APA 7th, with DOI</p>
        </button>
        <button onclick="openWritingTool('rephrase')" class="writing-tool-btn p-4 bg-white dark:bg-gray-700 rounded-lg shadow hover:shadow-lg transition-all border-2 border-transparent hover:border-primary">
          <i class="fas fa-sync-alt text-2xl text-primary mb-2"></i>
          <h3 class="font-semibold">Rephrase Text</h3>
          <p class="text-sm text-gray-600 dark:text-gray-400">AI / human‑like styles</p>
        </button>
      </div>
    </section>
    <!-- ThesisAid‑Yemen Commands -->
    <section class="mb-8 p-6 bg-gradient-to-r from-amber-500/10 to-yellow-500/10 dark:from-amber-500/20 dark:to-yellow-500/20 rounded-lg">
      <h2 class="text-2xl font-semibold mb-4"><i class="fas fa-terminal mr-2"></i>ThesisAid‑Yemen Commands</h2>
      <p class="text-sm text-gray-600 dark:text-gray-400 mb-3">Use slash commands to trigger specialized prompts. Examples: <code class="px-1 py-0.5 bg-gray-200 dark:bg-gray-700 rounded">/abstract Dengue in Hodeidah</code>, <code class="px-1 py-0.5 bg-gray-200 dark:bg-gray-700 rounded">/chapter 3</code>, <code class="px-1 py-0.5 bg-gray-200 dark:bg-gray-700 rounded">/refs</code>, <code class="px-1 py-0.5 bg-gray-200 dark:bg-gray-700 rounded">/translate_ar النص هنا</code>.</p>
      <div class="grid gap-3 md:grid-cols-[1fr_auto]">
        <input id="cmd-input" class="w-full px-4 py-3 border border-gray-300 dark:border-gray-600 rounded-lg bg-white dark:bg-gray-800" placeholder="Type a command… e.g., /chapter 2" />
        <div class="flex gap-2">
          <button id="btn-run-cmd" class="bg-primary text-white px-5 py-3 rounded-lg hover:bg-primary-dark transition-colors"><i class="fas fa-play mr-2"></i>Run</button>
          <button id="btn-export-master" class="bg-gray-700 text-white px-5 py-3 rounded-lg hover:bg-gray-900 transition-colors"><i class="fas fa-file-export mr-2"></i>Export Master Prompt</button>
        </div>
      </div>
      <p class="mt-3 text-xs text-gray-500">Note: <strong>APA 7th + Numeric in‑text</strong> + <strong>Smart‑DOI</strong> policies are enforced by the master system prompt.</p>
    </section>

    <!-- Uploads -->
    <section class="mb-8 p-6 bg-gradient-to-r from-blue-500/10 to-purple-500/10 dark:from-blue-500/20 dark:to-purple-500/20 rounded-lg">
      <h2 class="text-2xl font-semibold mb-4"><i class="fas fa-upload mr-2"></i>Upload Research Documents</h2>
      <p class="text-sm text-gray-600 dark:text-gray-400 mb-4">Upload PDF / DOCX / TXT / MD (max 10MB each). TXT/MD text is parsed locally; PDF/DOCX require a backend or additional client libraries.</p>
      <div id="drop" class="border-2 border-dashed border-gray-300 dark:border-gray-600 rounded-lg p-8 text-center hover:border-primary transition-colors cursor-pointer" aria-label="Upload area">
        <input id="file-input" type="file" multiple accept=".pdf,.docx,.txt,.md,.csv,.xls,.xlsx" class="hidden" />
        <i class="fas fa-cloud-upload-alt text-4xl text-gray-400 mb-3"></i>
        <p class="font-medium">Drop files here or click to upload</p>
        <p class="text-xs text-gray-500">Supported: PDF, DOCX, TXT, MD, <strong>CSV, XLS, XLSX</strong> (max 10MB each)</p>
        <button id="pick" class="mt-4 bg-primary text-white px-6 py-2 rounded-lg hover:bg-primary-dark transition-colors"><i class="fas fa-folder-open mr-2"></i>Choose Files</button>
      </div>

      <div id="files-wrap" class="hidden mt-5">
        <h3 class="text-lg font-semibold mb-2">Uploaded Files</h3>
        <div id="files-list" class="space-y-2"></div>
        <div class="flex flex-wrap gap-3 mt-4">
          <button id="btn-analyze" class="bg-indigo-500 text-white px-6 py-3 rounded-lg hover:bg-indigo-600 transition-colors"><i class="fas fa-chart-simple mr-2"></i>Analyze Content</button>
          <button id="btn-insights" class="bg-teal-500 text-white px-6 py-3 rounded-lg hover:bg-teal-600 transition-colors"><i class="fas fa-lightbulb mr-2"></i>Extract Insights</button>
          <button id="btn-summarize" class="bg-pink-500 text-white px-6 py-3 rounded-lg hover:bg-pink-600 transition-colors"><i class="fas fa-list-check mr-2"></i>Summarize</button>
          <button id="btn-clear" class="bg-red-500 text-white px-6 py-3 rounded-lg hover:bg-red-600 transition-colors"><i class="fas fa-trash mr-2"></i>Clear</button>
        </div>
      </div>
    </section>

    <!-- Progress Overview -->
    <section class="mb-8 p-6 bg-gray-50 dark:bg-gray-800 rounded-lg">
      <h2 class="text-2xl font-semibold mb-4"><i class="fas fa-chart-line mr-2"></i>Thesis Overview</h2>
      <div class="grid grid-cols-1 md:grid-cols-5 gap-4">
        <div class="text-center p-4 bg-white dark:bg-gray-700 rounded-lg shadow">
          <div class="text-2xl font-bold text-primary">110–140</div>
          <div class="text-sm text-gray-600 dark:text-gray-400">Total Pages</div>
        </div>
        <div class="text-center p-4 bg-white dark:bg-gray-700 rounded-lg shadow">
          <div id="stat-chapters" class="text-2xl font-bold text-primary">5</div>
          <div class="text-sm text-gray-600 dark:text-gray-400">Chapters</div>
        </div>
        <div class="text-center p-4 bg-white dark:bg-gray-700 rounded-lg shadow">
          <div id="stat-sections" class="text-2xl font-bold text-primary">36</div>
          <div class="text-sm text-gray-600 dark:text-gray-400">Sections</div>
        </div>
        <div class="text-center p-4 bg-white dark:bg-gray-700 rounded-lg shadow">
          <div id="stat-refs" class="text-2xl font-bold text-primary">105+</div>
          <div class="text-sm text-gray-600 dark:text-gray-400">Min References</div>
        </div>
        <div class="text-center p-4 bg-white dark:bg-gray-700 rounded-lg shadow">
          <div class="text-2xl font-bold text-primary">APA 7th</div>
          <div class="text-sm text-gray-600 dark:text-gray-400">Citation Style</div>
        </div>
      </div>
    </section>

    <!-- Thesis Structure -->
    <section class="space-y-6" id="chapters-container"></section>

    $1

    <!-- Writing Tools Modal -->
    <div id="writing-modal" class="fixed inset-0 bg-black/50 hidden items-center justify-center z-50 p-4">
      <div class="bg-white dark:bg-gray-800 rounded-lg shadow-xl max-w-4xl w-full max-h-[90vh] overflow-hidden">
        <div class="p-6 border-b border-gray-200 dark:border-gray-700">
          <div class="flex justify-between items-start">
            <div>
              <h3 id="writing-title" class="text-xl font-semibold">Writing Assistant</h3>
              <p id="writing-sub" class="text-sm text-gray-600 dark:text-gray-400 mt-1">AI‑powered tools</p>
            </div>
            <button id="writing-close" class="text-gray-400 hover:text-gray-600 dark:hover:text-gray-300"><i class="fas fa-times text-xl"></i></button>
          </div>
        </div>
        <div class="p-6 overflow-y-auto max-h-[70vh]">
          <div class="mb-4">
            <label class="block text-sm font-medium mb-2">Your text</label>
            <textarea id="writing-input" rows="8" class="w-full p-3 text-base border border-gray-300 dark:border-gray-600 rounded-lg bg-white dark:bg-gray-800 focus:ring-2 focus:ring-primary focus:border-transparent" placeholder="Paste or type text to analyze…"></textarea>
          </div>
          <div id="writing-options" class="mb-4"></div>
          <button id="writing-process" class="w-full bg-primary text-white py-3 rounded-lg hover:bg-primary-dark"><i class="fas fa-magic mr-2"></i>Process</button>
          <div id="writing-results" class="hidden mt-4 bg-gray-50 dark:bg-gray-700 p-4 rounded-lg">
            <h4 class="font-semibold mb-2">Results</h4>
            <div id="writing-output" class="prose dark:prose-invert max-w-none"></div>
          </div>
        </div>
        <div class="p-6 border-t border-gray-200 dark:border-gray-700 flex justify-end gap-2">
          <button id="writing-copy" class="hidden px-4 py-2 bg-primary text-white rounded-lg hover:bg-primary-dark"><i class="fas fa-copy mr-2"></i>Copy</button>
        </div>
      </div>
    </div>
        </div>
        <div class="p-6 border-t border-gray-200 dark:border-gray-700 flex justify-end gap-2">
          <button id="btn-copy" class="hidden px-4 py-2 bg-primary text-white rounded-lg hover:bg-primary-dark"><i class="fas fa-copy mr-2"></i>Copy</button>
          <button id="btn-export-md" class="hidden px-4 py-2 bg-gray-700 text-white rounded-lg hover:bg-gray-900"><i class="fas fa-file-export mr-2"></i>Export .md</button>
        </div>
      </div>
    </div>
  </div>

  <script>
    // ---------------------------
    // In-memory state
    // ---------------------------
    const state = {
      meta: {
        title: '',
        author: '',
        degree: 'Master of Science',
        institution: '',
        year: 2025,
        citation_style: 'APA 7th',
        ref_range: '2019–2025',
        numeric_cites: true,
        smart_doi: true
      },
      templateKey: 'thesis',
      chapters: [],
      uploads: [],
      parsedTextByFile: new Map()
    };

    // ---------------------------
    // Templates
    // ---------------------------
    const templates = {
      thesis: [
        {n:1, title:'Introduction', length:'15–20 pages', sections:[
          'Background of the Study','Problem Statement','Research Objectives & Hypotheses','Research Questions','Significance of the Study','Scope and Limitations','Organization of the Thesis'
        ], min_refs:15},
        {n:2, title:'Literature Review', length:'25–35 pages', sections:[
          'Theoretical Framework','Current State of Research','Key Studies and Findings','Research Gaps','Summary and Synthesis'
        ], min_refs:40},
        {n:3, title:'Methodology', length:'15–20 pages', sections:[
          'Research Design','Study Population and Sampling','Data Collection Methods','Research Instruments','Data Analysis Plan','Ethical Considerations'
        ], min_refs:15},
        {n:4, title:'Results and Analysis', length:'20–30 pages', sections:[
          'Descriptive Analysis','Main Findings','Statistical Analysis','Data Interpretation'
        ], min_refs:10},
        {n:5, title:'Discussion and Conclusion', length:'15–20 pages', sections:[
          'Discussion of Findings','Implications','Limitations','Future Research','Conclusion'
        ], min_refs:20}
      ],
      'research-paper': [
        {n:1,title:'Abstract',length:'~1 page',sections:['Abstract'],min_refs:0},
        {n:2,title:'Introduction',length:'2–3 pages',sections:['Background','Problem Statement','Objectives'],min_refs:10},
        {n:3,title:'Literature Review',length:'4–6 pages',sections:['Previous Research','Theoretical Framework'],min_refs:20},
        {n:4,title:'Methodology',length:'2–3 pages',sections:['Research Design','Data Collection','Analysis'],min_refs:8},
        {n:5,title:'Results',length:'3–4 pages',sections:['Findings','Analysis'],min_refs:5},
        {n:6,title:'Discussion & Conclusion',length:'3–4 pages',sections:['Discussion','Implications','Conclusion'],min_refs:15}
      ],
      'literature-review': [
        {n:1,title:'Introduction',length:'2–3 pages',sections:['Scope','Search Strategy','Inclusion Criteria'],min_refs:5},
        {n:2,title:'Thematic Analysis',length:'15–20 pages',sections:['Theme 1','Theme 2','Theme 3','Synthesis'],min_refs:60},
        {n:3,title:'Discussion',length:'5–8 pages',sections:['Key Findings','Research Gaps','Future Directions'],min_refs:20},
        {n:4,title:'Conclusion',length:'2–3 pages',sections:['Summary','Implications'],min_refs:10}
      ]
    };

    // ---------------------------
    // Utilities
    // ---------------------------
    const $$ = (sel, ctx=document) => ctx.querySelector(sel);
    const $$$ = (sel, ctx=document) => [...ctx.querySelectorAll(sel)];

    function alertToast(msg, type='info'){
      const wrap = document.createElement('div');
      wrap.className = `fixed top-4 right-4 z-[60] px-4 py-3 rounded-lg shadow-lg text-white ${type==='error'?'bg-red-500':type==='warn'?'bg-yellow-500':'bg-gray-900'}`;
      wrap.innerHTML = `<div class="flex items-center gap-2"><i class="fa-solid ${type==='error'?'fa-circle-exclamation':type==='warn'?'fa-triangle-exclamation':'fa-circle-info'}"></i><span>${msg}</span><button class="ml-3 opacity-80 hover:opacity-100" aria-label="Close" onclick="this.closest('div').remove()">✕</button></div>`;
      document.body.appendChild(wrap);
      setTimeout(()=>wrap.remove(), 4500);
    }

    function openModal(title, sub){
      $$('#modal-title').textContent = title;
      $$('#modal-sub').textContent = sub||'';
      $$('#modal').classList.remove('hidden');
      $$('#modal').classList.add('flex');
      $$('#btn-copy').classList.add('hidden');
      $$('#btn-export-md').classList.add('hidden');
      $$('#modal-body').innerHTML = `<div class='flex items-center justify-center py-12'><div class='text-center'><div class='animate-spin rounded-full h-12 w-12 border-b-2 border-primary mx-auto mb-4'></div><p class='text-gray-600 dark:text-gray-400'>Processing…</p></div></div>`;
    }
    function closeModal(){ $$('#modal').classList.add('hidden'); $$('#modal').classList.remove('flex'); }
    $$('#close').addEventListener('click', closeModal);

    function renderMarkdown(md){ return marked.parse(md); }

    function download(filename, text) {
      const a = document.createElement('a');
      a.href = URL.createObjectURL(new Blob([text], {type:'text/markdown'}));
      a.download = filename;
      a.click();
    }

    function fileIcon(name){
      const ext = name.split('.').pop().toLowerCase();
      if (ext==='pdf') return 'fa-file-pdf';
      if (ext==='doc' || ext==='docx') return 'fa-file-word';
      if (ext==='txt') return 'fa-file-lines';
      if (ext==='md') return 'fa-file-code';
      if (ext==='csv') return 'fa-file-csv';
      if (ext==='xls' || ext==='xlsx') return 'fa-file-excel';
      return 'fa-file';
    }

    // DOI helpers
    const doiRegex = /10\.\d{4,9}\/[-._;()/:A-Z0-9]+/i;
    const hasDOI = (s) => doiRegex.test(s || '');
    const toDOILink = (s) => `https://doi.org/${s.replace(/^https?:\/\/doi\.org\//i,'')}`;

    // ---------------------------
    // Outline + Stats
    // ---------------------------
    function setTemplate(key){
      state.templateKey = key;
      state.chapters = templates[key].map(c=>({...c}));
      renderChapters();
      recalcStats();
    }

    function recalcStats(){
      const sections = state.chapters.reduce((a,c)=>a+c.sections.length,0);
      const refs = state.chapters.reduce((a,c)=>a+c.min_refs,0);
      $$('#stat-chapters').textContent = state.chapters.length;
      $$('#stat-sections').textContent = sections;
      $$('#stat-refs').textContent = refs + '+';
    }

    function renderChapters(){
      const cont = $$('#chapters-container');
      cont.innerHTML = '';
      state.chapters.forEach(ch=>{
        const card = document.createElement('div');
        card.className = 'bg-white dark:bg-gray-800 rounded-lg shadow-lg overflow-hidden';
        card.innerHTML = `
        <div class="p-6 border-b border-gray-200 dark:border-gray-700">
          <div class="flex justify-between items-start">
            <div class="flex items-center">
              <div class="bg-primary text-white rounded-full w-10 h-10 flex items-center justify-center mr-4 text-lg font-bold">${ch.n}</div>
              <div>
                <h3 class="text-xl font-semibold">Chapter ${ch.n}: ${ch.title}</h3>
                <div class="flex flex-wrap gap-4 mt-2 text-sm text-gray-600 dark:text-gray-400">
                  <span><i class="fas fa-file-alt mr-1"></i>${ch.length}</span>
                  <span><i class="fas fa-list mr-1"></i>${ch.sections.length} sections</span>
                  <span><i class="fas fa-quote-right mr-1"></i>${ch.min_refs}+ refs</span>
                </div>
              </div>
            </div>
            <div class="flex gap-2">
              <button class="btn-gen-full bg-primary text-white px-4 py-2 rounded-lg hover:bg-primary-dark text-sm" data-n="${ch.n}"><i class="fas fa-wand-magic-sparkles mr-2"></i>Generate Full</button>
            </div>
          </div>
        </div>
        <div class="p-6">
          <div class="grid gap-3">
            ${ch.sections.map(sec=>`
              <div class='flex justify-between items-center p-4 bg-gray-50 dark:bg-gray-700 rounded-lg hover:bg-gray-100 dark:hover:bg-gray-600'>
                <div class='flex items-center'><i class='fas fa-file-lines text-primary mr-3'></i><span class='font-medium'>${sec}</span></div>
                <button class='btn-gen-sec text-primary hover:text-primary-dark text-sm' data-n='${ch.n}' data-sec='${sec}'><i class='fas fa-play mr-1'></i>Generate</button>
              </div>
            `).join('')}
          </div>
        </div>`;
        cont.appendChild(card);
      });
      // bind buttons
      $$$('.btn-gen-full').forEach(b=>b.addEventListener('click',()=>generateContent(parseInt(b.dataset.n), 'full')));
      $$$('.btn-gen-sec').forEach(b=>b.addEventListener('click',()=>generateContent(parseInt(b.dataset.n), b.dataset.sec)));
    }

    // ---------------------------
    // Prompt Builder (encodes your defaults: numeric cites, APA 7, smart DOI)
    // ---------------------------
    function buildContext(){
      const topic = $$('#topic').value.trim();
      state.meta.title = topic;
      state.meta.author = $$('#author').value.trim();
      state.meta.degree = $$('#degree').value.trim();
      state.meta.institution = $$('#institution').value.trim();
      state.meta.year = parseInt($$('#year').value || '2025', 10);
      state.meta.citation_style = $$('#citation-style').value;
      state.meta.ref_range = $$('#ref-range').value.trim();
      state.meta.numeric_cites = $$('#numeric-cites').checked;
      state.meta.smart_doi = $$('#smart-doi').checked;
      return state.meta;
    }

    function buildPolicyText(){
      const a = [];
      if (state.meta.numeric_cites) a.push('Use numeric in-text citations [1–N].');
      a.push(`Reference list in ${state.meta.citation_style}. Always show DOI as https://doi.org/... if available.`);
      if (state.meta.smart_doi) a.push('If DOI missing, include a working hyperlink to the source (PubMed/WHO/journal site).');
      a.push(`Prioritize ${state.meta.ref_range} sources; use seminal older works when necessary.`);
      a.push('Abstract must not contain citations.');
      return a.join('\n');
    }

    function buildChapterPrompt(ch, section){
      const ctx = buildContext();
      const policy = buildPolicyText();
      const base = `You are an expert academic writer. Topic: "${ctx.title}". Degree: ${ctx.degree}. Year: ${ctx.year}. Citation style: ${ctx.citation_style}.`;
      const sectionsCsv = ch.sections.join(', ');
      if (section==='full'){
        return `${base}\nWrite Chapter ${ch.n}: ${ch.title} (${ch.length}). Sections: ${sectionsCsv}. Minimum references: ${ch.min_refs}.\nPolicies:\n${policy}\nWrite formally, comprehensive, rigorous. Include tables/figures suggestions.`;
      }
      return `${base}\nWrite the section "${section}" from Chapter ${ch.n}: ${ch.title} (chapter span: ${ch.length}). Prioritize ${ctx.ref_range}.\nPolicies:\n${policy}`;
    }

    // ---------------------------
    // Adapters: where to send prompts
    // NOTE: Browsers cannot safely call paid APIs with secrets. Provide a backend
    // route like /api/generate that proxies to your LLM (OpenAI/Claude/etc.).
    // Below we ship a demo stub that just echoes the prompt guidance so UI works.
    // ---------------------------
    async function llmGenerate(prompt){
      // TODO: replace this with your real backend call, e.g.:
      // const res = await fetch('/api/generate', {method:'POST', headers:{'Content-Type':'application/json'}, body: JSON.stringify({prompt})});
      // const data = await res.json();
      // return data.content;
      // --- DEMO STUB ---
      return `# ✨ Demo Output\n\nThis is a **placeholder**. Connect a backend to get real content.\n\n---\n\n**Prompt sent to LLM:**\n\n\u0060\u0060\u0060\n${prompt}\n\u0060\u0060\u0060`;
    }

    // ---------------------------
    // Generation
    // ---------------------------
    async function generateContent(chNumber, section){
      const topic = $$('#topic').value.trim();
      if (!topic){ alertToast('Please enter a research topic first','warn'); return; }
      const ch = state.chapters.find(c=>c.n===chNumber);
      if (!ch){ alertToast('Chapter not found','error'); return; }
      const title = section==='full' ? `Chapter ${ch.n}: ${ch.title}` : `${section} — Chapter ${ch.n}`;
      openModal(title, 'Generating content…');
      try{
        const prompt = buildChapterPrompt(ch, section);
        const md = await llmGenerate(prompt);
        $$('#modal-body').innerHTML = renderMarkdown(md);
        $$('#btn-copy').classList.remove('hidden');
        $$('#btn-export-md').classList.remove('hidden');
      }catch(err){
        $$('#modal-body').innerHTML = `<div class='text-center py-8'><i class='fas fa-triangle-exclamation text-red-500 text-3xl mb-4'></i><p class='text-red-600 dark:text-red-400'>${err?.message||'Generation error'}</p></div>`;
      }
    }

    // Copy & export
    $$('#btn-copy').addEventListener('click',()=>{
      const text = $$('#modal-body').innerText;
      navigator.clipboard.writeText(text).then(()=>{
        $$('#btn-copy').innerHTML = '<i class="fas fa-check mr-2"></i>Copied!';
        setTimeout(()=> $$('#btn-copy').innerHTML = '<i class="fas fa-copy mr-2"></i>Copy', 1500);
      }).catch(()=>alertToast('Copy failed – select and copy manually','warn'));
    });
    $$('#btn-export-md').addEventListener('click',()=>{
      const ctx = buildContext();
      const text = $$('#modal-body').innerText;
      download((ctx.title||'content').replace(/[^a-z0-9-_]+/gi,'_') + '.md', text);
    });

    // ---------------------------
    // Uploads
    // ---------------------------
    const drop = $$('#drop');
    const fileInput = $$('#file-input');
    const pick = $$('#pick');

    pick.addEventListener('click',()=>fileInput.click());
    drop.addEventListener('click', (e)=>{
      if (e.target.id==='pick') return; // actual pick button
      fileInput.click();
    });
    drop.addEventListener('dragover', (e)=>{ e.preventDefault(); drop.classList.add('border-primary','bg-primary/5'); });
    drop.addEventListener('dragleave', (e)=>{ e.preventDefault(); drop.classList.remove('border-primary','bg-primary/5'); });
    drop.addEventListener('drop', (e)=>{
      e.preventDefault(); drop.classList.remove('border-primary','bg-primary/5');
      handleFiles([...e.dataTransfer.files]);
    });
    fileInput.addEventListener('change', (e)=> handleFiles([...e.target.files]));

    function handleFiles(files){
      const ok = [];
      for (const f of files){
        const allowed = ['pdf','docx','txt','md','csv','xls','xlsx'];
        const ext = f.name.split('.').pop().toLowerCase();
        if (!allowed.includes(ext)){ alertToast(`Unsupported type: ${f.name}`,'warn'); continue; }
        if (f.size > 10*1024*1024){ alertToast(`Too large: ${f.name}`,'warn'); continue; }
        ok.push(f);
      }
      if (ok.length){ state.uploads.push(...ok); renderUploads(); alertToast(`${ok.length} file(s) added`); }
    }

    function renderUploads(){
      const wrap = $$('#files-wrap');
      const list = $$('#files-list');
      if (!state.uploads.length){ wrap.classList.add('hidden'); list.innerHTML=''; return; }
      wrap.classList.remove('hidden');
      list.innerHTML = state.uploads.map((f,i)=>{
        return `<div class='flex items-center justify-between p-3 bg-white dark:bg-gray-700 rounded-lg border border-gray-200 dark:border-gray-600'>
          <div class='flex items-center gap-3'>
            <i class='fa-solid ${fileIcon(f.name)} text-primary'></i>
            <div>
              <div class='font-medium'>${f.name}</div>
              <div class='text-xs text-gray-500'>${(f.size/1024).toFixed(1)} KB</div>
            </div>
          </div>
          <div class='flex items-center gap-2'>
            <button class='text-sky-600 hover:text-sky-800 text-sm' onclick='previewFile(${i})'><i class="fa-solid fa-eye mr-1"></i>Preview</button>
            <button class='text-red-500 hover:text-red-700' onclick='removeFile(${i})'><i class='fa-solid fa-trash'></i></button>
          </div>
        </div>`;
      }).join('');
    }

    window.previewFile = async function(idx){
      const f = state.uploads[idx];
      openModal('Preview: '+f.name, 'Quick preview (parsed text if available)');
      const ext = f.name.split('.').pop().toLowerCase();
      let text = state.parsedTextByFile.get(f.name);
      if (!text){
        try { text = await parseFileToText(f); state.parsedTextByFile.set(f.name, text||''); } catch {}
      }
      if (text){
        const snippet = text.slice(0, 4000);
        $$('#modal-body').innerHTML = renderMarkdown('```\n'+snippet+'\n```');
        $$('#btn-copy').classList.remove('hidden');
      } else {
        $$('#modal-body').innerHTML = `<div class='p-4 text-sm'>Preview for ${ext.toUpperCase()} requires parsing support.</div>`;
      }
    }

    window.remov = function(idx){ state.uploads.splice(idx,1); renderUploads(); };

    $$('#btn-clear').addEventListener('click', ()=>{ state.uploads = []; state.parsedTextByFile.clear(); renderUploads(); });

    // ---------------------------
    // Basic local analysis (works on TXT/MD only). For PDFs/DOCX wire to backend.
    // ---------------------------
    function concatAllText(){
      let text = '';
      for (const f of state.uploads){
        const cached = state.parsedTextByFile.get(f.name);
        if (cached) text += '\n\n' + cached;
      }
      return text.trim();
    }

    function wordCount(s){ return (s.match(/\b\w+\b/g)||[]).length; }
    function sentenceCount(s){ return (s.match(/[.!?]+\s|\n/g)||[]).length+1; }

    function extractDOIs(s){ return [...new Set((s.match(new RegExp(doiRegex,'gi'))||[]))]; }

    function extractReferencesBlocks(s){
      // very naive – looks for lines containing year (19xx/20xx) and a period
      return (s.split(/\n+/).filter(line=>/(19|20)\d{2}/.test(line) && /\./.test(line))).slice(0,200);
    }

    // Local "plagiarism" (similarity) across uploaded texts using 3-gram shingles + Jaccard
    function shingles(text, k=3){
      const tokens = (text.toLowerCase().match(/\b\w+\b/g)||[]);
      const set = new Set();
      for (let i=0;i<tokens.length-k+1;i++) set.add(tokens.slice(i,i+k).join(' '));
      return set;
    }
    function jaccard(a,b){
      const i = new Set([...a].filter(x=>b.has(x)));
      const u = new Set([...a, ...b]);
      return u.size? i.size/u.size : 0;
    }

    async function analyzeUploads(){
      openModal('Document Analysis', `Analyzing ${state.uploads.length} file(s)`);
      // ensure we have text for txt/md
      for (const f of state.uploads){
        const ext = f.name.split('.').pop().toLowerCase();
        if ((ext==='txt'||ext==='md') && !state.parsedTextByFile.get(f.name)){
          state.parsedTextByFile.set(f.name, await f.text());
        }
      }
      const text = concatAllText();
      const words = wordCount(text);
      const sents = sentenceCount(text);
      const dois = extractDOIs(text);
      const refs = extractReferencesBlocks(text);

      // similarity matrix
      const sims = [];
      for (let i=0;i<state.uploads.length;i++){
        for (let j=i+1;j<state.uploads.length;j++){
          const A = state.parsedTextByFile.get(state.uploads[i].name)||'';
          const B = state.parsedTextByFile.get(state.uploads[j].name)||'';
          if (!A || !B) continue;
          const score = jaccard(shingles(A), shingles(B));
          sims.push({a:state.uploads[i].name,b:state.uploads[j].name,score});
        }
      }

      const md = `## Overview\n\n- Files: **${state.uploads.length}**\n- Words (TXT/MD only): **${words}**\n- Sentences (approx): **${sents}**\n\n## DOIs Detected\n${dois.length? dois.map(d=>`- [${d}](${toDOILink(d)})`).join('\n') : '_None found_'}\n\n## Reference-like Lines (sample)\n${refs.length? refs.slice(0,20).map(r=>`- ${r}`).join('\n') : '_No obvious reference lines detected_'}\n\n## Pairwise Similarity (Jaccard on 3-grams)\n${sims.length? sims.map(s=>`- **${s.a}** × **${s.b}** → ${(s.score*100).toFixed(1)}%`).join('\n') : '_Not enough plain-text to compare_'}\n`;
      $$('#modal-body').innerHTML = renderMarkdown(md);
      $$('#btn-copy').classList.remove('hidden');
      $$('#btn-export-md').classList.remove('hidden');
    }

    async function extractInsights(){
      openModal('Insights', 'Based on uploaded TXT/MD content');
      const text = concatAllText();
      const md = `### Suggested Research Questions\n- What methodological gaps persist within the ${state.meta.title||'current'} literature?\n- Which populations/regions are under-studied?\n\n### Potential Methods\n- Mixed-methods with stratified sampling;\n- Time-series analysis if longitudinal data available.\n\n### Data Opportunities\n- Leverage hospital registries;\n- Linkage with environmental or census datasets.\n\n> Tip: Connect a backend LLM to turn this into tailored, high-quality insights from your actual files.`;
      $$('#modal-body').innerHTML = renderMarkdown(md);
      $$('#btn-copy').classList.remove('hidden');
      $$('#btn-export-md').classList.remove('hidden');
    }

    async function summarizeUploads(){
      openModal('Summaries', 'Per‑document (TXT/MD)');
      const chunks = [];
      for (const f of state.uploads){
        const t = state.parsedTextByFile.get(f.name);
        if (!t) continue;
        const snippet = t.split(/\n+/).slice(0,8).join(' ');
        chunks.push(`**${f.name}**\n\n- Executive Summary: ${snippet.slice(0,240)}…\n- Key Methods: _detect via backend_\n- Major Findings: _detect via backend_\n- Strengths/Limitations: _detect via backend_\n- Relevance: _score via backend_`);
      }
      const md = chunks.length? chunks.join('\n\n---\n\n') : '_No plain-text documents available to summarize._';
      $$('#modal-body').innerHTML = renderMarkdown(md);
      $$('#btn-copy').classList.remove('hidden');
      $$('#btn-export-md').classList.remove('hidden');
    }

    // ---------------------------
    // ThesisAid‑Yemen: Master System Prompt & Command Router
    // ---------------------------

    function thesisAidMasterPrompt(){
      const ctx = buildContext();
      const topic = ctx.title || '[Set your topic]';
      return `### FINAL EXPORT: ThesisAid-Yemen Master System Prompt\n\n**ROLE:** You are **ThesisAid-Yemen**, an AI-powered academic writing assistant developed in collaboration with **Hodeidah University**. You possess **15+ years of experience** in epidemiological research, with specialized expertise in the Yemeni context, conflict medicine, and the work of local researchers like Dr. Al-Kamarany. Your purpose is to generate complete, publication-ready theses on public health issues in Yemen.\n\n**LANGUAGE:** Formal Academic English for main content. Generate mirrored Arabic translations for abstracts, appendices, and consent forms.\n\n**CITATION PROTOCOL:**\n- **Style:** APA 7th Edition.\n- **Format:** Numeric in-text citations (\`[1]\`, \`[2, 3]\`).\n- **Verification:** **DOI IS MANDATORY.** For every citable source, provide a verified DOI hyperlink (\`https://doi.org/10.xxxx/xxxx\`).\n- **Fallback:** If no DOI exists, provide a stable URL and retrieval date.\n- **Key Authors:** Prioritize and integrate work by **Al-Kamarany MA, Al-Sakkaf KA, Shawk B, Al-Mekhlafi HM, Rabaan AA, WHO, UNICEF, MSF.**\n\n**CORE PRINCIPLES:**\n- **Originality:** Zero-tolerance for plagiarism. All content is original synthesis.\n- **Conflict-Sensitive:** All analysis must consider the impact of war, healthcare collapse, and humanitarian access.\n- **Locally Relevant:** Center the research on Hodeidah and Yemen, using local data and authors.\n- **Rigor:** Employ advanced statistical reporting (OR, CI, p-values, AR/CFR formulas).\n\n**CONTEXT:** Current Topic → **${topic}**; Degree → **${ctx.degree}**; Year → **${ctx.year}**; Institution → **${ctx.institution||'Your University'}**.\n\n---\n\n### THESIS STRUCTURE & PROMPT LIBRARY\n(Use the following when the user requests a chapter/section.)\n\n**PROMPT 1: ABSTRACT & KEYWORDS**\nGenerate a 300-word structured abstract for a thesis on \"${topic}\" in Hodeidah, Yemen. Structure: Background, Objectives, Methods, Results, Conclusion, Recommendations. Use numeric citations \`[1]\`. Include 5–7 keywords. **Append a formal Arabic translation of the entire abstract.**\n\n**PROMPT 2: CHAPTER 1 – INTRODUCTION (15+ pages)**\nWrite Chapter 1: Introduction for a thesis on \"${topic}\". Cover: Global burden; Epidemiology in conflict zones; Yemen
    $$('#btn-outline').addEventListener('click', ()=>{
      const topic = $$('#topic').value.trim();
      if (!topic){ alertToast('Please enter a research topic first','warn'); return; }
      const key = $$('#rtype').value;
      setTemplate(key);
      openModal('Research Outline', `Template: ${key}`);
      const outline = state.chapters.map(ch=>`### Chapter ${ch.n}: ${ch.title}\n- Length: ${ch.length}\n- Sections: ${ch.sections.map(s=>`\`${s}\``).join(', ')}\n- Min references: ${ch.min_refs}`).join('\n\n');
      $$('#modal-body').innerHTML = renderMarkdown(outline);
      $$('#btn-copy').classList.remove('hidden');
      $$('#btn-export-md').classList.remove('hidden');
    });

    $$('#btn-search').addEventListener('click', ()=>{
      const topic = $$('#topic').value.trim();
      if (!topic){ alertToast('Please enter a research topic first','warn'); return; }
      openModal('Literature Search Builder', `Search plan for: "${topic}"`);
