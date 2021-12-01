<p>please help me bid</p>

<script>
import { onMount } from 'svelte'
import { dev } from '$app/env'

let url = dev ? 'http://localhost:3000' : 'https://pleasehelpme.games'

onMount(() => {
  window.parent.postMessage({
    message: 'from bid',
    nonce: 1,
  }, url)

  window.addEventListener("message", (event) => {
    if (event.origin !== url)
      // handle this better
      return;

    console.log({ event })

    event.source.postMessage('neato', {
      targetOrigin: event.origin
    });
  }, false);
})
</script>
