# RAG System Implementation - Assignment 2

## Overview
Implementation of a Retrieval-Augmented Generation (RAG) system using the RAG Mini Wikipedia dataset. The system includes naive baseline, retrieval experiments, and production enhancements (query rewriting + confidence scoring).

## Dataset
- **Source**: [RAG Mini Wikipedia](https://huggingface.co/datasets/rag-datasets/rag-mini-wikipedia)
- **Passages**: 3,200 Wikipedia passages
- **Test Queries**: 918 question-answer pairs

## System Components
- **Embedding Model**: sentence-transformers all-MiniLM-L6-v2 (384 dimensions)
- **Vector Database**: FAISS IndexFlatL2 (exact search)
- **Language Model**: Google Flan-T5-base (250M parameters)
- **Evaluation**: HuggingFace evaluate library (SQuAD metrics)

## Setup Instructions

### Google Colab (Recommended)
1. Open the notebook in Google Colab
2. Runtime → Change runtime type → GPU (if available)
3. Run cells sequentially from top to bottom
4. Total runtime: ~2-3 hours

### Local Setup
```bash
pip install -r requirements.txt
jupyter notebook rag_assignment.ipynb
```

## File Structure
```
assignment2-rag/
├── rag_assignment.ipynb          # Main notebook
├── README.md                      # This file
├── requirements.txt               # Dependencies
├── technical_report.pdf           # Full analysis
├── ai_usage_log.md               # AI assistance documentation
└── results/
    ├── rag_results_basic_top1.csv
    ├── rag_results_top3.csv
    └── rag_results_enhanced.csv
```

## Results Summary

| System | F1 Score | Exact Match |
|--------|----------|-------------|
| Naive (Top-1) | 47.59% | 39.43% |
| Top-3 Retrieval | 47.17% | 38.02% |
| Enhanced (Rewriting + Confidence) | 37.38% | 31.48% |

**Key Finding**: Top-1 retrieval outperformed both top-3 and enhanced variants. Additional context and aggressive filtering decreased performance.

## Expected Runtime
- EDA: 5 minutes
- Embedding generation: 3 minutes
- FAISS setup: 10 seconds
- Query processing (918 queries): 20-25 minutes per system
- Total: ~2 hours for complete pipeline

## Known Limitations
- Query rewriting limited by Flan-T5-base capabilities
- RAGAs evaluation requires OpenAI API (not included)
- Confidence threshold not optimized on validation set
- No semantic chunking or preprocessing applied

## Contact
For questions about this implementation, refer to the technical report or course materials.