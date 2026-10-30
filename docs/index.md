---
layout: default
---

# Structured Pruning of Feedback Delay Networks

<p class="subtitle">A perceptually lossless pruning algorithm for Feedback Delay Networks (FDNs).</p>

<p><a href="https://github.com/cucuwritescode/fdn_pruning">Code on GitHub</a> &middot; paper on arXiv soon</p>

<hr class="section-divider">

## Background

### Feedback Delay Networks
- FDN's are recursive filters used for artificial reverb and decorrelation.
- Amongst other methods to synthesise reverberation, FDN's are particularly efficient computationally, nonetheless their time complexity is <em>O</em>(<em>N</em><sup>2</sup>).

Here's a 4x4 FDN:

![4x4 FDN diagram](pngs/fig_fdn.svg)

As shown, they consist of a set of delays and a feedback matrix through which the delay outputs are coupled to the delay inputs. The highlighted feedback matrix is the only part we touch.

### The ideal FDN triad

This paper formalises a threefold trade-off that's featured on this line of research since its early days.

![The ideal FDN triad](pngs/fig_triad.svg)

As shown on the diagram, known structures don't fully satisfy all three requirements simultaneously. This work flips the design approach of FDN's from a "ground-up" to a "top to bottom" perspective:

> What if we start from a differentiable (trained), nice-sounding, dense FDN and try to prune it without losing perceptual/acoustic quality, instead of designing it with the lowest possible N&times;N feedback matrix?

<hr class="section-divider">

## Method

The dense feedback matrix is replaced by a few stages of fixed routing and small orthogonal blocks, fitted in two phases:

- **Matrix fitting.** Match the dense matrix entry by entry; each small block has an exact closed-form update.
- **Response refinement.** Adjust all blocks jointly so the complete reverberator's magnitude response matches the dense one.

![Two-phase projection pipeline](pngs/fig_pipeline.svg)

Every stage is orthogonal by construction, so the pruned FDN preserves energy exactly, at every step of the optimisation. Delays, gains and attenuation stay fixed; only the mixing changes.

<hr class="section-divider">

## Benchmark Results

Compiled C++ with ARM NEON intrinsics on Apple M2, vs Apple Accelerate BLAS (SGEMV). Labels give speedups over isolated-call dense BLAS; staged times are measured in blocks of 512 calls.

![Runtime performance](pngs/fig_runtime.svg)

The fastest benchmarked kernels use radix-4 at *N* = 16, 32, 64, 128 and pairwise stages at *N* = 256. At *N* = 256, coefficient storage falls from 65,536 to 768 floats.

<hr class="section-divider">

## Impulse Responses

<div class="audio-section">
<h3>N = 64, radix-4, L = 2 <span class="speed-badge">13.7&times; faster</span></h3>
<div class="audio-grid">
  <div class="audio-card">
    <div class="card-label">Dense (trained)</div>
    <audio controls preload="none"><source src="audio/IR_N64_dense.wav" type="audio/wav"></audio>
  </div>
  <div class="audio-card">
    <div class="card-label">Radix-4 (projected)</div>
    <audio controls preload="none"><source src="audio/IR_N64_radix4_L2.wav" type="audio/wav"></audio>
  </div>
</div>
</div>

<p>Our staged 64&times;64 feedback matrix runs in 18.2 ns per sample, cheaper than a dense 16&times;16 feedback matrix (39.1 ns).</p>

<div class="audio-section">
<h3>N = 128, pairwise, L = 3 <span class="speed-badge">14.1&times; faster</span></h3>
<div class="audio-grid">
  <div class="audio-card">
    <div class="card-label">Dense (trained)</div>
    <audio controls preload="none"><source src="audio/IR_N128_dense.wav" type="audio/wav"></audio>
  </div>
  <div class="audio-card">
    <div class="card-label">Pairwise (projected)</div>
    <audio controls preload="none"><source src="audio/IR_N128_pairwise_L3.wav" type="audio/wav"></audio>
  </div>
</div>
</div>

<p>Our staged 128&times;128 feedback matrix runs in 44.4 ns per sample, cheaper than a dense 32&times;32 feedback matrix (71.0 ns).</p>


<hr class="section-divider">

## Convolved Examples &mdash; N = 64, radix-4, L = 2 <span class="speed-badge">13.7&times;</span>

