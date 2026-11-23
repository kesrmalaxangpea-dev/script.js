<!DOCTYPE html>
<html lang="th" class="dark">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>NEXUS HUB | ศูนย์รวมดาวน์โหลดไฟล์ & คู่มือการติดตั้ง</title>
  <meta name="description" content="ศูนย์รวมไฟล์ดาวน์โหลดหลัก คู่มือการติดตั้ง และเซิร์ฟเวอร์สำรองอย่างเป็นทางการ" />
  <link rel="icon" type="image/svg+xml" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 64 64'%3E%3Cdefs%3E%3ClinearGradient id='g' x1='0%25' y1='0%25' x2='100%25' y2='100%25'%3E%3Cstop offset='0%25' stop-color='%2300f5d4'/%3E%3Cstop offset='100%25' stop-color='%237b2cbf'/%3E%3C/linearGradient%3E%3C/defs%3E%3Crect width='64' height='64' rx='16' fill='%23050811'/%3E%3Cpath d='M18 18h10l18 28V18h-8v14L24 18H18v28h8V32l12 14h8V18' fill='url(%23g)'/%3E%3C/svg%3E" />

  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Sans+Thai:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;600;700&family=Orbitron:wght@600;700;800;900&display=swap" rel="stylesheet" />
  <script src="https://unpkg.com/lucide@latest"></script>
  <link rel="stylesheet" href="style.css" />
