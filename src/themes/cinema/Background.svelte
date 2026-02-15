<script lang="ts">
  import { spring } from 'svelte/motion';

  let coords = spring({ x: 50, y: 50 }, {
    stiffness: 0.04,
    damping: 0.4
  });

  function handleMouseMove(event: MouseEvent) {
    const nx = (event.clientX / window.innerWidth) * 2 - 1;
    const ny = (event.clientY / window.innerHeight) * 2 - 1;
    coords.set({ x: 50 + nx * 8, y: 50 + ny * 8 });
  }
</script>

<svelte:window onmousemove={handleMouseMove} />

<!-- Japanese Aesthetic Background -->
<div class="fixed inset-0 -z-10 overflow-hidden bg-[#faf9f6]">
  <!-- Paper Texture -->
  <div class="paper-texture absolute inset-0 opacity-[0.35]"></div>
  
  <!-- Soft Gradient Overlay -->
  <div 
    class="soft-light absolute -translate-x-1/2 -translate-y-1/2 w-[120vmax] h-[120vmax] opacity-40 pointer-events-none"
    style="top: {$coords.y}%; left: {$coords.x}%;"
  ></div>
  
  <!-- Grid Lines (Subtle) -->
  <div class="grid-lines absolute inset-0 opacity-[0.02]"></div>
  
  <!-- Corner Accents -->
  <div class="corner-accent top-left"></div>
  <div class="corner-accent top-right"></div>
  <div class="corner-accent bottom-left"></div>
  <div class="corner-accent bottom-right"></div>
</div>

<style>
  @keyframes float-light {
    0%, 100% { 
      transform: translate(-50%, -50%) scale(1);
      opacity: 0.4;
    }
    50% { 
      transform: translate(-50%, -50%) scale(1.15);
      opacity: 0.5;
    }
  }

  @keyframes fade-accent {
    0%, 100% { opacity: 0.3; }
    50% { opacity: 0.6; }
  }

  .paper-texture {
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 300 300' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='paperFilter'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.6' numOctaves='3' stitchTiles='stitch'/%3E%3CfeColorMatrix type='saturate' values='0'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23paperFilter)' fill='%23e8e6e0'/%3E%3C/svg%3E");
    background-size: 200px 200px;
    mix-blend-mode: multiply;
  }

  .soft-light {
    background: radial-gradient(
      circle,
      rgba(255, 235, 215, 0.8) 0%,
      rgba(245, 220, 200, 0.5) 25%,
      rgba(230, 215, 205, 0.3) 50%,
      transparent 70%
    );
    animation: float-light 25s ease-in-out infinite;
    filter: blur(100px);
  }

  .grid-lines {
    background-image: 
      linear-gradient(rgba(100, 100, 100, 0.08) 1px, transparent 1px),
      linear-gradient(90deg, rgba(100, 100, 100, 0.08) 1px, transparent 1px);
    background-size: 40px 40px;
  }

  .corner-accent {
    position: absolute;
    width: 60px;
    height: 60px;
    opacity: 0.15;
    animation: fade-accent 4s ease-in-out infinite;
  }

  .top-left {
    top: 20px;
    left: 20px;
    border-top: 2px solid #a89080;
    border-left: 2px solid #a89080;
  }

  .top-right {
    top: 20px;
    right: 20px;
    border-top: 2px solid #a89080;
    border-right: 2px solid #a89080;
    animation-delay: 1s;
  }

  .bottom-left {
    bottom: 20px;
    left: 20px;
    border-bottom: 2px solid #a89080;
    border-left: 2px solid #a89080;
    animation-delay: 2s;
  }

  .bottom-right {
    bottom: 20px;
    right: 20px;
    border-bottom: 2px solid #a89080;
    border-right: 2px solid #a89080;
    animation-delay: 3s;
  }
</style>
