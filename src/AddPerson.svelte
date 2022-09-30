
<script>
    import axios from 'axios';
let firstName;
let lastName;
let age;
let title;
let description;
let price;


async function handleSumbit()  {
    console.log(title, description,price);
        
		let form = document.getElementById('form')
       const json = JSON.stringify({ title, description, price });

        const res = await axios.post('http://localhost:3000/products', {title, description, price});

        // Axios automatically sets the `Content-Type` based on the
        // 2nd parameter to `axios.post()`.
        res.data.headers['Content-Type']; // 'application/x-www-form-urlencoded',
	};



</script>

<form on:submit|preventDefault={handleSumbit} id="form"> 
 
        <input id="title" type="text" placeholder="title" name="title" bind:value={title}>
        <input id="description" type="text" placeholder="description" name="description" bind:value={description}>
        <input id="price" type="number" placeholder="price" name="price" bind:value={price}>

    <br />
    <button id="btnSubmit" type="submit">Save</button>
</form>

