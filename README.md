# Nils Matteson

I make vLLM start faster. vLLM contributor and Inferact open-source fellow, working with
Simon Mo (vLLM's lead maintainer) on engine cold start and hot-swap. M.S. CS at Northeastern,
Silicon Valley. San Jose.

### vLLM cold start

I own the cold-start lane of vLLM's Q3 2026 roadmap
([#48193](https://github.com/vllm-project/vllm/issues/48193)), split out from the main roadmap
with Simon because startup does not belong to any single SIG. The lane treats startup as a
retained-state frontier: six starting points from an empty machine to a live engine, each with
its own clock, and a ship contract every mechanism has to meet (prove it engaged, a
correct-token oracle, a negative control that can fail, explicit artifact identity and
invalidation). I maintain the issue, triage contributors into it, and keep the measurements honest.

What the lane has shipped and measured:

- **Where a truly cold start actually goes.** Official-image pull to first correct token is 188.7 s
  (A10, Qwen3-8B, n=3): image pull 80 s, imports and config 45 s, compile 21 s, model download 16 s,
  graph capture 7 s. That ledger orders the whole program.
- **Initialized-engine snapshots**, [#51360](https://github.com/vllm-project/vllm/pull/51360),
  approved by Simon. Checkpoint an initialized engine with CRIU and restore it instead of rebuilding:
  warm activation 23.9 s to 9.4 s on an A10, the restore step itself 0.3 s, reproduced independently
  on H20. Fails closed and never silently replaces ordinary startup.
- **Sleep-mode backends**, [#44074](https://github.com/vllm-project/vllm/pull/44074) (RFC
  [#34303](https://github.com/vllm-project/vllm/issues/34303)), merged into core with
  [#47243](https://github.com/vllm-project/vllm/pull/47243). The pluggable abstraction that hot-swap
  and 0.6 s resident wake build on.
- **Boot foundations, merged.** Compile-cache keys that were silently invalidating on every boot
  ([#47356](https://github.com/vllm-project/vllm/pull/47356),
  [#47573](https://github.com/vllm-project/vllm/pull/47573)), the memory-profiling result persisted
  across boots ([#47388](https://github.com/vllm-project/vllm/pull/47388)), the fast-start docs and
  compile-cache volume example ([#47374](https://github.com/vllm-project/vllm/pull/47374),
  [#49782](https://github.com/vllm-project/vllm/pull/49782)).
- **Startup UX, in review.** `vllm --help` and `--version` served from pre-rendered pages with zero
  runtime imports, 3.3 s to under a quarter second
  ([#54841](https://github.com/vllm-project/vllm/pull/54841)); bytecode compiled into the Docker image,
  serve import 6.5 s to 2.2 s per process ([#55422](https://github.com/vllm-project/vllm/pull/55422)).
- **Measure before merging.** [#48194](https://github.com/vllm-project/vllm/issues/48194) reads the whole
  history of download-at-entry (merged, reverted six hours later, never relanded), runs a paired
  measurement, and proposes a go/no-go protocol instead of another PR.

Around it: a merged fix in [Foundry](https://github.com/foundry-org/foundry/pull/8) (CUDA-graph
materialization for instant cold start), a portable JIT cache key for
[DeepGEMM](https://github.com/deepseek-ai/DeepGEMM/pull/398), and reviews of the snapshot work in
NVIDIA Dynamo. All vLLM PRs: [merged and open](https://github.com/vllm-project/vllm/pulls?q=is%3Apr+author%3Amatteso1).

### Projects

| | |
|---|---|
| [**thaw**](https://github.com/thaw-ai/thaw) | git for live LLM sessions. Snapshot a running vLLM/SGLang session (weights, KV cache, scheduler state) to a file, fork it into N children that skip prefill, diff it on a laptop. Rust + CUDA. `pip install thaw-vllm`. The vLLM work above grew out of it. |
| [**Re-feeding Is Not Replaying**](https://arxiv.org/abs/2606.15621) | arXiv, sole author. Token-credit methods rebuild model state by re-feeding the transcript and assume that reproduces the same state. Measured on stock vLLM it does not; batch-invariant kernels fix it bit-exactly. Under $10 of compute. |
| [**Recall**](https://github.com/matteso1/recall) | League of Legends overlay that says what to buy next and why, from live inventory and gold. Shop-legal purchasing, builds from real per-role data, Swiftplay prep. Rust + Tauri. |
| [**madison-bus-eta**](https://madisonbuseta.com) | Live arrival predictions for every Madison Metro route. XGBoost + Mondrian conformal prediction, 35% more accurate than the official API. |
| [**ProjectGorgon**](https://github.com/matteso1/ProjectGorgon) | Medusa-style speculative decoding for Llama-3-8B with hand-written CUDA kernels. Where I learned GPU programming; led to thaw. |
| [**sentinel**](https://github.com/matteso1/sentinel) | Kafka-style log streaming engine in Go: LSM storage, skip-list memtable, Raft, gRPC. |

Talk: [Deploying RAG in Bedrock vs. Local](https://uw-madison-datascience.github.io/ML-X-Nexus/Applications/Videos/Forums/mlx_2026-02-17.html), ML+X Forum.

**nilsmatteson@icloud.com** · [nilsmatteson.com](https://nilsmatteson.com) · [thaw.sh](https://thaw.sh) · [linkedin](https://www.linkedin.com/in/nilsmatteson)
