# 🚀 GUIDA DEPLOY SU GITHUB E FIREBASE

## ✅ STATO ATTUALE PROGETTO

**Completato:**
- ✅ Brochure bilingue (IT/EN) implementata
- ✅ Sistema i18n completo con vue-i18n
- ✅ QR code generation funzionante
- ✅ Responsive design ottimizzato
- ✅ Componenti Quasar (q-header, q-toolbar, q-card)
- ✅ Immagini PNG ottimizzate (logo-sst.png, ospedale.png)
- ✅ Professional README.md creato
- ✅ .copilot-rules.md con standard sviluppo
- ✅ firebase.json configurato
- ✅ GitHub Actions workflow (.github/workflows/firebase-deploy.yml)
- ✅ .gitignore aggiornato con Firebase entries
- ✅ Git commit iniziale completato

**Commit Hash:** `c421ad5`  
**Branch:** `master`

---

## 📋 PROSSIMI PASSI

### **STEP 1: Creare Repository GitHub**

1. Vai su https://github.com/new
2. Compila:
   - **Repository name:** `brochureCar` (o altro nome a scelta)
   - **Description:** "Carta d'Accoglienza Terapia Intensiva NOA - Bilingual Medical Brochure"
   - **Visibility:** Public (o Private se preferisci)
   - **⚠️ NON selezionare:** "Add a README file" (già presente)
   - **⚠️ NON selezionare:** "Add .gitignore" (già presente)
   - **License:** MIT (opzionale, già menzionato in README)
3. Click **"Create repository"**

---

### **STEP 2: Collegare Repository Locale a GitHub**

Dopo aver creato il repository, GitHub ti mostrerà le istruzioni. Usa questi comandi:

```bash
# Aggiungi il remote GitHub (sostituisci TUO-USERNAME con il tuo username)
git remote add origin https://github.com/TUO-USERNAME/brochureCar.git

# Rinomina branch master → main (opzionale, ma raccomandato)
git branch -M main

# Push iniziale
git push -u origin main
```

**Esempio concreto:**
```bash
# Se il tuo username GitHub è "mario-rossi"
git remote add origin https://github.com/mario-rossi/brochureCar.git
git branch -M main
git push -u origin main
```

---

### **STEP 3: Creare Progetto Firebase**

1. Vai su https://console.firebase.google.com/
2. Click **"Add project"** (Aggiungi progetto)
3. Compila:
   - **Project name:** `brochure-icu` (o altro nome)
   - **Google Analytics:** Disabilita (non necessario per hosting statico)
4. Click **"Create project"**
5. Attendi completamento setup (~30 secondi)

---

### **STEP 4: Configurare Firebase Hosting**

Nel tuo progetto Firebase appena creato:

1. Menu laterale → **Hosting**
2. Click **"Get started"**
3. Installazione Firebase CLI (se non già fatto):
   ```bash
   npm install -g firebase-tools
   ```
4. Login Firebase:
   ```bash
   firebase login
   ```
5. Inizializza progetto:
   ```bash
   # Nella cartella /home/nyk-ai/projects/brochureCar
   firebase init hosting
   ```
   
   Rispondi alle domande:
   - **Select a default Firebase project:** Seleziona `brochure-icu` (o il nome scelto)
   - **What do you want to use as your public directory?** `dist/spa`
   - **Configure as a single-page app (rewrite all urls to /index.html)?** `Yes`
   - **Set up automatic builds and deploys with GitHub?** `No` (useremo GitHub Actions)
   - **File dist/spa/index.html already exists. Overwrite?** `No`

6. Deploy manuale (primo test):
   ```bash
   yarn build
   firebase deploy
   ```

7. Firebase ti darà l'URL di produzione:
   ```
   ✔ Deploy complete!
   
   Project Console: https://console.firebase.google.com/project/brochure-icu/overview
   Hosting URL: https://brochure-icu.web.app
   ```

---

### **STEP 5: Configurare GitHub Secrets per CI/CD**

Per abilitare deploy automatico con GitHub Actions:

1. **Ottieni Service Account Firebase:**
   ```bash
   firebase login:ci
   ```
   Copia il token generato (inizia con `1//...`)

2. **Vai su GitHub Repository → Settings → Secrets and variables → Actions**

3. **Aggiungi 3 secrets:**
   
   **Secret 1: FIREBASE_SERVICE_ACCOUNT**
   ```bash
   # Genera service account JSON
   firebase init hosting:github
   ```
   Segui le istruzioni, copia il contenuto JSON generato.
   
   Su GitHub:
   - Click **"New repository secret"**
   - Name: `FIREBASE_SERVICE_ACCOUNT`
   - Value: Incolla il JSON completo
   - Click **"Add secret"**

   **Secret 2: FIREBASE_PROJECT_ID**
   - Name: `FIREBASE_PROJECT_ID`
   - Value: `brochure-icu` (o il tuo project ID Firebase)
   - Click **"Add secret"**

   **Secret 3: GITHUB_TOKEN**
   - ℹ️ Questo è già fornito automaticamente da GitHub, **NON serve aggiungerlo manualmente**

---

### **STEP 6: Test Deploy Automatico**

1. Fai una modifica qualsiasi (es. aggiungi commento in `BrochurePage.vue`)
2. Commit e push:
   ```bash
   git add .
   git commit -m "test: Test CI/CD deployment"
   git push origin main
   ```

3. Vai su **GitHub Repository → Actions**
4. Vedrai il workflow "Deploy to Firebase Hosting" in esecuzione
5. Attendi completamento (~2-3 minuti)
6. Verifica deploy su `https://brochure-icu.web.app`

