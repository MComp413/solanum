<script lang="ts">
  import WheelSection from "./WheelSection.svelte";

  export let subliminarImage: string;
  export let waitingAudio: string;
  export let spinAudio: string;
  export let resultAudio: string;

  export let wheelSections: SectionData[];
  let orderedWheelSections: SectionData[];
  let totalSections: number;
  let rotation = 0;
  let displaySubliminar = false;

  $: orderedWheelSections = wheelSections.sort((a, b) => a.order - b.order);
  $: totalSections = wheelSections.length;

  function callSubliminarTimeouts() {
    setTimeout(() => (displaySubliminar = true), 5.5 * 1000);
    setTimeout(() => (displaySubliminar = false), 5.75 * 1000);
  }

  function playSpinTrack() {
    const audio = new Audio(`./public/audio/${spinAudio}`);
    audio.play();
    setTimeout(() => {
      audio.pause();
    }, 10 * 1000);
  }

  function spin() {
    const randomResult = Math.random();

    callSubliminarTimeouts();
    playSpinTrack();

    const spins = randomResult + 20;
    rotation += 360 * spins;
  }
</script>

<div class="wheel">
  <button on:click={spin} class="center"><span>🥔</span></button>
  <div class="section-container" style="transform: rotate({rotation}deg)">
    {#each orderedWheelSections as section}
      <WheelSection wheelSection={section} {totalSections} />
    {/each}
  </div>
</div>

<div
  hidden={!displaySubliminar}
  class="subliminar"
  style="background-image: url('./public/img/{subliminarImage}');"
/>

<style lang="scss">
  .wheel {
    display: flex;
    position: relative;
    height: 40rem;
    width: 40rem;

    overflow: hidden;

    border-radius: 50%;
    border: 15px solid white;
  }

  .section-container {
    display: flex;
    position: relative;
    height: 100%;
    width: 100%;
    transition: transform 10s ease;
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
    font-size: 35pt;
    line-height: 35pt;

    height: 15%;
    width: 15%;
    padding: 0;
    margin: 0;
    border: 0;

    box-shadow: none;
    background-color: white;

    position: absolute;
    align-self: center;
    left: calc(50% - 7.5%);
    z-index: 10;

    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 50%;
  }

  .subliminar {
    background-repeat: no-repeat;
    background-size: cover;
    position: fixed;
    height: 98.2%;
    width: 99.5%;
    z-index: 11;
  }
</style>
