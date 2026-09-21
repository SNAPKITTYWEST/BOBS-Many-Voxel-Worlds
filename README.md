# BOB Agent Quantum Voxel Civilization

**IBM Bob 2.0 Hackathon 2026** · Sovereign multi-agent simulation across a 3D quantum voxel world.

---

## Live Frontend

Open `voxel/frontend/index.html` directly in any browser — no build step, no install.

Or serve locally:
```bash
cd voxel/frontend
node tools/static-server.mjs
# → http://localhost:3000
```

---

## What it is

A 1024×256×1024 voxel world. Three agent types — **Pioneer**, **Architect**, **Sentinel** — each with their own reasoning loop, perception, and reward signal.

- Every agent decision flows through: Jordan-gated transitions → NAND safety filter → Gumbel-Softmax selection
- Every state change is signed and appended to a WORM ledger
- Entropy bound H ≤ 0.20 nats enforced at the pipeline gate — not a soft limit
- Adaptive minefields shift based on agent path history
- NASM bridge compiles gate sequences to x86-64 SIMD — 100× faster than Python for the inner gate loop

---

## Stack

| Layer | Technology |
|---|---|
| Quantum simulation | Python — `quantum-world/` |
| Voxel engine | Rust — `sovereign-voxel-civilization/` |
| Assembly bridge | NASM x86-64 — `assembly/` |
| Frontend | Three.js (vanilla JS, importmaps) — `voxel/frontend/` |
| Formal verification | Lean 4 — `formal/` |
| IR | Haskell — `ir/` |
| Quantum circuits | Guppy — `guppy/`, Quipper — `quipper/`, Yao.jl — `yao_jl/` |
| Topological protection | Coq — `mqs/coq/` |

---

## Run

**Frontend (browser — no install):**
```bash
open voxel/frontend/index.html
```

**Python quantum simulation:**
```bash
pip install -r requirements.txt
python quantum-world/main.py
```

**Rust voxel engine:**
```bash
cd sovereign-voxel-civilization
cargo run --release --bin simulator 1000
```

**Assembly bridge:**
```bash
cd assembly
make
```

---

## Architecture

```
Python Quantum Sim          Rust Voxel Engine
(quantum-world/)            (sovereign-voxel-civilization/)
        │                           │
        └──────── JSON export ──────┘
                      │
               Three.js Frontend
               (voxel/frontend/)
```

The frontend loads world state from `simulation_state.json` when present, or runs with built-in sample data.

---

## Formal foundations

- `formal/SparseVoxelEncoding.lean` — Lean 4 proof of coupon-collector shot bound O(A log A)
- `mqs/coq/MQS/TopologicalProtection.v` — Coq proof of topological protection
- `ir/quantum_ir_schema.json` — Canonical quantum IR schema

---

## Novel contributions

See [NOVEL_CONTRIBUTIONS.md](NOVEL_CONTRIBUTIONS.md) and [SUBMISSION.md](SUBMISSION.md).

Built for **IBM Bob 2.0 Hackathon** · September 25–27, 2026
