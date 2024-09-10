<script lang="ts">
  import TitleCard from "$lib/components/homepage/titlecard.svelte";
  import TitleCardM from "$lib/components/homepage/titlecardm.svelte";
  import Experience from "$lib/components/homepage/experience.svelte";
  import ExperienceM from "$lib/components/homepage/experiencem.svelte";
</script>

<div class="pc">
  <TitleCard/>
  <div class="section-space"></div>
  <Experience/>
</div>
<div class="mobile">
  <TitleCardM/>
  <div class="section-space"></div>
  <ExperienceM/>
</div>

<style>
  .section-space {
    height: 10vh;
  }
  .pc {
    margin-top: 10vh;
  }
  .mobile {
    display: none;
  }
  @media (max-device-width: 1000px) {
    .pc {
      display: none;
    }
    .mobile {
      display: block;
    }
  }
</style>