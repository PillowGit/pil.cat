<script lang="ts">
  import TitleCard from "$lib/components/homepage/titlecard.svelte";
  import TitleCardM from "$lib/components/homepage/titlecardm.svelte";
</script>

<div class="pc">
  <TitleCard/>
</div>
<div class="mobile">
  <TitleCardM/>
</div>

<div class="space"></div>
<p class="xs-text">
  More to come soon
</p>

<style>
  .space {
    height: 30vh;
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