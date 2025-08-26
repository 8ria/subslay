# SubSlay 💅🏻

🧠✨ **Text to Emoji Transformation powered by Rust + WebAssembly**

---

## 🧾 Overview

**SubSlay** is a blazing-fast emoji transformer powered by a pure Rust core compiled to WebAssembly, offering semantic text-to-emoji conversion with stylish flair.

* The emoji transformation logic lives in the Rust crate `subslay`.
* The WebAssembly wrapper crate `subslay-wasm` exposes the functionality for web use.
* The static frontend is hosted via GitHub Pages on the `gh-pages` branch and consumes the WASM package from `subslay-wasm`.

🔗 [Try the Demo](https://subslay.app/)<br>
🔬 Source code is maintained in the [`main`](https://github.com/8ria/subslay/tree/main) branch.

---

## 💡 Features

* 🦀 Core emoji transformation implemented in Rust as a reusable crate
* ⚡ WebAssembly wrapper for fast browser execution
* 🧬 Uses GloVe embeddings + Levenshtein distance fallback
* 🌐 Static frontend deployed on GitHub Pages with WASM package auto-updates
* 🎨 Stylish glassmorphism UI with animated gradient text and emojis
* 🔥 Instant, debounced input-to-emoji transformation with error handling

> ✨ **Example**: `"Hello, World!"` → `"👋 🌏"`

---

## 🛠️ How It Works

* The **`subslay` crate** contains the core logic:
  * Parses `emoji.json` (keyword → emoji map)
  * Loads GloVe vectors (`glove.txt`) for semantic similarity
  * Uses Levenshtein distance as a fallback

* The **`subslay-wasm` crate** wraps the core with `wasm-bindgen`, exposing a `WasmStylist` class to JavaScript.

* The **frontend**:
  * Loads the WASM package built by `wasm-pack`
  * Uses the embedded JSON and GloVe data within the WASM module, avoiding separate static file fetches
  * Provides a sleek interface for users to input text and see emoji output live

---

## 🚀 Getting Started (Local Development)

### 1. Clone and build the Rust crates

```bash
git clone https://github.com/8ria/subslay.git
cd subslay
cargo build --release              # Build core crate
cd ../subslay-wasm
wasm-pack build --target web       # Build WASM package
```

### 2. Serve the frontend

Copy or link your `pkg/` folder generated from `subslay-wasm` to your `website/` folder.

```bash
cd ../website
python3 -m http.server 8000
```

Open `http://localhost:8000` in your browser.

---

## 🌍 Deployment Workflow

* The [`gh-pages`](https://github.com/8ria/subslay/tree/gh-pages) branch hosts the static site (frontend files + WASM pkg).
* A GitHub Actions workflow automatically:

  * Builds the WASM package from `subslay-wasm` on `main` branch pushes
  * Cleans old WASM files from `gh-pages/pkg`
  * Copies new WASM build into `gh-pages/pkg`
  * Commits and pushes changes, preserving other assets like `index.html`, `images/`, and `CNAME`

---

## 📁 Project Structure

```
main/
├── subslay/                    # Core Rust crate (logic + data)
│   ├── Cargo.toml
│   ├── src/lib.rs
│   ├── static/
│   │   ├── emoji.json
│   │   └── glove.txt
│   └── README.md
│
└── subslay-wasm/               # WASM wrapper crate exposing wasm_bindgen API
    ├── Cargo.toml
    └── src/lib.rs
```

---

## 🧑‍💻 Contributing

Pull requests are welcome! Consider contributing by:
* Adding or refining emoji mappings
* Improving embedding logic or fallback handling
* Optimizing WASM build or Rust performance
* Enhancing the frontend UI/UX

---

## 📄 License

MIT License © [AndriaK](mailto:hey@andriaK.com)

---

## 🎉 SubSlay Tools

- 🧠 `subslay` — Core Rust emoji binding crate
- 💬 `discord-bot` — Fun emoji Discord bot using SubSlay
- 🌐 `subslay.app` — Web client for live emoji translation

---

> *"Built to slay, not obey."* 💅🏻
