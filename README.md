# Article to HTML Converter — OpenAI API

A Python tool that transforms plain text articles into structured, 
styled HTML pages using the OpenAI API. For each section, the model 
automatically suggests contextually relevant image placements and 
generates ready-to-use image prompts (e.g. for DALL·E or Midjourney).

## What it does

- Reads a plain `.txt` article as input
- Sends content to OpenAI GPT model with a structured prompt
- Returns a formatted HTML file with:
  - Semantic structure (headings, paragraphs, sections)
  - Image placeholder tags with AI-generated descriptive prompts
  - A preview template (`podglad.html`) for quick visual check

## Demo

Input (`artykul.txt`):
```
Artificial intelligence is transforming healthcare...
```

Output (`artykul.html`):
```html
<section>
  <h2>AI in Healthcare</h2>
  <p>Artificial intelligence is transforming healthcare...</p>
  <img src="image_placeholder.jpg" alt="A futuristic hospital 
  with AI diagnostic screens and robotic assistants">
</section>
```

## How to run

1. Clone the repository
2. Install dependencies:
```bash
   pip install openai requests easygui
```
3. Place your article as `artykul.txt` in the project folder
4. Run the script:
```bash
   python main.py
```
5. Enter your OpenAI API key when prompted
6. Output: `artykul.html` generated in the same folder

## Tech stack

- Python 3.x
- OpenAI API (GPT)
- easygui — API key input dialog
- HTML / CSS — output template

## Project context

Built as a practical demonstration of LLM integration — 
using prompt engineering to control structured output format 
and automate content enrichment workflows.
