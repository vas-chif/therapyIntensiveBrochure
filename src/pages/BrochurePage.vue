<script setup lang="ts">
import { ref, computed } from 'vue';
import { useI18n } from 'vue-i18n';
import logoSst from '../assets/logo-sst.png';
import ospedaleImg from '../assets/ospedale.png';
import qrCodeStatic from '../assets/qr-code.png';

const { t, locale } = useI18n();
const qrCodeUrl = ref(qrCodeStatic);
const showQrDialog = ref(false);

const currentLang = computed(() => {
  const lang = locale.value.startsWith('it') ? 'it' : 'en';
  return lang === 'it' ? '🇮🇹 IT' : '🇬🇧 EN';
});

// Immagini PNG
const logoBase64 = ref(logoSst);
const ospedaleBase64 = ref(ospedaleImg);

// Identificazione personale
const staffIdentification = computed(() => [
  { color: '#87CEEB', label: t('staff.nurse') },
  { color: '#0000FF', label: t('staff.coordinator') },
  { color: '#800020', label: t('staff.oss') },
  { color: '#CCCCCC', label: t('staff.doctor') },
]);

// Metodi
const changeLang = (lang: string) => {
  const localeMap: { [key: string]: string } = {
    it: 'it-IT',
    en: 'en-US',
  };
  locale.value = localeMap[lang] || lang;
};

const callPhone = () => {
  window.location.href = 'tel:0585498692';
};

const sendEmail = () => {
  window.location.href = 'mailto:terapiaintensivanoa@uslnordovest.toscana.it';
};

const openUrp = () => {
  window.open('https://www.uslnordovest.toscana.it/', '_blank');
};

