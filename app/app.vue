<script setup>
/* --- 1. DATA & LOGIKA --- */
import { ref } from 'vue'

const nama = "Nur Fajri Fa'iz"
const role = "Software Engineer Enthusiast"
const bio = "Fokus pada pengembangan arsitektur yang skalabel, efisien, dan user-centric untuk solusi masa depan."

const halamanAktif = ref('proyek') 

// DATA LINK SOSIAL MEDIA - Sudah diperbarui dengan link aslimu
const sosmed = [
  { name: "GitHub", icon: "🐙", link: "https://github.com/2283230010-ops" },
  { name: "LinkedIn", icon: "💼", link: "https://www.linkedin.com/in/nur-fajri-fa-iz-aa60a6288" },
  { name: "Instagram", icon: "📸", link: "https://instagram.com/nrfjrfz" },
  { name: "WhatsApp", icon: "💬", link: "https://wa.me/6281529012005" }
]

const skills = [
  { name: "JavaScript/ES6", icon: "💻" },
  { name: "Nuxt.js / Vue", icon: "🚀" },
  { name: "Node.js", icon: "🌐" },
  { name: "Git & Agile", icon: "📁" }
]

const projects = [
  { judul: "Smart News Portal", tech: "Nuxt.js", desc: "Arsitektur portal berita dengan optimasi performa tinggi." },
  { judul: "E-Commerce Suite", tech: "Nuxt 3", desc: "Sistem toko online dengan manajemen state modern." },
  { judul: "Data Analytics", tech: "Vue.js", desc: "Dashboard monitoring data real-time." }
]
</script>

<template>
  <div class="main-wrapper">
    <div class="bg-overlay"></div>
    
    <header class="logo-nav">
      <div class="logo-glass"><img src="/logo-kompas.png" alt="Kompas" class="img-k"></div>
      <div class="logo-glass"><img src="/logo-untirta.png" alt="Untirta" class="img-u"></div>
    </header>

    <main class="content-grid">
      
      <aside class="card-white sidebar">
        <div class="profile-section">
          <div class="avatar-wrapper">
            <img src="/foto-profil.png" alt="Profile" class="avatar-img" />
          </div>
          <div class="badge-role">Software Engineering</div>
          <h1 class="text-name">{{ nama }}</h1>
          <p class="text-role">{{ role }}</p>
          <div class="divider"></div>
        </div>

        <div class="info-section">
          <label>Profile Bio</label>
          <p class="text-bio">{{ bio }}</p>
        </div>

        <div class="info-section">
          <label>Social Connections</label>
          <div class="sosmed-row">
            <a v-for="s in sosmed" 
               :key="s.name" 
               :href="s.link" 
               target="_blank" 
               class="sosmed-pill">
              {{ s.icon }} {{ s.name }}
            </a>
          </div>
        </div>

        <div class="info-section">
          <label>Technical Skills</label>
          <div class="skill-grid">
            <div v-for="s in skills" :key="s.name" class="skill-pill">
              {{ s.icon }} {{ s.name }}
            </div>
          </div>
        </div>

        <button class="btn-action" @click="halamanAktif = halamanAktif === 'proyek' ? 'profil' : 'proyek'">
          {{ halamanAktif === 'proyek' ? 'Lihat Engineering Philosophy 👤' : 'Kembali ke Portofolio 🚀' }}
        </button>
      </aside>

      <section class="card-white main-content">
        <transition name="fade" mode="out-in">
          <div :key="halamanAktif">
            <div v-if="halamanAktif === 'proyek'">
              <h2 class="section-title">Featured Engineering Works</h2>
              <div class="project-grid">
                <div v-for="p in projects" :key="p.judul" class="project-card-inner">
                  <div class="badge-tech">{{ p.tech }}</div>
                  <h3>{{ p.judul }}</h3>
                  <p>{{ p.desc }}</p>
                  <div class="btn-explore">Explore Architecture →</div>
                </div>
              </div>
            </div>

            <div v-else>
              <h2 class="section-title">Engineering Philosophy</h2>
              <div class="philosophy-content">
                <div class="phil-box">
                  <h3>Technical Vision</h3>
                  <p>Membangun sistem yang tidak hanya berjalan, tetapi juga efisien, aman, dan mudah dikelola dalam skala industri besar.</p>
                </div>
                <div class="divider"></div>
                <div class="phil-box">
                  <h3>Commitment to Kompas</h3>
                  <p>Berdedikasi menghadirkan inovasi teknologi perangkat lunak untuk mendukung integritas jurnalisme Kompas di era digital.</p>
                </div>
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

