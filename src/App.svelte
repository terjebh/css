<script>
  import ParameterGroup from "./components/ParameterGroup.svelte";
  import { fade } from "svelte/transition";
  let x = 0,
    y = 10,
    blur = 10,
    spread = 0,
    color = "#aaa",
    radius = 5,
    inset = false,
    size = 100;

  $: boxShadow = `box-shadow: ${x}px ${y}px ${blur}px ${spread}px ${color}${
    inset ? " inset" : ""
  };`;
  $: boxSize = `width: ${size}px; height: ${size}px;`;
  $: borderRadius = `border-radius: ${radius}px;`;

  let copied = false;
</script>

<style>
  h2,
  h3 {
    text-align: center;
  }

  h3 {
    background: rgb(4, 187, 4);
    color: white;
    border-radius: 5px;
    padding: 10px;
  }

  .ranges {
    display: flex;
    flex-wrap: wrap;
    width: 40%;
    margin: auto;
    flex-direction: column;
  }
  .options {
    display: grid;
    flex-direction: column;
    justify-content: space-evenly;
    grid-area: options;
    grid-template-areas: "left right";
  }

  .card {
    margin: 50px auto;
    padding: 20px;
    grid-area: card;
  }

  article {
    display: grid;
    grid-template-areas:
      "card"
      "options";
  }

  @media screen and (max-width: 700px) {
    .ranges,
    .options {
      margin: 0;
    }

    .options {
      height: 50vh;
      grid-template-areas:
        "left"
        "right";
      overflow-y: scroll;
      overflow-x: hidden;
    }
  }
</style>

<main>
  <h2>Box shadow generator</h2>
  {#if copied === true}
    <h3 transition:fade>Successfully copied to clipboard!</h3>
  {/if}
  <article>
    <section class="card" style={`${boxShadow} ${borderRadius} ${boxSize}`} />
    <section class="options">
      <section class="ranges">
        <ParameterGroup name={'x-axis'} bind:value={x} min={-100} max={100} />
        <ParameterGroup name={'y-axis'} bind:value={y} min={-100} max={100} />
        <ParameterGroup name={'blur'} bind:value={blur} min={0} max={200} />
        <ParameterGroup
          name={'spread'}
          bind:value={spread}
          min={-50}
          max={100} />
      </section>
      <section class="boxShape">
        <ParameterGroup name={'size'} bind:value={size} min={100} max={200} />
        <ParameterGroup
          name={'border radius'}
          bind:value={radius}
          min={0}
          max={size / 1.5} />
        <ParameterGroup name={'color'} bind:value={color} type="color" />
        <ParameterGroup name={'inset'} bind:value={inset} type="checkbox" />
        <ParameterGroup
          name={'css'}
          type={'text'}
          bind:value={boxShadow}
          bind:copied />
      </section>
    </section>
  </article>
</main>
