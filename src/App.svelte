<script>
	import { executeGraphql } from "./utils.js";
	import { userInfo } from './store'

	import Keycloak from "keycloak-js";
	let kc = new Keycloak("/keycloak.json");

	let logged_in = null;

	let todos = [];

	kc.init({ onLoad: "check-sso" }).then((auth) => {
		logged_in = auth;
		if (auth) {
			logged_in = true;

			kc.loadUserInfo().then((user) => {
				user.token = kc.idToken
				userInfo.set(user)
			});
		}
	});

</script>

<h1>Svelte keycloak</h1>

{#if logged_in && $userInfo.preferred_username}

	<pre>{JSON.stringify($userInfo, null,2)}</pre>
	You are logged in as {$userInfo.preferred_username}

	<button
		on:click={() => {
			kc.logout();
		}}>Logout</button
	>

{/if}

{#if logged_in == false}
	You are not logged in
	<button
		on:click={() => {
			kc.login();
		}}>Login</button
	>
{/if}
