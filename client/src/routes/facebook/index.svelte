<script>
    	import { onMount } from 'svelte';

	onMount(() => {
        fbAsyncInit()
	});
	 const fbAsyncInit = function () {
		FB.init({
			appId: '2945418792437629',
			cookie: true,
			xfbml: true,
			version: "v12.0"
		});

		FB.AppEvents.logPageView();
	};

	(function (d, s, id) {
		var js,
			fjs = d.getElementsByTagName(s)[0];
		if (d.getElementById(id)) {
			return;
		}
		js = d.createElement(s);
		js.id = id;
		js.src = 'https://connect.facebook.net/en_US/sdk.js';
		fjs.parentNode.insertBefore(js, fjs);
	})(document, 'script', 'facebook-jssdk');

	export function loginWithFacebook() {
        console.log("zeze")
		FB.login(
			(response) => {
				const {
					authResponse: { accessToken, userID }
				} = response;

				fetch('https://localhost:4000/user/facebook-login', {
					method: 'POST',
					headers: {
						'Content-type': 'application/json'
					},
					body: JSON.stringify({ accessToken, userID })
				}).then((res) => {
					console.log(res);
				});
			},
			{ scope: 'public_profile, email' }
		);
	}
</script>

<button on:click|preventDefault={loginWithFacebook}> Click me </button>
