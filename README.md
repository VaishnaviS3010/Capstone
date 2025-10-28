# From Data Overload to Clear Insights — Tackling Cybersecurity Vulnerabilities with AI

**Live demo:** https://capstonedashboard.streamlit.app

**Authors:** Vaishnavi Sadul, Dhaval Jariwala, Yihua Cai, Yuze Li  
**Presented as:** Poster and project demo (refer to project poster and IEEE template for conference formatting)

---

## 1. Project Overview
Cybersecurity vulnerability data (NVD: KEV & CVE) is large, noisy, and hard to translate into actionable decisions. This project applies domain-specific NLP and interactive visualization to convert unstructured vulnerability descriptions into clear, prioritized insights via:

- Custom Named Entity Recognition (NER) tailored for cybersecurity text.  
- An interactive Streamlit dashboard for exploratory data analysis and visual maps.  
- A knowledge graph that reveals relationships and risk pathways between vulnerabilities, suppliers, and products.

---

## 2. Demo
Open the interactive dashboard to explore the results:  
**https://capstonedashboard.streamlit.app**

---

## 3. Key Features
- **NER & Smart Tagging:** Extract vulnerability names, short descriptions, risk types, affected suppliers and products.  
- **EDA Dashboard:** Heatmaps, temporal trends, supplier-risk co-occurrence, and bar charts showing risky products per supplier.  
- **Knowledge Graph:** Interactive visualization of linked entities to identify clusters and cascading risk.  
- **Model Evaluation:** Track precision, recall, and F1-score to compare pre-trained vs fine-tuned models.

---

## 4. Datasets
- **Known Exploited Vulnerabilities (KEV)** — used as annotated training data for domain-specific NER.  
- **Common Vulnerabilities and Exposures (CVE)** — used for exploratory data analysis and testing.

> Both datasets were sourced from the National Vulnerability Database (NVD).

---

## 5. Methodology (high level)
1. **Data collection & preprocessing:** ingest KEV & CVE, normalize fields, remove duplicates, tokenization and basic cleaning.  
2. **Annotation:** design schema and annotate domain-specific labels (e.g., `vulnerability_name`, `short_description`, `risk_type`, `supplier`, `product`).  
3. **NER model development:** build and fine-tune a SpaCy pipeline; compare off-the-shelf vs fine-tuned models and iterate on annotations.  
4. **Visualization & dashboard:** pipe results into a Streamlit app supporting dynamic filtering, heatmaps, time-series, and a knowledge-graph view.  
5. **Evaluation:** compute precision, recall, and F1; iterate until performance and utility meet the project goals.

---

## 6. Repo structure (suggested)
```
/
├─ data/
│  ├─ raw/               # raw KEV & CVE downloads (keep original files here)
│  ├─ processed/         # cleaned CSV/JSONL used for training/EDA
├─ notebooks/
│  ├─ eda.ipynb          # exploratory analysis and visual experiments
├─ src/
│  ├─ data_prep.py       # ingestion + cleaning + conversion scripts
│  ├─ annotate/          # annotation guidelines & helper scripts
│  ├─ train_ner.py       # script to train SpaCy NER
│  ├─ evaluate.py        # evaluation scripts (precision / recall / f1)
│  ├─ build_knowledge_graph.py
│  ├─ app/
│     ├─ streamlit_app.py
│     ├─ dashboard_utils.py
├─ models/               # saved model checkpoints and artifacts
├─ graphs/               # output knowledge graphs, graphml files
├─ requirements.txt
├─ README.md
└─ LICENSE
```

---

## 7. Quickstart — Run the dashboard locally
> Tested on Python 3.10+. Adjust if using a different Python version.

1. Clone:
```bash
git clone <repo-url>
cd <repo-name>
```

2. Create & activate venv:
- macOS / Linux:
```bash
python3 -m venv venv
source venv/bin/activate
```
- Windows (PowerShell):
```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Run Streamlit app:
```bash
streamlit run src/app/streamlit_app.py
```

---

## 8. Training & Evaluation (example commands)
> Adapt paths and hyperparameters to your setup.

- Train NER:
```bash
python src/train_ner.py --train data/processed/kev_train.jsonl --output models/ner_custom
```

- Evaluate:
```bash
python src/evaluate.py --model models/ner_custom --test data/processed/cve_test.jsonl
# prints precision, recall, f1 (and optionally confusion matrix / per-class metrics)
```

- Build knowledge graph:
```bash
python src/build_knowledge_graph.py --ner-output models/ner_custom --out graphs/kg.graphml
```

---

## 9. Dependencies (example)
`requirements.txt` should include (pin versions as needed):
```
pandas
numpy
spacy
scikit-learn
streamlit
networkx
pyvis
plotly
matplotlib
tqdm
```

---

## 10. Results & Impact
- The **custom SpaCy model** demonstrated improved entity recognition on KEV/CVE text compared to generic models (higher precision / recall / F1).  
- The Streamlit dashboard and knowledge graph reduce manual triage time by enabling interactive exploration — making vulnerability analysis accessible to non-technical stakeholders.  
- Visual maps and co-occurrence analyses reveal supplier-product risk clusters useful for prioritization and mitigation.

---

## 11. Key Data-Analyst Skills Demonstrated
- Data Cleaning & Preparation  
- Exploratory Data Analysis (EDA) & Visualization (Streamlit)  
- Model Evaluation & Statistical Metrics (precision / recall / F1)  
- Dashboard Development & Insight Communication  
- Relationship Mapping & Knowledge Graphs

---

## 12. Acknowledgments
Thanks to Wisr AI (Rob Goehring) and Prof. Dr. Qurat Ul-Ain-Azim for their support and feedback.

---

## 13. Contact
**Lead author:** Vaishnavi Sadul — sadul.v@northeastern.edu

If you use or build on this project, please cite the poster and the demo.

---

## 14. License
This project is released under the **MIT License** — modify or choose another license as needed.
