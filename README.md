 # Nils Matteson

  Senior @ UW-Madison, CS + Data Science (graduating May 2026). Solo founder of
  [thaw](https://thaw.sh) — building the fork primitive for live LLM inference. Open-source,
  pip-installable, integrates with vLLM and SGLang. Background in ML reliability (uncertainty
  quantification, OOD detection, conformal prediction) and systems work on the side.

  Some things I've built:

  - **[thaw](https://github.com/thaw-ai/thaw)** — snapshot a running LLM session (weights + KV
    cache + scheduler state + prefix-hash table) and hydrate it into N divergent children that
    skip prefill and diverge from the fork point. Hero receipt: ForkPool init 22.3s one-time →
    0.88s median per round across 5 rounds × 4 branches × 64 tokens on H100 + Llama-3.1-8B, all
    bit-identical at the fork boundary. 70B TP=2 sleep/wake on 2×H100 also bit-identical, 145
    GiB freed via CuMemAllocator. ~9,400 LOC Rust core across 5 crates + ~3,000 LOC Python; now
    also runs on Apple Silicon (MLX). On PyPI as `thaw-vllm` / `thaw-native`.

  - **[ProjectGorgon](https://github.com/matteso1/ProjectGorgon)** — Medusa-style speculative
    decoding for Llama-3-8B with custom CUDA kernels. 5-head architecture, per-head loss
    weighting (λ_k = 0.8^k), trained on UltraChat 200k. Taught myself GPU programming for this;
    led directly to thaw.

  - **[madison-bus-eta](https://madisonbuseta.com)** — live. Real-time arrival predictions for
    all 29 Madison Metro routes. XGBoost on 47 features, Mondrian conformal prediction (90%
    coverage guarantee), nightly retraining with deployment gates, DeckGL map, bus-bunching
    detection. 35% more accurate than the official API.

  - **KohakuRAG_UI** — RAG system for AI sustainability Q&A, deployed on AWS Bedrock. Built for
    UW's Research Cyberinfrastructure group.

  - **sentinel** — Kafka-inspired distributed log streaming engine in Go. Custom LSM-tree
    storage, skip list memtable, Raft consensus, gRPC wire protocol. 1.7M ops/sec on the skip
    list.

  - **lockbox** — zero-trust, air-gapped password manager. AES-256-GCM + Argon2id, TOTP 2FA,
    compiles to a single `.exe`. No cloud, no telemetry, no network calls.

  Talk: [*Deploying RAG in Bedrock vs. Local*](https://uw-madison-datascience.github.io/ML-X-Nexus/Applications/Videos/Forums/mlx_2026-02-17.html) — ML+X Forum, Feb 2026.

  Currently full-time on thaw. Open to conversations with people working on inference
  infrastructure, agent systems, LLM RL post-training, or anything composability-related at the
  GPU-state layer. Reach me at **nils@thaw.sh**.

  [thaw.sh](https://thaw.sh) · [linkedin](https://www.linkedin.com/in/nilsmatteson) · [github](https://github.com/matteso1)
