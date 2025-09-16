# Enhancing Medical Dialogue Summarization with Keyword and Medical Entity Extraction

## 📖 Overview
This project explores enhancing **medical dialogue summarization** by integrating **keyword** and **medical entity extraction**. The goal is to improve the accuracy and coherence of automatically generated summaries of patient–clinician conversations, reducing clinician burnout from manual documentation and improving clinical workflows.

We evaluate multiple NLP models for both **entity extraction** (BioBERT, Medical NER, KeyBERT) and **summarization** (Flan-T5, LED_Large), combining these approaches to increase the presence of medically relevant terminology in generated summaries.

---

## 🎯 Research Objective
- **Problem:** Existing summarization models often miss key medical terms, leading to incomplete or misleading summaries.  
- **Goal:** Ensure that summaries capture **critical medical terminology** while maintaining readability and clinical utility.  
- **Approach:** Compare baseline summarization models with versions enhanced by **NER and keyword extraction**.  

---

## 📊 Datasets
We use both short and long dialogue datasets to ensure robustness:  
- **MTS-Dialog** – 1,501 short medical dialogues  
- **ACI-Bench** – clinician–patient interactions (long dialogues)  
- **Dialogue_G** – synthetic long dialogues  

**Data splits:** 80% train / 7% validation / 13% test  

---

## ⚙️ Methodology
1. **Entity Extraction Models**
   - **KeyBERT** – keyword extraction without labeled data  
   - **BioBERT** – biomedical NER (diseases, chemicals)  
   - **Medical NER (DeBERTa-based)** – extracts diseases, symptoms, procedures, medications, etc.  

2. **Summarization Models**
   - **Flan-T5 Large** – best baseline for short dialogues  
   - **LED_Large** – best baseline for long dialogues  

3. **Integration Strategy**
   - Extracted entities are concatenated with the original dialogue.  
   - Prompted summarization models use entities as guidance (e.g., *"Summarize into subjective and assessment sections, using these entities…"*)  
   - Applied **LoRA fine-tuning** and **4-bit quantization** for efficiency.  

4. **Evaluation Metrics**
   - **ROUGE-1, ROUGE-2, ROUGE-L** (precision, recall, F1)  
   - **Error analysis** for entity misidentification and overfitting risks  

---

## 📈 Results
- **Short dialogues:**  
  - Baseline **Flan-T5 Large** outperformed NER-augmented versions.  
  - Adding entities caused **overfitting** and worse generalization.  

- **Long dialogues:**  
  - **LED_Large + Medical NER** achieved the **best performance**.  
  - Improved ROUGE scores and better capture of relevant medical content (e.g., correctly incorporating “pain medication” into summaries).  

- **Keyword extraction (KeyBERT):** Failed to capture medical relevance (e.g., produced noisy terms like “psychiatrist seeing long”).  

---

## ⚠️ Limitations
- **Entity misidentification:** NER sometimes incorrectly introduced conditions not present in the dialogue (e.g., mislabeling "no history of cancer" as "cancer").  
- **Overemphasis on entities:** Led to repetitive or incomplete summaries.  
- **Short dialogue challenge:** Entity integration reduced performance compared to baseline.  

---

## ✅ Conclusion
- **Best setup:** LED_Large with Medical NER for **long dialogues**.  
- **Short dialogues:** Baseline Flan-T5 Large remains superior without NER integration.  
- **Future work:**  
  - Improve entity context understanding (e.g., distinguishing presence vs. absence).  
  - Explore advanced summarization strategies (e.g., GPT-based models, reinforcement learning).  
  - Refine NER integration methods to reduce noise and mislabeling.  

---

## 👥 Team
This project was created by **UC Berkeley Master of Information and Data Science (MIDS)** students as part of the **Natural Language Processing with Deep Learning (W266)** course

- Tingting Li
- Agnese Minazzo
- Michelle Sinani
