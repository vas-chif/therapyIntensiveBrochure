# 🧠 MEMORIA PROGETTO & CHAT HISTORY

> **Progetto**: Brochure Digitale Terapia Intensiva NOA (Nuovo Ospedale Apuano)
> **Repository**: `https://github.com/vas-chif/therapyIntensiveBrochure.git`
> **Branch**: `main`
> **Versione**: 1.0.0
> **Ultimo Aggiornamento**: 19 Dicembre 2025

---

## 📜 STORIA DEL PROGETTO (Cosa abbiamo fatto finora)

### 1. 🚀 Inizializzazione & Setup
- Partiti da una richiesta di convertire documenti testuali (`carta.txt`, `brochure.html`) in una Web App moderna.
- **Stack Tecnologico**: Vue 3, Quasar Framework v2.18, TypeScript, Vite.
- **Package Manager**: Yarn (Mandatorio).

### 2. 💻 Sviluppo Core (`BrochurePage.vue`)
- Creata pagina principale responsive.
- **Componenti Quasar**: `q-header`, `q-toolbar`, `q-card`, `q-btn-dropdown` (lingua).
- **Assets**: Sostituite immagini Base64 con file PNG ottimizzati (`logo-sst.png`, `ospedale.png`) in `src/assets/`.
- **QR Code**: Implementata generazione dinamica con libreria `qrcode`.
  - *Feature*: Nascosto su schermo, visibile solo in stampa (`@media print`).

### 3. 🌍 Internazionalizzazione (i18n)
- Implementato sistema bilingue completo (**Italiano** / **Inglese**).
- Struttura: `src/i18n/it-IT` e `src/i18n/en-US`.
- Selettore lingua dinamico con flag (🇮🇹/🇬🇧).

### 4. 🔧 Fix & Refactoring
- **Bug Fixes**:
  - Risolti errori ESLint (async/await su QRCode).
  - Corretto mapping locale (`it` -> `it-IT`).
  - Aggiornato link URP (https://www.uslnordovest.toscana.it/).
- **UI Improvements**:
  - Modificato Footer: Da `q-footer` (fixed) a `<footer>` standard (scrollable) per migliorare UX su mobile.

### 5. 📚 Documentazione Professionale
- Creato **`README.md`**: Documentazione completa, badge, quick start, struttura progetto.
- Creato **`.copilot-rules.md`**: Standard di sviluppo (Medical/WCAG 2.1 AA, Security, TypeScript).
- Creato **`DEPLOY_GUIDE.md`**: Guida passo-passo per deploy su Firebase e GitHub.

### 6. ☁️ Deployment & CI/CD
- **Firebase**: Configurato `firebase.json` (Hosting, Cache headers, SPA rewrites).
- **GitHub Actions**: Creato workflow `.github/workflows/firebase-deploy.yml` per deploy automatico.
- **Git**:
  - Inizializzato repository.
  - Commit iniziale massivo (v1.0.0).
  - Push su remote `origin` (`vas-chif/therapyIntensiveBrochure`).

---

## 📍 DOVE SIAMO RIMASTI (Stato Attuale)

**✅ COMPLETATO:**
- Il codice è stabile, builda correttamente (`yarn build`).
- Il repository è sincronizzato su GitHub.
- La documentazione è completa.

**⏳ IN SOSPESO / PROSSIMI PASSI:**
1. **Configurazione Secrets GitHub**:
   - Bisogna aggiungere `FIREBASE_SERVICE_ACCOUNT` e `FIREBASE_PROJECT_ID` su GitHub per attivare la CI/CD.
2. **Setup Firebase Console**:
   - Creare progetto su Firebase Console se non ancora fatto.
3. **Roadmap Futura (v1.1.0)**:
   - Aggiunta lingua Francese.
   - Dark Mode.
   - Analytics.

---

## 🤖 ISTRUZIONI PER L'AI (Come procedere)

Quando riprendi il lavoro su questo progetto:
1. **Leggi sempre questo file** per avere il contesto immediato.
2. **Riferimenti**:
   - Regole di sviluppo: `.copilot-rules.md`
   - Guida Deploy: `DEPLOY_GUIDE.md`
3. **Stile Coding**:
   - Usa **Yarn**.
   - **TypeScript** Strict Mode.
   - **Composition API** (`<script setup>`).
   - **WCAG 2.1 AA** (Accessibilità è prioritaria).
4. **Obiettivo**: Mantenere il progetto "Zero Cost" e pronto per la produzione ospedaliera.

---
*File generato automaticamente da GitHub Copilot - Non modificare manualmente se non per aggiornare lo stato.*
