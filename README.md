[README.md](https://github.com/user-attachments/files/27564349/README.md)
# RunningWO — Workout Builder for GPS Watches

<div align="center">

![RunningWO](https://img.shields.io/github/v/release/DaryanLab/garminwo-app?label=RunningWO&color=00a88c&style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Windows-0078D6?style=for-the-badge&logo=windows)
![Tauri](https://img.shields.io/badge/Tauri-v2-24C8DB?style=for-the-badge&logo=tauri)
![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)
![Language](https://img.shields.io/badge/Languages-FR%20%7C%20EN%20%7C%20ES-orange?style=for-the-badge)

**Créez, éditez et envoyez vos séances de course directement sur votre montre GPS.**  
*Build, edit and send your running workouts directly to your GPS watch.*

[🇫🇷 Français](#français) · [🇬🇧 English](#english)

</div>

---

## 🇫🇷 Français

### Présentation

RunningWO est une application desktop (Windows) construite avec **Tauri v2 + Rust + HTML/JS**. Elle permet aux coureurs de concevoir des séances structurées (intervalles, blocs répétés, échauffement, retour au calme) et de les envoyer directement sur leur montre GPS via Garmin Connect ou de les exporter en JSON/FIT.

### ✨ Fonctionnalités

**Création de séances**
- Étapes : Échauffement, Intervalle, Récupération, Retour au calme
- Blocs répétés avec N répétitions
- Glisser-déposer pour réorganiser les étapes et les blocs
- Duplication et coller d'étapes entre blocs

**Cibles d'entraînement**
- 🏃 **Allure** (min/km) avec tolérance configurable — Seuil & Récup indépendants
- ❤️ **Zone FC** (1–5) calculée depuis votre FC max — Intervalle & Récup indépendants
- ❤️ **FC min/max** (bpm) — Intervalle & Récup indépendants
- 🦵 **Cadence** (spm)
- Conversion globale de toutes les étapes en un clic ("Séance en")

**Widgets de réglage rapide**
- Widgets repliables (▾) avec mémoire d'état
- Sauvegarde persistante des réglages (Reset / Sauver)

**IA intégrée**
- Analyse de texte collé (description de séance en langage naturel → étapes structurées)
- Compatible **Claude (Anthropic)** et **Gemini (Google)**
- Clés API configurables dans les Options

**Export & Envoi**
- 📥 Générer JSON Garmin
- ⌚ Envoyer sur la montre (via `rwo-send`)
- 🔴 Envoyer vers **Garmin Connect** (multi-comptes, jusqu'à 5 comptes)
- 🖨️ Imprimer l'aperçu de la séance

**Mes séances**
- Sauvegarde locale des séances en cours
- Chargement, renommage, suppression
- Incluses dans le fichier de sauvegarde `.rwo`

**Templates**
- Bibliothèque de séances types (fractionné, seuil, endurance, VO2max…)

**Sauvegarde / Restauration**
- Export `.rwo` (format texte JSON)
- Données sensibles **chiffrées AES-GCM 256 bits** (clés API, mots de passe Garmin)
- Import avec restauration complète, y compris les clés API et les comptes Garmin

**Paramètres**
- 🌍 3 langues : Français, English, Español
- 🌙 Thème clair / sombre
- Multi-comptes Garmin Connect (jusqu'à 5 par utilisateur)

### 🛠️ Stack technique

| Couche | Technologie |
|--------|-------------|
| Desktop shell | Tauri v2 (Rust) |
| Frontend | HTML / CSS / JavaScript vanilla |
| Envoi montre | Binaire Rust `rwo-send` |
| Upload GC | Node.js `garmin-connect` bundled |
| Chiffrement | Web Crypto API — AES-GCM 256 + PBKDF2 |
| IA | Claude Sonnet (Anthropic) · Gemini Flash (Google) |

### 📦 Installation

> Téléchargez l'installateur `.exe` depuis la page **Releases** GitHub.

1. Lancez `RunningWO_x.x.x_x64-setup.exe`
2. L'application s'installe et se lance
3. Configurez votre clé API Claude ou Gemini dans **⚙️ Options**
4. C'est prêt !

### 🔑 Clés API

| IA | Obtenir une clé |
|----|----------------|
| Claude (Anthropic) | [console.anthropic.com/settings/keys](https://console.anthropic.com/settings/keys) |
| Gemini (Google) | [aistudio.google.com/app/apikey](https://aistudio.google.com/app/apikey) |

> Les clés API sont stockées localement et ne sont jamais partagées.  
> Le fichier de sauvegarde `.rwo` les chiffre en AES-GCM avant export.

### 📁 Structure du projet

```
RunningWO/
├── app/
│   └── index.html          # Interface principale (tout-en-un)
├── src-tauri/
│   ├── src/lib.rs           # Bridge Rust ↔ JS
│   ├── tauri.conf.json      # Config Tauri
│   ├── Cargo.toml           # Dépendances Rust
│   └── capabilities/
│       └── default.json     # Permissions Tauri
├── garmin-upload-bundled.js # Envoi vers Garmin Connect
├── rwo-send/                # Binaire Rust d'envoi montre
└── version.bat / version.ps1  # Script de bump de version
```

### 📝 Développement

```bash
# Installer les dépendances
npm install

# Lancer en mode développement
npm run tauri dev

# Builder l'installateur
npm run tauri build
```

> **Règle importante :** Ne jamais modifier `index.html` programmatiquement depuis Tauri.  
> Toutes les modifications HTML doivent être faites manuellement dans VS Code.

### 🗺️ Roadmap

- [ ] Support Polar / Suunto / Coros / Wahoo
- [ ] Lecture de séances depuis image (OCR local via Tesseract.js)
- [ ] IA locale via Ollama (sans connexion internet)
- [ ] Synchronisation cloud optionnelle
- [ ] Application mobile companion

### ☕ Soutenir le projet

Si RunningWO t'est utile, un petit café est toujours apprécié !

[![Ko-fi](https://img.shields.io/badge/Ko--fi-Support-FF5E5B?style=for-the-badge&logo=ko-fi)](https://ko-fi.com/YDARLAVOIX)

---

## 🇬🇧 English

### Overview

RunningWO is a Windows desktop application built with **Tauri v2 + Rust + HTML/JS**. It allows runners to design structured workouts (intervals, repeat blocks, warm-up, cool-down) and send them directly to their GPS watch via Garmin Connect or export them as JSON/FIT.

### ✨ Features

**Workout Creation**
- Steps: Warm-up, Interval, Recovery, Cool-down
- Repeat blocks with N repetitions
- Drag & drop to reorder steps and blocks
- Copy/paste steps between blocks

**Training Targets**
- 🏃 **Pace** (min/km) with configurable tolerance — Threshold & Recovery independent
- ❤️ **HR Zone** (1–5) calculated from your max HR — Interval & Recovery independent
- ❤️ **HR min/max** (bpm) — Interval & Recovery independent
- 🦵 **Cadence** (spm)
- One-click global conversion of all steps ("Session as")

**Quick Setting Widgets**
- Collapsible widgets (▾) with persistent state
- Persistent settings storage (Reset / Save)

**Built-in AI**
- Paste text analysis (natural language workout description → structured steps)
- Compatible with **Claude (Anthropic)** and **Gemini (Google)**
- API keys configurable in Options

**Export & Send**
- 📥 Generate Garmin JSON
- ⌚ Send to watch (via `rwo-send`)
- 🔴 Send to **Garmin Connect** (multi-account, up to 5 accounts)
- 🖨️ Print workout preview

**My Workouts**
- Local workout library
- Load, rename, delete
- Included in `.rwo` backup file

**Templates**
- Library of preset workouts (intervals, threshold, endurance, VO2max…)

**Backup / Restore**
- `.rwo` export (JSON text format)
- Sensitive data **AES-GCM 256-bit encrypted** (API keys, Garmin passwords)
- Full import with restoration of API keys and Garmin accounts

**Settings**
- 🌍 3 languages: Français, English, Español
- 🌙 Light / dark theme
- Multi-account Garmin Connect (up to 5 per user)

### 🛠️ Tech Stack

| Layer | Technology |
|-------|------------|
| Desktop shell | Tauri v2 (Rust) |
| Frontend | Vanilla HTML / CSS / JavaScript |
| Watch upload | Rust binary `rwo-send` |
| GC upload | Node.js `garmin-connect` bundled |
| Encryption | Web Crypto API — AES-GCM 256 + PBKDF2 |
| AI | Claude Sonnet (Anthropic) · Gemini Flash (Google) |

### 📦 Installation

> Download the `.exe` installer from the **Releases** page on GitHub.

1. Run `RunningWO_x.x.x_x64-setup.exe`
2. The application installs and launches
3. Configure your Claude or Gemini API key in **⚙️ Options**
4. You're ready!

### 🔑 API Keys

| AI | Get a key |
|----|-----------|
| Claude (Anthropic) | [console.anthropic.com/settings/keys](https://console.anthropic.com/settings/keys) |
| Gemini (Google) | [aistudio.google.com/app/apikey](https://aistudio.google.com/app/apikey) |

> API keys are stored locally and never shared.  
> The `.rwo` backup file encrypts them with AES-GCM before export.

### 🗺️ Roadmap

- [ ] Support for Polar / Suunto / Coros / Wahoo
- [ ] Workout image reading (local OCR via Tesseract.js)
- [ ] Local AI via Ollama (no internet required)
- [ ] Optional cloud sync
- [ ] Mobile companion app

### ☕ Support the project

If RunningWO is useful to you, a small coffee is always appreciated!

[![Ko-fi](https://img.shields.io/badge/Ko--fi-Support-FF5E5B?style=for-the-badge&logo=ko-fi)](https://ko-fi.com/YDARLAVOIX)

---

<div align="center">

**RunningWO** · Application non officielle · Non affiliée à Garmin Ltd.  
Développée par **Yannick DARLAVOIX** · © 2026  
Powered by [Tauri](https://tauri.app) · [Claude](https://anthropic.com) · [Gemini](https://aistudio.google.com)

</div>