// Genera QR Code rimosso in favore di immagine statica
</script>
<template>
  <q-page class="brochure-page">
    <!-- Header con Toolbar Quasar -->
    <q-header class="bg-primary header text-white q-pa-sm">
      <q-toolbar>
        <q-avatar square style="width: 50px; height: 30px">
          <img :src="logoBase64" alt="Logo SST" />
        </q-avatar>

        <q-toolbar-title class="text-center">
          <div class="header-title-text">
            <div class="text-h6 text-weight-bold" style="font-size: 16px">{{ $t('title') }}</div>
          </div>
        </q-toolbar-title>

        <q-btn flat round dense icon="qr_code" class="q-mr-sm" @click="showQrDialog = true" />

        <q-btn-dropdown flat dense :label="currentLang" dropdown-icon="language">
          <q-list>
            <q-item clickable v-close-popup @click="changeLang('it')">
              <q-item-section>
                <q-item-label>🇮🇹 Italiano</q-item-label>
              </q-item-section>
            </q-item>
            <q-item clickable v-close-popup @click="changeLang('en')">
              <q-item-section>
                <q-item-label>🇬🇧 English</q-item-label>
              </q-item-section>
            </q-item>
          </q-list>
        </q-btn-dropdown>
      </q-toolbar>
    </q-header>

    <!-- Immagine Ospedale -->
    <div class="hospital-image-section">
      <q-toolbar class="text-white">
        <q-toolbar-title>
          <div class="text-subtitle2">{{ $t('subtitle') }}</div>
          <div class="text-caption">{{ $t('location') }}</div>
        </q-toolbar-title>
      </q-toolbar>
      <q-img :src="ospedaleBase64" alt="Ospedale" class="hospital-image" />
    </div>

    <!-- Contenuto -->

    <!-- Mission -->
    <q-card class="section-card mission-card">
      <q-card-section>
        <div class="section-title">
          <q-icon name="favorite" color="primary" size="md" />
          <h3>{{ $t('mission.title') }}</h3>
        </div>
        <p class="mission-text">{{ $t('mission.text') }}</p>
      </q-card-section>
    </q-card>

    <!-- Contatti -->
    <q-card class="section-card">
      <q-card-section>
        <div class="section-title">
          <q-icon name="phone" color="primary" size="md" />
          <h3>{{ $t('contacts.title') }}</h3>
        </div>
        <q-list dense>
          <q-item>
            <q-item-section avatar>
              <q-icon name="person" color="blue-7" />
            </q-item-section>
            <q-item-section>
              <q-item-label>{{ $t('contacts.director') }}</q-item-label>
              <q-item-label caption>Dott. S. Antonelli</q-item-label>
            </q-item-section>
          </q-item>
          <q-item>
            <q-item-section avatar>
              <q-icon name="supervised_user_circle" color="blue-7" />
            </q-item-section>
            <q-item-section>
              <q-item-label>{{ $t('contacts.coordinator') }}</q-item-label>
              <q-item-label caption>M. Bienamè</q-item-label>
            </q-item-section>
          </q-item>
          <q-item clickable @click="callPhone">
            <q-item-section avatar>
              <q-icon name="call" color="green" />
            </q-item-section>
            <q-item-section>
              <q-item-label>TEL: 0585498692</q-item-label>
            </q-item-section>
          </q-item>
          <q-item clickable @click="sendEmail">
            <q-item-section avatar>
              <q-icon name="email" color="orange" />
            </q-item-section>
            <q-item-section>
              <q-item-label caption class="text-wrap">
                terapiaintensivanoa@uslnordovest.toscana.it
              </q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>

    <!-- Accesso Visitatori -->
    <q-card class="section-card access-card">
      <q-card-section>
        <div class="section-title">
          <q-icon name="schedule" color="primary" size="md" />
          <h3>{{ $t('access.title') }}</h3>
        </div>
        <div class="access-hours">
          <q-icon name="access_time" size="2em" color="primary" />
          <span class="hours-text">12:00 - 20:00</span>
        </div>
        <q-list dense class="access-rules">
          <q-item v-for="(rule, index) in $tm('access.rules')" :key="index">
            <q-item-section avatar>
              <q-icon name="check_circle" color="positive" size="sm" />
            </q-item-section>
            <q-item-section>
              <q-item-label>{{ rule }}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>

    <!-- Regole d'accesso -->
    <q-card class="section-card">
      <q-card-section>
        <div class="section-title">
          <q-icon name="rule" color="primary" size="md" />
          <h3>{{ $t('rules.title') }}</h3>
        </div>
        <q-list dense>
          <q-item v-for="(rule, index) in $tm('rules.items')" :key="index">
            <q-item-section avatar>
              <q-icon name="info" color="blue-7" size="sm" />
            </q-item-section>
            <q-item-section>
              <q-item-label>{{ rule }}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>

    <!-- Funzioni della Struttura -->
    <q-card class="section-card">
      <q-card-section>
        <div class="section-title">
          <q-icon name="local_hospital" color="primary" size="md" />
          <h3>{{ $t('functions.title') }}</h3>
        </div>
        <p v-for="(text, index) in $tm('functions.items')" :key="index" class="info-text">
          {{ text }}
        </p>
      </q-card-section>
    </q-card>

    <!-- Informazioni Cliniche -->
    <q-card class="section-card">
      <q-card-section>
        <div class="section-title">
          <q-icon name="medical_information" color="primary" size="md" />
          <h3>{{ $t('clinical.title') }}</h3>
        </div>
        <p class="info-text">{{ $t('clinical.text') }}</p>
      </q-card-section>
    </q-card>

    <!-- Dimissione -->
    <q-card class="section-card">
      <q-card-section>
        <div class="section-title">
          <q-icon name="description" color="primary" size="md" />
          <h3>{{ $t('discharge.title') }}</h3>
        </div>
        <q-list dense>
          <q-item v-for="(item, index) in $tm('discharge.items')" :key="index">
            <q-item-section avatar>
              <q-icon name="assignment" color="blue-7" size="sm" />
            </q-item-section>
            <q-item-section>
              <q-item-label>{{ item }}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>

    <!-- Identificazione Personale -->
    <q-card class="section-card staff-card">
      <q-card-section>
        <div class="section-title">
          <q-icon name="badge" color="primary" size="md" />
          <h3>{{ $t('staff.title') }}</h3>
        </div>
        <q-list dense>
          <q-item v-for="(staff, index) in staffIdentification" :key="index">
            <q-item-section avatar>
              <div class="color-badge" :style="{ backgroundColor: staff.color }"></div>
            </q-item-section>
            <q-item-section>
              <q-item-label>{{ staff.label }}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>

    <!-- URP -->
    <q-card class="section-card urp-card">
      <q-card-section>
        <div class="section-title">
          <q-icon name="feedback" color="primary" size="md" />
          <h3>{{ $t('urp.title') }}</h3>
        </div>
        <p class="info-text">{{ $t('urp.text') }}</p>
        <q-btn
          outline
          color="primary"
          :label="$t('urp.link')"
          icon="open_in_new"
          @click="openUrp"
          class="q-mt-sm"
        />
      </q-card-section>
    </q-card>

    <!-- QR Code -->
    <q-card class="section-card qr-card">
      <q-card-section class="text-center">
        <h4>{{ $t('qr.title') }}</h4>
        <div class="qr-container">
          <img :src="qrCodeUrl" alt="QR Code" style="width: 200px" />
        </div>
        <p class="qr-caption">{{ $t('qr.caption') }}</p>
      </q-card-section>
    </q-card>

    <!-- Dialog QR Code -->
    <q-dialog v-model="showQrDialog">
      <q-card class="q-pa-md text-center" style="min-width: 300px">
        <q-card-section>
          <div class="text-h6">{{ $t('qr.title') }}</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <img :src="qrCodeUrl" alt="QR Code" style="width: 100%; max-width: 300px" />
          <div class="text-caption q-mt-sm">{{ $t('qr.caption') }}</div>
        </q-card-section>

        <q-card-actions align="center">
          <q-btn flat label="Chiudi" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>

    <!-- Footer -->
    <footer class="footer">
      <div class="footer-content">
        <div class="footer-title">
          {{ $t('footer.text') }}
        </div>
        <div style="font-size: 10px">
          Created by
          <a
            class="created-by caption text-secondary"
            href="https://uniqueyouagency.com/#/"
            target="_blank"
            rel="noopener noreferrer"
            style="text-decoration: none"
          >
            <span class="text-weight-bolder text-purple-10">
              Unique<span class="text-red-8">You</span>Agency</span
            >
          </a>
        </div>
      </div>
    </footer>
  </q-page>
