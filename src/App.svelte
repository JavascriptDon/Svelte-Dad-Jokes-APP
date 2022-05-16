<script>
import { onMount } from "svelte";
import { Col, Container, Row, Button} from "sveltestrap";
import { getJokeData } from "./api/api.js";
import Transition from "./components/transition.svelte";
import Joke from "./components/joke.svelte";
var randomJoke;
var jokes = [];
var mode = "loading";

onMount(async () => {
    await onRandomJoke();
  });

async function onRandomJoke() {
    try {
      mode = "loading";
      await sleep(500);
      randomJoke = await getJokeData();
      await sleep(500);
      mode = "random";
    } catch (e) {
      alert("Oops! You've Encountered An Error.");
    }
  }
  const sleep = delayMS => new Promise(res => setTimeout(res, delayMS));

</script>

<style>
  :global(.random-joke) {
    width: 100%;
  }

  :global(h1){
    color: white;
  }

  :global(.row) {
    margin-top: 10px;
    padding: 10px;
  }

  :global(.joke-container){
  border-radius: 10px;
  background-color: #00092C;
  }  
</style>

<Container class="joke-container">
	<Row>
		<Col>
			<h1>The Best Dad Jokes!</h1>
		</Col>
	</Row>
	<Row>
	<Col>
	  <Button on:click={onRandomJoke} class="random-joke" color="danger">
        Random Joke
      </Button>
	</Col>
	</Row>
	{#if mode === 'random'}
    <Transition>
      <Row>
        <Col>
          <Joke joke={randomJoke}/>
        </Col>
      </Row>
    </Transition>
  {/if}
</Container>