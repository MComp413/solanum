<script lang="ts">
  export let wheelSection: SectionData;
  export let totalSections: number;

  $: rotation = (360 / totalSections) * wheelSection.order;
  $: textRotation = 180 / totalSections;
  $: fr = 100 / totalSections;
</script>

<div
  class="wheel-section"
  style="transform: rotate({rotation}deg); background-color: {wheelSection.backgroundColor}; "
>
  <span style="transform: rotate({textRotation}deg)">{wheelSection.label}</span>
</div>

<style lang="scss">
  .wheel-section {
    position: absolute;
    transform-origin: bottom right;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 50%;
    width: 50%;
    border-radius: 15%;
    clip-path: polygon(0% 60%, 0% 0%, 60% 0%, 100% 100%);

    span {
      font-size: xx-large;
      font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
      font-weight: 700;
      letter-spacing: 0.15rem;
      text-shadow: 0px 0px 5px 5px black;
    }
  }
</style>
