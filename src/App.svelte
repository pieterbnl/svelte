<script>
	import ContactCard from './ContactCard.svelte';

	let name = "Pieter";
	let age = 39;
	let title = "";	
	let description = "";
	let image = "";
		
	$: uppercaseName = name.toUpperCase(); // reruns whenever name changes
	// $: console.log(name);

	$: if (name == "Beernink") {
		console.log("it runs")
		age = 39;
	}

	function incrementAge() {
		age += 1;
	}

	function changeName() {
		name = 'Beernink';
	}

	function nameInput(event) {
		const enteredValue = event.target.value;
		name = enteredValue;
	}

	function jobTitleInput(event) {
		const enteredValue = event.target.value;
		jobTitle = enteredValue;
	}

	function descriptionInput(event) {
		const enteredValue = event.target.value;
		description = enteredValue;
	}
</script>

<style>
	h1 {
		color: purple;
	}
</style>

<h1>Hello {uppercaseName}! I've been told you are {age} years of age?</h1>
<button on:click="{incrementAge}">Age up</button><br><br><br>

<!-- <button on:click="{changeName}">Change Name</button> -->
<!-- <td><input type="text" value="{name}" on:input="{nameInput}"/></td> -->

<table>
	<th>User details</th>
	<tr>
		<td>Name:</td>
		<td><input type="text" bind:value={name} /></td>		
	</tr>	
	<tr>
		<td>Job Title: </td>
		<td><input type="text" bind:value={title} /></td>
	</tr>	
	<tr>
		<td>Description:</td>
		<td><textarea rows="3" bind:value={description}></textarea></td>
	</tr>	
	<tr>
		<td>Image URL:</td>
		<td><input type="text" bind:value={image} /></td>
	</tr>	
</table>
<br><br>

<strong>User details card</strong>

<ContactCard 
userName={name} 
jobTitle={title} 
description={description} 
userImage={image} />