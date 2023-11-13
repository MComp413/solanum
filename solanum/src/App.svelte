<script lang="ts">
  import { envConstants } from "./constants";
  import SectionEdit from "./lib/SectionEdit.svelte";
  import Wheel from "./lib/Wheel.svelte";

  const subliminarImage = envConstants["subliminarImage"];
  const waitingAudio = envConstants["waitingAudio"];
  const spinAudio = envConstants["spinAudio"];
  const resultAudio = envConstants["resultAudio"];

  const waitingAudioNode = new Audio(`./public/audio/${waitingAudio}`);
  function stopWaitingTrack() {
    waitingAudioNode.pause();
  }

  let wheelReset: boolean = false;
  let wheelSections: SectionData[] = [];
  let maxId: number = 0;

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

  function playWaitingTrack() {
    waitingAudioNode.play();
  }
</script>

<main class="container">
  <SectionEdit bind:wheelSections {copySection} {deleteSection} {addSection} />
  {#key wheelReset}
    <Wheel
      {wheelSections}
      {resultAudio}
      {spinAudio}
      {subliminarImage}
      {stopWaitingTrack}
    />
  {/key}
  <div class="controls">
    <button on:click={() => playWaitingTrack()}> Vinheta </button>
    <button class="reset" on:click={() => (wheelReset = !wheelReset)}>
      Reset
    </button>
  </div>
</main>

<style>
  .container {
    padding: 0;
    height: 100%;
    max-height: 100%;
    position: relative;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    height: 100%;
  }

  .controls {
    position: fixed;
    display: flex;
    flex-direction: column;
    bottom: 0;
    right: 0;
  }
</style>
