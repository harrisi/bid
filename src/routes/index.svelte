<p>please help me bid</p>

<script>
import { onMount } from 'svelte'
import { dev } from '$app/env'

let url = dev ? 'http://localhost:3000' : 'https://pleasehelpme.games'

onMount(() => {
  if (window.opener) {
    window.opener.postMessage({
	    message: 'cool',
	    nonce: 1,
    }, url)
  }

  window.addEventListener("message", (event) => {
    if (event.origin !== url)
      return;

    console.log(event.data)

    // Assuming you've verified the origin of the received message (which
    // you must do in any case), a convenient idiom for replying to a
    // message is to call postMessage on event.source and provide
    // event.origin as the targetOrigin.
    // @ts-ignore
    event.source.postMessage({
	    message: 'neato',
	    nonce: 2,
    }, event.origin);
  }, false);

})
</script>
