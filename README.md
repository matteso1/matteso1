# Nils Matteson

I make vLLM start faster. I built [thaw](https://github.com/thaw-ai/thaw) to snapshot and fork live LLM sessions.

**vLLM contributor and Inferact open-source fellow**, working with Simon Mo on cold start and model hot-swap. Based in San Jose.

### vLLM

I maintain the [cold-start roadmap](https://github.com/vllm-project/vllm/issues/48193). My merged work includes [pluggable sleep-mode backends](https://github.com/vllm-project/vllm/pull/44074), [compile-cache invalidation fixes](https://github.com/vllm-project/vllm/pull/47356), and [memory-profile reuse across boots](https://github.com/vllm-project/vllm/pull/47388).

Current work, in review:

- **[Engine snapshots](https://github.com/vllm-project/vllm/pull/51360):** restore an initialized engine instead of rebuilding it. **23.9 s → 9.4 s** from command start to first correct token versus ordinary warm startup (A10, Qwen3-0.6B, TP1, warm model and compile caches; median, n=5 per arm).
- **[Fast CLI help](https://github.com/vllm-project/vllm/pull/54841):** `vllm --help` in **40 ms instead of 3.5 s** by keeping it out of the runtime import graph (Apple M5, Python 3.12; median, n=5 per arm).
- **[Precompiled Python bytecode](https://github.com/vllm-project/vllm/pull/55422):** move compilation into the image build so fresh containers do less work before serving.

[All vLLM contributions](https://github.com/vllm-project/vllm/pulls?q=is%3Apr+author%3Amatteso1).

### [thaw](https://github.com/thaw-ai/thaw)

Snapshot a running LLM session, fork independent continuations from its KV state, and inspect or diff saved sessions on a laptop without a GPU. Rust + CUDA, with vLLM and SGLang integrations.

This is the project that led me into upstream vLLM.

### Research

**[Re-feeding Is Not Replaying](https://arxiv.org/abs/2606.15621)** · sole-author preprint.

Replaying a transcript can change which tokens a credit-estimation method identifies as important. I measured that against exact KV-state resume and a replica noise floor. Batch-invariant kernels eliminated the discrepancy in the tested configurations.

### Other things I've built

- **[Recall](https://github.com/matteso1/recall):** a Rust/Tauri League of Legends overlay that recommends your next purchase from live game state.
- **[ProjectGorgon](https://github.com/matteso1/ProjectGorgon):** speculative decoding with custom Triton/CUDA kernels. Where I learned GPU programming.
- **[sentinel](https://github.com/matteso1/sentinel):** a Go log-streaming engine with LSM storage, a write-ahead log, and replication.
- **[Madison Bus ETA](https://github.com/matteso1/madison-bus-eta):** arrival predictions with XGBoost and conformal uncertainty intervals. Retired; source available.

M.S. CS at Northeastern, Silicon Valley. B.S. Data Science, UW–Madison.

[Email](mailto:nilsmatteson@icloud.com) · [Website](https://nilsmatteson.com) · [LinkedIn](https://www.linkedin.com/in/nilsmatteson)
