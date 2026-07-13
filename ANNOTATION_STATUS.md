# Annotation Status & Coverage

Comprehensive breakdown of morphological annotation completeness across the Purépecha-Spanish corpus.

---

## Summary by Subcorpus

| Subcorpus | Total Pairs | Annotation Level | Coverage % | Status | Train/Test |
|-----------|------------|------------------|-----------|--------|------------|
| **Bible** | 5,159 | Partial (seg. + gloss) | 19.4% (1,000/5,159 train) | ✅ Partial | 1,000 train / — |
| **Constitution** | 1,549 | None | 0% | ⏸ Pending | — |
| **Chamoreau** | 841 | ✅ **Full** | 100% | ✅ Complete | 480 / 160 |
| **Narratives** | 162 | None | 0% | ⏸ Pending | — |
| **Multilingual** | 800 | ❌ Not released | — | — | — |
| **TOTAL (released)** | 7,711 | — | 23.3% (1,800 pairs) | — | — |
| **ANNOTATED SUBSET (Chamoreau)** | **800** | ✅ Full (seg. + gloss + analysis) | 100% | ✅ Complete | 640 / 160 |
| **ANNOTATED SUBSET (Bible)** | **1,000** | ⚠ Partial (seg. + gloss only) | 19.4% | ✅ Complete | 1,000 / — |

**Key note**: The annotation layer covers 1,800 pairs total: 800 fully annotated pairs from Chamoreau (segmentation + gloss + strategic analysis, deduplicated with Multilingual) and 1,000 partially annotated pairs from the Bible train set (segmentation + gloss only, no strategic analysis). This represents 23.3% of the released corpus (7,711 pairs).

---

## Detailed Breakdown

### 1. Bible (Diósïri Karakata P'urheepecha Jimbo)

**Subcorpus size**: 5,159 parallel pairs  
**Purépecha tokens**: 75,273  
**Spanish tokens**: 95,821  
**Mean sentence length (Pu)**: 14.59 tokens  
**Annotation status**: ⏸ **None**

