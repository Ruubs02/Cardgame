<script lang="ts">
	import { goto } from '$app/navigation';
	import { supabase } from '$lib/supabase';

	let email = '';
	let password = '';
	let username = '';

	let errorMessage = '';

	const handleSignUp = async () => {
		try {
			// Sign up with Email and Password and add them to the Auth Users table
			const { data: authData, error: authError } = await supabase.auth.signUp({
				email,
				password
			});

			// Add the Username to the players table
			if (authData.user) {
				const { error: dbError } = await supabase.from('players').insert([
					{
						user_id: authData.user.id,
						name: username
					}
				]);
			}

			if (authError) throw authError;

			goto('/');
		} catch (error) {
			if (error instanceof Error) {
				errorMessage = error.message;
			}
		}
	};
</script>

<main class="mx-auto max-w-md p-6">
	<h1 class="mb-6 text-2xl font-bold">Sign Up</h1>

	<!-- Sign Up Form -->
	<form on:submit|preventDefault={handleSignUp}>
		<!-- Username input -->
		<div class="mb-4">
			<label class="block text-sm font-medium text-gray-700" for="username">Username</label>
			<input
				class="mt-1 w-full rounded border border-gray-300 p-2"
				type="username"
				id="username"
				bind:value={username}
				required
			/>
		</div>

		<!-- Email input -->
		<div class="mb-4">
			<label class="block text-sm font-medium text-gray-700" for="email">Email</label>
			<input
				class="mt-1 w-full rounded border border-gray-300 p-2"
				type="email"
				id="email"
				bind:value={email}
				required
			/>
		</div>

		<!-- Password input -->
		<div class="mb-4">
			<label class="block text-sm font-medium text-gray-700" for="password">Password</label>
			<input
				class="mt-1 w-full rounded border border-gray-300 p-2"
				type="password"
				id="password"
				bind:value={password}
				required
			/>
		</div>

		{#if errorMessage}
			<p class="mt-2 text-sm text-red-500">{errorMessage}</p>
		{/if}

		<button type="submit" class="mt-4 w-full rounded bg-blue-500 p-2 text-white hover:bg-blue-600">
			Sign Up
		</button>
	</form>

	<div class="mt-4 text-center">
		<p class="text-sm">
			Already have an account? <a href="/auth/login" class="text-blue-500">Login</a>
		</p>
	</div>
</main>
