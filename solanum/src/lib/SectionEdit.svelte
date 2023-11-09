<script lang="ts">
  import SectionCard from "./SectionCard.svelte";

  let wheelSections: SectionData[] = [];
  let maxId = 0;
  let hidden: boolean = false;

  function copySection(sectionId: number) {
    const sectionToCopyIndex = wheelSections.findIndex(
      (section) => section.sectionId === sectionId
    );
    if (sectionToCopyIndex < 0) return;

    const sectionToCopy = wheelSections[sectionToCopyIndex];
    wheelSections.splice(sectionToCopyIndex, 0, { ...sectionToCopy });
    wheelSections = wheelSections;
  }

  function deleteSection(sectionId: number) {
    const sectionToDeleteIndex = wheelSections.findIndex(
      (section) => section.sectionId === sectionId
    );
    if (sectionToDeleteIndex < 0) return;

    wheelSections.splice(sectionToDeleteIndex, 1);
    wheelSections = wheelSections;

    if (wheelSections.length === 0) maxId = 0;
  }

  function addSection() {
    maxId += 1;
    wheelSections.push({
      backgroundColor: "#ffffff",
      backgroundImage: "",
      label: "",
      order: wheelSections.length,
      sectionId: maxId,
      weight: 1,
    });
    wheelSections = wheelSections;
  }
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
