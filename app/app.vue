<script setup>
/* --- 1. DATA & LOGIKA --- */
import { ref, computed } from 'vue'

// Data Profil
const nama = "Nur Fajri Fa'iz"
const role = "Software Engineer Enthusiast"
const bio = "Fokus pada pengembangan arsitektur yang skalabel, efisien, dan user-centric untuk solusi masa depan."

const halamanAktif = ref('proyek') 

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

// Data Proyek (Termasuk IoT EWS dengan Telegram)
const projects = [
  { 
    judul: "Smart News Portal", 
    tech: "Nuxt.js", 
    desc: "Arsitektur portal berita dengan optimasi performa tinggi dan SEO friendly.",
    link: "https://github.com/2283230010-ops/smart-news" 
  },
  { 
    judul: "IoT Early Warning System", 
    tech: "Arduino IDE", 
    desc: "Sistem deteksi dini berbasis ESP32/ESP8266 yang mengirimkan notifikasi peringatan real-time via Telegram Bot saat sensor mendeteksi anomali.",
    link: "https://github.com/2283230010-ops/ews-iot-telegram" 
  },
  { 
    judul: "E-Commerce Suite", 
    tech: "Nuxt 3", 
    desc: "Sistem toko online dengan manajemen state modern dan integrasi payment gateway.",
    link: "https://github.com/2283230010-ops/ecommerce" 
  },
  { 
    judul: "Data Analytics", 
    tech: "Vue.js", 
    desc: "Dashboard monitoring data real-time dengan visualisasi grafik interaktif.",
    link: "https://github.com/2283230010-ops/analytics" 
  }
]

// Logika Navigasi
const labelTombol = computed(() => 
  halamanAktif.value === 'proyek' ? 'Lihat Engineering Philosophy 👤' : 'Kembali ke Portofolio 🚀'
)

const toggleHalaman = () => {
  halamanAktif.value = halamanAktif.value === 'proyek' ? 'profil' : 'proyek'
}
</script>

<template>
  <div class="main-wrapper">
    <div class="bg-overlay"></div>
    
    <header class="logo-nav" role="banner">
      <div class="logo-glass" aria-label="Logo Kompas">
        <img src="/logo-kompas.png" alt="Kompas" class="img-k">
      </div>
      <div class="logo-glass" aria-label="Logo Untirta">
        <img src="/logo-untirta.png" alt="Untirta" class="img-u">
      </div>
    </header>

    <main class="content-grid">
      
      <aside class="card-white sidebar">
        <section class="profile-section">
          <div class="avatar-wrapper">
            <img src="/foto-profil.png" alt="Foto Profil Nur Fajri Faiz" class="avatar-img" />
          </div>
          <div class="badge-role">SOFTWARE ENGINEERING</div>
          <h1 class="text-name">{{ nama }}</h1>
          <p class="text-role">{{ role }}</p>
          <div class="divider"></div>
        </section>

        <section class="info-section">
          <label>Bio Profile</label>
          <p class="text-bio">{{ bio }}</p>
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

      <section class="card-white main-content">
        <transition name="page-fade" mode="out-in">
          <div :key="halamanAktif">
            
            <div v-if="halamanAktif === 'proyek'">
              <h2 class="section-title">Featured Engineering Works</h2>
              <div class="project-grid">
                <a v-for="p in projects" 
                   :key="p.judul" 
                   :href="p.link" 
                   target="_blank" 
                   rel="noopener"
                   class="project-card-link">
                  <article class="project-card-inner">
                    <div :class="['badge-tech', p.tech === 'Arduino IDE' ? 'badge-arduino' : '']">
                      {{ p.tech }}
                    </div>
                    <h3>
                      {{ p.judul }} 
                      <span v-if="p.desc.includes('Telegram')" class="tg-icon" title="Telegram Integrated">✈️</span>
                    </h3>
                    <p>{{ p.desc }}</p>
                    <div class="btn-explore">
                      Explore Architecture <span class="arrow">→</span>
                    </div>
                  </article>
                </a>
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
  background: linear-gradient(135deg, rgba(0,0,0,0.75) 0%, rgba(0,0,0,0.45) 100%);
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
}
.badge-role {
  background: #fef3c7; color: #92400e; padding: 6px 14px;
  border-radius: 10px; font-size: 0.75rem; font-weight: 800; letter-spacing: 0.5px;
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
.btn-action:hover { background: #be123c; transform: translateY(-2px); box-shadow: 0 10px 25px rgba(225, 29, 72, 0.35); }

/* --- Proyek --- */
.project-card-link { text-decoration: none; color: inherit; display: block; }
.section-title { font-size: 1.8rem; color: #111; margin-bottom: 35px; font-weight: 800; }
.project-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 24px; }

.project-card-inner {
  background: #fcfcfc; padding: 35px; border-radius: 24px;
  border: 1px solid #f3f3f3; transition: all 0.4s ease; height: 100%;
  display: flex; flex-direction: column;
}

.project-card-link:hover .project-card-inner {
  background: #ffffff; border-color: #d4af37; transform: translateY(-8px);
  box-shadow: 0 20px 40px rgba(0,0,0,0.06);
}

.badge-tech { color: #b45309; font-size: 0.75rem; font-weight: 800; margin-bottom: 15px; text-transform: uppercase; }
.badge-arduino { 
  color: #00878F !important; 
  background: rgba(0, 135, 143, 0.1); 
  padding: 4px 10px; border-radius: 8px; border: 1px solid rgba(0, 135, 143, 0.3);
}

.tg-icon { font-size: 1.2rem; margin-left: 8px; }
.btn-explore { margin-top: auto; padding-top: 25px; font-weight: 800; color: #111; font-size: 0.85rem; display: flex; align-items: center; gap: 10px; }
.arrow { transition: transform 0.3s ease; }
.project-card-link:hover .arrow { transform: translateX(8px); }

/* --- Animasi --- */
.page-fade-enter-active, .page-fade-leave-active { transition: all 0.4s ease; }
.page-fade-enter-from { opacity: 0; transform: translateY(20px); }
.page-fade-leave-to { opacity: 0; transform: translateY(-20px); }

@media (max-width: 1100px) {
  .content-grid { grid-template-columns: 1fr; }
  .main-wrapper { padding-top: 130px; }
  .sidebar { position: static; }
}
</style>