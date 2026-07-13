# Building Computational Resources for Purépecha: Parallel Corpus, Morphological Annotation, and Quantitative Characterization of Inter-Source Variation

A computational resource for **Purépecha** (language isolate, ~128,344 speakers, Michoacán, Mexico) featuring **8,511 sentence pairs** compiled from five sources with quantified orthographic and morphological variation, plus a reproducible linguistic annotation pipeline.

**Status**: v1.0.0-rc1 (pre-release candidate)  
**License**: [CC-BY-SA-4.0](LICENSE)  
**Languages**: Purépecha–Spanish (parallel)  
**Annotation Layer**: 1,800 pairs (23.3% of corpus): 800 fully annotated (Chamoreau; segmentation + gloss + strategic analysis) and 1,000 partially annotated (Bible train set; segmentation + gloss only)

---

## 📖 Citation

If you use this resource, please cite the companion paper:

```bibtex
@article{gonzalez2025purepecha,
  author    = {González-Servín, Cecilia and Kolesnikova, Olga and Maldonado Sifuentes, Christian},
  title     = {Building Computational Resources for {P}urépecha: Parallel Corpus, 
              Morphological Annotation, and Quantitative Characterization of 
              Inter-Source Variation},
  journal   = {Language Resources and Evaluation},
  year      = {2026},
  note      = {Submitted to Language Resources and Evaluation, Special Focus on Less-Resourced Languages},
  url       = {https://github.com/CeciGonSer/purepecha-spanish-corpus},
  doi       = {[Zenodo DOI pending publication]}
}
```

For individual subcorpora, additionally cite the original sources (see Section 6.3 of the paper and [`docs/SOURCES.md`](docs/SOURCES.md)).

---

## Quick Start

### Load the full corpus
```python
from datasets import load_dataset

# From HuggingFace Hub (when released)
corpus = load_dataset("CeciGonSer/purepecha-spanish-corpus")

# Or locally from pickle
import pickle
with open('data/purepecha_corpus.pkl', 'rb') as f:
    corpus = pickle.load(f)

# Access individual subcorpora
bible = corpus['bible']
constitution = corpus['constitution']
chamoreau = corpus['chamoreau']
narratives = corpus['narratives']
```

### Explore annotated examples
```python
# Chamoreau corpus includes full annotation
annotated = corpus['chamoreau']['train']
example = annotated[0]

print(f"Spanish:      {example['es']}")
print(f"Purépecha:    {example['pu']}")
print(f"Segmentation: {example['segmentacion']}")
print(f"Gloss:        {example['glosa']}")
print(f"Analysis:     {example['analisis_estrategico']}")
```

For detailed loading and processing code, see [`scripts/load_dataset.py`](scripts/load_dataset.py).

---

## 📊 Corpus Overview

| Subcorpus | Source | Pairs | Pur. Tokens | Sp. Tokens | Annotation | Dialect Clue | Release |
|-----------|--------|-------|-------------|------------|------------|--------------|---------|
| **Bible** | Diósïri Karakata P'urheepecha Jimbo (2011) | 5,159 | 75,273 | 95,821 | Partial (seg. + gloss, 1,000 train pairs) | Western Highland (pua) | ✅ CC-BY-SA |
| **Constitution** | INALI 2017 (collegiate group of translators) | 1,549 | 55,722 | 66,837 | None | Mixed/transitional | ✅ CC-BY-SA |
| **Chamoreau** | Hablemos purépecha (2009, pedagogical) | 841 | 2,762 | 3,351 | ✅ Full | Lake Pátzcuaro-affiliated | ✅ CC-BY-SA |
| **Narratives** | Mondragón et al. (1995, traditional tales) | 162 | 6,033 | 7,481 | None | Multi-regional (4 regions) | ✅ CC-BY-SA |
| **Multilingual** | Soriano García (2018, Archive Colmex) | 800 | 2,833 | 3,526 | None | Jarácuaro (Lake Pátzcuaro) | ❌ Restricted |
| **TOTAL** | — | 8,511 | 142,623 | 177,016 | 800 pairs | — | 7,711 released |

**Key findings** (from paper Section 3):
- **Three orthographic convention groups** identifiable by /w/, /j/, and /ŋ/ treatment (Section 3.3)
- **Six morphological indicators** with differentiated distribution across sources (Section 3.4)
- **Reflexive korhe** (Bible-dominant) contradicts ISO 639-3 classification as "Western Highland"
- **Lexical overlap near zero** (Jaccard <0.030), reflecting orthographic + linguistic + domain variation

---

## 📝 Data Format & Structure

