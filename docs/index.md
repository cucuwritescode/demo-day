---
layout: default
---

# Structured Pruning of Feedback Delay Networks

**Facundo Franchino** — University of York, 2026

Supplemental audio examples. Each pair compares a dense (trained) FDN reverb against its staged projection at the same channel count. The staged version is computationally cheaper while preserving acoustic quality.

---

## Benchmark Results

Compiled C++ with ARM NEON intrinsics on Apple M-series, vs Apple Accelerate BLAS. Layer count *L* chosen per-*N* by listening test.

| N | L | &sigma;<sub>&rho;</sub> dense (dB) | &sigma;<sub>&rho;</sub> staged (dB) | t<sub>mix</sub> dense (ms) | t<sub>mix</sub> staged (ms) | LSD (dB) | Speedup vs BLAS |
|---|---|---|---|---|---|---|---|
| 4 | 8 | 3.0 | 3.0 | 1325 | 1325 | 0.00 | 17.4&times; |
| 8 | 6 | 6.8 | 6.8 | 205 | 205 | 0.90 | 2.5&times; |
| 16 | 4 | 8.2 | 8.0 | 125 | 175 | 2.46 | 3.6&times; |
| 32 | 10 | 7.1 | 7.8 | 305 | 305 | 0.11 | 1.2&times; |
| 64 | 3 | 7.8 | 7.8 | 85 | 65 | 4.25 | 6.9&times; |
| 128 | 6 | 9.0 | 8.3 | 105 | 135 | 2.04 | 7.4&times; |
| 256 | &le;8 | 8.1 | 8.1 | 115 | 145 | 1.48 | &ge;10.5&times; |

---

## Impulse Responses

### N = 16, L = 4

**Dense (trained)**
<audio controls><source src="audio/IR_N16_dense.wav" type="audio/wav"></audio>

**Staged (projected)**
<audio controls><source src="audio/IR_N16_L4.wav" type="audio/wav"></audio>

### N = 64, L = 3

**Dense (trained)**
<audio controls><source src="audio/IR_N64_dense.wav" type="audio/wav"></audio>

**Staged (projected)**
<audio controls><source src="audio/IR_N64_L3.wav" type="audio/wav"></audio>

---

## Convolved Examples — N = 16, L = 4 (3.6&times;)

### Singing

**Dry**
<audio controls><source src="audio/singing_dry.wav" type="audio/wav"></audio>

**Dense (trained)**
<audio controls><source src="audio/singing_N16_dense.wav" type="audio/wav"></audio>

**Staged (projected)**
<audio controls><source src="audio/singing_N16_L4.wav" type="audio/wav"></audio>

### Drums

**Dry**
<audio controls><source src="audio/drums_dry.wav" type="audio/wav"></audio>

**Dense (trained)**
<audio controls><source src="audio/drums_N16_dense.wav" type="audio/wav"></audio>

**Staged (projected)**
<audio controls><source src="audio/drums_N16_L4.wav" type="audio/wav"></audio>

### Orchestral

**Dry**
<audio controls><source src="audio/13_Orchestral_dry.wav" type="audio/wav"></audio>

**Dense (trained)**
<audio controls><source src="audio/13_Orchestral_N16_dense.wav" type="audio/wav"></audio>

**Staged (projected)**
<audio controls><source src="audio/13_Orchestral_N16_L4.wav" type="audio/wav"></audio>

---

## Convolved Examples — N = 64, L = 3 (6.9&times;)

### Singing

**Dense (trained)**
<audio controls><source src="audio/singing_N64_dense.wav" type="audio/wav"></audio>

**Staged (projected)**
<audio controls><source src="audio/singing_N64_L3.wav" type="audio/wav"></audio>

### Drums

**Dense (trained)**
<audio controls><source src="audio/drums_N64_dense.wav" type="audio/wav"></audio>

**Staged (projected)**
<audio controls><source src="audio/drums_N64_L3.wav" type="audio/wav"></audio>

### Orchestral

**Dense (trained)**
<audio controls><source src="audio/13_Orchestral_N64_dense.wav" type="audio/wav"></audio>

**Staged (projected)**
<audio controls><source src="audio/13_Orchestral_N64_L3.wav" type="audio/wav"></audio>
