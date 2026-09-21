# BOB Agent Quantum Voxel Civilization

**IBM Bob 2.0 Hackathon 2026** · September 25–27 · $10,000 prize pool  
**Authors:** Ahmad × Jessica (SnapKitty)

> Autonomous agents live, build, and survive across a 3D quantum voxel world.  
> Every decision is cryptographically sealed. Every belief state is verifiable. Every lie gets caught.

---

## Live Frontend

**[https://snapkittywest.github.io/BOBS-Many-Voxel-Worlds/](https://snapkittywest.github.io/BOBS-Many-Voxel-Worlds/)**

Or run locally — no build step:
```bash
cd voxel/frontend
node tools/static-server.mjs    # → http://localhost:3000
```

---

## What This Is

A 1024×256×1024 voxel world running a sovereign multi-agent simulation with four integrated layers:

```
┌─────────────────────────────────────────────────────┐
│  LAYER 4: Agent Orchestration                       │
│  Birth / growth / death / learning / WORM ledger    │
├─────────────────────────────────────────────────────┤
│  LAYER 3: AOQD Quantum Biomimetic Engine            │
│  ∂ρ/∂t = -i[H,ρ] + Γ·L[ρ]  ·  H ≤ 0.20 nats      │
├─────────────────────────────────────────────────────┤
│  LAYER 2: IBM Granite LLM Cognition                 │
│  Granite 8B/34B via Bedrock · vLLM offline fallback │
├─────────────────────────────────────────────────────┤
│  LAYER 1: NASM x86-64 Gate Kernel                   │
│  Hadamard/CNOT/Rx/Rz → SSE/AVX2 · 100× over Python │
└─────────────────────────────────────────────────────┘
```

**Three agent types** — Pioneer, Architect, Sentinel — emerge from identical POMDP base class + role-specific reward shaping. Every decision flows:

```
Jordan-gated transition → NAND safety filter → Gumbel-Softmax selection → Blake3 seal → WORM append
```

If an agent lies about its belief state, Ed25519 + Blake3 cryptographic verification catches it with probability 1 − 2⁻²⁵⁶.

---

## Novel Contributions

Full writeup: [NOVEL_CONTRIBUTIONS.md](NOVEL_CONTRIBUTIONS.md)

1. **Cryptographically-Sealed POMDP** — Decentralized multi-agent POMDPs where every belief-state update is WORM-sealed with Blake3 + Ed25519. O(1) Byzantine verification vs O(N) consensus rounds.

2. **Dynamic Hazard Matrix Physics** — Adaptive minefields redistributing threat density via simulated annealing in response to multi-agent activity gradients. Emergent swarm evasion without explicit coordination.

3. **Jordan-Gated Discrete Action Selection** — Extension of continuous Jordan-form transitions to discrete action spaces via Gumbel-Softmax with NAND safety-kernel filtering and trust-deed verification.

4. **Three-Role Emergent Specialization** — Pioneer/Architect/Sentinel morphologies emerging from identical base class + reward shaping. Validated over 50+ hour simulations.

---

## Stack

| Layer | Technology | Location |
|---|---|---|
| Frontend | Three.js · vanilla JS · importmaps | `voxel/frontend/` |
| Quantum simulation | Python · AOQD · NumPy/SciPy | `quantum-world/` |
| Voxel engine | Rust · POMDP · Ed25519 + Blake3 | `sovereign-voxel-civilization/` |
| LLM cognition | IBM Granite 8B/34B via Bedrock | `quantum-world/engine/granite_quantum_compiler.py` |
| Assembly bridge | NASM x86-64 SSE/AVX2 | `assembly/quantum_nasm_bridge.asm` |
| Quantum circuits | Guppy · Quipper · Yao.jl | `guppy/` · `quipper/` · `yao_jl/` |
| IR | Haskell | `ir/` |
| Formal verification | Lean 4 · Coq | `formal/` · `mqs/coq/` |
| Topological protection | Rust MQS substrate | `mqs/crates/` |

---

## Quickstart

```bash
# 1. Python quantum simulation
pip install -r requirements.txt
python quantum-world/main.py

# 2. Rust voxel engine
cd sovereign-voxel-civilization
cargo run --release --bin simulator 1000

# 3. Assembly bridge
cd assembly && make

# 4. Frontend — open in browser
open voxel/frontend/index.html
```

Full setup: [QUICKSTART.md](QUICKSTART.md)

---

## Agent Characters

| Agent | Role | LISP Core |
|---|---|---|
| Alice | Builder / Architect | `(define purpose (lambda () (build (find-empty-space))))` |
| Charlie | Explorer / Pioneer | `(define purpose (lambda () (explore (find-unknown))))` |
| Diana | Philosopher | `(define purpose (lambda () (contemplate (observe-self))))` |
| Eve | Scientist / Sentinel | `(define purpose (lambda () (experiment (hypothesize))))` |
| Frank | Artist | `(define purpose (lambda () (create (find-harmony))))` |

---

## Bob 2.0 Sessions

Session documentation: [bob-sessions/](bob-sessions/)  
Screenshots: [screenshots/](screenshots/)

---

## Formal Foundations

- `formal/SparseVoxelEncoding.lean` — Lean 4 proof: coupon-collector shot bound O(A log A) for A-atom reconstruction under H ≤ 0.20 nats
- `mqs/coq/MQS/TopologicalProtection.v` — Coq proof of topological protection
- `ir/quantum_ir_schema.json` — Canonical quantum IR schema (Haskell-derived)

---

## Submission

[SUBMISSION.md](SUBMISSION.md) · [NOVEL_CONTRIBUTIONS.md](NOVEL_CONTRIBUTIONS.md) · [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)

Built with IBM Bob 2.0 · SnapKitty · September 2026
