<script>
	import { supabase } from '$lib/supabase';

	let email = '';
	let password = '';

	let errorMessage = '';
	let successMessage = '';

	const handleSignUp = async () => {
		errorMessage = ''; // Reset error message before submission
		successMessage = ''; // Reset success message

		try {
			// Call Supabase sign-up API
			const { data, error } = await supabase.auth.signUp({
				email,
				password
			});

			if (error) {
				errorMessage = error.message; // If error, show the message
			} else {
				successMessage = 'Check your email to confirm your account!';
				// Optionally, redirect or take additional actions
			}
		} catch (err) {
			errorMessage = 'Something went wrong. Please try again later.'; // General error handling
		}
	};
</script>

<main class="mx-auto max-w-md p-6">
	<h1 class="mb-6 text-2xl font-bold">Sign Up</h1>

	<!-- Sign-up Form -->
	<form on:submit|preventDefault={handleSignUp}>
		<!-- Email Input -->
		<div class="mb-4">
			<label for="email" class="block text-sm font-medium text-gray-700">Email</label>
			<input
				type="email"
				id="email"
				bind:value={email}
				class="mt-1 w-full rounded border border-gray-300 p-2"
				required
			/>
		</div>

		<!-- Password Input -->
		<div class="mb-4">
			<label for="password" class="block text-sm font-medium text-gray-700">Password</label>
			<input
				type="password"
				id="password"
				bind:value={password}
				class="mt-1 w-full rounded border border-gray-300 p-2"
				required
			/>
		</div>

		<!-- Error Message -->
		{#if errorMessage}
			<p class="mt-2 text-sm text-red-500">{errorMessage}</p>
		{/if}

		<!-- Success Message -->
		{#if successMessage}
			<p class="mt-2 text-sm text-green-500">{successMessage}</p>
		{/if}

		<button type="submit" class="mt-4 w-full rounded bg-blue-500 p-2 text-white hover:bg-blue-600">
			Sign Up
		</button>
	</form>

	<!-- Login Link (if user already has an account) -->
	<div class="mt-4 text-center">
		<p class="text-sm">Already have an account? <a href="/login" class="text-blue-500">Login</a></p>
	</div>
</main>
