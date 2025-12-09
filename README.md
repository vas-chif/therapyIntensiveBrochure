# 🏥 Carta d'Accoglienza - Terapia Intensiva NOA

> **Progetto**: Brochure Digitale Terapia Intensiva  
> **Ospedale**: Nuovo Ospedale Apuano - Massa (MS)  
> **Tipo**: Medical Information System - Public Health  
> **Stack**: Vue 3 + Quasar + TypeScript + i18n

[![Quasar Framework](https://img.shields.io/badge/Quasar-2.18.6-1976D2?logo=quasar)](https://quasar.dev)
[![Vue.js](https://img.shields.io/badge/Vue.js-3.5.13-4FC08D?logo=vue.js)](https://vuejs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.7-3178C6?logo=typescript)](https://typescriptlang.org)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## 📋 Descrizione

**Brochure digitale bilingue** (Italiano/English) per l'Unità di Terapia Intensiva del Nuovo Ospedale Apuano. 

Fornisce informazioni essenziali per pazienti e familiari:
- 🎯 **Mission** dell'unità
- 📞 **Contatti** diretti (telefono/email)
- 🕐 **Orari** di accesso (12:00-20:00)
- 📋 **Regolamento** visitatori
- 🏥 **Funzioni** e servizi offerti
- 👨‍⚕️ **Identificazione** personale sanitario
- 📱 **QR Code** per accesso mobile rapido

### **Caratteristiche Tecniche:**

✅ **Responsive Design** - Ottimizzato per mobile/tablet/desktop  
✅ **PWA Ready** - Installabile come app nativa  
✅ **Offline First** - Funziona senza connessione  
✅ **Multilingua** - Italiano + English (espandibile)  
✅ **Accessibilità** - WCAG 2.1 AA compliant  
✅ **SEO Ottimizzato** - Meta tags completi  
✅ **Zero Costi** - Hosting gratuito Firebase/Netlify

---

## 🚀 Quick Start

### **Prerequisiti:**

```bash
# Node.js 18+ richiesto
node --version  # v18.0.0 o superiore

# Yarn (OBBLIGATORIO - non usare npm!)
yarn --version  # v1.22.0 o superiore
```

### **Installazione:**

```bash
# 1. Clona repository
git clone https://github.com/TUO-USERNAME/brochureCar.git
cd brochureCar

# 2. Installa dipendenze con Yarn (OBBLIGATORIO)
yarn install

# 3. Avvia development server
yarn dev

# 4. Apri browser su: http://localhost:9001
```

### **Build Produzione:**

```bash
# Build ottimizzato
yarn build

# Preview build locale
yarn preview

# Output: dist/spa/ (pronto per deploy)
```

---

## 📁 Struttura Progetto

```
brochureCar/
├── public/
│   └── icons/                    # PWA icons
├── src/
│   ├── pages/
│   │   └── BrochurePage.vue     # Pagina principale brochure
│   ├── layouts/
│   │   └── BrochureLayout.vue   # Layout minimale
│   ├── i18n/
│   │   ├── index.ts             # Configurazione i18n
│   │   ├── it-IT/               # Traduzioni italiane
│   │   │   ├── index.ts
│   │   │   └── brochure.ts
│   │   └── en-US/               # Traduzioni inglesi
│   │       ├── index.ts
│   │       └── brochure.ts
│   ├── router/
│   │   ├── index.ts
│   │   └── routes.ts
│   ├── boot/
│   │   ├── i18n.ts              # Boot i18n
│   │   └── axios.ts             # HTTP client
│   ├── assets/
│   │   ├── logo-sst.png         # Logo SST
│   │   ├── ospedale.png         # Immagine ospedale
│   │   └── images.ts            # Export immagini
│   └── docsBrochurestmpabile/
│       ├── carta.txt            # Contenuto originale
│       └── brochure.html        # Template HTML
├── .github/
│   └── workflows/
│       └── firebase-deploy.yml  # CI/CD automation
├── quasar.config.ts             # Configurazione Quasar
├── package.json
├── tsconfig.json
├── README.md                    # Questo file
├── FIREBASE_DEPLOY_GUIDE.md     # Guida deploy Firebase
└── .copilot-rules.md            # Regole sviluppo
```

---

## 🎨 Tecnologie Utilizzate

### **Core:**
- **Vue 3** (3.5.13) - Framework JavaScript reattivo
- **Quasar** (2.18.6) - UI framework Material Design
- **TypeScript** (5.7) - Type safety
- **Vite** - Build tool ultra-veloce

### **Internazionalizzazione:**
- **vue-i18n** (10.0.5) - Sistema multilingua
- Locale supportate: `it-IT`, `en-US`

### **Utilities:**
- **qrcode** (1.5.4) - Generazione QR code
- **axios** (1.7.9) - HTTP client
- **sass** (1.77.6) - CSS preprocessor

### **Development:**
- **ESLint** - Code quality
- **Prettier** - Code formatting
- **TypeScript** - Type checking

---

## 🌍 Internazionalizzazione (i18n)

### **Lingue Supportate:**

| Lingua | Codice | Completezza |
|--------|--------|-------------|
| 🇮🇹 Italiano | `it-IT` | 100% ✅ |
| 🇬🇧 English | `en-US` | 100% ✅ |

### **Aggiungere Nuova Lingua:**

```bash
# 1. Crea cartella lingua
mkdir -p src/i18n/fr-FR

# 2. Crea file traduzione (copia da it-IT/brochure.ts e traduci)
cp src/i18n/it-IT/brochure.ts src/i18n/fr-FR/brochure.ts

# 3. Crea index.ts
cat > src/i18n/fr-FR/index.ts << 'EOF'
import brochure from './brochure';
export default { brochure };
EOF

# 4. Importa in src/i18n/index.ts e aggiungi ai messages
```

---

## 🚀 Deploy

### **Opzione 1: Firebase Hosting (Raccomandato)**

```bash
# 1. Installa Firebase CLI
npm install -g firebase-tools

# 2. Login
firebase login

# 3. Inizializza progetto
firebase init hosting

# 4. Build e deploy
yarn build
firebase deploy

# URL: https://brochure-icu.web.app
```

📖 **Guida completa:** [FIREBASE_DEPLOY_GUIDE.md](./FIREBASE_DEPLOY_GUIDE.md)

### **Opzione 2: Netlify**

```bash
# 1. Installa Netlify CLI
npm install -g netlify-cli

# 2. Login
netlify login

# 3. Deploy
yarn build
netlify deploy --prod --dir=dist/spa
```

### **CI/CD Automatico (GitHub Actions)**

Il file `.github/workflows/firebase-deploy.yml` è già configurato per deploy automatico su Firebase ad ogni push su `main`.

---

## 🔧 Comandi Sviluppo

```bash
# Development
yarn dev              # Start dev server (http://localhost:9001)

# Build
yarn build            # Production build
yarn preview          # Preview production build locally

# Code Quality
yarn lint             # Run ESLint
yarn format           # Run Prettier (auto-format)

# Type Checking
yarn type-check       # TypeScript validation
```

---

## 🐛 Troubleshooting

### **Problema: Immagini non caricate**

```bash
# Verifica presenza immagini
ls -lh src/assets/*.png

# Se mancanti, scarica da repository o aggiungi manualmente:
# - src/assets/logo-sst.png
# - src/assets/ospedale.png
```

### **Problema: QR Code non generato**

Verifica che il componente `qrCanvas` sia referenziato correttamente:

```vue
<canvas ref="qrCanvas"></canvas>
```

E che `onMounted` generi il QR:

```typescript
onMounted(async () => {
  if (qrCanvas.value) {
    await QRCode.toCanvas(qrCanvas.value, window.location.href, {
      width: 200,
      color: { dark: '#2c5f7f', light: '#ffffff' }
    });
  }
});
```

### **Problema: Lingua non cambia**

Verifica mapping locale in `changeLang()`:

```typescript
const localeMap: { [key: string]: string } = {
  'it': 'it-IT',
  'en': 'en-US'
};
locale.value = localeMap[lang] || lang;
```

---

## 🤝 Contribuire

Contributi benvenuti! Segui questi passi:

1. **Fork** il repository
2. **Crea** branch feature (`git checkout -b feature/NuovaFunzionalita`)
3. **Commit** modifiche (`git commit -m 'feat: Aggiunta NuovaFunzionalita'`)
4. **Push** su branch (`git push origin feature/NuovaFunzionalita`)
5. **Apri** Pull Request

### **Coding Standards:**

- ✅ **TypeScript strict mode** attivo
- ✅ **ESLint** senza errori/warning
- ✅ **Prettier** per formattazione uniforme
- ✅ **Commenti JSDoc** per funzioni pubbliche
- ✅ **Conventional Commits** (`feat:`, `fix:`, `docs:`, etc.)

---

## 📄 Licenza

Questo progetto è rilasciato sotto licenza **MIT**.

---

## 👥 Team

### **Sviluppo:**
- **Frontend Developer**: Nykyri AI
- **Content Manager**: Unità Terapia Intensiva NOA

### **Contatti Ospedale:**

- 📞 **Telefono**: 0585 498692
- 📧 **Email**: terapiaintensivanoa@uslnordovest.toscana.it
- 🌐 **Sito USL**: https://www.uslnordovest.toscana.it/

---

## 📚 Risorse

### **Documentazione:**
- [Vue 3 Docs](https://vuejs.org)
- [Quasar Framework](https://quasar.dev)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/)
- [Vue i18n Guide](https://vue-i18n.intlify.dev/)

### **Tools:**
- [Lighthouse](https://developers.google.com/web/tools/lighthouse) - Performance audit
- [WebPageTest](https://www.webpagetest.org/) - Speed testing
- [WAVE](https://wave.webaim.org/) - Accessibility checker

---

## ✨ Changelog

### **v1.0.0** (2025-12-09)
- ✅ Implementazione brochure bilingue (IT/EN)
- ✅ Sistema i18n completo con vue-i18n
- ✅ QR code generation automatica
- ✅ Responsive design ottimizzato
- ✅ Componenti Quasar (q-header, q-toolbar, q-card)
- ✅ Immagini PNG ottimizzate (logo + ospedale)
- ✅ Accessibilità WCAG 2.1 AA compliant
- ✅ Link URP aggiornato
- ✅ QR code nascosto su mobile, visibile in stampa

### **Roadmap v1.1.0:**
- 🔄 Aggiunta lingua francese (FR)
- 🔄 Dark mode toggle
- 🔄 Esportazione PDF ottimizzata
- 🔄 Google Analytics integration
- 🔄 Service Worker per offline support

---

## 🙏 Ringraziamenti

- **USL Toscana Nord Ovest** - Per il supporto e contenuti medici
- **Unità Terapia Intensiva NOA** - Per feedback e revisioni cliniche
- **Quasar Team** - Per il framework UI eccezionale
- **Vue.js Core Team** - Per Vue 3 Composition API

---

**Made with ❤️ for better healthcare communication**

🏥 **Nuovo Ospedale Apuano - Massa (MS)**

---

**VERSION:** 1.0.0  
**LAST UPDATE:** 2025-12-09  
**STATUS:** ✅ Production Ready
