<script lang="ts">
  export let wheelSections: SectionData[];
</script>

<div>
  <div class="center">🥔</div>
  <div class="wheelSections">
    {#each wheelSections as section}
      <div class="section">
        {section.label}
      </div>
    {/each}
  </div>
</div>