### Directory structure
```
data/
├── bible/
│   ├── purepecha_bible.pkl
│   ├── purepecha_bible.json
│   ├── purepecha_bible_annotated.pkl    # 1,000 train pairs (segmentation + gloss)
│   └── purepecha_bible_annotated.json
├── constitution/
│   ├── purepecha_constitution.pkl
│   └── purepecha_constitution.json
├── chamoreau/
│   ├── purepecha_chamoreau.pkl
│   ├── purepecha_chamoreau.json
│   ├── purepecha_chamoreau_annotated.pkl    # 800 pairs (full annotation)
│   └── purepecha_chamoreau_annotated.json
└── narratives/
    ├── purepecha_narratives.pkl
    └── purepecha_narratives.json
```

### JSON record example (from Chamoreau, with annotation)
```json
{
  "es": "en la casa no hay gente",
  "pu": "juchinio noompe kuhiripu jarhasti",
  "segmentacion": "juchi-ni-o noompe kuhiripu ja-rha-s-ti",
  "glosa": "posesivo1-objetivo-residencial nada persona estar-formativo-aoristo-asertivo3",
  "analisis_estrategico": "Para alinear con la referencia, el locativo se construye sobre el posesivo de primera persona a través del sufijo residencial -o, y el verbo existencial 'estar' se conjuga en aoristo asertivo de tercera persona, produciendo la lectura presencial 'no hay (gente)'."
}
```

### JSON record example (Bible, without annotation)
```json
{
  "es": "Y les dijo: ...",
  "pu": "Apuri k'a intsïki..."
}
```

---

## 🏷️ Linguistic Annotation Layer

**Coverage**: 800 deduplicated pairs (Chamoreau + Multilingual overlap removed)  
**Models used**: Gemini 2.5 Pro (segmentation/gloss) + Gemini 3 Flash with RAG (strategic analysis)  
**Process**: Reference-assisted annotation over Chamoreau grammar (2009)  

### Annotation scheme

Each annotated pair includes three levels:

1. **Morphological Segmentation**
   - Root and affixes separated by hyphens
   - Preserves allomorphic variants for linguistic fidelity
   - Example: `juchi-ni-o` (house-POSS.1-RESID)
  - Field name in JSON: `segmentacion`

2. **Interlinear Gloss** (Spanish labels, convertible to Leipzig Rules)
   - One-to-one correspondence with segmentation
   - Spanish labels reflect pedagogical intent for Mexican Spanish-speaking users
   - Abbreviation mapping to Leipzig Rules provided in appendix

3. **Strategic Analysis** (Translation Guide)
   - 1–2 sentence synthesis of key transformation from gloss to Spanish
   - Explains register, word order, implicit arguments, idiomatic gaps
   - Useful for chain-of-thought model training or pedagogical purposes

### Important limitation
**Lexical leakage**: Strategic analysis was generated with access to the reference Spanish translation. For training predictive models (inference without Spanish), regenerate this layer via blind process.

For full specification, see [`docs/annotation_scheme.md`](docs/annotation_scheme.md).

---

## 🔬 Machine Translation Experiments

See Section 5 of the paper for full results. Key findings (with MarianMT + mBART):

| Training Set | BLEU (Pu→Es) | Notes |
|--------------|--------------|-------|
| Bible alone | 9.37 | Large but lexically repetitive (religious register) |
| Constitution alone | 15.8 | Formulaic legal text; models memorize recurrent phrases |
| **Chamoreau alone** | **19.71** | Pedagogical; short sentences; typical structures |
| **Multilingual alone** | **21.50** | Best single source; linguistically motivated |
| **Chamoreau + Multilingual** | **28.60** | Positive transfer; related register + morphology |
| Bible + Constitution + Chamoreau + Multilingual | 10.02 | Dilution by extreme heterogeneity |
| Narratives alone | ~2 | Too few examples + long, lexically diverse sentences |

**Interpretation**: Pedagogical + linguistic sources transfer well to each other but degrade average performance when mixed with religious or narrative texts. Per-domain performance is preserved but model cannot generalize across domains.

---

## 📚 Orthographic & Morphological Variation

The paper (Sections 3.3–3.4) quantifies systematic variation across sources:

