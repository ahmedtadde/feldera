<script lang="ts">
  import type { ErrorResponse } from '$lib/services/manager'

  let { error, showActions = false }: { error: ErrorResponse; showActions?: boolean } = $props()
  let showMore = $state(false)
</script>

<div class="flex max-w-[1600px] flex-nowrap gap-2 rounded-container border border-error-500 p-4">
  <div class=" fd fd-circle-alert text-[20px] text-error-500"></div>
  <div class="flex flex-col {showMore ? 'gap-2' : 'sm:flex-row'} w-full overflow-hidden">
    <div class=" flex flex-col {showMore ? '' : ''} ">
      <div class="pb-2 font-semibold">
        The last execution of the pipeline failed with the error code: {error.error_code}
      </div>
      <span class=" whitespace-pre-wrap {showMore ? 'max-h-96 overflow-auto' : 'line-clamp-2'}">
        {error.message}
      </span>
      <button
        onclick={() => {
          showMore = !showMore
        }}
        class="text-start underline"
      >
        {#if showMore}
          Show less
        {:else}
          Show more
        {/if}
      </button>
    </div>
    {#if showActions}
      <div class="ml-auto self-end text-end {showMore ? ' -mt-4' : ''}">
        <button class="btn preset-filled-primary-500">Restart</button>
      </div>
    {/if}
  </div>
</div>