</head>
<body class="antialiased selection:bg-cyan-400 selection:text-slate-950">

  <canvas id="bg-canvas"></canvas>
  <div class="ambient-glow glow-cyan"></div>
  <div class="ambient-glow glow-purple"></div>

  <!-- แถบนำทางด้านบน -->
  <header class="sticky top-0 z-40 glass-panel border-b border-cyan-500/20">
    <div class="max-w-6xl mx-auto px-4 sm:px-6">
      <div class="flex flex-col md:flex-row md:items-center md:justify-between py-3.5 gap-3">
        <!-- โลโก้ -->
        <div class="flex items-center justify-between">
          <a href="#main" onclick="switchTab('main')" class="flex items-center gap-3 group">
            <div class="w-10 h-10 rounded-xl bg-gradient-to-br from-cyan-400 via-sky-500 to-purple-600 p-[2px] shadow-lg shadow-cyan-500/25">
              <div class="w-full h-full bg-[#050811] rounded-[10px] flex items-center justify-center">
                <i data-lucide="cpu" class="w-5 h-5 text-cyan-400"></i>
              </div>
            </div>
            <div>
              <div class="flex items-center gap-2">
                <span class="font-display font-black text-xl tracking-wider gradient-text">NEXUS HUB</span>
                <span class="px-2 py-0.5 text-[10px] font-mono font-bold uppercase tracking-wider rounded-md bg-emerald-500/15 text-emerald-300 border border-emerald-500/40">ONLINE</span>
              </div>
              <p class="text-[11px] text-slate-400 tracking-wide">Official Download & Installation Portal</p>
            </div>
          </a>

          <button onclick="copySiteUrl()" class="md:hidden inline-flex items-center gap-1.5 px-3 py-1.5 rounded-lg bg-slate-900/90 border border-slate-700/80 text-xs text-slate-300 hover:text-cyan-400 transition">
            <i data-lucide="share-2" class="w-3.5 h-3.5"></i> แชร์
          </button>
        </div>

        <!-- เมนูสลับ 3 หน้า -->
        <div class="flex items-center gap-2">
          <nav class="flex items-center gap-1.5 bg-slate-950/75 p-1.5 rounded-xl border border-slate-800/90 overflow-x-auto w-full md:w-auto">
            <button id="nav-main" onclick="switchTab('main')" class="nav-btn active flex-1 md:flex-none flex items-center justify-center gap-2 px-4 py-2 rounded-lg text-sm font-medium border border-transparent whitespace-nowrap">
              <i data-lucide="download-cloud" class="w-4 h-4"></i>
              <span>หน้าดาวน์โหลดหลัก</span>
            </button>
            <button id="nav-guide" onclick="switchTab('guide')" class="nav-btn flex-1 md:flex-none flex items-center justify-center gap-2 px-4 py-2 rounded-lg text-sm font-medium text-slate-400 hover:text-white border border-transparent whitespace-nowrap">
              <i data-lucide="book-open-check" class="w-4 h-4"></i>
              <span>คู่มือ & วิธีติดตั้ง</span>
            </button>
            <button id="nav-backup" onclick="switchTab('backup')" class="nav-btn flex-1 md:flex-none flex items-center justify-center gap-2 px-4 py-2 rounded-lg text-sm font-medium text-slate-400 hover:text-white border border-transparent whitespace-nowrap">
              <i data-lucide="server-cog" class="w-4 h-4"></i>
              <span>ลิงก์สำรอง / ชั่วคราว</span>
            </button>
          </nav>

          <button onclick="copySiteUrl()" title="คัดลอกลิงก์เว็บไซต์" class="hidden md:inline-flex items-center gap-1.5 px-3.5 py-2.5 rounded-xl bg-slate-900/80 hover:bg-slate-800 border border-slate-700/80 hover:border-cyan-500/50 text-xs font-medium text-slate-300 hover:text-cyan-300 transition shrink-0">
            <i data-lucide="share-2" class="w-4 h-4 text-cyan-400"></i>
            <span>แชร์เว็บ</span>
          </button>
        </div>
      </div>
    </div>
  </header>

  <main class="max-w-6xl mx-auto px-4 sm:px-6 pt-8 pb-20">

    <!-- ==================== 1. หน้าดาวน์โหลดหลัก ==================== -->
    <section id="tab-main" class="tab-section active space-y-8">
      <div class="relative overflow-hidden rounded-3xl glass-panel neon-border-cyan p-6 sm:p-10">
        <div class="relative z-10 max-w-3xl space-y-4">
          <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-cyan-500/10 border border-cyan-500/30 text-cyan-300 text-xs font-mono">
            <span class="w-2 h-2 rounded-full bg-emerald-400 animate-ping"></span>
            <span>SERVER STATUS: READY FOR DEPLOYMENT</span>
          </div>
          <h1 class="text-3xl sm:text-5xl font-bold tracking-tight leading-tight">
            ศูนย์รวมดาวน์โหลดไฟล์ <br />
            <span class="gradient-text">รวดเร็ว ปลอดภัย พร้อมใช้งาน</span>
          </h1>
          <p class="text-slate-300 text-sm sm:text-base leading-relaxed">
            รวมไฟล์ติดตั้งและเครื่องมือสำคัญทั้งหมดไว้ในที่เดียว หากพบปัญหาการติดตั้งหรือเกิด Error สามารถเปิดดูขั้นตอนแก้ไขได้ที่หน้า
            <button onclick="switchTab('guide')" class="text-cyan-400 underline underline-offset-4 hover:text-cyan-300 font-medium">คู่มือ & วิธีติดตั้ง</button>
          </p>
        </div>
      </div>

      <!-- แถบค้นหาและตัวกรอง (แสดงอัตโนมัติเมื่อมีไฟล์) -->
      <div id="main-controls" class="hidden flex-col sm:flex-row gap-3 items-stretch sm:items-center justify-between">
        <div class="relative flex-1 max-w-md">
          <i data-lucide="search" class="w-4 h-4 text-slate-400 absolute left-3.5 top-1/2 -translate-y-1/2"></i>
          <input id="search-input" type="text" oninput="renderMainDownloads()" placeholder="ค้นหาชื่อไฟล์, เวอร์ชัน..." class="w-full pl-10 pr-4 py-2.5 rounded-xl bg-slate-900/90 border border-slate-700/80 text-sm text-white placeholder-slate-400 focus:outline-none focus:border-cyan-400 transition" />
        </div>
        <div id="category-filters" class="flex items-center gap-2 overflow-x-auto pb-1 sm:pb-0">
          <button onclick="setCategory('all')" data-cat="all" class="cat-btn px-3.5 py-2 rounded-xl text-xs font-semibold bg-cyan-500 text-slate-950 transition whitespace-nowrap">ทั้งหมด</button>
          <button onclick="setCategory('app')" data-cat="app" class="cat-btn px-3.5 py-2 rounded-xl text-xs font-semibold bg-slate-900 text-slate-300 border border-slate-800 hover:border-cyan-500/40 transition whitespace-nowrap">แอป / ตัวติดตั้ง</button>
          <button onclick="setCategory('script')" data-cat="script" class="cat-btn px-3.5 py-2 rounded-xl text-xs font-semibold bg-slate-900 text-slate-300 border border-slate-800 hover:border-cyan-500/40 transition whitespace-nowrap">สคริปต์ / Mod</button>
          <button onclick="setCategory('tool')" data-cat="tool" class="cat-btn px-3.5 py-2 rounded-xl text-xs font-semibold bg-slate-900 text-slate-300 border border-slate-800 hover:border-cyan-500/40 transition whitespace-nowrap">เครื่องมือเสริม</button>
        </div>
      </div>

      <!-- พื้นที่แสดงรายการดาวน์โหลด -->
      <div id="main-downloads-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-5"></div>
    </section>

    <!-- ==================== 2. หน้าคู่มือ & วิธีติดตั้ง ==================== -->
    <section id="tab-guide" class="tab-section space-y-8">
      <div class="rounded-3xl glass-panel border border-purple-500/30 p-6 sm:p-8 flex flex-col md:flex-row md:items-center justify-between gap-4">
        <div class="space-y-2">
          <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-purple-500/15 border border-purple-500/30 text-purple-300 text-xs font-mono">
            <i data-lucide="file-text" class="w-3.5 h-3.5"></i>
            <span>OFFICIAL DOCUMENTATION</span>
          </div>
          <h2 class="text-2xl sm:text-3xl font-bold text-white">คู่มือการติดตั้ง & วิธีแก้ไขปัญหา</h2>
          <p class="text-sm text-slate-300">โปรดอ่านลำดับขั้นตอนการติดตั้งด้านล่างอย่างละเอียด หากพบ Error ให้ทำตามคู่มือสำรองทันที</p>
        </div>
        <button onclick="jumpToBackupGuide()" class="self-start md:self-center inline-flex items-center gap-2 px-4 py-2.5 rounded-xl bg-amber-500/15 hover:bg-amber-500/25 border border-amber-500/40 text-amber-300 text-sm font-medium transition shrink-0">
          <i data-lucide="alert-triangle" class="w-4 h-4"></i>
          <span>ข้ามไปดูคู่มือที่ 2 (สำรอง)</span>
        </button>
      </div>

      <!-- คู่มือที่ 1 และ 2 -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
        <!-- คู่มือการติดตั้ง 1 -->
        <div id="card-guide-1" class="rounded-2xl glass-panel border border-rose-500/40 p-6 flex flex-col justify-between space-y-5 relative overflow-hidden">
          <div class="space-y-4">
            <div class="flex items-center justify-between gap-2">
              <span class="px-3 py-1 rounded-lg bg-rose-500/15 border border-rose-500/30 text-rose-300 text-xs font-mono font-bold">คู่มือการติดตั้ง 1</span>
              <span class="inline-flex items-center gap-1.5 text-xs font-mono text-rose-400">
                <span class="w-2 h-2 rounded-full bg-rose-500 animate-ping"></span> STATUS: ERROR
              </span>
            </div>
            <h3 class="text-xl font-bold text-white">คำแนะนำในการติดตั้ง (วิธีหลัก)</h3>
            <div class="p-4 rounded-xl bg-slate-950/90 border border-slate-800 space-y-3">
              <p class="text-slate-200 text-sm sm:text-base leading-relaxed">
                คำแนะนำในการติดตั้ง การที่คุณจะติดตั้ง ควรดูวิธีนี้
              </p>
              <div class="p-3.5 rounded-lg bg-rose-950/50 border border-rose-500/40 font-mono text-xs sm:text-sm text-rose-400 overflow-x-auto">
                <div class="flex items-center gap-2 text-rose-300 font-bold mb-1">
                  <i data-lucide="terminal" class="w-4 h-4"></i>
                  <span>SYSTEM LOG OUTPUT:</span>
                </div>
                <code class="tracking-wider select-all">error________________________________________________________________</code>
              </div>
            </div>
          </div>
          <div class="pt-2">
            <button onclick="jumpToBackupGuide()" class="w-full py-3 px-4 rounded-xl bg-gradient-to-r from-rose-500/20 to-amber-500/20 hover:from-rose-500/30 hover:to-amber-500/30 border border-amber-400/50 text-amber-200 font-semibold text-sm flex items-center justify-center gap-2 transition">
              <i data-lucide="arrow-right-circle" class="w-4 h-4 text-amber-400"></i>
              <span>เกิด Error! สลับไปดู คู่มือการติดตั้ง 2 (สำรอง)</span>
            </button>
          </div>
        </div>

        <!-- คู่มือการติดตั้ง 2 (สำรอง) -->
        <div id="card-guide-2" class="rounded-2xl glass-panel border border-cyan-500/40 p-6 space-y-5 relative overflow-hidden transition-all duration-500">
          <div class="flex items-center justify-between gap-2">
            <span class="px-3 py-1 rounded-lg bg-cyan-500/15 border border-cyan-500/30 text-cyan-300 text-xs font-mono font-bold">คู่มือการติดตั้ง 2 ( สำรอง )</span>
            <span class="inline-flex items-center gap-1.5 text-xs font-mono text-emerald-400">
              <i data-lucide="shield-check" class="w-4 h-4"></i> RECOMMENDED
            </span>
          </div>

          <div class="p-4 rounded-xl bg-gradient-to-r from-cyan-500/10 to-purple-500/10 border border-cyan-500/30">
            <p class="text-cyan-200 text-sm sm:text-base font-medium leading-relaxed">
              "oh my god ไม่น่าเชื่อเลย ถ้าคู่มือแรกของคุณนั้นเกิด error และนั่นควรมาที่คู่มือที่ 2"
            </p>
          </div>

          <div class="space-y-3">
            <div class="flex items-start gap-3.5 p-3.5 rounded-xl bg-slate-900/80 border border-slate-800">
              <div class="w-7 h-7 rounded-lg bg-cyan-500 text-slate-950 font-display font-bold text-sm flex items-center justify-center shrink-0 mt-0.5">1</div>
              <div>
                <h4 class="font-bold text-white text-sm">ขั้นตอนที่ 1</h4>
                <p class="text-slate-300 text-sm mt-0.5">แค่คุณติดตั้งสิ่งแรกก่อน</p>
              </div>
            </div>

            <div class="flex items-start gap-3.5 p-3.5 rounded-xl bg-slate-900/80 border border-slate-800">
              <div class="w-7 h-7 rounded-lg bg-purple-500 text-white font-display font-bold text-sm flex items-center justify-center shrink-0 mt-0.5">2</div>
              <div>
                <h4 class="font-bold text-white text-sm">ขั้นตอนที่ 2</h4>
                <p class="text-slate-300 text-sm mt-0.5">แล้วคุณก็ค่อยติดตั้งตัวที่ 2 ตามทีหลัง</p>
              </div>
            </div>

            <div class="flex items-start gap-3.5 p-3.5 rounded-xl bg-emerald-950/30 border border-emerald-500/30">
              <div class="w-7 h-7 rounded-lg bg-emerald-500 text-slate-950 font-display font-bold text-sm flex items-center justify-center shrink-0 mt-0.5">✓</div>
              <div>
                <h4 class="font-bold text-emerald-300 text-sm">ผลลัพธ์</h4>
                <p class="text-slate-200 text-sm mt-0.5">แล้วเมื่อคุณทำมันสำเร็จมันก็จะสามารถเปิดได้</p>
              </div>
            </div>
          </div>

          <div class="p-4 rounded-xl bg-amber-500/10 border border-amber-500/40 flex items-start gap-3">
            <i data-lucide="alert-octagon" class="w-5 h-5 text-amber-400 shrink-0 mt-0.5"></i>
            <div class="text-sm">
              <span class="font-bold text-amber-300 block">ข้อควรทราบกรณีเปิดใช้งานไม่ได้:</span>
              <span class="text-amber-100/90">แต่ถ้ามันเปิดไม่ได้ โปรดทราบว่าเครื่องของคุณอาจไม่รองรับ.?</span>
            </div>
          </div>
        </div>
      </div>

      <!-- วิธีแตกไฟล์และติดตั้งพื้นฐาน -->
      <div class="space-y-4 pt-2">
        <h3 class="text-xl font-bold text-white flex items-center gap-2">
          <i data-lucide="folder-archive" class="w-5 h-5 text-cyan-400"></i>
          <span>วิธีดาวน์โหลด & แตกไฟล์พื้นฐาน (Android / PC)</span>
        </h3>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
          <div class="rounded-2xl glass-panel border border-slate-800 p-5 space-y-2.5">
            <div class="w-10 h-10 rounded-xl bg-cyan-500/15 text-cyan-400 flex items-center justify-center font-display font-bold">01</div>
            <h4 class="font-bold text-white">ดาวน์โหลดไฟล์ให้ครบ</h4>
            <p class="text-xs sm:text-sm text-slate-400 leading-relaxed">กดปุ่มดาวน์โหลดจากหน้าหลัก รอให้เบราว์เซอร์โหลดจนครบ 100% หากลิงก์หลักช้าให้สลับไปใช้หน้าลิงก์สำรอง</p>
          </div>
          <div class="rounded-2xl glass-panel border border-slate-800 p-5 space-y-2.5">
            <div class="w-10 h-10 rounded-xl bg-purple-500/15 text-purple-400 flex items-center justify-center font-display font-bold">02</div>
            <h4 class="font-bold text-white">การแตกไฟล์ (.ZIP / .RAR)</h4>
            <p class="text-xs sm:text-sm text-slate-400 leading-relaxed">บน Android แนะนำใช้แอป <span class="text-cyan-300 font-medium">ZArchiver</span> หรือ <span class="text-cyan-300 font-medium">MT Manager</span> กดที่ไฟล์แล้วเลือก <em>"Extract here"</em></p>
          </div>
          <div class="rounded-2xl glass-panel border border-slate-800 p-5 space-y-2.5">
            <div class="w-10 h-10 rounded-xl bg-emerald-500/15 text-emerald-400 flex items-center justify-center font-display font-bold">03</div>
            <h4 class="font-bold text-white">ติดตั้งตามลำดับ</h4>
            <p class="text-xs sm:text-sm text-slate-400 leading-relaxed">เปิดสิทธิ์ <em>"ติดตั้งแอปที่ไม่รู้จัก"</em> แล้วติดตั้งตัวแรกก่อน จากนั้นค่อยติดตั้งตัวที่ 2 ตามคู่มือสำรองด้านบน</p>
          </div>
        </div>
      </div>

      <!-- คำถามที่พบบ่อย (FAQ) -->
      <div class="rounded-2xl glass-panel border border-slate-800 p-6 space-y-4">
        <h3 class="text-lg font-bold text-white flex items-center gap-2">
          <i data-lucide="help-circle" class="w-5 h-5 text-purple-400"></i>
          <span>คำถามที่พบบ่อย (FAQ)</span>
        </h3>
        <div class="space-y-2.5" id="faq-container">
          <div class="rounded-xl bg-slate-900/70 border border-slate-800 overflow-hidden">
            <button onclick="toggleFaq(this)" class="w-full px-4 py-3.5 text-left flex items-center justify-between text-sm font-semibold text-slate-200 hover:text-cyan-300">
              <span>ทำไมกดติดตั้งตามคู่มือแรกแล้วขึ้น Error?</span>
              <i data-lucide="chevron-down" class="w-4 h-4 transition-transform"></i>
            </button>
            <div class="hidden px-4 pb-4 text-xs sm:text-sm text-slate-400 border-t border-slate-800/80 pt-3">
              หากคู่มือแรกเกิด Error ให้ทำตาม <strong class="text-cyan-300">คู่มือการติดตั้ง 2 (สำรอง)</strong> โดยติดตั้งไฟล์แรกให้เสร็จก่อน แล้วจึงติดตั้งไฟล์ที่ 2 ตามทีหลังครับ
            </div>
          </div>
          <div class="rounded-xl bg-slate-900/70 border border-slate-800 overflow-hidden">
            <button onclick="toggleFaq(this)" class="w-full px-4 py-3.5 text-left flex items-center justify-between text-sm font-semibold text-slate-200 hover:text-cyan-300">
              <span>ติดตั้งครบทั้ง 2 ตัวแล้ว แต่ยังกดเปิดแอปไม่ได้?</span>
              <i data-lucide="chevron-down" class="w-4 h-4 transition-transform"></i>
            </button>
            <div class="hidden px-4 pb-4 text-xs sm:text-sm text-slate-400 border-t border-slate-800/80 pt-3">
              ตามคู่มือระบุไว้ว่า หากทำครบทุกขั้นตอนแล้วยังเปิดไม่ได้ อาจเป็นเพราะ <strong class="text-amber-300">สเปกหรือเวอร์ชันระบบของเครื่องคุณไม่รองรับ</strong> ครับ
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ==================== 3. หน้าลิงก์สำรอง / ชั่วคราว ==================== -->
    <section id="tab-backup" class="tab-section space-y-8">
      <div class="rounded-3xl glass-panel border border-amber-500/35 p-6 sm:p-8 flex flex-col lg:flex-row lg:items-center justify-between gap-6">
        <div class="space-y-2 max-w-2xl">
          <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-amber-500/15 border border-amber-500/30 text-amber-300 text-xs font-mono">
            <i data-lucide="clock" class="w-3.5 h-3.5"></i>
            <span>MIRROR & TEMPORARY NODE</span>
          </div>
          <h2 class="text-2xl sm:text-3xl font-bold text-white">เซิร์ฟเวอร์สำรอง & ไฟล์ชั่วคราว</h2>
          <p class="text-sm text-slate-300 leading-relaxed">
            ใช้สำหรับอัปโหลดไฟล์ชั่วคราว ไฟล์ทดสอบ หรือลิงก์สำรองในกรณีที่เซิร์ฟเวอร์หลักปิดปรับปรุง
          </p>
        </div>

        <div class="bg-slate-950/80 border border-slate-800 rounded-2xl p-4 w-full lg:w-80 space-y-2.5">
          <label class="text-xs font-mono text-slate-400 flex items-center gap-1.5">
            <i data-lucide="key-round" class="w-3.5 h-3.5 text-amber-400"></i>
            <span>รหัสผ่านปลดล็อกไฟล์ชั่วคราว (ถ้ามี)</span>
          </label>
          <div class="flex gap-2">
            <input id="temp-pass-input" type="password" placeholder="กรอกรหัสผ่าน..." class="flex-1 min-w-0 px-3 py-2 rounded-lg bg-slate-900 border border-slate-700 text-xs text-white focus:outline-none focus:border-amber-400" />
            <button onclick="unlockTempFiles()" class="px-3.5 py-2 rounded-lg bg-amber-500 hover:bg-amber-400 text-slate-950 font-bold text-xs transition shrink-0">ปลดล็อก</button>
          </div>
          <p id="temp-pass-msg" class="text-[11px] text-slate-500">สงวนไว้สำหรับไฟล์ลับเฉพาะกิจ</p>
        </div>
      </div>

      <!-- พื้นที่แสดงรายการไฟล์สำรอง -->
      <div id="backup-downloads-grid" class="grid grid-cols-1 md:grid-cols-2 gap-5"></div>
    </section>

  </main>

  <!-- Toast แจ้งเตือน -->
  <div id="toast" class="fixed bottom-5 right-5 z-50 translate-y-24 opacity-0 pointer-events-none transition-all duration-300">
    <div class="flex items-center gap-3 px-4 py-3 rounded-xl bg-slate-900/95 border border-cyan-500/50 shadow-xl shadow-cyan-950/50 text-sm text-white">
      <i data-lucide="check-circle-2" class="w-4 h-4 text-cyan-400 shrink-0"></i>
      <span id="toast-text">ดำเนินการสำเร็จ</span>
    </div>
  </div>

  <!-- Footer -->
  <footer class="border-t border-slate-800/80 bg-[#04060d]/90 py-6 text-center text-xs text-slate-500">
    <div class="max-w-6xl mx-auto px-4 flex flex-col sm:flex-row items-center justify-between gap-2">
      <p>© 2026 <span class="text-slate-300 font-semibold">NEXUS HUB</span>. Hosted on GitHub Pages.</p>
      <p class="font-mono text-[11px] text-slate-600">BUILD: v1.0.0-PROD</p>
    </div>
  </footer>

  <script src="script.js"></script>