</template>

<style scoped lang="scss">
.brochure-page {
  max-width: 100%;
  background: linear-gradient(135deg, #e8f4f8 0%, #f9f9f9 100%);
}

// .header-title-text {
//   text-align: center;
//   line-height: 1.3;
//   font-size: 20px;
// }

.hospital-image-section {
  width: 100%;
  padding: 20px;
  text-align: center;
  background: linear-gradient(135deg, #2c5f7f 0%, #1a4460 100%);
}

.hospital-image {
  width: 100%;
  max-width: 300px !important;
  height: auto;
  border-radius: 12px;
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.4);
  margin: 20px 10px 0 10px;
}

.section-card {
  margin: 15px;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.section-title {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 15px;
  padding-bottom: 8px;
  border-bottom: 2px solid #2c5f7f;

  h3 {
    margin: 0;
    font-size: 1.2rem;
    color: #2c5f7f;
    font-weight: bold;
  }
}

.mission-card {
  background: linear-gradient(135deg, #e8f4f8 0%, #d4e9f2 100%);
}

.mission-text {
  font-style: italic;
  font-size: 1.05rem;
  line-height: 1.6;
  color: #1a4460;
  text-align: center;
  padding: 10px;
}

.access-card {
  background: #f0f8ff;
}

.access-hours {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 15px;
  padding: 20px;
  background: white;
  border-radius: 10px;
  margin: 15px 0;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);

  .hours-text {
    font-size: 1.8rem;
    font-weight: bold;
    color: #2c5f7f;
  }
}

.access-rules {
  background: white;
  border-radius: 8px;
  padding: 10px;
}

.info-text {
  line-height: 1.6;
  margin-bottom: 12px;
  text-align: justify;
}

.staff-card {
  background: #fff8dc;
}

.color-badge {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  border: 2px solid #ccc;
}

.urp-card {
  background: #ffe4e1;
}

.qr-card {
  background: white;
  display: none; /* Nascondi su schermo */
}

/* Mostra QR solo in stampa */
@media print {
  .qr-card {
    display: block;
  }
}

.qr-container {
  display: flex;
  justify-content: center;
  margin: 20px 0;

  canvas {
    border: 3px solid #2c5f7f;
    border-radius: 10px;
    padding: 10px;
  }
}

.qr-caption {
  font-size: 0.9rem;
  color: #666;
  margin-top: 10px;
}

.footer {
  background: #2c5f7f;
  color: white;
  text-align: center;
  padding: 10px;
  margin-top: 30px;
  border-radius: 8px 8px 0 0;
  width: 100%;
}

.header {
  padding: 10px;
  border-radius: 0 0 8px 8px;
}

.footer-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
}

.footer-title {
  font-size: 0.9rem;
  margin: 0;
}

@media (max-width: 600px) {
  .header-text h1 {
    font-size: 1.2rem;
  }

  .header-text h2 {
    font-size: 1rem;
  }

  .section-card {
    margin: 10px;
  }
}
</style>
