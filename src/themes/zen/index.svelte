<script lang="ts">
  import { format } from 'date-fns';
  import type { PageData } from '../../routes/$types';
  import { createMemoList } from '$lib/memo.svelte';

  let { data, config }: { data: PageData; config: any } = $props();
  const memoList = createMemoList(() => data, config);
</script>

<div class="min-h-screen bg-[#fafafa] text-[#1a1a1a] {config.theme}">
  <div class="max-w-4xl mx-auto px-6 md:px-16 py-20">
    <!-- Header -->
    <header class="mb-24 relative">
      <div class="flex items-baseline gap-8">
        <h1 class="text-5xl md:text-6xl font-light tracking-tight text-[#1a1a1a] relative">
          {config.title}
          <div class="absolute -bottom-2 left-0 w-12 h-px bg-[#1a1a1a]"></div>
        </h1>
      </div>
      <p class="mt-8 text-sm text-[#7a7a7a] font-light tracking-wide max-w-md">
        {config.description}
      </p>

      {#if memoList.selectedTag}
        <div class="mt-12 flex items-center gap-4">
          <span class="text-xs text-[#999] uppercase tracking-widest">Filter</span>
          <button
            class="text-sm font-light text-[#1a1a1a] underline underline-offset-4 decoration-1 hover:decoration-2 transition-all"
            onclick={() => memoList.selectTag(null)}
          >
            #{memoList.selectedTag} ×
          </button>
        </div>
      {/if}
    </header>

    <!-- Timeline -->
    <div class="relative">
      <!-- Timeline vertical line -->
      <div class="absolute left-0 top-0 bottom-0 w-px bg-[#e0e0e0] hidden md:block"></div>

      {#each memoList.visibleMemos as memo, i}
        <article 
          class="relative pl-0 md:pl-12 mb-20 group"
          id={memo.slug}
          style="animation: fadeIn 0.6s ease-out {i * 0.1}s both"
        >
          <!-- Timeline dot -->
          <div class="absolute left-0 top-1 hidden md:block">
            <div class="w-2 h-2 rounded-full bg-[#1a1a1a] -translate-x-[3.5px] group-hover:scale-150 transition-transform duration-300"></div>
          </div>

          <!-- Date -->
          <time class="block text-xs text-[#999] mb-4 font-light tracking-widest uppercase">
            {format(memo.date, 'MMM dd, yyyy')}
          </time>

          <!-- Content -->
          <div
            class="prose-zen text-[0.95rem] leading-[1.9] text-[#2a2a2a] font-light
              [&_h1]:text-2xl [&_h1]:font-light [&_h1]:tracking-tight [&_h1]:text-[#1a1a1a] [&_h1]:mt-8 [&_h1]:mb-4 [&_h1]:leading-tight
              [&_h2]:text-xl [&_h2]:font-light [&_h2]:tracking-tight [&_h2]:text-[#1a1a1a] [&_h2]:mt-6 [&_h2]:mb-3 [&_h2]:leading-snug
              [&_h3]:text-lg [&_h3]:font-normal [&_h3]:text-[#1a1a1a] [&_h3]:mt-5 [&_h3]:mb-2
              [&_p]:mb-5 [&_p]:text-[#2a2a2a] [&_p:last-child]:mb-0
              [&_a]:text-[#1a1a1a] [&_a]:underline [&_a]:underline-offset-4 [&_a]:decoration-1 [&_a]:hover:decoration-2 [&_a]:transition-all
              [&_img]:my-8 [&_img]:max-w-full [&_img]:rounded-none [&_img]:opacity-90
              [&_ul]:list-none [&_ul]:pl-0 [&_ul]:my-5 [&_ul]:space-y-2
              [&_ul_li]:relative [&_ul_li]:pl-6 [&_ul_li]:before:content-['·'] [&_ul_li]:before:absolute [&_ul_li]:before:left-0 [&_ul_li]:before:text-[#999]
              [&_ol]:list-none [&_ol]:pl-0 [&_ol]:my-5 [&_ol]:space-y-2 [&_ol]:counter-reset-[item]
              [&_ol_li]:relative [&_ol_li]:pl-6 [&_ol_li]:counter-increment-[item] [&_ol_li]:before:content-[counter(item)'.'] [&_ol_li]:before:absolute [&_ol_li]:before:left-0 [&_ol_li]:before:text-[#999] [&_ol_li]:before:text-xs
              [&_blockquote]:border-l-2 [&_blockquote]:border-[#d0d0d0] [&_blockquote]:pl-6 [&_blockquote]:my-6 [&_blockquote]:text-[#5a5a5a] [&_blockquote]:italic [&_blockquote]:font-light
              [&_blockquote_p]:text-[#5a5a5a]
              [&_code]:text-[0.85rem] [&_code]:bg-[#f5f5f5] [&_code]:px-2 [&_code]:py-0.5 [&_code]:rounded-none [&_code]:text-[#1a1a1a] [&_code]:font-mono [&_code]:font-normal
              [&_pre]:bg-[#f5f5f5] [&_pre]:p-6 [&_pre]:my-6 [&_pre]:overflow-x-auto [&_pre]:text-[0.85rem] [&_pre]:leading-relaxed [&_pre]:rounded-none
              [&_pre_code]:bg-transparent [&_pre_code]:p-0 [&_pre_code]:text-[#1a1a1a]
              [&_table]:w-full [&_table]:my-6 [&_table]:text-[0.9rem] [&_table]:border-collapse
              [&_th]:text-left [&_th]:font-normal [&_th]:text-[#1a1a1a] [&_th]:pb-3 [&_th]:border-b [&_th]:border-[#e0e0e0]
              [&_td]:py-3 [&_td]:border-b [&_td]:border-[#f0f0f0] [&_td]:text-[#2a2a2a]
              [&_strong]:font-medium [&_strong]:text-[#1a1a1a]
              [&_em]:italic [&_em]:text-[#2a2a2a]
              [&_.tag-link]:text-[0.85rem] [&_.tag-link]:text-[#666] [&_.tag-link]:mr-2 [&_.tag-link]:no-underline [&_.tag-link]:hover:text-[#1a1a1a] [&_.tag-link]:transition-colors [&_.tag-link]:cursor-pointer [&_.tag-link]:font-normal
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

          <!-- Separator -->
          <div class="mt-12 h-px w-full bg-gradient-to-r from-transparent via-[#e0e0e0] to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-500"></div>
        </article>
      {/each}
    </div>

    <!-- Load More -->
    {#if memoList.visibleCount < data.memos.length}
      <div class="mt-20 text-center relative">
        <div class="absolute left-0 top-1/2 w-full h-px bg-[#e0e0e0] -translate-y-1/2"></div>
        <button
          class="relative bg-[#fafafa] px-8 py-2 text-xs text-[#999] uppercase tracking-widest hover:text-[#1a1a1a] transition-colors font-light"
          onclick={memoList.loadMore}
        >
          More
        </button>
      </div>
    {/if}

    <!-- Empty State -->
    {#if data.memos.length === 0}
      <div class="text-center py-20">
        <p class="text-sm text-[#999] font-light tracking-wide">空</p>
      </div>
    {/if}
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