</body>
</html>
:root {
  --bg-dark: #050811;
  --neon-cyan: #00f5d4;
  --neon-purple: #9b5de5;
}

* {
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: 'IBM Plex Sans Thai', sans-serif;
  background-color: var(--bg-dark);
  color: #e2e8f0;
  min-height: 100vh;
  overflow-x: hidden;
  position: relative;
}

/* Scrollbar สไตล์นีออน */
::-webkit-scrollbar {
  width: 8px;
  height: 8px;
}

::-webkit-scrollbar-track {
  background: #050811;
}

::-webkit-scrollbar-thumb {
  background: linear-gradient(180deg, #00f5d4, #7b2cbf);
  border-radius: 9999px;
}

.font-display {
  font-family: 'Orbitron', sans-serif;
}

.font-mono {
  font-family: 'JetBrains Mono', monospace;
}

/* พื้นหลัง Canvas อนุภาค */
#bg-canvas {
  position: fixed;
  inset: 0;
  width: 100%;
  height: 100%;
  z-index: -2;
  pointer-events: none;
}

/* แสงฟุ้งด้านหลัง */
.ambient-glow {
  position: fixed;
  width: 480px;
  height: 480px;
  border-radius: 50%;
  filter: blur(130px);
  opacity: 0.16;
  pointer-events: none;
  z-index: -1;
}

