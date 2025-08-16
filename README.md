# 🎨 La Matriz — Sentiment Momentum

> *From words to motion through color.*

La Matriz is a pipeline that transforms **short text phrases** into **color momentum sequences** and **PNG visualizations**.  
It maps words → RGB values using a semantic dataset, builds a coherent path through color space, computes **momentum vectors** between steps, and renders both a **3D trajectory** and a **color strip with semantic overlays**.

This project is built for the [Internet of Agents Hackathon](https://lablab.ai/event/internet-of-agents) as an experimental **agent-ready pipeline**.

---

## ✨ Features

- **Natural Language Preprocessing** (NLTK-based, fallback safe)
- **Word → RGB Mapping** via semantic CSV lookup
- **Seed Word Expansion** with fuzzy matching for robustness
- **Coherent Color Sequence Generation** (biased random walk)
- **Momentum Calculation** (per-step direction, magnitude, normalization)
- **Dual Visualization:**
  - 3D color trajectory in RGB space
  - Strip of sequence with semantic words + momentum bars
- **PNG Export** for hackathon demos & creative use

---

## 📂 Repo Structure

```

.
├── src/
│   ├── pipeline.py          # Core classes and functions
│   └── visualization.py     # Plotting helpers
├── notebooks/
│   └── demo.ipynb           # Colab-ready walkthrough
├── results/
│   └── sample\_strip.png     # Example output
├── README.md
└── requirements.txt

````

---

## 🚀 Quickstart

### 1. Clone & install
```bash
git clone https://github.com/YOUR-USERNAME/la-matriz.git
cd la-matriz
pip install -r requirements.txt
````

### 2. Run demo notebook

Open in Colab:
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR-USERNAME/la-matriz/blob/main/notebooks/demo.ipynb)

### 3. Example usage

```python
from pipeline import NLTKPreprocessor, SemanticMapper, PhraseAnalyzer, generate_color_sequence, calculate_momentum, visualize

input_phrase = "i feel inspired but not creative"
pipeline = SemanticMapper(
    url="https://hebbkx1anhila5yf.public.blob.vercel-storage.com/semantic_rgb_mapping-7Fyy0MQQFX3s6KmXIryYY5kH3cG2qk.csv"
)
pipeline.fit([input_phrase])

# Preprocess
preproc = NLTKPreprocessor()
tokens = preproc.transform([input_phrase])[0]

# Analyze seeds
analyzer = PhraseAnalyzer(pipeline.word_to_rgb_map, pipeline.all_semantic_words)
counts, seeds = analyzer.analyze(tokens)

# Generate sequence + momentum
seq = generate_color_sequence(seeds, pipeline.word_to_rgb_map, pipeline.semantic_df, length=8)
mom = calculate_momentum(seq)

# Visualize
visualize(seq, mom, pipeline.semantic_df, pipeline.rgb_to_words_map, title="Momentum Strip", input_phrase=input_phrase)
```

---

## 🖼 Example Output

3D RGB path + sequence strip (seeds auto-labeled with semantic words):

![Example Output](results/sample_strip.png)

---

## 🤖 Hackathon Context

This pipeline is the **core engine** of La Matriz. In hackathon use, each step (analyze → sequence → render) can be exposed as a **Coral Protocol Agent**, enabling discovery and chaining with other participants’ agents.

* **Analyze Agent:** Text → tokens + seeds
* **Sequence Agent:** Seeds → RGB momentum path
* **Render Agent:** Path → PNGs + JSON

---

## 📌 Roadmap

* [ ] Wrap pipeline into `lamatriz` Python package
* [ ] Add Streamlit/HuggingFace demo front-end
* [ ] Expose as Coral Protocol Agents for discovery
* [ ] Stretch: **text-conditioned nectar attractor** for dual-thread oscillation

---

## 🧩 Requirements

* Python 3.10+
* pandas, numpy, matplotlib
* scikit-learn
* nltk
* requests

(see `requirements.txt` for full list)

---

## 📜 License

GNU General Public License v3.0

---

## 💡 Acknowledgments

* [NLTK](https://www.nltk.org/) for NLP tools
* [scikit-learn](https://scikit-learn.org/stable/) for pipeline structures
* [Matplotlib](https://matplotlib.org/) for visualization
* [Coral Protocol](https://docs.coralprotocol.org/CoralDoc/CoreConcepts/AgentDiscovery) for hackathon agent discovery
