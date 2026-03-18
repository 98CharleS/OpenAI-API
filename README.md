# Article HTML Generator with OpenAI

![Python](https://img.shields.io/badge/python-3.10%2B-blue.svg)
![OpenAI](https://img.shields.io/badge/API-OpenAI-412991.svg)
![Model](https://img.shields.io/badge/model-gpt--3.5--turbo-green.svg)
![License](https://img.shields.io/badge/license-MIT-lightgrey.svg)

A Python tool that reads a plain-text article, sends it to the OpenAI API, and generates a structured HTML file with suggested image placeholders. Each placeholder includes a ready-to-use image generation prompt in the `alt` attribute and a `<figcaption>` description below it.

---

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [How It Works](#-how-it-works)
- [Project Structure](#-project-structure)
- [Requirements](#-requirements)
- [Installation](#-installation)
- [Usage](#-usage)
- [Output](#-output)
- [Notes](#-notes)
- [License](#-license)

---

## 📌 Project Overview

The script takes a plain-text article (fetched from a URL or read locally) and uses the OpenAI Chat API (`gpt-3.5-turbo`) to convert it into an HTML body with:

- structured headings and paragraphs,
- `<img>` placeholders inserted at contextually appropriate locations,
- `alt` attributes containing detailed prompts ready for image generation tools,
- `<figcaption>` descriptions below each image.

The output is a raw HTML snippet (no `<html>` / `<head>` tags) meant to be pasted into `szablon.html` for preview.

---

## 💡 How It Works

```
artykul.txt / URL
       │
       ▼
  source_text_validation()
  (tries URL first, falls back to local file)
       │
       ▼
  generating_article()
  (sends text + prompt to OpenAI Chat API)
       │
       ▼
  saving_article()
  (writes HTML body to artykul.html)
```

1. **Text retrieval** — `source_text_validation()` first tries to fetch the article from a hardcoded URL. If that fails (timeout or network error), it falls back to reading `artykul.txt` from the local directory.
2. **HTML generation** — `generating_article()` sends the article text along with a Polish-language prompt to `gpt-3.5-turbo`. The prompt instructs the model to return only the `<body>` content with `<img>` placeholders and `<figcaption>` tags.
3. **Saving** — the generated HTML snippet is saved as `artykul.html`.
4. **Preview** — open `podglad.html` in a browser to see the rendered result (it already includes the full HTML shell with CSS styling). To use your own content, paste the generated snippet into `szablon.html`.

---

## 📁 Project Structure

```
OpenAI-API/
│
├── main.py           # Main script: fetches text, calls OpenAI API, saves output
├── artykul.txt       # Sample input article (local fallback)
├── artykul.html      # Generated output — raw HTML body snippet
├── podglad.html      # Preview file: full HTML page with the generated content applied
├── szablon.html      # Empty HTML template to paste artykul.html content into
└── README.md
```

---

## 🔧 Requirements

- Python 3.10+
- An active [OpenAI API key](https://platform.openai.com/api-keys)

Dependencies:

```
openai
requests
easygui
```

---

## 🚀 Installation

1. Clone the repository:

```bash
git clone https://github.com/98CharleS/OpenAI-API.git
cd OpenAI-API
```

2. (Optional) Create and activate a virtual environment:

```bash
python -m venv venv
source venv/bin/activate      # Linux/macOS
venv\Scripts\activate         # Windows
```

3. Install dependencies:

```bash
pip install openai requests easygui
```

---

## 💻 Usage

1. Place your input article as `artykul.txt` in the project folder (or rely on the default URL in the script).
2. Run the script:

```bash
python main.py
```

3. A dialog box will appear asking for your OpenAI API key — paste it and confirm.
4. The script generates `artykul.html` in the same directory.
5. Open `podglad.html` in a browser to preview the result, or paste the content of `artykul.html` into `szablon.html` for a clean template-based preview.

---

## 📄 Output

The generated `artykul.html` contains only the `<body>` content — headings, paragraphs, and image placeholders. Example structure:

```html
<h1>Sztuczna inteligencja: wpływ i wyzwania</h1>
<p>Sztuczna inteligencja to dziedzina nauki...</p>

<img src="image_placeholder.jpg" alt="AI algorithms analysing large datasets" />
<figcaption>Illustration of artificial intelligence analysing data.</figcaption>

<h2>Wyzwania etyczne i społeczne</h2>
<p>Kluczowym wyzwaniem jest zapewnienie etycznego...</p>
```

The `alt` attribute of each `<img>` contains a detailed prompt suitable for image generation tools such as DALL·E, Midjourney, or Stable Diffusion.

---

## 📝 Notes

- The script uses `gpt-3.5-turbo` by default. To switch to `gpt-4o` or another model, update the `model` parameter in `generating_article()`.
- Text encoding: the script applies an `iso-8859-1` → `utf-8` re-encoding step to handle Polish characters fetched from the remote URL. Local files are assumed to be UTF-8.
- `max_tokens` is set to `1000` — for longer articles, increase this value or switch to a model with a larger context window.

---

## 📜 License

This project is available under the [MIT License](LICENSE).
