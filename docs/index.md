---
layout: default
title: Structured Pruning of Feedback Delay Networks
---

# Supplemental Material

**Facundo Franchino** — University of York, 2026

Each pair compares a dense (trained) FDN reverb against its staged projection at the same channel count.

---

## Benchmark Results

Compiled C++ with ARM NEON intrinsics on Apple M-series, vs Apple Accelerate BLAS. Layer count *L* chosen per-*N* by listening test.

| N | L | σ_ρ dense (dB) | σ_ρ staged (dB) | t_mix dense (ms) | t_mix staged (ms) | LSD (dB) | Speedup |
|---|---|---|---|---|---|---|---|
| 4 | 8 | 3.0 | 3.0 | 1325 | 1325 | 0.00 | **17.4×** |
| 8 | 6 | 6.8 | 6.8 | 205 | 205 | 0.90 | **2.5×** |
| 16 | 4 | 8.2 | 8.0 | 125 | 175 | 2.46 | **3.6×** |
| 32 | 10 | 7.1 | 7.8 | 305 | 305 | 0.11 | **1.2×** |
| 64 | 3 | 7.8 | 7.8 | 85 | 65 | 4.25 | **6.9×** |
| 128 | 6 | 9.0 | 8.3 | 105 | 135 | 2.04 | **7.4×** |
| 256 | ≤8 | 8.1 | 8.1 | 115 | 145 | 1.48 | **≥10.5×** |

---

## Impulse Responses

### N = 16, L = 4

**Dense (trained)**
<audio controls>
  <source src="audio/IR_N16_dense.wav" type="audio/wav">
</audio>

**Staged (projected)**
<audio controls>
  <source src="audio/IR_N16_L4.wav" type="audio/wav">
</audio>

### N = 64, L = 3

**Dense (trained)**
<audio controls>
  <source src="audio/IR_N64_dense.wav" type="audio/wav">
</audio>

**Staged (projected)**
<audio controls>
  <source src="audio/IR_N64_L3.wav" type="audio/wav">
</audio>

---

## Convolved Examples — N = 16, L = 4 (3.6×)

### Singing

**Dry**
<audio controls>
  <source src="audio/singing_dry.wav" type="audio/wav">
</audio>

**Dense (trained)**
<audio controls>
  <source src="audio/singing_N16_dense.wav" type="audio/wav">
</audio>

**Staged (projected)**
<audio controls>
  <source src="audio/singing_N16_L4.wav" type="audio/wav">
</audio>

### Drums

**Dry**
<audio controls>
  <source src="audio/drums_dry.wav" type="audio/wav">
</audio>

**Dense (trained)**
<audio controls>
  <source src="audio/drums_N16_dense.wav" type="audio/wav">
</audio>

**Staged (projected)**
<audio controls>
  <source src="audio/drums_N16_L4.wav" type="audio/wav">
</audio>

### Orchestral

**Dry**
<audio controls>
  <source src="audio/13_Orchestral_dry.wav" type="audio/wav">
</audio>

**Dense (trained)**
<audio controls>
  <source src="audio/13_Orchestral_N16_dense.wav" type="audio/wav">
</audio>

**Staged (projected)**
<audio controls>
  <source src="audio/13_Orchestral_N16_L4.wav" type="audio/wav">
</audio>

---

## Convolved Examples — N = 64, L = 3 (6.9×)

### Singing

**Dense (trained)**
<audio controls>
  <source src="audio/singing_N64_dense.wav" type="audio/wav">
</audio>

**Staged (projected)**
<audio controls>
  <source src="audio/singing_N64_L3.wav" type="audio/wav">
</audio>

### Drums

**Dense (trained)**
<audio controls>
  <source src="audio/drums_N64_dense.wav" type="audio/wav">
</audio>

**Staged (projected)**
<audio controls>
  <source src="audio/drums_N64_L3.wav" type="audio/wav">
</audio>

### Orchestral

**Dense (trained)**
<audio controls>
  <source src="audio/13_Orchestral_N64_dense.wav" type="audio/wav">
</audio>

**Staged (projected)**
<audio controls>
  <source src="audio/13_Orchestral_N64_L3.wav" type="audio/wav">
</audio>
