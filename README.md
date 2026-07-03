# Nils Matteson

vLLM contributor (two merged core PRs) and vLLM open-source fellow, sponsored by Inferact,
working on engine cold-start and model hot-swap. Creator of [thaw](https://thaw.sh), open-source
infrastructure for snapshotting and forking live LLM inference. Sole author of an arXiv
measurement study on replay noise. B.S. Data Science + CS, UW-Madison (May 2026); M.S. CS at
Northeastern's Silicon Valley campus starting September 2026; based in San Jose. Background in
ML reliability (uncertainty quantification, OOD detection, conformal prediction).

Some things I've built:

- **vLLM (upstream)**: [#44074](https://github.com/vllm-project/vllm/pull/44074), a pluggable
  sleep-mode backend abstraction ([RFC #34303](https://github.com/vllm-project/vllm/issues/34303)),
  merged into core July 2026 with review engagement from NVIDIA Dynamo and Alibaba Cloud
  engineers; follow-up [#47243](https://github.com/vllm-project/vllm/pull/47243) merged the same
  day. Open: [#47356](https://github.com/vllm-project/vllm/pull/47356) (found while measuring:
  the documented fast-boot flag silently invalidates the compile cache),
  [#47374](https://github.com/vllm-project/vllm/pull/47374), and
  [#47388](https://github.com/vllm-project/vllm/pull/47388) (persist the memory-profiling
  result across boots). The fellowship work starts from a measured H100 phase ledger of where
  vLLM boot time actually goes.

- **["Re-feeding Is Not Replaying"](https://arxiv.org/abs/2606.15621)** (arXiv:2606.15621, sole
  author): every published token-credit method rebuilds model state by re-feeding the transcript
  and assumes that reproduces the same state. Measured on stock vLLM, it does not: credit
  estimates at low-margin decision tokens shift at rates 14 to 28 points above a replica noise
  floor. vLLM's batch-invariant kernels eliminate the effect bit-exactly. Total compute under $10.

- **[thaw](https://github.com/thaw-ai/thaw)**: snapshot a running LLM session (weights + KV
  cache + scheduler state + prefix-hash table) and hydrate it into N divergent children that
  skip prefill and diverge from the fork point. Hero receipt: ForkPool init 22.3s one-time, then
  0.88s median per round across 5 rounds x 4 branches x 64 tokens on H100 + Llama-3.1-8B, all
  bit-identical at the fork boundary. 70B TP=2 sleep/wake on 2xH100 also bit-identical, 145 GiB
  freed via CuMemAllocator. ~9,400 LOC Rust core across 5 crates + ~3,000 LOC Python; also runs
  on Apple Silicon (MLX). On PyPI as `thaw-vllm` / `thaw-native`. The vLLM work above grew out
  of it.

- **[ProjectGorgon](https://github.com/matteso1/ProjectGorgon)**: Medusa-style speculative
  decoding for Llama-3-8B with custom CUDA kernels. 5-head architecture, per-head loss
  weighting (λ_k = 0.8^k), trained on UltraChat 200k. Taught myself GPU programming for this;
  led directly to thaw.

- **[madison-bus-eta](https://madisonbuseta.com)**: live. Real-time arrival predictions for
  all 29 Madison Metro routes. XGBoost on 47 features, Mondrian conformal prediction (90%
  coverage guarantee), nightly retraining with deployment gates, DeckGL map, bus-bunching
  detection. 35% more accurate than the official API.

- **KohakuRAG_UI**: RAG system for AI sustainability Q&A, deployed on AWS Bedrock. Built for
  UW's Research Cyberinfrastructure group.

- **sentinel**: Kafka-inspired distributed log streaming engine in Go. Custom LSM-tree
  storage, skip list memtable, Raft consensus, gRPC wire protocol. 1.7M ops/sec on the skip
  list.

- **lockbox**: zero-trust, air-gapped password manager. AES-256-GCM + Argon2id, TOTP 2FA,
  compiles to a single `.exe`. No cloud, no telemetry, no network calls.

Talk: [*Deploying RAG in Bedrock vs. Local*](https://uw-madison-datascience.github.io/ML-X-Nexus/Applications/Videos/Forums/mlx_2026-02-17.html), ML+X Forum, Feb 2026.

Currently: vLLM open-source fellow (July: container cold-start; August: hot-swap). Open to
conversations with people working on inference infrastructure, GPU runtimes, agent systems, or
LLM RL post-training. Reach me at **nils@thaw.sh**.

[nilsmatteson.com](https://nilsmatteson.com) · [thaw.sh](https://thaw.sh) · [arXiv](https://arxiv.org/abs/2606.15621) · [linkedin](https://www.linkedin.com/in/nilsmatteson)

