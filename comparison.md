# RAG System Performance Comparison

## Overall Metrics Summary

| System | F1 Score | Exact Match | Mean Per-Q F1 | Questions F1>0.5 | Questions F1=0 |
|--------|----------|-------------|---------------|------------------|----------------|
| **Naive (Top-1)** | **47.59%** | **39.43%** | **0.408** | **372 (40.5%)** | **457 (49.8%)** |
| Top-3 Retrieval | 47.17% | 38.02% | 0.411 | N/A | N/A |
| Enhanced (Rewriting + Confidence) | 37.38% | 31.48% | 0.320 | N/A | N/A |

## Key Findings

### Best Performer: Naive RAG with Top-1 Retrieval
- Achieved highest F1 (47.59%) and EM (39.43%) scores
- Simple top-1 retrieval outperformed more complex approaches
- Basic instruction prompting matched dataset format best

### Top-3 Retrieval Experiment
- **Result**: Performance decreased slightly (-0.41 F1, -1.42 EM)
- **Insight**: Additional context introduced noise rather than helpful information
- **Implication**: More context ≠ better performance for this dataset/model combination

### Enhanced System (Two Production Features)
- **Result**: Performance decreased significantly (-10.20 F1, -7.95 EM)
- **Root Causes**:
  1. Query rewriting ineffective with Flan-T5-base (minimal query changes)
  2. Confidence threshold too aggressive (75th percentile filtered 25% of answers)
  3. Combination amplified negative effects
- **Learning**: Enhancements must be validated individually before combining

## System Configuration

| Component | Specification |
|-----------|--------------|
| Embedding Model | sentence-transformers all-MiniLM-L6-v2 (384d) |
| Vector Database | FAISS IndexFlatL2 (exact search) |
| Language Model | Google Flan-T5-base (250M params) |
| Prompt Strategy | Basic instruction |
| Dataset | RAG Mini Wikipedia (3,200 passages, 918 queries) |

## Prompting Strategy Results

| Strategy | Output Quality | Selected? |
|----------|---------------|-----------|
| Basic Instruction | Concise, format-aligned | ✓ Yes |
| Few-Shot (2 examples) | Marginal improvement, longer prompts | ✗ No |
| Chain-of-Thought | Too verbose for short answers | ✗ No |

## Retrieval Strategy Analysis

### Distance Distribution (Naive System)
- Mean distance: 0.665
- Median distance: 0.637
- 75th percentile: 0.784 (used as confidence threshold)

### Retrieval Quality Impact
- **Top-1**: Focused, reduced noise → Best performance
- **Top-3**: More coverage but introduced confusion → Slight decrease

## Enhancement Implementation Details

### Query Rewriting
- **Model**: Flan-T5-base
- **Effectiveness**: Limited (most queries unchanged)
- **Recommendation**: Use stronger models (GPT-4, Claude) for production

### Confidence Scoring  
- **Threshold**: 0.7835 (75th percentile of distances)
- **Effect**: Filtered ~25% of answers as low-confidence
- **Impact**: Reduced recall more than improved precision
- **Recommendation**: Optimize on validation set, not training distribution

## Production Recommendations

Based on experimental findings:

1. **Keep it simple**: Top-1 retrieval sufficient for this dataset scale
2. **Model quality matters**: Flan-T5-base insufficient for query rewriting
3. **Validate enhancements separately**: Test individual improvements before combining
4. **Optimize thresholds properly**: Use validation set, not statistical percentiles
5. **Consider stronger LLMs**: Larger models would likely improve all metrics

## Evaluation Attempted

- ✓ F1 Score and Exact Match (HuggingFace evaluate)
- ✓ Per-question analysis and distribution
- ✗ RAGAs (failed due to OpenAI API requirements, local model config unsuccessful)

---

**Conclusion**: Naive RAG with simple top-1 retrieval and basic prompting provides the best performance baseline. Production enhancements require careful validation and stronger models than Flan-T5-base for meaningful improvement.