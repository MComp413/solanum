<script lang="ts">
  import SectionEdit from "./lib/SectionEdit.svelte";
  import Wheel from "./lib/Wheel.svelte";

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
</script>

<main class="container">
  <SectionEdit bind:wheelSections {copySection} {deleteSection} {addSection} />
  <Wheel {wheelSections} />
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
</style>
