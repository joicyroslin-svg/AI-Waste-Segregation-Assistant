# ♻️ AI Waste Segregation Assistant

> A browser-based prototype that helps users correctly identify and segregate common household waste items, aligned with **UN SDG 12 – Responsible Consumption and Production**.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Problem Statement](#problem-statement)
- [Proposed Solution](#proposed-solution)
- [Target Users](#target-users)
- [Key Features](#key-features)
- [How the AI Workflow Works](#how-the-ai-workflow-works)
- [Technologies Used](#technologies-used)
- [Project Structure](#project-structure)
- [Setup and Installation](#setup-and-installation)
- [How to Run](#how-to-run)
- [Example Usage](#example-usage)
- [Responsible AI Considerations](#responsible-ai-considerations)
- [Limitations](#limitations)
- [Future Improvements](#future-improvements)
- [SDG 12 Alignment](#sdg-12-alignment)
- [Project Status](#project-status)
- [Author](#author)

---

## Project Overview

The **AI Waste Segregation Assistant** is a conversational, single-page web prototype that accepts a waste item's name or description from the user and responds with:

- A **waste category** classification (Biodegradable, Recyclable, Non-recyclable, Hazardous, or E-waste)
- A **disposal recommendation** for that category
- A **sustainability tip** to reduce waste at source
- A **confidence level** (High, Medium, or Low) that is always stated transparently

The prototype is entirely self-contained in one HTML file — no server, no backend, no external API calls. Everything runs locally in the browser.

---

## Problem Statement

Improper waste disposal — putting hazardous items in general bins, contaminating recyclables with food residue, or discarding e-waste with household rubbish — contributes to environmental harm. Many people are uncertain about which bin an item belongs to, especially for ambiguous items like food-contaminated containers, expired medicines, or old electronics. This uncertainty leads to avoidable pollution and wasted recoverable materials.

---

## Proposed Solution

A lightweight, accessible assistant that a user can open instantly in any browser and query by typing a waste item's name or description. The assistant uses a keyword-scoring knowledge base to identify the item and return a structured response. When the input is unclear, the assistant asks for clarification rather than guessing, supporting responsible decision-making.

An optional image upload is also supported: the user can attach a photo, and the assistant will use the image filename as a text hint to attempt classification. The prototype is transparent about the limitation that image content is not visually analysed.

---

## Target Users

- **College and university students** learning about sustainability and responsible consumption
- **General public** seeking quick, accessible waste disposal guidance
- **Educators** demonstrating conversational AI applications in environmental contexts

---

## Key Features

| Feature | Description |
|---|---|
| Conversational chat interface | Chat-style UI with user and AI bubbles, typing animation |
| 5-category waste classification | Biodegradable, Recyclable, Non-recyclable, Hazardous, E-waste |
| Structured response format | Item · Category · Disposal · Tip · Confidence for every result |
| Confidence levels | High / Medium / Low, always displayed with colour-coded badges |
| Uncertainty handling | Unclear inputs trigger a clarification request instead of a guess |
| Image input (filename hint) | Attach a photo; filename is used as a text hint with honest limitations stated |
| Uncertainty banners | Medium and Low confidence results show explicit warning banners |
| Responsible AI panel | Collapsible panel covering transparency, privacy, image limitations, and unsupported claims policy |
| Local disposal disclaimer | Persistent notice that local guidelines always take precedence |
| How it works pipeline | Visual 5-step flow: User Input → AI Identification → Classification → Disposal Guidance → Tip |
| Sample inputs | Eight quick-send buttons covering common waste types |
| No external dependencies | Fully self-contained; runs offline with no internet connection required |

---

## How the AI Workflow Works

```
User Input ──► AI Identification ──► Waste Classification ──► Disposal Guidance ──► Sustainability Tip
```

### Step-by-step

1. **User Input** — The user types a waste item name or description (e.g. "used battery"), or optionally attaches an image whose filename is used as a text hint.

2. **AI Identification** — The input is normalised to lowercase and scored against a curated knowledge base (`KB`) of 18 waste item entries. Each entry contains keyword arrays; the classifier assigns a relevance score based on exact matches, substring inclusion, and partial overlap.

3. **Waste Classification** — The highest-scoring entry is selected (minimum score threshold required). The confidence level is set to:
   - **High** — strong keyword match
   - **Medium** — marginal match, or image-based input (always capped at Medium)
   - **Low** — weak single-term match
   - If no entry meets the threshold, the assistant asks for clarification.

4. **Disposal Guidance** — The matched entry's disposal instructions are returned, covering where to place the item, how to prepare it, and any safety precautions.

5. **Sustainability Tip** — One short, actionable tip is provided to help the user reduce or better manage that type of waste in the future.

### Knowledge base categories and item coverage

| Category | Items covered |
|---|---|
| 🟢 Biodegradable | Fruit peels/scraps, food waste/kitchen organics, garden/green waste |
| 🔵 Recyclable | PET plastic bottles, paper/cardboard, glass bottles/jars, aluminium/metal cans |
| ⚫ Non-recyclable | Food-contaminated containers, styrofoam/polystyrene, soft plastics/film packaging, single-use hygiene products |
| 🔴 Hazardous | Used batteries, expired/unused medicines, paint/solvents, household chemicals/pesticides |
| 🟣 E-waste | Mobile phones/smartphones, computers/laptops/peripherals, chargers/cables/earphones, large household appliances |

---

## Technologies Used

| Technology | Role |
|---|---|
| HTML5 | Page structure and semantic markup |
| CSS3 | Styling, layout (Flexbox), responsive design, animations |
| Vanilla JavaScript (ES6+) | Classification logic, DOM manipulation, event handling, FileReader API |
| Browser FileReader API | Reading selected image files for preview (no upload or server transmission) |

**No frameworks, libraries, build tools, package managers, or external services are used.**  
The entire application is a single file: `index.html`.

---

## Project Structure

```
AI-Waste-Segregation-Assistant/
├── index.html      # Complete application — HTML, CSS, and JavaScript in one file
├── README.md       # Project documentation (this file)
└── .gitignore      # Git ignore rules for OS/editor artefacts
```

There are no subdirectories, asset folders, configuration files, or dependency manifests because the project has none.

> **Note on `requirements.txt`:** This project has no Python code and no Python dependencies. A `requirements.txt` is not applicable and has not been created.

---

## Setup and Installation

No installation is required.

The application has no dependencies to install, no build step to run, and no server to start.

**Prerequisites:** Any modern web browser (Chrome, Firefox, Edge, Safari).

---

## How to Run

### Option 1 — Open directly in a browser

1. Download or clone this repository.
2. Open `index.html` in any modern web browser.

```bash
# Clone the repository
git clone https://github.com/<your-username>/ai-waste-segregation-assistant.git

# Navigate into the folder
cd ai-waste-segregation-assistant

# Open the file (Windows)
start index.html

# Open the file (macOS)
open index.html

# Open the file (Linux)
xdg-open index.html
```

### Option 2 — Use a local static server (optional)

If you prefer to serve it via localhost (e.g. for development):

```bash
# Using Python (if installed)
python -m http.server 8000
# Then open: http://localhost:8000
```

No configuration, environment variables, or credentials are needed.

---

## Example Usage

Type any of the following into the chat input, or click the quick-send sample buttons:

| Input | Expected response |
|---|---|
| `Used plastic water bottle` | Recyclable — rinse, crush, place in dry recycling bin |
| `Banana peel` | Biodegradable — compost or wet waste bin |
| `Used battery` | Hazardous — battery drop-off point, never general bin |
| `Food container with leftover food` | Non-recyclable (Medium confidence) — scrape food first, then check container material |
| `Old smartphone` | E-waste — authorised collection centre, wipe data first |
| `Expired medicine` | Hazardous — pharmacy take-back programme, never flush |
| `Broken glass` | Non-recyclable — wrap securely, general waste only |
| `Newspaper` | Recyclable — flatten, dry recycling bin |

**Unclear input example:** Typing `"thing"` or `"stuff"` will trigger a clarification request asking for the material, use, and contamination status — the assistant will not guess.

**Image input example:** Click "📷 Attach image", select a photo named `old-battery.jpg`. The filename `old battery` is extracted as a text hint and classified as Hazardous with a maximum of Medium confidence. An image limitation notice is displayed with every image-based result.

---

## Responsible AI Considerations

The following responsible AI behaviours are implemented directly in the application:

### Transparency
- Every response includes a **confidence level** (High / Medium / Low) displayed as a colour-coded badge.
- The basis for each classification (keyword matching against a local knowledge base) is described in the UI.

### Uncertainty handling
- When no knowledge base entry reaches the minimum relevance threshold, the assistant **asks for clarification** with specific follow-up questions rather than returning a guess.
- Medium and Low confidence results display a visible **uncertainty warning banner** explaining the limitation.
- Image-based inputs are **always capped at Medium confidence**, regardless of how well the filename matches.

### Honest image input disclosure
- The application cannot analyse image content visually. This limitation is stated:
  - in the upload area before submission
  - in the Responsible AI panel
  - in an image result notice attached to every image-based response

### Privacy
- **No data is transmitted.** All processing runs entirely in the user's browser.
- Images are loaded using the browser's FileReader API for local preview only — they are never uploaded, stored, or retained.
- No analytics, tracking scripts, cookies, or external requests are present.

### Avoiding unsupported claims
- Sustainability tips use qualitative, widely-accepted language.
- No specific statistics, accuracy figures, research citations, or benchmark results are stated unless they are directly verifiable from the code itself.

### Avoiding overconfident classification
- Ambiguous item types (e.g. food containers, which may be recyclable once cleaned) are stored in the knowledge base with **Medium** confidence pre-assigned.
- Marginal keyword matches are automatically downgraded from High to Medium or Low.

---

## Limitations

| Limitation | Description |
|---|---|
| Fixed knowledge base | The classifier can only recognise the 18 item types explicitly defined in the `KB` array. Items outside this set will trigger a clarification request. |
| Text-only classification | No visual AI or image recognition is used. Image input relies solely on the filename as a text hint. |
| No real-time data | Disposal guidance reflects general best practice and does not retrieve live local facility information. |
| Language | The application supports English input only. |
| Local rules vary | Waste segregation rules differ by municipality. The application provides general guidance, not jurisdiction-specific instructions. |
| Prototype scope | This is a student prototype intended for demonstration and learning, not production deployment. |

---

## Future Improvements

The following are possible directions for extending this prototype. None of these are currently implemented.

- **Expand the knowledge base** — add more item types and subcategories
- **Multi-language support** — detect and respond in the user's preferred language
- **Real image classification** — integrate a client-side machine learning model (e.g. TensorFlow.js with a custom-trained waste classifier) to analyse image content rather than relying on filenames
- **Geolocation-aware guidance** — retrieve local disposal facility information based on the user's location
- **Feedback loop** — allow users to flag incorrect classifications to improve future accuracy
- **Accessibility improvements** — keyboard navigation, screen-reader labels, high-contrast mode

---

## SDG 12 Alignment

This project directly supports **UN Sustainable Development Goal 12 — Responsible Consumption and Production**, specifically:

- **Target 12.5** — By 2030, substantially reduce waste generation through prevention, reduction, recycling, and reuse. This tool supports informed recycling and waste diversion decisions.
- **Target 12.8** — By 2030, ensure that people everywhere have the relevant information and awareness for sustainable development and lifestyles in harmony with nature. This tool makes waste segregation knowledge accessible and actionable for everyday users.

The assistant reinforces the waste management hierarchy by guiding users toward composting, recycling, and responsible disposal rather than defaulting to landfill.

---

## Project Status

**Student prototype — demonstration / educational use only.**

The prototype is complete and functional for its intended demonstration scope. It runs entirely in the browser with no setup required.

---

## Author

Developed as a student project for an AI for Sustainability course.  
Aligned with UN SDG 12 – Responsible Consumption and Production.

---

*This prototype is for educational purposes. Always follow your local municipality's official waste disposal guidelines.*
