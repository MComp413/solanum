<script lang="ts">
  export let sectionId: number;
  export let label: string;
  export let backgroundColor: string;
  export let backgroundImage: string;
  export let weight: number = 1;
  export let order: number;

  export let copySection: (id: number) => void;
  export let deleteSection: (id: number) => void;
</script>

<div class="wrapper">
  <div class="row">
    <input type="text" name="label" bind:value={label} placeholder="Label" />
    <input name="backgroundColor" type="color" bind:value={backgroundColor} />
    <!-- <button on:click={() => copySection(sectionId)}> 📄</button> -->
    <button on:click={() => deleteSection(sectionId)}> ❌ </button>
  </div>
  <div class="row">
    <!-- <label>
      <span>Arquivo</span>
      <input
        hidden
        name="backgroundImage"
        type="file"
        bind:value={backgroundImage}
      />
    </label>
    <input name="weight" type="number" bind:value={weight} /> -->
  </div>
  <div class="row" />
</div>

<style lang="scss">
  .wrapper {
    display: flex;
    flex-direction: column;
    row-gap: 0.5rem;
  }

  .row {
    display: flex;
    flex-direction: row;
    column-gap: 0.5rem;
  }
</style>
