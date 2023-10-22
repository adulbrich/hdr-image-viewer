<script>
  import { open } from "@tauri-apps/api/dialog";
  import { appDataDir, join } from "@tauri-apps/api/path";
  import { invoke, convertFileSrc } from "@tauri-apps/api/tauri";
  import { onMount } from "svelte";

  // Open a selection dialog for image files
  let selected = [];
  let assets = [];
  async function dialog() {
    selected = await open({
      multiple: true,
      filters: [
        {
          name: "Image",
          extensions: ["png", "jpeg"],
        },
      ],
    });
    assets = selected.map((item) => convertFileSrc(item));
  }
  function onDelete(asset) {
    assets = assets.filter((t) => t != asset);
  }
</script>

<div>
  <button
    class="border-2 rounded p-4 bg-slate-300 hover:bg-slate-400"
    on:click={dialog}>Select files...</button
  >
  <!-- <p>{selected}</p> -->
  <ul class="border-2 rounded p-4 my-2">
    {#each assets as asset (asset)}
      <li>{asset} <button class="border-2 p-2" on:click={onDelete(asset)}>X</button></li>
    {/each}
  </ul>
  {#each assets as asset}
    <img class="inline m-2 max-w-24 max-h-24" src={asset} alt="test" />
  {/each}
</div>
