<script>
  import { Card } from "sveltestrap";
  export let joke;
</script>

<style>
  :global(.joke-text){
  font-family: 'Montserrat', sans-serif;
  font-weight: bold;
  text-align: center;
  }
</style>

<Card class="joke-text" body>{joke}</Card>