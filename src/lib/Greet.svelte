<script>
  import { invoke } from '@tauri-apps/api/tauri'

  let name = ''
  let greetMsg = ''

  async function greet() {
    greetMsg = await invoke('greet', { name })
  }
</script>

<div class="my-12">
  <input class="border-2 rounded p-4" id="greet-input" placeholder="Enter a name..." bind:value="{name}" />
  <button class="border-2 rounded p-4 bg-slate-200 hover:bg-slate-400" on:click="{greet}">Greet</button>
  <p>{greetMsg}</p>
</div>