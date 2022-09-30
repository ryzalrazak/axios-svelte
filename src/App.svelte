<script>
	import axios from "axios";
	import { onMount } from "svelte";
	import AddPerson from './AddPerson.svelte';
	const proxy = "http://localhost:8082/"
	//import cors from 'cors';

	// const submitForm = (event) => {
	// 	const formData = new FormData(event.target)
	// 	console.log(event);

	// };

	// const submitForm = () => {
	// 	console.log(firstName, lastName, age);
	// 	let form = document.getElementById('form');
	// 		axios.post('https://localhost:3001/users', new FormData (form))
	// 		.then(res => {
	// 			console.log(formData);
	// 		})
	// }

	

	let axdata = [];

	const getUsers = () => {
		axios.get("https://jsonplaceholder.typicode.com/users").then((res) => {
			axdata = res.data;
			console.log(res);
		});
	};

	onMount(getUsers);

	let users = [];

	const getUser = () => {
		axios.get("http://localhost:3000/products").then((response) => {
			users = response.data;
			console.log(response);
		});
	};

	onMount(getUser);


	
</script>

<main>
	<h1>TESTING</h1>

	<AddPerson />

	<h3>Fetch API from json Placeholder</h3>
	{#await axdata}
		Loading...
	{:then axdata}
		<ul>
			{#each axdata as data}
				<li>{data.name}</li>
			{/each}
		</ul>
	{:catch error}
		{error}
	{/await}

	<h3>Fetch API localhost</h3>

	{#await users}
		Loading...
	{:then users}
		<ul>
			{#each users as user}
				<li>{user.title}</li>
			{/each}
		</ul>
	{:catch error}
		{error}
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
