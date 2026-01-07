<script setup>
/* --- 1. DATA & LOGIKA --- */
import { ref, computed } from 'vue'

// Data Profil (Pastikan file ini ada di folder public Anda)
const profil = {
  nama: "Nur Fajri Fa'iz",
  role: "Software Engineer Enthusiast",
  bio: "Fokus pada pengembangan arsitektur yang skalabel, efisien, dan user-centric untuk solusi masa depan.",
  fotoProfil: "/foto-profil.png",
  fotoCV: "/cv-fajri.png" // Taruh file gambar CV Anda di public/cv-fajri.png
}

const halamanAktif = ref('proyek') 
const selectedArch = ref(null)
const showCV = ref(false)

// Data Media Sosial
const sosmed = [
  { name: "GitHub", icon: "🐙", link: "https://github.com/2283230010-ops" },
  { name: "LinkedIn", icon: "💼", link: "https://www.linkedin.com/in/nur-fajri-fa-iz-aa60a6288" },
  { name: "Instagram", icon: "📸", link: "https://instagram.com/nrfjrfz" },
  { name: "WhatsApp", icon: "💬", link: "https://wa.me/6281529012005" }
]

// Data Keahlian
const skills = [
  { name: "JavaScript/ES6", icon: "💻" },
  { name: "Nuxt.js / Vue", icon: "🚀" },
  { name: "Node.js", icon: "🌐" },
  { name: "Arduino IDE", icon: "🤖" },
  { name: "Delphi", icon: "🏺" },
  { name: "Git & Agile", icon: "📁" }
]

// Data Proyek + Architecture Details
const projects = [
  { 
    id: "news",
    judul: "Smart News Portal", 
    tech: "Nuxt.js", 
    desc: "Arsitektur portal berita dengan optimasi performa tinggi dan SEO friendly.",
    link: "https://github.com/2283230010-ops/smart-news",
    arch: {
      points: [
        { t: "SEO Optimization", d: "SSR (Server Side Rendering) untuk indexing artikel yang cepat." },
        { t: "Dynamic Hydration", d: "Pemuatan komponen berat hanya saat dibutuhkan oleh user." }
      ],
      stack: ["Nuxt.js", "Vue 3", "Tailwind CSS", "Nitro"],
      flow: ["Browser", "Nuxt Server", "Content API", "Database"]
    }
  },
  { 
    id: "iot",
    judul: "IoT Early Warning System", 
    tech: "Arduino IDE", 
    isIoT: true,
    desc: "Sistem deteksi dini berbasis ESP32/ESP8266 yang mengirimkan notifikasi peringatan via Telegram Bot saat sensor mendeteksi anomali.",
    link: "https://github.com/2283230010-ops/ews-iot-telegram",
    arch: {
      points: [
        { t: "Real-time Alerting", d: "Integrasi Telegram Bot API untuk notifikasi instan (milisetik)." },
        { t: "Edge Computing", d: "Logika pemrosesan sensor di mikrokontroler untuk respon cepat." }
      ],
      stack: ["ESP32", "Arduino C++", "Telegram Bot API", "WiFi Manager"],
      flow: ["Sensors", "ESP32 Controller", "WiFi Cloud", "User Telegram"]
    }
  },
  { 
    id: "ecommerce",
    judul: "E-Commerce Suite", 
    tech: "Nuxt 3", 
    desc: "Sistem toko online dengan manajemen state modern dan integrasi payment gateway.",
    link: "https://github.com/2283230010-ops/ecommerce",
    arch: {
      points: [
        { t: "State Persistence", d: "Manajemen keranjang belanja menggunakan Pinia dengan sinkronisasi local storage." },
        { t: "Payment Loop", d: "Integrasi Webhook Midtrans untuk verifikasi status bayar otomatis." }
      ],
      stack: ["Nuxt 3", "Pinia", "Prisma ORM", "PostgreSQL"],
      flow: ["Frontend", "Server Route", "Payment API", "Database"]
    }
  },
  { 
    id: "analytics",
    judul: "Data Analytics", 
    tech: "Vue.js", 
    desc: "Dashboard monitoring data real-time dengan visualisasi grafik interaktif.",
    link: "https://github.com/2283230010-ops/analytics",
    arch: {
      points: [
        { t: "Reactive Data", d: "Visualisasi data yang terupdate secara reaktif menggunakan Chart.js." },
        { t: "Data Filtering", d: "Logika filter sisi klien untuk performa dashboard yang responsif." }
      ],
      stack: ["Vue 3", "Chart.js", "Axios", "Composition API"],
      flow: ["Data API", "Data Transformer", "Pinia Store", "Charts Rendering"]
    }
  }
]