.main-wrapper {
  min-height: 100vh;
  background: url('/bg-koran.jpg') center/cover fixed;
  font-family: 'Plus Jakarta Sans', sans-serif;
  padding: 140px 40px 60px;
  position: relative;
}

.bg-overlay {
  position: absolute; top: 0; left: 0; right: 0; bottom: 0;
  background: rgba(0, 0, 0, 0.45); z-index: 0;
}

.logo-nav, .content-grid { position: relative; z-index: 1; }

.logo-nav {
  position: absolute; top: 40px; left: 50%; transform: translateX(-50%);
  display: flex; gap: 20px;
}

.logo-glass {
  background: rgba(255, 255, 255, 0.85); backdrop-filter: blur(12px);
  padding: 12px 28px; border-radius: 16px; display: flex; align-items: center;
  box-shadow: 0 10px 25px rgba(0,0,0,0.15);
}

.img-k { height: 24px; } .img-u { height: 30px; }

.content-grid {
  display: grid; grid-template-columns: 420px 1fr; gap: 40px;
  max-width: 1400px; margin: 0 auto;
}

.card-white {
  background: #f8f9fa; border-radius: 32px; padding: 50px;
  box-shadow: 0 20px 40px rgba(0,0,0,0.3);
}

.avatar-img { width: 120px; height: 120px; border-radius: 50%; border: 4px solid white; box-shadow: 0 5px 15px rgba(0,0,0,0.1); margin-bottom: 20px; }

.badge-role {
  background: #fae1b1; color: #8a6d3b; padding: 6px 16px;
  border-radius: 12px; font-size: 0.8rem; font-weight: 800; display: inline-block;
}

.text-name { font-size: 2.4rem; color: #1a1a1a; margin: 12px 0 8px; font-weight: 800; }
.text-role { color: #666; font-size: 1.1rem; font-weight: 500; }
.divider { width: 100%; height: 1px; background: #e5e5e5; margin: 30px 0; }

label { font-size: 0.75rem; font-weight: 800; color: #999; text-transform: uppercase; letter-spacing: 1.5px; display: block; margin-bottom: 12px; }
.text-bio { font-size: 1rem; color: #444; line-height: 1.7; margin-bottom: 35px; }

.sosmed-row { display: flex; flex-wrap: wrap; gap: 12px; margin-bottom: 35px; }
.sosmed-pill {
  background: white; padding: 12px 18px; border-radius: 14px;
  font-size: 0.9rem; color: #333; font-weight: 700;
  text-decoration: none; border: 1px solid #eee;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1); display: flex; align-items: center; gap: 10px;
}
.sosmed-pill:hover { background: #d4af37; color: white; transform: translateY(-5px); box-shadow: 0 8px 20px rgba(212, 175, 55, 0.3); }

.skill-grid { display: flex; flex-wrap: wrap; gap: 10px; margin-bottom: 35px; }
.skill-pill { background: #eee; padding: 10px 16px; border-radius: 12px; font-size: 0.85rem; color: #333; font-weight: 600; }

.btn-action {
  width: 100%; background: #ef4444; color: white; border: none;
  padding: 20px; border-radius: 18px; font-weight: 800; cursor: pointer; transition: 0.3s;
}
.btn-action:hover { background: #dc2626; transform: scale(1.02); box-shadow: 0 10px 25px rgba(239, 68, 68, 0.4); }

.section-title { font-size: 2rem; color: #1a1a1a; margin-bottom: 40px; font-weight: 800; }
.project-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 25px; }
.project-card-inner {
  background: white; padding: 35px; border-radius: 24px;
  border: 1px solid #eee; transition: 0.4s;
}
.project-card-inner:hover { transform: translateY(-8px); border-color: #d4af37; box-shadow: 0 15px 30px rgba(0,0,0,0.05); }

.badge-tech { color: #d4af37; font-size: 0.8rem; font-weight: 800; margin-bottom: 15px; }
.btn-explore { margin-top: 25px; font-weight: 800; color: #1a1a1a; font-size: 0.9rem; }

/* Animasi Transition */
.fade-enter-active, .fade-leave-active { transition: all 0.4s ease; }
.fade-enter-from, .fade-leave-to { opacity: 0; transform: translateY(20px); }

@media (max-width: 1200px) { .content-grid { grid-template-columns: 1fr; } .sidebar { position: static; } }
</style>