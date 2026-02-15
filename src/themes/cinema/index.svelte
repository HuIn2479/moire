<script lang="ts">
  import { format } from 'date-fns';
  import type { PageData } from '../../routes/$types';
  import { createMemoList } from '$lib/memo.svelte';
  import Background from './Background.svelte';

  let { data, config }: { data: PageData; config: any } = $props();
  const memoList = createMemoList(() => data, config);
</script>

<div class="min-h-screen text-[#3a3a3a] {config.theme} font-sans">
  <Background />

  <div class="relative z-10 max-w-6xl mx-auto px-6 md:px-12 py-12 md:py-20">
    
    <!-- Japanese Magazine Header -->
    <header class="mb-16 md:mb-24">
      <div class="flex flex-col gap-8">
        
        <!-- Title Section - Japanese Typography -->
        <div class="relative">
          <!-- Small Label -->
          <div class="flex items-center gap-3 mb-4">
            <div class="w-12 h-[1px] bg-[#9d8b7c]"></div>
            <span class="text-[11px] font-medium tracking-[0.25em] uppercase text-[#9d8b7c]">
              Film Journal
            </span>
          </div>
          
          <!-- Main Title -->
          <h1 class="text-4xl md:text-6xl font-light tracking-[-0.02em] text-[#2d2d2d] mb-3 leading-[1.1] antialiased">
            {config.title}
          </h1>
          
          <!-- Description -->
          <p class="text-base md:text-lg text-[#7a7a7a] font-light leading-[1.75] max-w-2xl antialiased">
            {config.description}
          </p>
          
          <!-- Decorative Line -->
          <div class="mt-6 w-full h-[1px] bg-gradient-to-r from-[#9d8b7c] via-[#9d8b7c]/30 to-transparent"></div>
        </div>

        <!-- Tag Filter - Polaroid Style -->
        {#if memoList.selectedTag}
          <div class="animate-in fade-in slide-in-from-top-3 duration-500">
            <button
              class="group inline-flex items-center gap-3 px-5 py-2.5 bg-white border border-[#d4c4b0] rounded-sm shadow-[0_2px_8px_rgba(0,0,0,0.08)] text-[#6b5d4f] text-sm font-medium transition-all duration-300 ease-out hover:shadow-[0_4px_16px_rgba(0,0,0,0.12)] hover:-translate-y-0.5"
              onclick={() => memoList.selectTag(null)}
            >
              <span class="text-[#9d8b7c]">🎬</span>
              <span class="tracking-wide">#{memoList.selectedTag}</span>
              <span class="text-xs opacity-60 group-hover:opacity-100 transition-opacity duration-200">✕</span>
            </button>
          </div>
        {/if}
      </div>
    </header>

    <!-- Article List -->
    <div class="space-y-8 md:space-y-12">
      {#each memoList.visibleMemos as memo, i}
        <article 
          class="group"
          id={memo.slug}
          style="animation: slideInUp 0.6s ease-out {i * 0.1}s both;"
        >
          
          <!-- Clapperboard Card -->
          <div class="relative bg-white border border-[#e8e0d5] rounded-sm shadow-[0_4px_20px_rgba(0,0,0,0.04)] overflow-hidden transition-all duration-500 ease-[cubic-bezier(0.16,1,0.3,1)] hover:shadow-[0_8px_32px_rgba(0,0,0,0.08),0_2px_4px_rgba(157,139,124,0.1)] hover:-translate-y-1.5">
            
            <!-- Clapperboard Top Bar -->
            <div class="relative bg-gradient-to-r from-[#2d2d2d] to-[#4a4a4a] px-6 py-4 flex items-baseline justify-between">
              <!-- Left: Diagonal Stripes -->
              <div class="flex items-center gap-2">
                <div class="flex gap-1">
                  <div class="w-8 h-12 bg-[#f5f5f5] -skew-x-12"></div>
                  <div class="w-8 h-12 bg-[#2d2d2d] -skew-x-12"></div>
                  <div class="w-8 h-12 bg-[#f5f5f5] -skew-x-12"></div>
                  <div class="w-8 h-12 bg-[#2d2d2d] -skew-x-12"></div>
                </div>
              </div>
              
              <!-- Right: Date Label -->
              <div class="flex flex-col items-end text-right">
                <span class="text-white text-xs font-mono tracking-wider opacity-80">
                  {format(memo.date, 'yyyy.MM.dd')}
                </span>
                <span class="text-white/60 text-[10px] font-mono tracking-wider">
                  {format(memo.date, 'HH:mm:ss')}
                </span>
              </div>
            </div>

            <!-- Content Area -->
            <div class="px-6 md:px-10 py-8 md:py-10">
              
              <!-- Date Display - Japanese Style -->
              <div class="flex items-baseline gap-4 mb-7 pb-5 border-b border-[#e8e0d5]">
                <div class="flex items-baseline gap-2.5">
                  <span class="text-5xl md:text-6xl font-extralight text-[#9d8b7c] leading-none tabular-nums tracking-tighter">
                    {format(memo.date, 'dd')}
                  </span>
                  <div class="flex flex-col gap-0.5">
                    <span class="text-xs font-medium uppercase tracking-[0.15em] text-[#9d8b7c]">
                      {format(memo.date, 'MMM')}
                    </span>
                    <span class="text-xs font-light text-[#b5a59a] tabular-nums">
                      {format(memo.date, 'yyyy')}
                    </span>
                  </div>
                </div>
                <div class="flex-1 h-[1px] bg-gradient-to-r from-[#9d8b7c]/20 to-transparent"></div>
              </div>

              <!-- Article Content -->
              <div
                class="prose-filmlog text-[1rem] leading-[1.9] text-[#3a3a3a] font-light antialiased
                  max-w-none
                  [&_h1]:text-2xl [&_h1]:md:text-3xl [&_h1]:font-light [&_h1]:text-[#2d2d2d] [&_h1]:mt-8 [&_h1]:mb-4 [&_h1]:leading-[1.3] [&_h1]:tracking-[-0.01em] [&_h1]:border-b [&_h1]:border-[#e8e0d5] [&_h1]:pb-3
                  [&_h2]:text-xl [&_h2]:md:text-2xl [&_h2]:font-light [&_h2]:text-[#2d2d2d] [&_h2]:mt-7 [&_h2]:mb-3 [&_h2]:leading-[1.4] [&_h2]:tracking-[-0.01em]
                  [&_h3]:text-lg [&_h3]:md:text-xl [&_h3]:font-normal [&_h3]:text-[#4a4a4a] [&_h3]:mt-6 [&_h3]:mb-2 [&_h3]:tracking-[-0.005em]
                  [&_h4]:text-base [&_h4]:font-medium [&_h4]:text-[#6b5d4f] [&_h4]:mt-5 [&_h4]:mb-2 [&_h4]:uppercase [&_h4]:tracking-wider [&_h4]:text-sm
                  [&_p]:mb-6 [&_p]:text-[#3a3a3a] [&_p]:leading-[1.9] [&_p]:tracking-[0.003em]
                  [&_p:first-of-type]:text-[1.1rem] [&_p:first-of-type]:text-[#2d2d2d] [&_p:first-of-type]:leading-[2] [&_p:first-of-type]:font-normal [&_p:first-of-type]:tracking-[0.005em]
                  [&_a]:text-[#7d6b5d] [&_a]:no-underline [&_a]:border-b [&_a]:border-[#9d8b7c]/30 [&_a]:transition-all [&_a]:duration-200 [&_a]:hover:border-[#9d8b7c] [&_a]:hover:text-[#6b5d4f]
                  [&_strong]:text-[#2d2d2d] [&_strong]:font-semibold [&_strong]:tracking-[0.003em]
                  [&_em]:text-[#6b5d4f] [&_em]:not-italic [&_em]:border-b [&_em]:border-dotted [&_em]:border-[#9d8b7c]/40 [&_em]:tracking-[0.005em]
                  [&_img]:w-full [&_img]:my-8 [&_img]:rounded-sm [&_img]:shadow-[0_8px_24px_rgba(0,0,0,0.08)] [&_img]:border-8 [&_img]:border-white [&_img]:transition-transform [&_img]:duration-300 [&_img]:hover:scale-[1.01]
                  [&_blockquote]:border-l-4 [&_blockquote]:border-[#9d8b7c] [&_blockquote]:bg-[#faf9f6] [&_blockquote]:rounded-r-sm [&_blockquote]:pl-6 [&_blockquote]:pr-4 [&_blockquote]:py-5 [&_blockquote]:my-8 [&_blockquote]:text-[#4a4a4a] [&_blockquote]:italic [&_blockquote]:text-base [&_blockquote]:leading-[1.8] [&_blockquote]:tracking-[0.005em]
                  [&_blockquote_p]:mb-0 [&_blockquote_p]:text-[#4a4a4a]
                  [&_ul]:pl-6 [&_ul]:list-none [&_ul]:mb-6 [&_ul]:space-y-2
                  [&_ul_li]:relative [&_ul_li]:pl-2 [&_ul_li::before]:content-['●'] [&_ul_li::before]:absolute [&_ul_li::before]:left-[-1em] [&_ul_li::before]:text-[#9d8b7c] [&_ul_li::before]:text-xs
                  [&_ol]:pl-6 [&_ol]:list-decimal [&_ol]:list-inside [&_ol]:mb-6 [&_ol]:space-y-2
                  [&_ol_li]:text-[#3a3a3a] [&_ol_li::marker]:text-[#9d8b7c] [&_ol_li::marker]:font-normal
                  [&_code]:font-mono [&_code]:text-[0.9em] [&_code]:bg-[#f5f3f0] [&_code]:text-[#6b5d4f] [&_code]:px-2 [&_code]:py-0.5 [&_code]:rounded [&_code]:border [&_code]:border-[#e8e0d5]
                  [&_pre]:bg-[#2d2d2d] [&_pre]:border [&_pre]:border-[#4a4a4a] [&_pre]:p-6 [&_pre]:my-8 [&_pre]:overflow-x-auto [&_pre]:rounded [&_pre]:shadow-[0_4px_16px_rgba(0,0,0,0.12)]
                  [&_pre_code]:bg-transparent [&_pre_code]:text-[#e8e0d5] [&_pre_code]:p-0 [&_pre_code]:border-0
                  [&_hr]:border-0 [&_hr]:h-[1px] [&_hr]:bg-gradient-to-r [&_hr]:from-transparent [&_hr]:via-[#e8e0d5] [&_hr]:to-transparent [&_hr]:my-10
                  [&_table]:w-full [&_table]:border-collapse [&_table]:my-8 [&_table]:text-sm
                  [&_th]:bg-[#faf9f6] [&_th]:text-left [&_th]:p-3 [&_th]:font-medium [&_th]:text-[#2d2d2d] [&_th]:border-b-2 [&_th]:border-[#e8e0d5] [&_th]:text-xs [&_th]:uppercase [&_th]:tracking-wider
                  [&_td]:p-3 [&_td]:border-b [&_td]:border-[#f5f3f0] [&_td]:text-[#3a3a3a]
                  [&_.tag-link]:inline-block [&_.tag-link]:text-[11px] [&_.tag-link]:font-medium [&_.tag-link]:text-[#7d6b5d] [&_.tag-link]:bg-[#f5f3f0] [&_.tag-link]:px-3 [&_.tag-link]:py-1.5 [&_.tag-link]:rounded-full [&_.tag-link]:mr-2 [&_.tag-link]:mb-2 [&_.tag-link]:tracking-[0.05em] [&_.tag-link]:no-underline [&_.tag-link]:border [&_.tag-link]:border-[#e8e0d5] [&_.tag-link]:transition-all [&_.tag-link]:duration-200 [&_.tag-link]:ease-out [&_.tag-link]:hover:bg-[#9d8b7c] [&_.tag-link]:hover:text-white [&_.tag-link]:hover:border-[#9d8b7c] [&_.tag-link]:hover:shadow-[0_2px_8px_rgba(157,139,124,0.25)] [&_.tag-link]:hover:-translate-y-0.5
                "
                onclick={(e) => {
                  const target = e.target as HTMLElement;
                  if (target.classList.contains('tag-link')) {
                    e.stopPropagation();
                    const tag = target.dataset.tag;
                    if (tag) memoList.selectTag(tag);
                  }
                }}
                role="presentation"
              >
                {@html memo.content}
              </div>
            </div>

            <!-- Film Strip Bottom -->
            <div class="h-3 bg-gradient-to-r from-[#9d8b7c]/10 via-[#9d8b7c]/5 to-transparent"></div>
          </div>

          <!-- Scene Number Label (Film Style) -->
          <div class="flex items-center gap-2 mt-4 ml-6">
            <div class="text-[10px] font-mono tracking-[0.2em] text-[#9d8b7c]/50 uppercase tabular-nums">
              Scene {String(i + 1).padStart(3, '0')}
            </div>
            <div class="flex-1 h-px bg-gradient-to-r from-[#9d8b7c]/10 to-transparent"></div>
          </div>
        </article>
      {/each}
    </div>

    <!-- Load More Button -->
    {#if memoList.visibleCount < data.memos.length}
      <div class="mt-16 md:mt-20 pt-10 border-t border-[#e8e0d5] text-center">
        <button 
          class="group inline-flex items-center gap-3 px-8 py-3.5 bg-white rounded-sm border-2 border-[#9d8b7c]/30 text-[#7d6b5d] text-sm font-medium tracking-[0.1em] uppercase transition-all duration-300 ease-out hover:bg-[#9d8b7c] hover:text-white hover:border-[#9d8b7c] hover:shadow-[0_4px_20px_rgba(157,139,124,0.2)] hover:-translate-y-1"
          onclick={memoList.loadMore}
        >
          <span>Continue</span>
          <svg class="w-4 h-4 transition-transform duration-300 group-hover:translate-y-0.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
          </svg>
        </button>
      </div>
    {/if}

    <!-- Footer - Minimal -->
    <footer class="mt-24 md:mt-32 pt-8 border-t border-[#e8e0d5] text-center">
      <p class="text-[10px] text-[#9d8b7c]/40 uppercase tracking-[0.2em] font-medium antialiased">
        © {new Date().getFullYear()} · {config.author.toUpperCase()} · Generated by MOIRE
      </p>
    </footer>
  </div>
</div>

<style>
  @keyframes slideInUp {
    from {
      opacity: 0;
      transform: translateY(40px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  :global(body.cinema) {
    background-color: #faf9f6;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Helvetica Neue', 'Hiragino Sans GB', 'Hiragino Kaku Gothic ProN', 'Noto Sans CJK JP', 'Yu Gothic', 'Microsoft YaHei', sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-rendering: optimizeLegibility;
    font-feature-settings: 'kern' 1, 'liga' 1;
  }
</style>
