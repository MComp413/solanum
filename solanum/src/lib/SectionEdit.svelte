<script lang="ts">
  import SectionCard from "./SectionCard.svelte";

  export let wheelSections: SectionData[];
  export let copySection: (id: number) => void;
  export let deleteSection: (id: number) => void;
  export let addSection: () => void;

  let hidden: boolean = false;
</script>

<div class="wrapper">
  <div class="header">
    <button on:click={() => (hidden = !hidden)}>
      {#if hidden}
        {">>"}
      {:else}
        {"<<"}
      {/if}
    </button>
  </div>
  {#if !hidden}
    <ol>
      {#each wheelSections as section}
        <li>
          <SectionCard
            sectionId={section.sectionId}
            bind:label={section.label}
            bind:backgroundColor={section.backgroundColor}
            bind:backgroundImage={section.backgroundImage}
            bind:weight={section.weight}
            bind:order={section.order}
            {copySection}
            {deleteSection}
          />
        </li>
      {/each}
      <li>
        <button on:click={addSection}> + </button>
      </li>
    </ol>
  {/if}
</div>

<style lang="scss">
  .wrapper {
    display: flex;
    flex-direction: column;
    width: min-content;
    height: 100%;
  }

  .header {
    display: flex;
    flex-direction: row-reverse;
    height: 10%;
  }

  ol {
    list-style-type: none;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
    row-gap: 1rem;
    overflow-y: auto;
    height: 90%;
  }
</style>
