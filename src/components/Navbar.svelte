<script>
  import { NAV_ITEMS, PERSONAL_INFO } from '../lib/data.js';

  export let theme = 'dark';
  export let mobileOpen = false;
  export let onToggleTheme = () => {};
  export let onToggleMobile = () => {};
  export let onNavigate = () => {};

  function scrollTo(href) {
    onNavigate(href);
  }
</script>

{#if mobileOpen}
  <div
    class="mobile-overlay open"
    role="button"
    tabindex="-1"
    onclick={() => onToggleMobile()}
    onkeydown={(e) => e.key === 'Enter' && onToggleMobile()}
  ></div>
{/if}

<nav class="mobile-nav {mobileOpen ? 'open' : ''}">
  <div class="flex flex-col gap-6">
    {#each NAV_ITEMS as item}
      <button class="nav-link text-lg" onclick={() => scrollTo(item.href)}>{item.label}</button>
    {/each}
    <hr style="border-color: var(--border); margin: 8px 0" />
    <a href={PERSONAL_INFO.evanietech} target="_blank" rel="noopener noreferrer" class="nav-link text-lg">
      evanietech.com ↗
    </a>
  </div>
</nav>

<header class="navbar">
  <div class="max-w-[1200px] mx-auto px-6 h-16 flex items-center justify-between">
    <button
      class="text-xl font-bold tracking-tight gradient-text"
      style="cursor:pointer;background:none;border:none"
      onclick={() => scrollTo('#hero')}
    >
      BIRAJ
    </button>

    <div class="navbar-desktop flex items-center gap-8">
      {#each NAV_ITEMS as item}
        <button class="nav-link" onclick={() => scrollTo(item.href)}>{item.label}</button>
      {/each}
      <a
        href={PERSONAL_INFO.evanietech}
        target="_blank"
        rel="noopener noreferrer"
        class="nav-link inline-flex items-center gap-1"
      >
        evanietech <span class="text-xs">↗</span>
      </a>
    </div>

    <div class="flex items-center gap-3">
      <button class="theme-toggle" onclick={onToggleTheme} aria-label="Toggle theme">
        {#if theme === 'dark'}
          <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round">
            <circle cx="12" cy="12" r="5"/><line x1="12" y1="1" x2="12" y2="3"/><line x1="12" y1="21" x2="12" y2="23"/>
            <line x1="4.22" y1="4.22" x2="5.64" y2="5.64"/><line x1="18.36" y1="18.36" x2="19.78" y2="19.78"/>
            <line x1="1" y1="12" x2="3" y2="12"/><line x1="21" y1="12" x2="23" y2="12"/>
            <line x1="4.22" y1="19.78" x2="5.64" y2="18.36"/><line x1="18.36" y1="5.64" x2="19.78" y2="4.22"/>
          </svg>
        {:else}
          <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"/>
          </svg>
        {/if}
      </button>

      <button
        class="navbar-mobile-toggle"
        onclick={onToggleMobile}
        style="background:none;border:none;color:var(--text-primary);cursor:pointer"
      >
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          {#if mobileOpen}
            <line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/>
          {:else}
            <line x1="3" y1="6" x2="21" y2="6"/><line x1="3" y1="12" x2="21" y2="12"/><line x1="3" y1="18" x2="21" y2="18"/>
          {/if}
        </svg>
      </button>
    </div>
  </div>
</header>