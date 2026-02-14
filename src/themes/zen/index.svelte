<script lang="ts">
  import { format } from 'date-fns';
  import type { PageData } from '../../routes/$types';
  import { createMemoList } from '$lib/memo.svelte';

  let { data, config }: { data: PageData; config: any } = $props();
  // We use a simple reactivity approach or simply pass data if createMemoList handles it.
  // Assuming createMemoList expects a getter for data.
  const memoList = createMemoList(() => data, config);
</script>

<!-- Main Container: Dark/Low-light Zen Style or High Contrast Paper Style. Let's go High Contrast Paper with a "Red Seal" vibe -->
<div class="min-h-screen bg-[#f4f4f4] text-[#111] selection:bg-[#c0392b] selection:text-white {config.theme} font-sans">
  
  <!-- Fixed Background Decoration -->
  <div class="fixed inset-0 pointer-events-none opacity-[0.03] z-0" 
       style="background-image: url('data:image/svg+xml,%3Csvg width=\'60\' height=\'60\' viewBox=\'0 0 60 60\' xmlns=\'http://www.w3.org/2000/svg\'%3E%3Cg fill=\'none\' fill-rule=\'evenodd\'%3E%3Cg fill=\'%23000000\' fill-opacity=\'1\'%3E%3Cpath d=\'M36 34v-4h-2v4h-4v2h4v4h2v-4h4v-2h-4zm0-30V0h-2v4h-4v2h4v4h2V6h4V4h-4zM6 34v-4H4v4H0v2h4v4h2v-4h4v-2H6zM6 4V0H4v4H0v2h4v4h2V6h4V4H6z\'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E');">
  </div>

  <div class="relative z-10 max-w-4xl mx-auto px-4 md:px-8 py-16 md:py-24">
    
    <!-- Hero Header -->
    <header class="mb-24 md:mb-32 flex flex-col items-center relative">
      <div class="w-20 h-1 bg-[#111] mb-8"></div>
      <h1 class="text-5xl md:text-7xl font-bold tracking-tighter text-[#111] text-center mb-6 mix-blend-multiply">
        {config.title}
      </h1>
      <p class="text-sm md:text-base text-[#555] font-medium tracking-wide uppercase text-center max-w-md leading-relaxed mb-8">
        {config.description}
      </p>

      <!-- Filter Tag -->
      {#if memoList.selectedTag}
        <div class="animate-in fade-in slide-in-from-top-4 duration-500">
          <button
            class="group relative inline-flex items-center gap-2 px-6 py-2 bg-[#111] text-white overflow-hidden transition-all hover:pr-8"
            onclick={() => memoList.selectTag(null)}
          >
             <span class="text-xs font-bold tracking-widest uppercase relative z-10">#{memoList.selectedTag}</span>
             <span class="absolute right-2 opacity-0 group-hover:opacity-100 transition-opacity text-xs z-10"></span>
          </button>
        </div>
      {/if}
    </header>

    <!-- Timeline Stream -->
    <div class="relative pl-0 md:pl-8 border-l-0 md:border-l-2 md:border-[#e5e5e5] space-y-20 md:space-y-0">
      
      {#each memoList.visibleMemos as memo, i}
        <article 
          class="relative grid grid-cols-1 md:grid-cols-[140px_1fr] gap-8 md:gap-16 mb-16 md:mb-24 group"
          id={memo.slug}
          style="animation: fadeIn 0.8s ease-out {i * 0.1}s both;"
        >
          <!-- Timeline Node (Desktop Only) -->
          <div class="hidden md:block absolute -left-[41px] top-6 w-4 h-4 rounded-full border-[3px] border-[#f4f4f4] bg-[#ccc] group-hover:bg-[#c0392b] group-hover:scale-125 transition-all duration-300 z-20"></div>

          <!-- Date / Meta Stamp -->
          <div class="flex md:flex-col justify-between md:justify-start items-baseline md:items-end text-right pt-4 sticky top-8 self-start">
             <div class="flex flex-col items-end">
               <span class="text-5xl md:text-6xl font-black text-[#e0e0e0] group-hover:text-[#c0392b] transition-colors duration-500 leading-none">
                 {format(memo.date, 'dd')}
               </span>
               <span class="text-xs md:text-sm font-bold tracking-widest uppercase text-[#999]">
                 {format(memo.date, 'MMM yyyy')}
               </span>
               <span class="text-[10px] text-[#ccc] font-mono mt-1">
                 {format(memo.date, 'HH:mm')}
               </span>
             </div>
          </div>

          <!-- Content Card -->
          <div class="relative bg-white p-6 md:p-10 shadow-[0_2px_4px_rgba(0,0,0,0.02)] border border-transparent group-hover:border-[#eee] group-hover:shadow-[0_20px_40px_rgba(0,0,0,0.08)] transition-all duration-500 rounded-sm">
            
            <!-- Dynamic Corner Accent -->
            <div class="absolute top-0 right-0 w-8 h-8 overflow-hidden z-10 opacity-0 group-hover:opacity-100 transition-opacity duration-300">
               <div class="absolute top-0 right-0 w-12 h-12 bg-[#c0392b] rotate-45 transform translate-x-1/2 -translate-y-1/2"></div>
            </div>

            <div
              class="prose-zen text-[1.05rem] leading-[1.8] text-[#333] font-normal
                max-w-none
                [&_h1]:text-2xl [&_h1]:font-bold [&_h1]:text-[#111] [&_h1]:mt-4 [&_h1]:mb-4
                [&_h2]:text-xl [&_h2]:font-bold [&_h2]:text-[#111] [&_h2]:mt-6 [&_h2]:mb-3
                [&_h3]:text-lg [&_h3]:font-bold [&_h3]:text-[#111] [&_h3]:mt-4 [&_h3]:mb-2
                [&_p]:mb-5 [&_p]:text-justify
                [&_a]:text-[#c0392b] [&_a]:border-b [&_a]:border-[#c0392b]/30 [&_a]:bg-[#c0392b]/5 [&_a]:px-1 [&_a]:no-underline [&_a]:transition-all [&_a]:hover:bg-[#c0392b] [&_a]:hover:text-white
                [&_img]:w-full [&_img]:rounded-sm [&_img]:my-6 [&_img]:shadow-sm
                [&_blockquote]:border-l-4 [&_blockquote]:border-[#c0392b] [&_blockquote]:bg-[#fafafa] [&_blockquote]:pl-6 [&_blockquote]:py-4 [&_blockquote]:my-6 [&_blockquote]:text-[#555] [&_blockquote]:italic
                [&_ul]:pl-5 [&_ul]:list-disc [&_ul]:mb-6 [&_ul_li]:mb-2 [&_ul_li::marker]:text-[#c0392b]
                [&_ol]:pl-5 [&_ol]:list-decimal [&_ol]:mb-6 [&_ol_li]:mb-2 [&_ol_li::marker]:text-[#c0392b] [&_ol_li::marker]:font-bold
                [&_code]:font-mono [&_code]:text-[0.85em] [&_code]:bg-[#f4f4f4] [&_code]:px-1.5 [&_code]:py-0.5 [&_code]:rounded-[2px] [&_code]:text-[#c0392b]
                [&_pre]:bg-[#1a1a1a] [&_pre]:p-6 [&_pre]:my-6 [&_pre]:overflow-x-auto [&_pre]:text-white [&_pre_code]:bg-transparent [&_pre_code]:text-white [&_pre_code]:p-0
                [&_hr]:border-t-2 [&_hr]:border-dashed [&_hr]:border-[#eee] [&_hr]:my-8
                [&_table]:w-full [&_table]:border-collapse [&_table]:my-6 [&_table]:text-sm
                [&_th]:bg-[#fafafa] [&_th]:text-left [&_th]:p-3 [&_th]:font-bold [&_th]:border-b-2 [&_th]:border-[#eee]
                [&_td]:p-3 [&_td]:border-b [&_td]:border-[#f4f4f4]
                [&_.tag-link]:inline-block [&_.tag-link]:text-[10px] [&_.tag-link]:font-bold [&_.tag-link]:text-[#999] [&_.tag-link]:bg-[#f4f4f4] [&_.tag-link]:px-2 [&_.tag-link]:py-1 [&_.tag-link]:rounded-sm [&_.tag-link]:mr-2 [&_.tag-link]:uppercase [&_.tag-link]:tracking-wider [&_.tag-link]:no-underline [&_.tag-link]:transition-colors [&_.tag-link]:hover:bg-[#111] [&_.tag-link]:hover:text-white
              "
              role="presentation"
              onclick={(e) => {
                const target = e.target as HTMLElement;
                if (target.classList.contains('tag-link')) {
                  const tag = target.dataset.tag;
                  if (tag) memoList.selectTag(tag);
                }
              }}
            >
              {@html memo.content}
            </div>

            <!-- Card Footer / End Mark -->
             <div class="mt-8 pt-6 border-t border-[#f4f4f4] flex justify-between items-center opacity-70 group-hover:opacity-100 transition-opacity">
                <div class="flex gap-2">
                   <div class="w-1.5 h-1.5 bg-[#ccc] rounded-full"></div>
                   <div class="w-1.5 h-1.5 bg-[#e5e5e5] rounded-full"></div>
                </div>
                <div class="text-[0.6rem] font-bold text-[#e0e0e0] uppercase tracking-widest group-hover:text-[#c0392b] transition-colors">
                  End of Memo
                </div>
             </div>

          </div>
        </article>
      {/each}
    </div>

    <!-- Load More -->
    {#if memoList.visibleCount < data.memos.length}
      <div class="py-24 text-center">
        <button
          class="group relative inline-flex items-center justify-center px-8 py-3 overflow-hidden font-bold text-white transition-all bg-[#111] border-2 border-[#111] hover:bg-white hover:text-[#111]"
          onclick={memoList.loadMore}
        >
          <span class="absolute w-0 h-0 transition-all duration-500 ease-out bg-white rounded-full group-hover:w-56 group-hover:h-56 opacity-10"></span>
          <span class="relative uppercase tracking-[0.2em] text-xs">Load More Content</span>
        </button>
      </div>
    {/if}
    
    <footer class="text-center py-10 border-t border-[#e5e5e5] mt-10">
       <div class="text-[#ccc] text-xs font-mono">
          DESIGNED_BY_{config.author.toUpperCase()} | GENERATED_BY_<a href="https://github.com/moirelog/moire" class="text-[#999] hover:text-[#1a1a1a] transition-colors">MOIRE</a>
       </div>
    </footer>

  </div>
</div>

<style>
  @keyframes fadeIn {
    from {
      opacity: 0;
      transform: translateY(20px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
</style>