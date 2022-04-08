<script>
	//Call free bored api 
	async function getActivity(){
		const res = await fetch('https://www.boredapi.com/api/activity');
		const activity = res.json();
		
		if(res.ok){		
			return activity
		}
		else{
			return new Error(activity);
		}
	}

	$:promise = getActivity();
	
	function handleClick(){
		//Reactive declartion is important here
		$:promise = getActivity();		
	}
</script>

<main>
	
	<button on:click={handleClick}>
		View Random Activity
	</button>

	{#await promise then value}
	<p>{value.activity}</p>
	{/await}
	
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>