**Source details**:
- New Testament translation by Mexican Bible Society (2011)
- ISBN: printed in Brazil; available via Bible.com and YouVersion app
- ISO 639-3 code: pua (Western Highland Purépecha, administrative classification)
- Orthography: Straight apostrophe ('), diaeresis ï for /ɨ/

**Why no annotation**: Resource quota limitations on generative models during annotation phase. Bible can be annotated in future versions (process is reproducible and scalable).

**Orthographic group**: Group 1 (Hispanic convention)

---

### 2. Political Constitution (Constitución Política de los Estados Unidos Mexicanos)

**Subcorpus size**: 1,549 parallel pairs  
**Purépecha tokens**: 55,722  
**Spanish tokens**: 66,837  
**Mean sentence length (Pu)**: 35.97 tokens  
**Annotation status**: ⏸ **None**

**Source details**:
- Published 2017 by INALI (part of bilingual constitutional initiative, 2010–2017)

- Translation carried out by "collegiate group of translators + linguists + legal advisors" in coordination with intercultural universities
- Orthography: Curly apostrophe (U+2019), reduced use of ï vs. Bible

**Why no annotation**: Resource quota limitations. The collegiate translation process and orthographic heterogeneity (evidence of multiple translators and 2015 INALI standardization transition) makes constitutional text valuable for dialectal research but requires careful model handling.

**Orthographic group**: Group 3 (Standard-mixed, shows internal iV/yV inconsistency)

**Notable finding**: Internal evidence of orthographic transition (18 iasï / 2 yasï within same source), supporting hypothesis that Constitution documents the 2015 INALI orthographic normalization process.

---

### 3. Chamoreau (Hablemos Purépecha. Wantee juchari anapu)

**Subcorpus size**: 841 parallel pairs  
**Annotated pairs**: 841 (100%)  
**Purépecha tokens**: 2,762 (untokenized), ~9,800 post-segmentation  
**Spanish tokens**: 3,351  
**Mean sentence length (Pu)**: 3.29 tokens  
**Annotation status**: ✅ **Complete**

**Source details**:
- Pedagogical-descriptive work by Claudine Chamoreau (2009)
- Published by Kw'anískuyarhani Group of Scholars of the Purépecha People, Morelia
- 552-page volume + CD with audio material
- Examples organized didactically around morphological paradigms
- **Key feature**: ~70% of examples have explicit morpheme segmentation in original text (spaces between morphemes), e.g., "wichu i x ti" instead of "wichuixti"
- Orthography: Curly apostrophe, systematically preserves ï
- Linguistic provenance: Primarily Lake Pátzcuaro region (Jarácuaro, Ihuatzio, Pacanda, Urandén) + Sierra/Meseta + Cañada de los Once Pueblos + Tiríndaro area

**Annotation coverage**:
- **Morphological segmentation**: 841/841 (100%) ✅
- **Interlinear gloss**: 841/841 (100%) ✅
- **Strategic analysis**: 841/841 (100%) ✅
- **Train/test split**: 480 train / 160 test (after deduplication with Multilingual)
- **Format**: JSON + Pickle (DatasetDict)

**Orthographic group**: Group 2 (Linguistic standard convention)

**Quality validation**: Spot inspections conducted during annotation suggest acceptable quality for exploratory purposes. No systematic human validation by Purépecha specialist linguist yet.

---

### 4. Narratives (Mondragón, Tello & Valdéz 1995)

**Subcorpus size**: 162 parallel pairs  
**Purépecha tokens**: 6,033  
**Spanish tokens**: 7,481  
**Mean sentence length (Pu)**: 37.25 tokens  
**Annotation status**: ⏸ **None**

**Source details**:
- Twelve traditional narrative texts
- Edited by Lucila Mondragón, Jacqueline Tello, Argelia Valdéz
- Published 1995 by Dirección General de Culturas Populares (CONACULTA)
- Part of *Lenguas de México* series, volume 12
- Rich documentation of geographical provenance per narrative (Table 4 in paper)
- Regional distribution: Localities from 3–4 of 4 traditional regions

**Notable detail on corpus construction**:
- Original PDF→text conversion lost important typographical characters (ï, curly apostrophes, demonstrative I-capital)
- **Orthographic restoration**: Using original RTF files, restored 142/162 pairs (87.7%)
- Remaining 20 pairs: titles without special characters or unavailable RTF sources
- **Released with explicit marking** of which pairs were restored

**Why no annotation**: Small subcorpus (162 pairs) with long, lexically diverse sentences makes it less suitable for initial annotation. Prioritized Chamoreau (pedagogical value) and Multilingual (linguistic motivation). Narratives can be annotated in v1.1.

**Orthographic group**: Group 1 (Hispanic convention, with internal orthographic variation reflecting multiple translators)

**Narrative provenance** (from Table 4 in paper):
- Narratives 1–4: Sierra/Meseta region
- Narratives 5–8: Lake Pátzcuaro region
- Narratives 9–10: Cañada de los Once Pueblos (including Angahuan, known for intelligibility difficulties)
- Narratives 11–12: Ciénega de Zacapu region

---

### 5. Multilingual (Soriano García 2018, Colmex Archives)

**Subcorpus size**: 800 parallel pairs  
**Purépecha tokens**: 2,833  
**Spanish tokens**: 3,526  
**Annotation status**: **Not released (restricted)**

**Source details**:
- Compiled by Miguel Salvador Soriano García (undergraduate thesis, Centro Universitario de los Lagos, University of Guadalajara, 2018)
- Supervisor: Dr. Jesús Ricardo Sevilla Escoboza
- Source: Archive of Indigenous Languages of Mexico, El Colegio de México
- **Geographical provenance**: Jarácuaro, Michoacán (Lake Pátzcuaro area)
- **Copyright**: Held by Colmex Archives; free consultation online but redistribution not authorized

**Why restricted**: Archive retains copyright and does not permit free redistribution. Data used for experiments (Section 5) but not included in public release.

**Orthographic group**: Group 2 (Linguistic standard) with distinctive Americanist transcription (ɨ for /ɨ/, š for postalveolar affricates, curly apostrophes)

**Nature of data**: Linguistically motivated examples designed to illustrate phonological, morphological, and syntactic peculiarities of Jarácuaro Purépecha (not everyday speech).

---

## Annotation Scheme (Summary)

The 800 annotated pairs include three annotation levels:

### Level 1: Morphological Segmentation
- Root + affixes separated by hyphens
- Preserves allomorphic variants
- Example: `juchi-ni-o` (house-POSS.1-RESID)

### Level 2: Interlinear Gloss
- Spanish-language labels (convertible to Leipzig Rules via provided mapping)
- One-to-one correspondence with segmentation
- Example labels: `posesivo1`, `objetivo`, `residencial`, `estar`, `formativo`, `aoristo`, `asertivo3`

### Level 3: Strategic Analysis (Translation Guide)
- 1–2 sentence explanation of gloss-to-Spanish transformation
- Documents word order changes, null arguments, idiomaticity, register shifts
- **Important limitation**: Generated with access to reference Spanish translation (lexical leakage) — not suitable for blind training without regeneration

**Full specification**: See [`docs/annotation_scheme.md`](docs/annotation_scheme.md)

---

## Construction Process

### Phase 1: Segmentation & Gloss (Gemini 2.5 Pro)
- **Model**: Gemini 2.5 Pro via Google AI Studio
- **Context**: Full Chamoreau (2009) grammar loaded as multimodal reference
- **Input**: 50–100 parallel pairs per call, structured JSON output
- **Coverage**: All 800 pairs

### Phase 2: Strategic Analysis (Gemini 3 Flash + RAG)
- **Model**: Gemini 3 Flash via API
- **Knowledge base**: Chamoreau manual fragmented into 1,000-char chunks (200-char overlap), vectorized with paraphrase-multilingual-MiniLM-L12-v2, indexed with FAISS
- **Retrieval**: Top 3 chunks per pair
- **Rationale**: Cost-efficient alternative to Phase 1 (20-call/day free limit on Gemini 3 Flash)
- **Coverage**: All 800 pairs

### Post-processing
- Deduplication: Chamoreau + Multilingual combined from ~1,641 → 800 unique pairs
- Format verification: All three annotation levels present, no empty fields
- Train/test split: 640 train / 160 test (fixed seed)

---

## Limitations

### 1. Lexical leakage in strategic analysis
- Model had access to Spanish translation during generation
- **For human use**: Useful (synthesizes translation reasoning)
- **For model training**: Not directly usable without regeneration via blind process
- **Recommendation**: For chain-of-thought models, regenerate analysis without translation access

### 2. Absence of systematic human validation
- Spot inspections conducted; no formal evaluation by Purépecha specialist linguist
- Acceptable for exploratory/computational purposes
- **For critical use** (pedagogical, formal linguistics): Recommend validation by native speakers or specialists

### 3. Heterogeneity between annotation phases
- Phase 1: Gemini 2.5 Pro (full grammar context)
- Phase 2: Gemini 3 Flash + RAG (synthetic task)
- Deliberate separation (different models suited different tasks) but systematic differences not quantified

### 4. Non-standardized gloss labels
- Spanish language (pedagogical intent for Mexican users)
- Not Leipzig Glossing Rules (mapping provided in appendix)
- Possible inconsistencies in manual mapping

---

## Machine Translation Experiments

See Section 5.2 of the paper for detailed results. BLEU scores (Purépecha→Spanish):

| Training Set | BLEU | Notes |
|--------------|------|-------|
| Chamoreau alone | 19.71 | Pedagogical source |
| Multilingual alone | 21.50 | Best single source |
| Chamoreau + Multilingual | 28.60 | Positive transfer (related register) |
| Bible alone | 9.37 | Large but repetitive (religious vocabulary) |
| Constitution alone | 15.8 | Formulaic legal text |
| Narratives alone | ~2 | Few pairs + long, diverse sentences |
| All combined | 10.02 | Dilution by extreme heterogeneity |

**Key finding**: Positive transfer between pedagogically similar sources (Chamoreau+Multilingual) but dilution when mixing heterogeneous registers. Per-domain performance preserved even in mixed training.

---

## Roadmap to v1.0.0 (Final Release)

- [x] Chamoreau corpus complete + full annotation
- [ ] Narratives correction + restoration documentation (✅ complete, no annotation)
- [ ] Quality validation (sample orthographic/morphological spot check)
- [ ] HuggingFace Hub upload finalized
- [ ] Zenodo DOI assigned
- [ ] Official v1.0.0 release (July–September 2025 target)

### Future versions (v1.1+)
- Annotation of Bible + Constitution (models, process scalable)
- Possible inclusion of additional sources (if located + permissions obtained)
- Human validation of strategic analysis by Purépecha specialist
- Systematic evaluation of inter-annotator agreement (if multiple annotators)

---

## Reporting Issues & Contributing

If you find errors or have suggestions:

1. **Open an Issue** on GitHub with:
   - Subcorpus name and pair ID
   - Description of the issue (annotation, translation, metadata)
   - Evidence (reference grammar, dialectal data) if applicable

2. **For critical errors** (annotation clearly wrong, metadata inaccurate): Include recommended correction

3. All contributions acknowledged in subsequent versions

---

## Data Access Formats

All annotated pairs available in both formats (and DatasetDict for HuggingFace):

```python
# Pickle (native Python)
import pickle
with open('purepecha_chamoreau_annotated.pkl', 'rb') as f:
    corpus = pickle.load(f)

# JSON (universal)
import json
with open('purepecha_chamoreau_annotated.json', 'r', encoding='utf-8') as f:
    corpus = json.load(f)

# HuggingFace DatasetDict
from datasets import load_dataset
corpus = load_dataset("CeciGonSer/purepecha-spanish-corpus")
```

---

**Last updated**: June 21, 2025  
**Annotation scheme version**: 1.0  
**Paper version**: Submitted to Language Resources and Evaluation (2025)
