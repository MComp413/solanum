<script lang="ts">
  export let wheelSection: SectionData;
  export let totalSections: number;

  function toRadians(degrees: number) {
    return (Math.PI * degrees) / 180;
  }

  $: apertureDegrees = 360 / totalSections;
  $: rotation = apertureDegrees * wheelSection.order;
  $: textRotation = apertureDegrees;

  $: aperturePercent =
    100 * (1 - Math.tan(toRadians(45 - apertureDegrees / 2)));
</script>

<div
  class="wheel-section"
  style="
  transform: rotate({rotation}deg);
  background-color: {wheelSection.backgroundColor};
  clip-path: polygon(0% {aperturePercent}%, 0% 0%, {aperturePercent}% 0%, 100% 100%)"
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

    span {
      font-size: xx-large;
      font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
      font-weight: 700;
      letter-spacing: 0.15rem;
      text-shadow: 0px 0px 5px 5px black;
    }
  }
</style>
