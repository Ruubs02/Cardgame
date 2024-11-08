<script lang="ts">
	import '../app.css';
	import { page } from '$app/stores';
	import Navbar from '../components/navbar.svelte';
</script>

{#if $page.url.pathname !== '/auth/login' && $page.url.pathname !== '/auth/signup'}
	<Navbar />
{/if}

<slot />