<div class="audio-section">
<h3><img src="pngs/voice_icon.png" alt="singing"> Singing</h3>
<div class="audio-grid">
  <div class="audio-card dry">
    <div class="card-label">Dry</div>
    <audio controls preload="none"><source src="audio/singing_dry.wav" type="audio/wav"></audio>
  </div>
  <div class="audio-card">
    <div class="card-label">Dense (trained)</div>
    <audio controls preload="none"><source src="audio/singing_N64_dense.wav" type="audio/wav"></audio>
  </div>
  <div class="audio-card">
    <div class="card-label">Radix-4 (projected)</div>
    <audio controls preload="none"><source src="audio/singing_N64_radix4_L2.wav" type="audio/wav"></audio>
  </div>
</div>
</div>

<div class="audio-section">
<h3><img src="pngs/drums_icon.png" alt="drums"> Drums</h3>
<div class="audio-grid">
  <div class="audio-card dry">
    <div class="card-label">Dry</div>
    <audio controls preload="none"><source src="audio/drums_dry.wav" type="audio/wav"></audio>
  </div>
  <div class="audio-card">
    <div class="card-label">Dense (trained)</div>
    <audio controls preload="none"><source src="audio/drums_N64_dense.wav" type="audio/wav"></audio>
  </div>
  <div class="audio-card">
    <div class="card-label">Radix-4 (projected)</div>
    <audio controls preload="none"><source src="audio/drums_N64_radix4_L2.wav" type="audio/wav"></audio>
  </div>
</div>
</div>

<div class="audio-section">
<h3><img src="pngs/orchestra_icon.png" alt="orchestral"> Orchestral</h3>
<div class="audio-grid">
  <div class="audio-card dry">
    <div class="card-label">Dry</div>
    <audio controls preload="none"><source src="audio/13_Orchestral_dry.wav" type="audio/wav"></audio>
  </div>
  <div class="audio-card">
    <div class="card-label">Dense (trained)</div>
    <audio controls preload="none"><source src="audio/13_Orchestral_N64_dense.wav" type="audio/wav"></audio>
  </div>
  <div class="audio-card">
    <div class="card-label">Radix-4 (projected)</div>
    <audio controls preload="none"><source src="audio/13_Orchestral_N64_radix4_L2.wav" type="audio/wav"></audio>
  </div>
</div>
</div>

<hr class="section-divider">

## Convolved Examples &mdash; N = 128, pairwise, L = 3 <span class="speed-badge">14.1&times;</span>

<div class="audio-section">
<h3><img src="pngs/voice_icon.png" alt="singing"> Singing</h3>
<div class="audio-grid">
  <div class="audio-card">
    <div class="card-label">Dense (trained)</div>
    <audio controls preload="none"><source src="audio/singing_N128_dense.wav" type="audio/wav"></audio>
  </div>
  <div class="audio-card">
    <div class="card-label">Pairwise (projected)</div>
    <audio controls preload="none"><source src="audio/singing_N128_pairwise_L3.wav" type="audio/wav"></audio>
  </div>
</div>
</div>

<div class="audio-section">
<h3><img src="pngs/drums_icon.png" alt="drums"> Drums</h3>
<div class="audio-grid">
  <div class="audio-card">
    <div class="card-label">Dense (trained)</div>
    <audio controls preload="none"><source src="audio/drums_N128_dense.wav" type="audio/wav"></audio>
  </div>
  <div class="audio-card">
    <div class="card-label">Pairwise (projected)</div>
    <audio controls preload="none"><source src="audio/drums_N128_pairwise_L3.wav" type="audio/wav"></audio>
  </div>
</div>
</div>

<div class="audio-section">
<h3><img src="pngs/orchestra_icon.png" alt="orchestral"> Orchestral</h3>
<div class="audio-grid">
  <div class="audio-card">
    <div class="card-label">Dense (trained)</div>
    <audio controls preload="none"><source src="audio/13_Orchestral_N128_dense.wav" type="audio/wav"></audio>
  </div>
  <div class="audio-card">
    <div class="card-label">Pairwise (projected)</div>
    <audio controls preload="none"><source src="audio/13_Orchestral_N128_pairwise_L3.wav" type="audio/wav"></audio>
  </div>
</div>
</div>

<hr class="section-divider">

## Conclusions

We propose a new paradigm for FDN design. Rather than starting with a small structure and trying to make it sound good, we begin with the desired acoustic behaviour and make its implementation cheaper. Our results show that dense designs can be substantially simplified while closely preserving their sound, offering a practical route towards the ideal FDN triad of colourlessness, smoothness and low computational cost.
