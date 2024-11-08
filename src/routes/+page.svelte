<script>
	import { goto } from '$app/navigation';
	import { supabase } from '$lib/supabase';

	function handleRedirect() {
		goto('/game');
	}
</script>

<h1>Welcome to the Homepage</h1>

<button on:click={handleRedirect}>Create Game</button>
