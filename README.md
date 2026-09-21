# BOB Agent Quantum Voxel Civilization

**IBM Bob 2.0 Hackathon** · September 25–27, 2026  
**Ahmad × Jessica (SnapKitty)**

---

## Live Frontend

**[https://snapkittywest.github.io/BOBS-Many-Voxel-Worlds/](https://snapkittywest.github.io/BOBS-Many-Voxel-Worlds/)**

Or run locally — no build step, no install:
```bash
cd voxel/frontend
node tools/static-server.mjs   # → http://localhost:4173
```

---

## What is built

### Bob (`quantum-world/bob_interface.py`)
LangChain ReAct agent backed by Claude (claude-3-5-sonnet-20241022). Falls back to a keyword wisdom database when LangChain is unavailable. Has 10 custom tools: `voxel_action`, `get_agent_state`, `spawn_agent`, `broadcast_gossip`, `trade_resources`, `form_alliance`, `coordinate_action`, `get_voxel_state`, `mine_voxel`, `build_voxel`. Tracks emotional state (curious/proud/concerned/joyful/contemplative) and updates on each observation.

### Five agents (`quantum-world/agents/cognition.py`)
Spawned at startup in `main.py`. Each has a role, LISP core string, and a Perception → Plan → Execute loop. LISP is interpreted by a minimal interpreter — not compiled. Quantum signature via blake2b.

| Agent | Role | LISP core |
|---|---|---|
| Alice | BUILDER | `(define purpose (lambda () (build (find-empty-space))))` |
| Charlie | EXPLORER | `(define purpose (lambda () (explore (find-unknown))))` |
| Diana | PHILOSOPHER | `(define purpose (lambda () (contemplate (observe-self))))` |
| Eve | SCIENTIST | `(define purpose (lambda () (experiment (hypothesize))))` |
| Frank | ARTIST | `(define purpose (lambda () (create (find-harmony))))` |

### AOQD (`quantum-world/aoqd/algorithm.py`)
Arothmatic-Ohr Quantum Decoding. Reduces quantum state tomography from O(3ⁿ) to O(k log k) shots. Pipeline: voxelise geometry → build entanglement graph (NetworkX) → sample high-degree qubits → sparse recovery (ℓ₁ via lstsq) → QAOA energy optimisation (gradient descent).

### Quantum life engine (`quantum-world/engine/quantum_life_engine.py`)
Based on Scientific Reports 8, 14793 (2018). Agents represented as density matrices. Lindblad dissipation: `dρ/dt = -i[H,ρ] + γ(LρL† - ½{L†L,ρ})`, jump operator L = |0⟩⟨1|. Partial cloning via CNOT. Four-qubit mating circuit. Runs on Qiskit Aer (classical simulation — no QPU).

### Rust voxel engine (`sovereign-voxel-civilization/`)
1024×256×1024 sparse voxel octree. Entropy hard-capped at H ≤ 0.20 nats. Three agent roles (Pioneer / Architect / Sentinel) with full POMDP belief states. Builds and passes `cargo test`.

Key modules:
- `world/octree.rs` — sparse octree, SHA-3 voxel hashes
- `agents/agent.rs` — Jordan-gated hidden state update: `gate = sigmoid(h+e), update = tanh(h+e), h = gate*update`
- `pipeline/execution.rs` — 5-stage pipeline + NAND safety kernel + TrustDeed boundary checks
- `reasoning/gumbel_softmax.rs` — temperature-annealed action selection
- `hazards/minefield.rs` — adaptive density redistribution via Metropolis-Hastings simulated annealing
- `ledger/state_ledger.rs` — Ed25519 + SHA-3 + Merkle WORM ledger with deterministic replay
- `perception/raycasting.rs` — DDA 3D raycasting, 32×24 frustum

### NASM assembly bridge (`assembly/quantum_nasm_bridge.asm`)
301 lines of x86-64 NASM. Implements: `init_genotype` (|ψ⟩ = cos(θ/2)|0⟩ + sin(θ/2)|1⟩), `compute_sigma_z` (⟨σ_z⟩ = cos θ), `lindblad_step` (Lindblad dissipation), `partial_clone` (CNOT entanglement), `apply_mutation` (Rz rotation), `four_qubit_mate` (offspring θ = (θ₁+θ₂)/2). Taylor series cos/sin approximations.

### Voxel frontend (`voxel/frontend/`)
Vanilla JS + Three.js via importmaps. No build step. 15 digital twin agents (Pioneer/Architect/Sentinel), 13 material types, select/place/remove interaction modes, localStorage save/load, raycasting pick, instanced mesh rendering. Agent mesh is a SnapKitty cat humanoid (torso/head/ears/eyes/legs built from BoxGeometry).

### QIR pipeline (`guppy/`, `quipper/`, `yao_jl/`, `ir/`, `voxel/emitter/`)
Three independent quantum circuit frontends (Python/Guppy, Haskell/Quipper, Julia/Yao.jl) all lower to a shared QIR JSON schema (`ir/quantum_ir_schema.json`). The voxel emitter (`voxel/emitter/qir_to_vox.py`) converts QIR to MagicaVoxel `.vox` binary. 34/34 emitter tests pass. All three Bell state QIRs produce identical 5-voxel output.

### MQS substrate (`mqs/`)
Rust: Growth Hamiltonian (Fibonacci/Ising/ToricCode anyon models), ER bridge (GJW traversability, modular Hamiltonian, effective distance = 0 for EPR pairs). Haskell: braid monad, ER-EPR geometry (Ryu-Takayanagi throat area, modular flow). Coq: topological protection theorems. Prolog: audit rules.

### Formal verification
- `formal/SparseVoxelEncoding.lean` — Lean 4, zero-sorry core: proves coupon-collector shot bound O(A log A), noise-free recall, noisy shot bound, deterministic artifact verification
- `mqs/coq/MQS/TopologicalProtection.v` — Coq: topological protection, fidelity limit, ER=EPR (some real-analysis lemmas admitted)

---

## What is NOT connected

Per `VOXEL_FRONTEND_INTEGRATION_HANDOFF.md`: the Python simulation and Rust engine run as **separate processes with no shared data format and no IPC**. The Three.js frontend uses hardcoded Bell state data — it does not poll the simulation. The Granite quantum compiler requires a ~8B parameter HuggingFace model download. All quantum operations are Qiskit Aer classical simulation — no QPU anywhere.

---

## Run

```bash
# Python simulation + Bob + agents
pip install -r requirements.txt
python quantum-world/main.py

# Rust engine
cd sovereign-voxel-civilization
cargo run --release --bin simulator 1000

# Assembly
cd assembly && make

# Frontend
cd voxel/frontend && node tools/static-server.mjs

# Guppy tests
cd guppy && python -m pytest tests/ -v

# Voxel emitter tests
cd voxel/emitter && python -m pytest tests/ -v
```

---

## Bob 2.0 session docs

`/bob-sessions/` · `/screenshots/`

Built for IBM Bob 2.0 Hackathon · SnapKitty · September 2026