// Logika Navigasi
const labelTombol = computed(() => 
  halamanAktif.value === 'proyek' ? 'Lihat Engineering Philosophy 👤' : 'Kembali ke Portofolio 🚀'
)

const toggleHalaman = () => {
  halamanAktif.value = halamanAktif.value === 'proyek' ? 'profil' : 'proyek'
}

const openArch = (p) => {
  selectedArch.value = p
}
</script>

<template>
  <div class="main-wrapper">
    <div class="bg-overlay"></div>
    
    <!-- Header Branding -->
    <header class="logo-nav" role="banner">
      <div class="logo-glass" aria-label="Logo Kompas">
        <img src="/logo-kompas.png" alt="Kompas" class="img-k">
      </div>
      <div class="logo-glass" aria-label="Logo Untirta">
        <img src="/logo-untirta.png" alt="Untirta" class="img-u">
      </div>
    </header>

    <main class="content-grid">
      
      <!-- SIDEBAR -->
      <aside class="card-white sidebar">
        <section class="profile-section">
          <!-- Foto profil bisa diklik untuk buka CV -->
          <div class="avatar-wrapper cursor-pointer group" @click="showCV = true" title="Klik untuk lihat CV">
            <img :src="profil.fotoProfil" alt="Foto Profil" class="avatar-img transition-transform group-hover:scale-105" />
          </div>
          <div class="badge-role">SOFTWARE ENGINEERING</div>
          <h1 class="text-name">{{ profil.nama }}</h1>
          <p class="text-role">{{ profil.role }}</p>
          <div class="divider"></div>
        </section>

        <section class="info-section">
          <label>Bio Profile</label>
          <p class="text-bio">{{ profil.bio }}</p>
        </section>

        <section class="info-section">
          <label>Social Connections</label>
          <nav class="sosmed-row">
            <a v-for="s in sosmed" 
               :key="s.name" 
               :href="s.link" 
               target="_blank" 
               rel="noopener"
               class="sosmed-pill">
              <span class="icon">{{ s.icon }}</span> {{ s.name }}
            </a>
          </nav>
        </section>

        <section class="info-section">
          <label>Technical Skills</label>
          <div class="skill-grid">
            <div v-for="s in skills" :key="s.name" class="skill-pill">
              {{ s.icon }} {{ s.name }}
            </div>
          </div>
        </section>

        <button class="btn-action" @click="toggleHalaman" aria-live="polite">
          {{ labelTombol }}
        </button>
      </aside>

      <!-- MAIN CONTENT -->
      <section class="card-white main-content">
        <transition name="page-fade" mode="out-in">
          <div :key="halamanAktif">
            
            <div v-if="halamanAktif === 'proyek'">
              <h2 class="section-title">Featured Engineering Works</h2>
              <div class="project-grid">
                <article v-for="p in projects" :key="p.id" class="project-card-inner">
                  <div class="flex-row-header">
                    <div :class="['badge-tech', p.isIoT ? 'badge-arduino' : '']">
                      {{ p.tech }}
                    </div>
                    <a :href="p.link" target="_blank" class="link-github-small">GitHub ↗</a>
                  </div>
                  <h3>
                    {{ p.judul }} 
                    <span v-if="p.isIoT" class="tg-icon">✈️</span>
                  </h3>
                  <p>{{ p.desc }}</p>
                  
                  <button class="btn-explore-arch" @click="openArch(p)">
                    Explore Architecture <span class="arrow">→</span>
                  </button>
                </article>
              </div>
            </div>

            <div v-else>
              <h2 class="section-title">Engineering Philosophy</h2>
              <div class="philosophy-content">
                <article class="phil-box">
                  <div class="phil-header">
                    <span class="phil-icon">🎯</span>
                    <h3>Technical Vision</h3>
                  </div>
                  <p>Membangun sistem yang tidak hanya berjalan, tetapi juga efisien, aman, dan mudah dikelola dalam skala industri besar.</p>
                </article>
                <div class="divider"></div>
                <article class="phil-box">
                  <div class="phil-header">
                    <span class="phil-icon">📰</span>
                    <h3>Commitment to Kompas</h3>
                  </div>
                  <p>Berdedikasi menghadirkan inovasi teknologi perangkat lunak untuk mendukung integritas jurnalisme Kompas di era digital.</p>
                </article>
              </div>
            </div>

          </div>
        </transition>
      </section>
    </main>

    <!-- ARCHITECTURE MODAL -->
    <transition name="modal-fade">
      <div v-if="selectedArch" class="modal-overlay" @click.self="selectedArch = null">
        <div class="modal-container shadow-2xl">
          <button class="close-modal" @click="selectedArch = null">&times;</button>
          
          <div class="modal-content">
            <header class="mb-6">
              <span class="badge-blueprint">Engineering Blueprint</span>
              <h2 class="text-3xl font-black mt-2">{{ selectedArch.judul }}</h2>
            </header>

            <div class="modal-grid">
              <div class="modal-info">
                <div v-for="point in selectedArch.arch.points" :key="point.t" class="arch-point">
                  <h4 class="font-bold text-rose-600">{{ point.t }}</h4>
                  <p class="text-sm text-gray-600 leading-relaxed">{{ point.d }}</p>
                </div>
                
                <div class="mt-6">
                  <h4 class="text-xs font-black uppercase text-gray-400 mb-2">Development Stack</h4>
                  <div class="tag-row">
                    <span v-for="tag in selectedArch.arch.stack" :key="tag" class="arch-tag">{{ tag }}</span>
                  </div>
                </div>
              </div>

              <div class="modal-viz bg-slate-900 rounded-2xl p-6 flex flex-col items-center justify-center gap-3">
                 <div v-for="(step, i) in selectedArch.arch.flow" :key="step" class="flex flex-col items-center w-full">
                    <div class="viz-node">{{ step }}</div>
                    <div v-if="i < selectedArch.arch.flow.length - 1" class="viz-line"></div>
                 </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </transition>

    <!-- MODAL CV (Gambar dari public) -->
    <transition name="modal-fade">
      <div v-if="showCV" class="modal-overlay" @click.self="showCV = false">
        <div class="modal-container cv-container shadow-2xl">
          <button class="close-modal" @click="showCV = false">&times;</button>
          
          <div class="modal-content cv-scrollable custom-scrollbar">
            <header class="mb-6 text-center">
              <span class="badge-blueprint">Curriculum Vitae</span>
              <h2 class="text-2xl font-black mt-2">Professional Profile</h2>
            </header>
            
            <div class="cv-wrapper">
              <!-- Menampilkan gambar CV dari folder public -->
              <img :src="profil.fotoCV" alt="Curriculum Vitae Nur Fajri Fa'iz" class="cv-image" />
            </div>

            <div class="mt-8 text-center">
               <a :href="profil.fotoCV" download class="btn-download-cv">
                 Download CV (Image) 📥
               </a>
            </div>
          </div>
        </div>
      </div>
    </transition>

  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');

