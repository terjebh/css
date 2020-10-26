<script>
import { text } from "svelte/internal";


  export let name;
  export let value;
  export let min;
  export let max;
  export let type = "number";
  export let checked = false;
  export let copied = false;

  function copyCSS(e) {
    if ("clipboard" in navigator) {
      navigator.clipboard.writeText(value);
      copied = true;
      setTimeout(() => copied = false, 1000);
    } else {
      let textArea = document.createElement('textarea');
      textArea.textContent = e.target.value;
      textArea.focus();
      textArea.select();
      document.execCommand('copy');
      copied = true;
      setTimeout(() => copied = false, 1000);

    }
  }
</script>

<style>
  input[type="text"] {
    width: 250px;
  }

  input[type="number"] {
    width: 80px;
  }

  input[type="range"] {
    width: 200px;
  }

  label {
    padding-left: 10px;
  }

  .group {
    display: flex;
    flex-wrap: nowrap;
    width: 80%;
    border: none;
  }
  fieldset {
    border: none;
  }

  @media screen and (max-width: 700px) {
    .group {
      display: flex;
      flex-direction: row;
      /* flex-wrap: wrap; */
      justify-content: space-between;
    }
    input[type="number"] {
      width: 50px;
    }
  }
</style>

<label for={name}>{name}</label>
<fieldset class="group">
  {#if type === 'number'}
    <input type="range" {name} bind:value {min} {max} />
    <input type="number" name bind:value {min} {max} />
  {:else if type === 'color'}
    <input type="color" {name} bind:value style={`background: ${value};`} />
  {:else if type === 'checkbox'}
    <input type="checkbox" {name} bind:checked />
  {:else if type === 'text'}
    <input type="text" {name} bind:value />
    <button on:click={copyCSS}>Copy</button>
  {/if}
</fieldset>
