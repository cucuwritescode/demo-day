---
layout: default
---

# Structured Pruning of Feedback Delay Networks

<p class="subtitle">Supplemental audio examples comparing dense (trained) FDN reverbs against their staged projections. The staged version is computationally cheaper while preserving acoustic quality.</p>

<hr class="section-divider">

## Benchmark Results

Compiled C++ with ARM NEON intrinsics on Apple M-series, vs Apple Accelerate BLAS. Layer count *L* chosen per-*N* by listening test.

| N | L | &sigma;<sub>&rho;</sub> dense | &sigma;<sub>&rho;</sub> staged | t<sub>mix</sub> dense | t<sub>mix</sub> staged | LSD (dB) | Speedup |
|---|---|---|---|---|---|---|---|
| 4 | 8 | 3.0 dB | 3.0 dB | 1325 ms | 1325 ms | 0.00 | 17.4&times; |
| 8 | 6 | 6.8 dB | 6.8 dB | 205 ms | 205 ms | 0.90 | 2.5&times; |
| 16 | 4 | 8.2 dB | 8.0 dB | 125 ms | 175 ms | 2.46 | 3.6&times; |
| 32 | 10 | 7.1 dB | 7.8 dB | 305 ms | 305 ms | 0.11 | 1.2&times; |
| 64 | 3 | 7.8 dB | 7.8 dB | 85 ms | 65 ms | 4.25 | 6.9&times; |
| 128 | 6 | 9.0 dB | 8.3 dB | 105 ms | 135 ms | 2.04 | 7.4&times; |
| 256 | &le;8 | 8.1 dB | 8.1 dB | 115 ms | 145 ms | 1.48 | &ge;10.5&times; |

<hr class="section-divider">

## Impulse Responses

<div class="audio-section">
<h3>N = 16, L = 4 <span class="speed-badge">3.6&times; faster</span></h3>
<div class="audio-grid">
  <div class="audio-card">
    <div class="card-label">Dense (trained)</div>
    <audio controls><source src="audio/IR_N16_dense.wav" type="audio/wav"></audio>
  </div>
  <div class="audio-card">
    <div class="card-label">Staged (projected)</div>
    <audio controls><source src="audio/IR_N16_L4.wav" type="audio/wav"></audio>
  </div>
</div>
</div>

<div class="audio-section">
<h3>N = 64, L = 3 <span class="speed-badge">6.9&times; faster</span></h3>
<div class="audio-grid">
  <div class="audio-card">
    <div class="card-label">Dense (trained)</div>
    <audio controls><source src="audio/IR_N64_dense.wav" type="audio/wav"></audio>
  </div>
  <div class="audio-card">
    <div class="card-label">Staged (projected)</div>
    <audio controls><source src="audio/IR_N64_L3.wav" type="audio/wav"></audio>
  </div>
</div>
</div>

<hr class="section-divider">

## Convolved Examples &mdash; N = 16, L = 4 <span class="speed-badge">3.6&times;</span>

<div class="audio-section">
<h3><img src="pngs/voice_icon.png" alt="singing"> Singing</h3>
<div class="audio-grid">
  <div class="audio-card dry">
    <div class="card-label">Dry</div>
    <audio controls><source src="audio/singing_dry.wav" type="audio/wav"></audio>
  </div>
  <div class="audio-card">
    <div class="card-label">Dense (trained)</div>
    <audio controls><source src="audio/singing_N16_dense.wav" type="audio/wav"></audio>
  </div>
  <div class="audio-card">
    <div class="card-label">Staged (projected)</div>
    <audio controls><source src="audio/singing_N16_L4.wav" type="audio/wav"></audio>
  </div>
</div>
</div>

<div class="audio-section">
<h3><img src="pngs/drums_icon.png" alt="drums"> Drums</h3>
<div class="audio-grid">
  <div class="audio-card dry">
    <div class="card-label">Dry</div>
    <audio controls><source src="audio/drums_dry.wav" type="audio/wav"></audio>
  </div>
  <div class="audio-card">
    <div class="card-label">Dense (trained)</div>
    <audio controls><source src="audio/drums_N16_dense.wav" type="audio/wav"></audio>
  </div>
  <div class="audio-card">
    <div class="card-label">Staged (projected)</div>
    <audio controls><source src="audio/drums_N16_L4.wav" type="audio/wav"></audio>
  </div>
</div>
</div>

<div class="audio-section">
<h3><img src="pngs/orchestra_icon.png" alt="orchestral"> Orchestral</h3>
<div class="audio-grid">
  <div class="audio-card dry">
    <div class="card-label">Dry</div>
    <audio controls><source src="audio/13_Orchestral_dry.wav" type="audio/wav"></audio>
  </div>
  <div class="audio-card">
    <div class="card-label">Dense (trained)</div>
    <audio controls><source src="audio/13_Orchestral_N16_dense.wav" type="audio/wav"></audio>
  </div>
  <div class="audio-card">
    <div class="card-label">Staged (projected)</div>
    <audio controls><source src="audio/13_Orchestral_N16_L4.wav" type="audio/wav"></audio>
  </div>
</div>
</div>

<hr class="section-divider">

## Convolved Examples &mdash; N = 64, L = 3 <span class="speed-badge">6.9&times;</span>

<div class="audio-section">
<h3><img src="pngs/voice_icon.png" alt="singing"> Singing</h3>
<div class="audio-grid">
  <div class="audio-card">
    <div class="card-label">Dense (trained)</div>
    <audio controls><source src="audio/singing_N64_dense.wav" type="audio/wav"></audio>
  </div>
  <div class="audio-card">
    <div class="card-label">Staged (projected)</div>
    <audio controls><source src="audio/singing_N64_L3.wav" type="audio/wav"></audio>
  </div>
</div>
</div>

<div class="audio-section">
<h3><img src="pngs/drums_icon.png" alt="drums"> Drums</h3>
<div class="audio-grid">
  <div class="audio-card">
    <div class="card-label">Dense (trained)</div>
    <audio controls><source src="audio/drums_N64_dense.wav" type="audio/wav"></audio>
  </div>
  <div class="audio-card">
    <div class="card-label">Staged (projected)</div>
    <audio controls><source src="audio/drums_N64_L3.wav" type="audio/wav"></audio>
  </div>
</div>
</div>

<div class="audio-section">
<h3><img src="pngs/orchestra_icon.png" alt="orchestral"> Orchestral</h3>
<div class="audio-grid">
  <div class="audio-card">
    <div class="card-label">Dense (trained)</div>
    <audio controls><source src="audio/13_Orchestral_N64_dense.wav" type="audio/wav"></audio>
  </div>
  <div class="audio-card">
    <div class="card-label">Staged (projected)</div>
    <audio controls><source src="audio/13_Orchestral_N64_L3.wav" type="audio/wav"></audio>
  </div>
</div>
</div>