/* --- Layout Dasar --- */
.main-wrapper {
  min-height: 100vh;
  background: url('/bg-koran.jpg') center/cover fixed;
  font-family: 'Plus Jakarta Sans', sans-serif;
  padding: 140px 20px 60px;
  position: relative;
  overflow-x: hidden;
}

.bg-overlay {
  position: absolute; top: 0; left: 0; right: 0; bottom: 0;
  background: linear-gradient(135deg, rgba(0,0,0,0.85) 0%, rgba(0,0,0,0.55) 100%);
  z-index: 0;
}

/* --- Header --- */
.logo-nav {
  position: absolute; top: 40px; left: 50%; transform: translateX(-50%);
  display: flex; gap: 20px; z-index: 10;
}
.logo-glass {
  background: rgba(255, 255, 255, 0.95); backdrop-filter: blur(12px);
  padding: 10px 25px; border-radius: 16px; 
  box-shadow: 0 10px 30px rgba(0,0,0,0.25);
  display: flex; align-items: center; justify-content: center;
}
.img-k { height: 22px; }
.img-u { height: 28px; }

/* --- Grid & Cards --- */
.content-grid {
  position: relative; z-index: 1;
  display: grid; grid-template-columns: 380px 1fr; gap: 30px;
  max-width: 1300px; margin: 0 auto;
}
.card-white {
  background: #ffffff; border-radius: 28px; padding: 40px;
  box-shadow: 0 20px 60px -15px rgba(0, 0, 0, 0.35);
}

