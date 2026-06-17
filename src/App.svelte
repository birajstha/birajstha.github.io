<script>
  import { onMount } from 'svelte';
  import { getInitialTheme, applyTheme, persistTheme, toggleTheme as getToggled } from './lib/theme.js';
  import { initRevealAnimations, initScrollProgress, initTiltCards } from './lib/reveal.js';
  import { initParticleBackground } from './lib/particles.js';
  import Navbar from './components/Navbar.svelte';
  import Hero from './components/Hero.svelte';
  import About from './components/About.svelte';
  import Skills from './components/Skills.svelte';
  import Experience from './components/Experience.svelte';
  import Projects from './components/Projects.svelte';
  import LiveLab from './components/LiveLab.svelte';
  import Publications from './components/Publications.svelte';
  import Contact from './components/Contact.svelte';
  import Footer from './components/Footer.svelte';

  let theme = 'dark';
  let mobileOpen = false;
  let scrollY = 0;

  function handleThemeToggle() {
    theme = getToggled(theme);
    applyTheme(theme);
    persistTheme(theme);
  }

  function handleMobileToggle() {
    mobileOpen = !mobileOpen;
  }

  function handleNavigate(href) {
    mobileOpen = false;
    const el = document.querySelector(href);
    if (el) el.scrollIntoView({ behavior: 'smooth' });
  }

  onMount(() => {
    theme = getInitialTheme();
    applyTheme(theme);

    function onScroll() {
      scrollY = window.scrollY;
    }
    window.addEventListener('scroll', onScroll, { passive: true });

    setTimeout(() => {
      initScrollProgress();
      initRevealAnimations();
      initTiltCards();
    }, 100);

    initParticleBackground('bg-canvas', () => scrollY);
  });
</script>

<div class="scroll-progress"></div>
<canvas id="bg-canvas"></canvas>

<Navbar
  {theme}
  onToggleTheme={handleThemeToggle}
  {mobileOpen}
  onToggleMobile={handleMobileToggle}
  onNavigate={handleNavigate}
/>

<div class="content-wrapper">
  <Hero onNavigate={handleNavigate} />
  <About />
  <Skills />
  <Experience />
  <Projects />
  <LiveLab />
  <Publications />
  <Contact />
  <Footer />
</div>