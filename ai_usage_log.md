# AI Usage Log - Assignment 2: RAG System Implementation

## AI Tool Used
**Tool**: Claude.ai (Anthropic Claude Sonnet 4.5)  
**Access**: Free tier via claude.ai web interface  
**Usage Period**: October 2025

---

## Usage Summary

### 1. EDA Code
**Input**: Request for passage dataset analysis following starter notebook structure  
**Output**: Python code for length distributions, missing values, visualizations  
**Verification**: Ran code and reviewed outputs, interpreted token truncation implications

### 2. Embedding Generation
**Input**: Request for sentence-transformers implementation with FAISS  
**Output**: Code for encoding passages and creating vector index  
**Verification**: Verified 3,200 vectors indexed, debugged Milvus compatibility issues, switched to FAISS

### 3. Retrieval System
**Input**: Request for query search functionality  
**Output**: Code for embedding queries and FAISS search  
**Verification**: Tested on sample queries, verified retrieval accuracy

### 4. Prompt Engineering
**Input**: Request for three prompting strategies (basic, few-shot, chain-of-thought)  
**Output**: Prompt template functions  
**Verification**: Tested all three, selected basic prompt based on output format analysis

### 5. Answer Generation
**Input**: Request for Flan-T5 integration and batch processing  
**Output**: Code for loading model and processing 918 queries  
**Verification**: Monitored generation, spot-checked outputs

### 6. Evaluation Metrics
**Input**: Request for F1/EM calculation using HuggingFace evaluate  
**Output**: SQuAD metric implementation and per-question analysis  
**Verification**: Interpreted F1=47.59%, EM=39.43% results

### 7. Top-3 Retrieval Experiment
**Input**: Request for multi-passage retrieval comparison  
**Output**: Code for concatenating passages as context  
**Verification**: Analyzed why performance decreased

### 8. Enhancement Implementation
**Input**: Request for query rewriting and confidence scoring  
**Output**: Code for both enhancements  
**Verification**: Tested query rewriting effectiveness, reviewed confidence threshold, analyzed failure causes

### 9. RAGAs Evaluation Attempt
**Input**: Request for RAGAs with local model configuration  
**Output**: Code with LangChain wrapper for local Flan-T5  
**Verification**: Attempted execution, encountered API errors, decided to skip due to time constraints

---

**Personal Decisions Made**:
- Chose FAISS over Milvus based on Colab compatibility
- Selected basic prompting over alternatives based on output format
- Analyzed why enhancements failed and provided root cause analysis
- Made time management trade-offs (skipping RAGAs)
- Interpreted all experimental results independently