/* --- Sidebar --- */
.avatar-img { 
  width: 110px; height: 110px; border-radius: 50%; 
  border: 4px solid #f8f9fa; object-fit: cover; margin-bottom: 15px;
  box-shadow: 0 8px 20px rgba(0,0,0,0.1);
  display: block;
}
.badge-role {
  background: #fef3c7; color: #92400e; padding: 6px 14px;
  border-radius: 10px; font-size: 0.75rem; font-weight: 800; letter-spacing: 0.5px; display: inline-block;
}
.text-name { font-size: 2rem; color: #111; margin: 15px 0 5px; font-weight: 800; }
.text-role { color: #666; font-size: 1.05rem; margin-bottom: 10px; }
.divider { width: 100%; height: 1px; background: #f1f1f1; margin: 25px 0; }

label { 
  font-size: 0.7rem; font-weight: 800; color: #999; 
  text-transform: uppercase; letter-spacing: 1.5px; display: block; margin-bottom: 12px;
}
.text-bio { font-size: 0.95rem; color: #444; line-height: 1.7; margin-bottom: 30px; }

.sosmed-row { display: flex; flex-wrap: wrap; gap: 10px; margin-bottom: 30px; }
.sosmed-pill {
  background: #fdfdfd; padding: 10px 16px; border-radius: 12px;
  font-size: 0.85rem; color: #333; font-weight: 700;
  text-decoration: none; border: 1px solid #eee; transition: all 0.3s ease;
}
.sosmed-pill:hover { background: #111; color: #fff; transform: translateY(-3px); }

.skill-grid { display: flex; flex-wrap: wrap; gap: 8px; margin-bottom: 30px; }
.skill-pill { 
  background: #f8f9fa; padding: 8px 14px; border-radius: 10px; 
  font-size: 0.8rem; color: #555; font-weight: 600; border: 1px solid #f1f1f1;
}

.btn-action {
  width: 100%; background: #e11d48; color: white; border: none;
  padding: 18px; border-radius: 16px; font-weight: 800; cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}
.btn-action:hover { background: #be123c; transform: translateY(-2px); }

/* --- Proyek --- */
.section-title { font-size: 1.8rem; color: #111; margin-bottom: 35px; font-weight: 800; }
.project-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 24px; }

.project-card-inner {
  background: #fcfcfc; padding: 35px; border-radius: 24px;
  border: 1px solid #f3f3f3; transition: all 0.4s ease; height: 100%;
  display: flex; flex-direction: column;
}
.project-card-inner:hover {
  background: #ffffff; border-color: #e11d48; transform: translateY(-8px);
}
.flex-row-header { display: flex; justify-content: space-between; align-items: center; }
.link-github-small { font-size: 0.7rem; text-decoration: none; color: #999; font-weight: bold; }

.badge-tech { color: #b45309; font-size: 0.75rem; font-weight: 800; margin-bottom: 15px; text-transform: uppercase; }
.badge-arduino { color: #00878F !important; }

.btn-explore-arch { 
  margin-top: auto; padding-top: 25px; font-weight: 800; color: #e11d48; background: none; border: none; 
  cursor: pointer; text-align: left; font-family: inherit;
}
.arrow { transition: transform 0.3s ease; display: inline-block; }
.btn-explore-arch:hover .arrow { transform: translateX(8px); }

/* --- Modal Styles --- */
.modal-overlay {
  position: fixed; top: 0; left: 0; width: 100%; height: 100%;
  background: rgba(15, 23, 42, 0.9); backdrop-filter: blur(8px);
  z-index: 100; display: flex; align-items: center; justify-content: center; padding: 20px;
}
.modal-container {
  background: white; border-radius: 32px; width: 100%; max-width: 900px;
  padding: 40px; position: relative;
}
.close-modal { position: absolute; top: 20px; right: 25px; font-size: 2rem; border: none; background: none; cursor: pointer; color: #ccc; z-index: 110; }
.badge-blueprint { background: #fee2e2; color: #dc2626; padding: 4px 12px; border-radius: 8px; font-size: 0.65rem; font-weight: 900; text-transform: uppercase; }

.modal-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 40px; margin-top: 30px; }
.arch-point { margin-bottom: 20px; }
.arch-tag { background: #f1f5f9; padding: 4px 10px; border-radius: 8px; font-size: 0.7rem; font-weight: bold; color: #64748b; margin-right: 5px; }

.viz-node { background: #1e293b; border: 1px solid #334155; color: #fb7185; padding: 10px 20px; border-radius: 10px; font-size: 0.75rem; font-weight: bold; width: 100%; text-align: center; }
.viz-line { width: 2px; height: 15px; background: #334155; }

/* CV Specific Styles */
.cv-container {
  max-width: 800px;
  max-height: 90vh;
  display: flex;
  flex-direction: column;
}
.cv-scrollable {
  overflow-y: auto;
  padding-right: 10px;
}
.cv-wrapper {
  border: 1px solid #f1f5f9;
  border-radius: 16px;
  overflow: hidden;
}
.cv-image {
  width: 100%;
  height: auto;
  display: block;
}
.btn-download-cv {
  display: inline-block;
  background: #111;
  color: white;
  padding: 12px 24px;
  border-radius: 12px;
  font-weight: 800;
  text-decoration: none;
  font-size: 0.8rem;
  transition: all 0.3s ease;
}
.btn-download-cv:hover {
  background: #e11d48;
  transform: translateY(-2px);
}

/* Custom Scrollbar */
.custom-scrollbar::-webkit-scrollbar { width: 6px; }
.custom-scrollbar::-webkit-scrollbar-track { background: #f1f5f9; border-radius: 10px; }
.custom-scrollbar::-webkit-scrollbar-thumb { background: #ccc; border-radius: 10px; }
.custom-scrollbar::-webkit-scrollbar-thumb:hover { background: #999; }

/* --- Animasi --- */
.page-fade-enter-active, .page-fade-leave-active { transition: all 0.4s ease; }
.page-fade-enter-from { opacity: 0; transform: translateY(20px); }
.page-fade-leave-to { opacity: 0; transform: translateY(-20px); }

.modal-fade-enter-active, .modal-fade-leave-active { transition: all 0.3s ease; }
.modal-fade-enter-from, .modal-fade-leave-to { opacity: 0; transform: scale(0.95); }

@media (max-width: 1000px) {
  .content-grid { grid-template-columns: 1fr; }
  .modal-grid { grid-template-columns: 1fr; }
  .sidebar { position: static; }
}
</style>