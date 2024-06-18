<script lang="ts">
  const font_sizes: string[] = 
    ["title-text", "xl-text", "large-text", "small-text", "xs-text"];
</script>

{#each Object.entries(font_sizes) as [i, size]}
  <p class={size}>{parseInt(i)+1}. This is an example of "{size}" text</p>
{/each}
