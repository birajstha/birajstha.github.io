<script>
  import { onMount } from 'svelte';
  import { NEURO_FACTS } from '../lib/data.js';
  import { initEEGVisualization } from '../lib/eeg.js';

  let currentFactIndex = 0;
  let factTransitioning = false;

  function cycleFact() {
    if (factTransitioning) return;
    factTransitioning = true;
    setTimeout(() => {
      currentFactIndex = (currentFactIndex + 1) % NEURO_FACTS.length;
      factTransitioning = false;
    }, 400);
  }

  function jumpToFact(index) {
    currentFactIndex = index;
  }

  onMount(() => {
    initEEGVisualization('eeg-canvas');
    const interval = setInterval(cycleFact, 6000);
    return () => clearInterval(interval);
  });
</script>

<section id="experiment" class="section-alt">
  <div class="section-container">
    <div class="reveal"><span class="section-label">Live Lab</span></div>
    <div class="reveal-blur"><h2 class="section-title">Your Brain, Visualized</h2></div>
    <div class="reveal">
      <p class="max-w-2xl mb-8" style="color: var(--text-secondary);">
        A real-time simulated EEG waveform. Each channel represents a different frequency band
        — from delta (1.5 Hz) to beta (20 Hz) — with noise and harmonic coupling,
        just like real neural signals.
      </p>
    </div>

    <div class="grid md:grid-cols-2 gap-8 mt-6">
      <div class="glass-card reveal" style="transition-delay: 100ms; padding: 12px;">
        <canvas id="eeg-canvas"></canvas>
      </div>

      <div class="glass-card reveal flex flex-col justify-center" style="transition-delay: 300ms;">
        <div class="flex items-center gap-2 mb-3">
          <span style="width: 8px; height: 8px; border-radius: 50%; background: #22c55e; display: inline-block;"></span>
          <span class="text-sm" style="color: var(--text-muted);">Neuron fact — refreshing every 6s</span>
        </div>
        <div class="fact-fade-in">
          <p class="text-lg font-medium italic">"{NEURO_FACTS[currentFactIndex]}"</p>
        </div>
        <div class="flex gap-1.5 mt-4">
          {#each NEURO_FACTS as _, i}
            <button
              onclick={() => jumpToFact(i)}
              style="width: 8px; height: 8px; border-radius: 50%; border: none; cursor: pointer;
                     background: {i === currentFactIndex ? 'var(--accent)' : 'var(--border)'};
                     transition: background 0.3s;"
              aria-label="Fact {i + 1}"
            ></button>
          {/each}
        </div>
      </div>
    </div>
  </div>
</section>