# RAG Inference Optimization

Optimizing a Retrieval-Augmented Generation (RAG) pipeline for **latency and memory** without
sacrificing generation quality. This is the experimental code behind a first-authored paper
(*Enhancing Retrieval-Augmented Generation: Improving Performance through Optimization
Techniques*, **under review at Springer**, in collaboration with Samsung R&D Institute India / PRISM).

## What this does

A vanilla RAG pipeline (document retrieval → context injection → generation) is treated as a
baseline, and four optimization techniques are layered on and benchmarked against it across
**latency, memory footprint, and generation quality (BLEU)**:

| Technique | Idea |
|---|---|
| **FAISS vector retrieval** | Approximate nearest-neighbour search over document embeddings for fast retrieval |
| **LRU caching** | Cache results for frequently requested queries to skip repeated retrieval/generation |
| **INT8 quantization** | Store weights in 8-bit to cut memory and speed up inference, trading a small accuracy cost |
| **Model parallelism** | Split the model across devices to fit larger models / improve throughput |

**Headline result:** ~**34.6% reduction in inference time** with a substantially smaller memory
footprint while preserving generation quality, plus a characterization of the
accuracy–efficiency trade-off of INT8 quantization.

## Repository layout

```
RAG_Optimization.ipynb   # end-to-end experiments: baseline + the four optimizations + benchmarks
Data/                    # sample source document(s) used for retrieval
```

## Getting started

```bash
git clone https://github.com/Raghavesh101/RAG.git
cd RAG
```

Open `RAG_Optimization.ipynb` in Jupyter or Google Colab (a GPU runtime is recommended for the
quantization and parallelism sections) and run the cells top to bottom. Key dependencies:
`transformers`, `faiss`, and `torch`.

## Notes & limitations

- Built around a GPT-2-class generator and a small document set — the numbers illustrate the
  *relative* effect of each optimization, not an absolute production benchmark.
- BLEU is a coarse proxy for generation quality; treat the quality-preservation claim as
  directional.

## License

MIT — see [LICENSE](LICENSE).

## Contact

Raghavesh Mishra — [raghaveshm@gmail.com](mailto:raghaveshm@gmail.com) ·
[LinkedIn](https://www.linkedin.com/in/raghavesh-mishra-a31339240/)
