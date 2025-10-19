<script lang="ts">
  import { onMount } from "svelte";

  export let example: string;

  let exampleAreas: [string, [string, string][]][] = [];

  onMount(async () => {
    try {
      let resp = await fetch(
        `https://assets.od2net.org/severance_pbfs/areas.json`,
      );
      exampleAreas = await resp.json();
    } catch (err) {}
  });
</script>

<div>
  <label>
    Or load an example:
    <select bind:value={example}>
      <option value="">Custom file loaded</option>
      {#each exampleAreas as [country, areas]}
        <optgroup label={country}>
          {#each areas as [value, label]}
            <option {value}>{label}</option>
          {/each}
        </optgroup>
      {/each}
    </select>
  </label>
</div>
