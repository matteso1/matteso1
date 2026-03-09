### Nils Matteson

Senior @ UW-Madison, CS + Data Science. I work on ML reliability (uncertainty quantification, OOD detection, conformal prediction) and mess around with systems/security stuff on the side.

Some things I've built:

- [**ProjectGorgon**](https://github.com/matteso1/ProjectGorgon) — speculative decoding for Llama-3-8B w/ custom CUDA kernels. Taught myself GPU programming for this.
- [**madison-bus-eta**](https://github.com/matteso1/madison-bus-eta) — live at [madisonbuseta.com](https://madisonbuseta.com). Real-time bus arrival predictions for all 29 Madison Metro routes. XGBoost on 47 features, Mondrian conformal prediction (90% coverage guarantee), nightly retraining w/ deployment gates, DeckGL map, bus bunching detection. 35% more accurate than the official API.
- [**KohakuRAG_UI**](https://github.com/matteso1/KohakuRAG_UI) — RAG system for AI sustainability Q&A, deployed on AWS Bedrock. Built for UW's [Research Cyberinfrastructure](https://it.wisc.edu/about/division-of-information-technology/research-cyberinfrastructure/) group.
- [**sentinel**](https://github.com/matteso1/sentinel) — Kafka-inspired distributed log streaming engine in Go. Custom LSM-tree storage, skip list memtable, Raft consensus, gRPC wire protocol. 1.7M ops/sec on the skip list.
- [**lockbox**](https://github.com/matteso1/lockbox) — zero-trust, air-gapped password manager. AES-256-GCM + Argon2id, TOTP 2FA, compiles to a single .exe. No cloud, no telemetry, no network calls.

Talk: [Deploying RAG in Bedrock vs. Local](https://uw-madison-datascience.github.io/ML-X-Nexus/Applications/Videos/Forums/mlx_2026-02-17.html) — ML+X Forum, Feb 2026

Looking for ML engineering / applied research roles. [site](https://nilsmatteson.com) · [linkedin](https://linkedin.com/in/nilsmatteson)
