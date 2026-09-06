# Nils Matteson

I work on LLM inference engines. vLLM contributor and Inferact open-source fellow, currently on
engine cold start and model hot-swap. M.S. CS at Northeastern, Silicon Valley. San Jose.

### vLLM

Eight merged PRs in core, three open ([all of them](https://github.com/vllm-project/vllm/pulls?q=is%3Apr+author%3Amatteso1)).

- [#44074](https://github.com/vllm-project/vllm/pull/44074) pluggable sleep-mode backends ([RFC #34303](https://github.com/vllm-project/vllm/issues/34303)), the abstraction hot-swap builds on
- [#47388](https://github.com/vllm-project/vllm/pull/47388) persist the memory-profiling result across boots
- [#47356](https://github.com/vllm-project/vllm/pull/47356), [#47573](https://github.com/vllm-project/vllm/pull/47573) compile-cache keys that were silently invalidating on every boot
- [#54841](https://github.com/vllm-project/vllm/pull/54841), [#55422](https://github.com/vllm-project/vllm/pull/55422) open: CLI startup without importing the runtime, bytecode compiled into the image

### Projects

| | |
|---|---|
| [**thaw**](https://github.com/thaw-ai/thaw) | git for live LLM sessions. Snapshot a running vLLM/SGLang session (weights, KV cache, scheduler state) to a file, fork it into N children that skip prefill, diff it on a laptop. Rust + CUDA. `pip install thaw-vllm` |
| [**Re-feeding Is Not Replaying**](https://arxiv.org/abs/2606.15621) | arXiv, sole author. Token-credit methods rebuild model state by re-feeding the transcript and assume it reproduces the same state. Measured on stock vLLM it does not; batch-invariant kernels fix it bit-exactly. Under $10 of compute. |
| [**Recall**](https://github.com/matteso1/recall) | League of Legends overlay that says what to buy next and why, from live inventory and gold. Shop-legal purchasing, builds from real per-role data, Swiftplay prep. Rust + Tauri. |
| [**madison-bus-eta**](https://madisonbuseta.com) | live arrival predictions for every Madison Metro route. XGBoost + Mondrian conformal prediction, 35% more accurate than the official API. |
| [**ProjectGorgon**](https://github.com/matteso1/ProjectGorgon) | Medusa-style speculative decoding for Llama-3-8B with hand-written CUDA kernels. Where I learned GPU programming; led to thaw. |
| [**sentinel**](https://github.com/matteso1/sentinel) | Kafka-style log streaming engine in Go: LSM storage, skip-list memtable, Raft, gRPC. |

Talk: [Deploying RAG in Bedrock vs. Local](https://uw-madison-datascience.github.io/ML-X-Nexus/Applications/Videos/Forums/mlx_2026-02-17.html), ML+X Forum.

**nils@thaw.sh** · [nilsmatteson.com](https://nilsmatteson.com) · [thaw.sh](https://thaw.sh) · [linkedin](https://www.linkedin.com/in/nilsmatteson)