---

## 🎯 CHECKLIST PRE-DEPLOY

Prima di rendere pubblico il sito:

- [ ] ✅ Verifica contatti ospedale aggiornati
- [ ] ✅ Testa brochure su mobile/tablet/desktop
- [ ] ✅ Testa cambio lingua (IT ↔ EN)
- [ ] ✅ Testa QR code generation
- [ ] ✅ Verifica immagini caricate correttamente
- [ ] ✅ Testa link URP (https://www.uslnordovest.toscana.it/)
- [ ] ✅ Verifica accessibilità (WCAG 2.1 AA)
- [ ] ✅ Run Lighthouse audit (Performance ≥90, Accessibility ≥95)
- [ ] ✅ Testa stampa (QR code visibile)
- [ ] ✅ Nessun console.log() in produzione
- [ ] ✅ Nessun errore ESLint

---

## 🛠️ COMANDI UTILI

```bash
# Development
yarn dev                 # Start dev server (http://localhost:9001)

# Build & Deploy
yarn build              # Build produzione
yarn preview            # Preview build locale
firebase deploy         # Deploy su Firebase

# Code Quality
yarn lint               # ESLint check
yarn type-check         # TypeScript validation

# Git
git status              # Vedi modifiche
git add .               # Aggiungi tutti i file
git commit -m "msg"     # Commit con messaggio
git push origin main    # Push su GitHub

# Firebase
firebase login          # Login Firebase CLI
firebase projects:list  # Lista progetti Firebase
firebase hosting:channel:deploy preview  # Deploy su canale preview
```

---

## 🐛 TROUBLESHOOTING

### **Problema: Git push rifiutato**

```bash
# Se vedi "error: failed to push some refs"
git pull origin main --rebase
git push origin main
```

### **Problema: Firebase deploy fallito**

```bash
# Verifica login
firebase logout
firebase login

# Verifica progetto
firebase projects:list
firebase use brochure-icu

# Rebuild e retry
yarn build
firebase deploy
```

### **Problema: GitHub Actions fallito**

1. Vai su **GitHub → Actions → Failed workflow**
2. Click sul job fallito
3. Espandi step con errore
4. Leggi log errore
5. Verifica secrets configurati correttamente

**Errori comuni:**
- `FIREBASE_SERVICE_ACCOUNT` non configurato → Aggiungi secret
- `FIREBASE_PROJECT_ID` errato → Verifica ID progetto Firebase
- Build error → Testa locale con `yarn build`

### **Problema: Immagini non visibili su Firebase**

```bash
# Verifica presenza file
ls -lh src/assets/*.png

# Rebuild completo
rm -rf dist/
yarn build
firebase deploy
```

---

## 📊 MONITORAGGIO POST-DEPLOY

### **Firebase Console:**
- **Hosting**: https://console.firebase.google.com/project/brochure-icu/hosting
  - Deployment history
  - Usage stats (bandwidth, storage)
  - Custom domain setup (opzionale)

### **GitHub Actions:**
- **Workflows**: https://github.com/TUO-USERNAME/brochureCar/actions
  - Deployment logs
  - Build times
  - Success/failure rate

### **Analytics (Opzionale):**

Se vuoi tracciare visite:
```bash
yarn add firebase
```

Aggiungi a `quasar.config.ts`:
```typescript
// Firebase Analytics integration
```

---

## 🎓 RISORSE UTILI

### **Documentazione:**
- [Firebase Hosting Docs](https://firebase.google.com/docs/hosting)
- [GitHub Actions Docs](https://docs.github.com/en/actions)
- [Quasar Build Docs](https://quasar.dev/quasar-cli-vite/developing-spa/build-commands)

### **Tools:**
- [Firebase Console](https://console.firebase.google.com/)
- [GitHub](https://github.com/)
- [Lighthouse](https://developers.google.com/web/tools/lighthouse) - Performance audit

### **Support:**
- Firebase Support: https://firebase.google.com/support
- GitHub Support: https://support.github.com/
- Quasar Forum: https://forum.quasar.dev/

---

## 📝 TEMPLATE COMMIT MESSAGES

Per commit futuri:

```bash
# Feature
git commit -m "feat: Add French translation"

# Bug fix
git commit -m "fix: Correct contact email typo"

# Documentation
git commit -m "docs: Update README with deploy stats"

# Style
git commit -m "style: Improve header spacing"

# Refactor
git commit -m "refactor: Extract ContactCard component"

# Performance
git commit -m "perf: Optimize images to WebP format"

# Content update
git commit -m "content: Update opening hours"
```

---

## 🎉 PROSSIMI MIGLIORAMENTI (Roadmap v1.1.0)

Dopo deploy iniziale, considera:

- [ ] Aggiungere lingua francese (FR)
- [ ] Implementare dark mode
- [ ] Esportazione PDF ottimizzata
- [ ] Google Analytics integration
- [ ] Service Worker per offline support
- [ ] WebP images per migliori performance
- [ ] Custom domain (es. terapiaintensiva.noa.it)
- [ ] SEO audit completo
- [ ] Performance optimization (Lighthouse 100)

---

**Made with ❤️ for better healthcare communication**

🏥 **Nuovo Ospedale Apuano - Massa (MS)**

---

**DOCUMENT VERSION:** 1.0.0  
**LAST UPDATE:** 2025-12-09  
**NEXT REVIEW:** Dopo primo deploy Firebase