.glow-cyan {
  top: -120px;
  left: -100px;
  background: #00f5d4;
}

.glow-purple {
  bottom: -140px;
  right: -100px;
  background: #7b2cbf;
}

/* เอฟเฟกต์กระจก Glassmorphism */
.glass-panel {
  background: rgba(12, 18, 34, 0.72);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: 1px solid rgba(255, 255, 255, 0.08);
  box-shadow: 0 10px 35px -10px rgba(0, 0, 0, 0.65);
}

.neon-border-cyan {
  border: 1px solid rgba(0, 245, 212, 0.3);
  box-shadow: 0 0 28px rgba(0, 245, 212, 0.09);
}

.card-hover {
  transition: all 0.28s cubic-bezier(0.22, 1, 0.36, 1);
}

.card-hover:hover {
  transform: translateY(-4px);
  border-color: rgba(0, 245, 212, 0.55);
  box-shadow: 0 16px 36px -12px rgba(0, 245, 212, 0.22);
}

.gradient-text {
  background: linear-gradient(135deg, #00f5d4 0%, #38bdf8 50%, #c084fc 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

/* แท็บเมนู */
.nav-btn {
  transition: all 0.22s ease;
}

.nav-btn.active {
  background: linear-gradient(135deg, rgba(0, 245, 212, 0.18), rgba(155, 93, 229, 0.18));
  border-color: rgba(0, 245, 212, 0.5);
  color: #ffffff;
  box-shadow: 0 0 16px rgba(0, 245, 212, 0.18);
}

.tab-section {
  display: none;
  animation: fadeSlideIn 0.35s ease forwards;
}

.tab-section.active {
  display: block;
}

@keyframes fadeSlideIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.pulse-highlight {
  animation: highlightPulse 1.5s ease;
}

@keyframes highlightPulse {
  0%, 100% {
    box-shadow: 0 0 0 rgba(0, 245, 212, 0);
  }
  50% {
    box-shadow: 0 0 36px rgba(0, 245, 212, 0.65);
    border-color: #00f5d4;
  }
}

/* =====================================================================
   [จุดแก้ไขที่ 1] รายการไฟล์หน้าดาวน์โหลดหลัก (MAIN_DOWNLOADS)
   เมื่อต้องการลงไฟล์จริง ให้เพิ่มข้อมูลในวงเล็บก้ามปู [ ... ] ด้านล่างนี้
   ตัวอย่าง:
   {
     id: "app-1",
     title: "ชื่อแอปหรือไฟล์ของคุณ",
     version: "v1.0.0",
     size: "25 MB",
     category: "app", // เลือกได้: "app", "script", "tool"
     badge: "OFFICIAL",
     description: "รายละเอียดไฟล์ของคุณ",
     downloadUrl: "https://ใส่ลิงก์ดาวน์โหลดจริงของคุณที่นี่",
     updatedAt: "23 พ.ย. 2026"
   }
   ===================================================================== */
const MAIN_DOWNLOADS = [];

/* =====================================================================
   [จุดแก้ไขที่ 2] รายการไฟล์หน้าลิงก์สำรอง / ชั่วคราว (BACKUP_DOWNLOADS)
   ===================================================================== */
const TEMP_ACCESS_PASSCODE = "VIP2026";
const BACKUP_DOWNLOADS = [];

// =====================================================================
// ระบบทำงานหลักของเว็บไซต์
// =====================================================================
let currentCategory = "all";
let isTempUnlocked = false;

function renderMainDownloads() {
  const grid = document.getElementById("main-downloads-grid");
  const controls = document.getElementById("main-controls");
  const searchInput = document.getElementById("search-input");
  const searchTerm = searchInput ? searchInput.value.toLowerCase().trim() : "";

  if (MAIN_DOWNLOADS.length === 0) {
    controls.classList.add("hidden");
    controls.classList.remove("flex");
    grid.className = "grid grid-cols-1";
    grid.innerHTML = `
      <div class="rounded-3xl glass-panel border border-slate-800/90 p-10 sm:p-14 text-center space-y-5">
        <div class="w-16 h-16 mx-auto rounded-2xl bg-cyan-500/10 border border-cyan-500/30 flex items-center justify-center text-cyan-400">
          <i data-lucide="package-open" class="w-8 h-8"></i>
        </div>
        <div class="max-w-lg mx-auto space-y-2">
          <h3 class="text-xl sm:text-2xl font-bold text-white">พร้อมอัปโหลดไฟล์จริง</h3>
          <p class="text-sm text-slate-400 leading-relaxed">
            ขณะนี้ยังไม่มีรายการไฟล์เปิดให้ดาวน์โหลดในหน้าหลัก คุณสามารถอัปโหลดไฟล์และเพิ่มลิงก์ดาวน์โหลดจริงได้ตลอดเวลาในไฟล์ <code class="text-cyan-300 font-mono">script.js</code>
          </p>
        </div>
        <div class="pt-2">
          <button onclick="switchTab('guide')" class="inline-flex items-center gap-2 px-5 py-2.5 rounded-xl bg-cyan-500/15 hover:bg-cyan-500/25 border border-cyan-500/40 text-cyan-300 text-sm font-semibold transition">
            <i data-lucide="book-open" class="w-4 h-4"></i>
            <span>อ่านคู่มือการติดตั้งล่วงหน้า</span>
          </button>
        </div>
      </div>
    `;
    lucide.createIcons();
    return;
  }

  controls.classList.remove("hidden");
  controls.classList.add("flex");
  grid.className = "grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-5";

  const filtered = MAIN_DOWNLOADS.filter((item) => {
    const matchCat = currentCategory === "all" || item.category === currentCategory;
    const matchSearch =
      item.title.toLowerCase().includes(searchTerm) ||
      item.description.toLowerCase().includes(searchTerm) ||
      item.version.toLowerCase().includes(searchTerm);
    return matchCat && matchSearch;
  });

  if (filtered.length === 0) {
    grid.innerHTML = `
      <div class="col-span-full text-center py-12 glass-panel rounded-2xl border border-slate-800">
        <p class="text-slate-400 text-sm">ไม่พบไฟล์ที่ตรงกับคำค้นหาของคุณ</p>
      </div>
    `;
    return;
  }

  grid.innerHTML = filtered
    .map(
      (item) => `
      <article class="rounded-2xl glass-panel border border-slate-800/90 p-5 flex flex-col justify-between card-hover">
        <div class="space-y-3">
          <div class="flex items-center justify-between gap-2">
            <span class="px-2.5 py-1 rounded-md bg-cyan-500/10 border border-cyan-500/30 text-cyan-300 text-[11px] font-mono font-bold">
              ${item.badge || "RELEASE"}
            </span>
            <span class="text-xs font-mono text-slate-400">${item.version} • ${item.size}</span>
          </div>
          <h3 class="text-lg font-bold text-white leading-snug">${item.title}</h3>
          <p class="text-xs sm:text-sm text-slate-400 leading-relaxed">${item.description}</p>
        </div>
        <div class="pt-5 mt-4 border-t border-slate-800/80 flex items-center justify-between gap-3">
          <span class="text-[11px] text-slate-500 font-mono">อัปเดต: ${item.updatedAt}</span>
          <a href="${item.downloadUrl}" target="_blank" rel="noopener noreferrer"
             class="inline-flex items-center gap-2 px-4 py-2 rounded-xl bg-gradient-to-r from-cyan-400 to-sky-500 hover:from-cyan-300 hover:to-sky-400 text-slate-950 font-bold text-xs sm:text-sm shadow-lg shadow-cyan-500/20 transition">
            <i data-lucide="download" class="w-4 h-4"></i>
            <span>ดาวน์โหลด</span>
          </a>
        </div>
      </article>
    `
    )
    .join("");

  lucide.createIcons();
}

function renderBackupDownloads() {
  const grid = document.getElementById("backup-downloads-grid");

  if (BACKUP_DOWNLOADS.length === 0) {
    grid.className = "grid grid-cols-1";
    grid.innerHTML = `
      <div class="rounded-3xl glass-panel border border-slate-800/90 p-10 text-center space-y-4">
        <div class="w-14 h-14 mx-auto rounded-2xl bg-amber-500/10 border border-amber-500/30 flex items-center justify-center text-amber-400">
          <i data-lucide="server-off" class="w-7 h-7"></i>
        </div>
        <div class="max-w-md mx-auto space-y-1.5">
          <h3 class="text-lg sm:text-xl font-bold text-white">ยังไม่มีไฟล์ในเซิร์ฟเวอร์สำรอง</h3>
          <p class="text-xs sm:text-sm text-slate-400 leading-relaxed">
            พื้นที่นี้เตรียมไว้สำหรับลิงก์สำรองหรือไฟล์ชั่วคราว เมื่อต้องการใช้งานสามารถเพิ่มข้อมูลลงใน <code class="text-amber-300 font-mono">BACKUP_DOWNLOADS</code> ได้ทันที
          </p>
        </div>
      </div>
    `;
    lucide.createIcons();
    return;
  }

  grid.className = "grid grid-cols-1 md:grid-cols-2 gap-5";
  grid.innerHTML = BACKUP_DOWNLOADS.map((item) => {
    const locked = item.isSecret && !isTempUnlocked;
    return `
      <div class="rounded-2xl glass-panel border ${locked ? "border-amber-500/30" : "border-slate-800"} p-5 flex flex-col justify-between card-hover">
        <div class="space-y-2.5">
          <div class="flex items-center justify-between gap-2">
            <span class="px-2.5 py-0.5 rounded-md ${locked ? "bg-amber-500/15 text-amber-300 border-amber-500/30" : "bg-purple-500/15 text-purple-300 border-purple-500/30"} border text-[11px] font-mono">
              ${item.server}
            </span>
            <span class="text-xs font-mono text-slate-400">${item.size}</span>
          </div>
          <h3 class="text-base sm:text-lg font-bold text-white flex items-center gap-2">
            ${locked ? '<i data-lucide="lock" class="w-4 h-4 text-amber-400"></i>' : ""}
            <span>${item.title}</span>
          </h3>
          <p class="text-xs sm:text-sm text-slate-400">${item.description}</p>
        </div>
        <div class="pt-4 mt-4 border-t border-slate-800/80 flex items-center justify-between">
          <span class="text-[11px] font-mono text-amber-400/90">${item.expires}</span>
          ${
            locked
              ? `<span class="text-xs text-slate-500 font-mono">ต้องกรอกรหัสปลดล็อกด้านบน</span>`
              : `<a href="${item.downloadUrl}" target="_blank" rel="noopener noreferrer" class="inline-flex items-center gap-1.5 px-3.5 py-2 rounded-xl bg-amber-500/20 hover:bg-amber-500/30 border border-amber-500/50 text-amber-200 text-xs font-semibold transition">
                  <i data-lucide="external-link" class="w-3.5 h-3.5"></i>
                  <span>เปิดลิงก์สำรอง</span>
                </a>`
          }
        </div>
      </div>
    `;
  }).join("");

  lucide.createIcons();
}

function switchTab(tabName) {
  document.querySelectorAll(".tab-section").forEach((sec) => sec.classList.remove("active"));
  document.querySelectorAll(".nav-btn").forEach((btn) => {
    btn.classList.remove("active");
    btn.classList.add("text-slate-400");
  });

  const targetSec = document.getElementById(`tab-${tabName}`);
  const targetBtn = document.getElementById(`nav-${tabName}`);
  if (targetSec) targetSec.classList.add("active");
  if (targetBtn) {
    targetBtn.classList.add("active");
    targetBtn.classList.remove("text-slate-400");
  }
  window.scrollTo({ top: 0, behavior: "smooth" });
}

function setCategory(cat) {
  currentCategory = cat;
  document.querySelectorAll(".cat-btn").forEach((btn) => {
    if (btn.dataset.cat === cat) {
      btn.className = "cat-btn px-3.5 py-2 rounded-xl text-xs font-semibold bg-cyan-500 text-slate-950 transition whitespace-nowrap";
    } else {
      btn.className = "cat-btn px-3.5 py-2 rounded-xl text-xs font-semibold bg-slate-900 text-slate-300 border border-slate-800 hover:border-cyan-500/40 transition whitespace-nowrap";
    }
  });
  renderMainDownloads();
}

function jumpToBackupGuide() {
  switchTab("guide");
  setTimeout(() => {
    const card2 = document.getElementById("card-guide-2");
    if (card2) {
      card2.scrollIntoView({ behavior: "smooth", block: "center" });
      card2.classList.remove("pulse-highlight");
      void card2.offsetWidth;
      card2.classList.add("pulse-highlight");
    }
  }, 120);
}

function toggleFaq(btn) {
  const content = btn.nextElementSibling;
  const icon = btn.querySelector("svg");
  content.classList.toggle("hidden");
  if (icon) icon.classList.toggle("rotate-180");
}

function unlockTempFiles() {
  const input = document.getElementById("temp-pass-input").value.trim();
  const msg = document.getElementById("temp-pass-msg");
  if (input === TEMP_ACCESS_PASSCODE) {
    isTempUnlocked = true;
    msg.textContent = "ปลดล็อกสิทธิ์การเข้าถึงเรียบร้อยแล้ว!";
    msg.className = "text-[11px] text-emerald-400 font-medium";
    renderBackupDownloads();
    showToast("ปลดล็อกไฟล์ชั่วคราวสำเร็จ");
  } else {
    msg.textContent = "รหัสผ่านไม่ถูกต้อง กรุณาลองใหม่อีกครั้ง";
    msg.className = "text-[11px] text-rose-400 font-medium";
  }
}

function copySiteUrl() {
  const url = window.location.href;
  if (navigator.clipboard && window.location.href.startsWith("http")) {
    navigator.clipboard.writeText(url).then(() => showToast("คัดลอกลิงก์เว็บไซต์เรียบร้อยแล้ว!"));
  } else {
    showToast("พร้อมแชร์! อัปโหลดขึ้น GitHub เพื่อรับลิงก์สาธารณะ");
  }
}

function showToast(message) {
  const toast = document.getElementById("toast");
  const toastText = document.getElementById("toast-text");
  toastText.textContent = message;
  toast.classList.remove("translate-y-24", "opacity-0");
  setTimeout(() => {
    toast.classList.add("translate-y-24", "opacity-0");
  }, 2600);
}

// พื้นหลังแอนิเมชันอนุภาค (Interactive Particle Background)
function initParticles() {
  const canvas = document.getElementById("bg-canvas");
  if (!canvas) return;
  const ctx = canvas.getContext("2d");
  let particles = [];
  const count = window.innerWidth < 768 ? 28 : 55;

  function resize() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
  }
  resize();
  window.addEventListener("resize", resize);

  for (let i = 0; i < count; i++) {
    particles.push({
      x: Math.random() * canvas.width,
      y: Math.random() * canvas.height,
      vx: (Math.random() - 0.5) * 0.45,
      vy: (Math.random() - 0.5) * 0.45,
      r: Math.random() * 1.8 + 0.6,
      color: i % 2 === 0 ? "rgba(0, 245, 212, 0.45)" : "rgba(155, 93, 229, 0.45)"
    });
  }

  function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    for (let i = 0; i < particles.length; i++) {
      const p = particles[i];
      p.x += p.vx;
      p.y += p.vy;
      if (p.x < 0 || p.x > canvas.width) p.vx *= -1;
      if (p.y < 0 || p.y > canvas.height) p.vy *= -1;

      ctx.beginPath();
      ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
      ctx.fillStyle = p.color;
      ctx.fill();

      for (let j = i + 1; j < particles.length; j++) {
        const p2 = particles[j];
        const dist = Math.hypot(p.x - p2.x, p.y - p2.y);
        if (dist < 130) {
          ctx.beginPath();
          ctx.moveTo(p.x, p.y);
          ctx.lineTo(p2.x, p2.y);
          ctx.strokeStyle = `rgba(56, 189, 248, ${0.12 * (1 - dist / 130)})`;
          ctx.lineWidth = 0.7;
          ctx.stroke();
        }
      }
    }
    requestAnimationFrame(draw);
  }
  draw();
}

document.addEventListener("DOMContentLoaded", () => {
  renderMainDownloads();
  renderBackupDownloads();
  initParticles();
  lucide.createIcons();
});
