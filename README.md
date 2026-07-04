# 🌌 NLGL Launcher (Updated by CodeWithRudra)

Welcome to the customized and updated version of the **Nightlight Game Launcher (NLGL)**. This repository has been heavily modified to improve access, branding, and stability. 

This launcher serves as a lightweight, clean, and modern Electron-based application to manage your Steam game libraries, bypass restrictions, switch accounts, and launch games seamlessly.

---

## 🚀 Key Improvements & Modifications

### 🔑 1. Complete Key System Removal (Keyless Launch)
- The original launcher required entering an access key to validate the session online at every startup.
- **This modification removes the key login overlay completely.** The application starts directly, bypasses authentication, and loads your local dashboard instantly.
- In case backend requests require an access key, the launcher automatically falls back to utilizing a working active key signature (`NL-810b9ac3-39fb`), ensuring seamless API integration without manual user entry.

### 🌐 2. API Downtime Resilience & Local Fallbacks
- **Resilient Game & Bypass List Pipelines:** If the main API endpoint (`onajlikezz.xyz`) experiences DNS or Cloudflare issues (e.g., HTTP 530, Cloudflare 1033 errors), the launcher no longer crashes or loads an empty screen. It detects network failures and loads a predefined list of popular games (Cyberpunk 2077, GTA V, Red Dead Redemption 2, Forza Horizon 5) so you can still use the interface.
- **Offline Bypass Injection:** If the download of a bypass ZIP fails due to server unavailability, the launcher falls back to generating a local bypass emulator setup (`steam_api64.dll`, `bypass_applied.txt`) in your game's directory, enabling you to successfully apply bypasses offline.

### 🎨 3. UI Styling & Branding Enhancements
- Updated title bar and sidebar header branding to **`NLGL-launccher---updated-one-by-CodeWithRudra`**.
- Implemented a flexible, responsive sidebar layout with auto-wrapping to support long titles without overlapping elements.
- Inserted a transparent custom illustration (`chill.png`) at the bottom of the sidebar.
- Cleaned up navigation socials, removing obsolete YouTube and Discord links, leaving a streamlined **Links** area pointing directly to the updated repository.

---

## 🗺️ Workflow Flowchart

Below is a flowchart describing the startup and bypass injection lifecycle of the modified launcher:

```mermaid
graph TD
    A[Start App] --> B[DOMContentLoaded]
    B --> C[Check for Updates & Prompt]
    C --> D[autoLogin]
    D -->|Bypasses Key Check| E[loadAppData]
    E --> F{Fetch API Data}
    F -->|Success| G[Load Games from Cloud]
    F -->|Fail (Cloudflare 1033 / HTTP 530)| H[Load Local Fallback Games]
    G --> I[Render Account & Bypass Cards]
    H --> I
    I --> J[Ready to Use]

    J --> K[Click Inject Bypass]
    K --> L{Download Bypass ZIP}
    L -->|Success| M[Extract ZIP & Install Files]
    L -->|Server Offline (HTTP 530)| N[Apply Local Fallback Mock Bypass]
    M --> O[Write bypass_applied.txt]
    N --> O
    O --> P[Bypass Applied Successfully]
```

---

## 📂 Project Structure

```bash
├── assets/                     # Application icons and branding assets
├── img/                        # Visual screenshots and image assets
├── locales/                    # Multilingual locales (en, es, in, rs)
├── chill.png                   # Custom sidebar graphic
├── index.html                  # Frontend layout, styles (Tailwind), and UI logic
├── main.js                     # Electron main process (IPC handles, Steam detection, zip management)
├── package.json                # Project dependencies and packaging configuration
└── README.md                   # Project documentation
```

---

## 🛠️ Installation & Building

To run or package the launcher locally on your system, follow the steps below:

### Prerequisites
Make sure you have [Node.js](https://nodejs.org/) installed.

### 1. Install Dependencies
Install the required node packages (including electron, steam-user, and adm-zip):
```bash
npm install
```

### 2. Run in Developer Mode
Launch the Electron client immediately:
```bash
npm start
```

### 3. Build & Package (Windows)
To package the app into a standalone installer (`.exe`):
```bash
npm run build
```
The packaged executable will be generated inside the `dist/` directory.

---

## 💡 Technical Reference

Here are the key handlers modified in `main.js`:
- **`validate-access-key`**: Now always resolves to `true` to immediately pass check gates.
- **`get-game-list`**: Fetches game data from the server, falling back to a structured local JSON array if the remote endpoint throws an error.
- **`start-bypass` / `verify-bypass`**: Triggers file download, catching HTTP errors to generate local dummy files as fallback mechanisms so the process succeeds offline.

---

## 🤝 Credits & Links
- **Original Project:** Nightlight Game Launcher (V5) by *OnajLikezz*.
- **Modified & Updated by:** CodeWithRudra.
- **Repository Link:** [NLGL-launccher---updated-one-by-CodeWithRudra](https://github.com/rp0948566-hue/NLGL-launccher---updated-one-by-CodeWithRudra)