### Orthographic variation (Section 3.3)
- **/w/ phoneme**: Hispanic sources use uV; standard sources use w
- **/j/ (yod)**: Hispanic sources use iV; standard sources use y
- **Velar nasal /ŋ/**: Preserved in Bible/Narratives; absent in Chamoreau/Multilingual
- **Retroflex rh**: Chamoreau preserves (19.75/1000 chars); others lower frequency
- **Lateral l**: Constitution uses 4.42/1000 chars (highest); reflects dialectal variation

→ **Grouping**: 
  - **Group 1 (Hispanic)**: Bible, Narratives
  - **Group 2 (Linguistic Standard)**: Chamoreau, Multilingual
  - **Group 3 (Mixed)**: Constitution (documents 2015 INALI orthographic transition)

### Morphological variation (Section 3.4)
- **Reflexive korhe vs. kurhi**: Bible favors korhe (86.3%); others kurhi — contradicts ISO 639-3
- **Postposition variants**: Comitative (jinkuni/jinkoni/xinkuni); Instrumental (jimbo/jimpo)
- **Verbal morphology**: Aspectual markers, person agreement differ per source

**Interpretation**: Variation reflects domain (legal vs. pedagogical vs. narrative), register (formal vs. didactic), orthographic convention (pre/post-2015 INALI), and genuine regional dialect differences — which this work does not attempt to separate.

For detailed analysis, see [`docs/source_variation.md`](docs/source_variation.md).

---

## 📦 Release & Platforms

The resource is available on three platforms for accessibility and permanence:

- **GitHub** [`github.com/CeciGonSer/purepecha-spanish-corpus`](https://github.com/CeciGonSer/purepecha-spanish-corpus)  
  Main repository; code, documentation, supplementary notebooks, data

- **HuggingFace Hub** [`huggingface.co/datasets/CeciGonSer/purepecha-spanish-corpus`](https://huggingface.co/datasets/CeciGonSer/purepecha-spanish-corpus)  
  Direct loading: `load_dataset("CeciGonSer/purepecha-spanish-corpus")`

- **Zenodo** [`zenodo.org/record/...`](https://zenodo.org)  
  Permanent archival with DOI for citation; updated with each version

---

## 📋 License & Ethics

**License**: CC-BY-SA-4.0  
- **You can**: Share, adapt, use commercially
- **You must**: Attribute, indicate changes, license derivatives under CC-BY-SA-4.0

**Ethical commitments** (Section 6.4):
1. Do not commercialize without community consultation (Intercultural Indigenous University of Michoacán, UIIM)
2. Do not use for applications that stereotype, ridicule, or exoticize
3. Recognize cultural property; indigenous languages are living heritage, not "data"

**Responsibility note**: Research team does not include Purépecha native speakers at publication. We explicitly invite speakers, linguists, and community representatives to contribute to future versions.

For original source licenses and attributions, see [`docs/SOURCES_LICENSES.md`](docs/SOURCES_LICENSES.md).

---

## 🔧 Technical Details

**Python version**: 3.8+  
**Dependencies**: 
- `datasets` (HuggingFace)
- `pandas`, `numpy` (data processing)
- `sacrebleu` (BLEU scoring, experiments only)

**File formats**: pickle (native), JSON (universal), DatasetDict (HuggingFace)  
**Total size**: ~15 MB (all subcorpora + annotation)  
**Scripts**: See [`scripts/`](scripts/) for loading, processing, format conversion

---

## 📖 Documentation

- [`docs/annotation_scheme.md`](docs/annotation_scheme.md) — Full annotation specification with examples
- [`docs/source_variation.md`](docs/source_variation.md) — Detailed orthographic and morphological variation analysis
- [`docs/SOURCES_LICENSES.md`](docs/SOURCES_LICENSES.md) — Original source attribution and licenses per subcorpus
- [`data/ANNOTATION_STATUS.md`](data/ANNOTATION_STATUS.md) — Annotation coverage by subcorpus
- **Supplementary Jupyter notebook** — Reproducible code for all analyses, statistics, and experiments (`.ipynb` in repository root)

---

## 🤝 Contributing

This is v1.0.0-rc1. We welcome:

- **Bug reports** or **annotation corrections**: Open an Issue
- **Suggestions** for additional sources or improvements: Discussions
- **Pull requests** for documentation enhancements
- **Community collaboration**: Contact us for joint work

---

## 📬 Contact

**Curators**: Cecilia González-Servín, Olga Kolesnikova, Christian Maldonado Sifuentes  
**Institution**: CIC-IPN (Centro de Investigación en Computación, Instituto Politécnico Nacional), Mexico City

**Email**: [cgonzalezs2023@cic.ipn.mx](mailto:cgonzalezs2023@cic.ipn.mx)  
**GitHub Issues**: [`github.com/CeciGonSer/purepecha-spanish-corpus/issues`](https://github.com/CeciGonSer/purepecha-spanish-corpus/issues)

---

## 🔗 Related Work

- **Companion papers** (this work is part of a series):
  - González-Servín et al. (2025): Transformer on synthetic verb conjugations
  - González-Servín et al. (2026a): Domain adaptation with mBART-50
  - González-Servín et al. (2026b): Synthetic data augmentation with LLMs

- **Related resources**:
  - AmericasNLP shared tasks (Mager et al., 2021, 2023)
  - Py-Elotl package (Gutierrez-Vasques et al., 2025) — covers other Mexican indigenous languages
  - Comparative corpus (Mager & Meza, 2021) — five Mexican languages

---

**Last updated**: July 2026  
**Repository**: https://github.com/CeciGonSer/purepecha-spanish-corpus  
**Version**: 1.0.0-rc1
