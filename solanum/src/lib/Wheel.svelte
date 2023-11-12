<script lang="ts">
  import WheelSection from "./WheelSection.svelte";

  export let wheelSections: SectionData[];
  let orderedWheelSections: SectionData[];
  let totalSections: number;

  $: orderedWheelSections = wheelSections.sort((a, b) => a.order - b.order);
  $: totalSections = wheelSections.length;
</script>

<div class="wheel">
  <button class="center"><span>🥔</span></button>
  {#each orderedWheelSections as section}
    <WheelSection wheelSection={section} {totalSections} />
  {/each}
</div>

<style lang="scss">
  .wheel {
    display: flex;
    position: relative;
    height: 30rem;
    width: 30rem;

    overflow: hidden;

    border-radius: 50%;
    border: 5px solid white;
  }

  .center::before {
    content: "";
    height: 75%;
    width: 50%;
    background-color: white;
    position: absolute;
    bottom: 90%;
    clip-path: polygon(50% 0%, 15% 100%, 85% 100%);
  }

  .center {
    font-size: 25pt;
    line-height: 25pt;

    height: 10%;
    width: 10%;
    padding: 0;
    margin: 0;
    border: 0;

    box-shadow: none;
    background-color: white;

    position: absolute;
    align-self: center;
    left: 45%;
    z-index: 10;

    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 50%;
  }
</style>
