<script>
  import ContactCard from "./ContactCard.svelte";

  let name = "Max";
  let title = "";
  let image = "";
  let description = "";
  
  let formState = 'empty';

  let createdContacts = [];

  function addContact(event) {
    // event.preventDefault();
    if (
      name.trim().length == 0 || 
      title.trim().length == 0 || 
      image.trim().length == 0 || 
      description.trim().length == 0
    ) {
      formState = 'invalid';
      return;
    }
    // create object with key pair values
    // first example solution, using push, won't be detected by svelte 
    // therefore, use second example solution instead
    //
    // createdContacts.push({
    //   name: name, 
    //   jobTitle: title, 
    //   imageUrl: image, 
    //   desc: description  
    // });
    // formState = 'done';

    createdContacts = [
      ...createdContacts,
      {
      id: Math.random(),
      name: name, 
      jobTitle: title, 
      imageUrl: image, 
      desc: description  
    }];
    formState = 'done';
  }

function deleteFirst() {
  createdContacts = createdContacts.slice(1);
}

function deleteLast() {
  createdContacts = createdContacts.slice(0, -1);
}

</script>

<style>
  #form {
    width: 30rem;
    max-width: 100%;
    margin: 1rem 0;
  }
</style>

<form id="form">
  <div class="form-control">
    <label for="userName">User Name</label>
    <input type="text" bind:value={name} id="userName" />
  </div>
  <div class="form-control">
    <label for="jobTitle">Job Title</label>
    <input type="text" bind:value={title} id="jobTitle" />
  </div>
  <div class="form-control">
    <label for="image">Image URL</label>
    <input type="text" bind:value={image} id="image" />
  </div>
  <div class="form-control">
    <label for="desc">Description</label>
    <textarea rows="3" bind:value={description} id="desc" />
  </div>
  <button on:click|preventDefault={addContact} type="submit">Add Contact Card</button>
</form>

<!-- <button on:click={deleteFirst}>Delete First</button>
<button on:click={deleteLast}>Delete Last</button> -->
<!-- <button on:click="{(event) => {createdContacts = createdContacts.slice(1);}}">Delete First</button> -->
<button on:click="{event => createdContacts = createdContacts.slice(1)}>Delete First</button>
<button on:click={deleteLast}>Delete Last</button>

{#if formState === 'invalid'}
  <p>Incomplete input.</p>
{:else}
  <p>Please enter your data and hit the button.</p>
{/if}

{#each createdContacts as contact, i (contact.id)}
  <h2>#{i+1}</h2>
  <ContactCard 
    userName={contact.name} 
    jobTitle={contact.jobTitle} 
    description={contact.desc}
    userImage={contact.imageUrl} /> 
<!-- else case reacts on when the array is empty -->
{:else}
  <p>No contacts found. Please add at least one contact.</p>
{/each}