<script>
	import { goto } from '$app/navigation';

	function handleRedirect() {
		goto('/auth/signup'); // Redirect to '/signup' page
	}
</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://svelte.dev/docs/kit">svelte.dev/docs/kit</a> to read the documentation</p>

<button on:click={handleRedirect}>Go to Login</button>
