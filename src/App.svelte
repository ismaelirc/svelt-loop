<script>
  import ContactCard from "./ContactCard.svelte";

  let name = "";
  let title = "";
  let image = "";
  let description = "";
  let formState = 'empty';

  let createdContacts = [];

  function addContact(){
    if(name.trim().length == 0 || title.trim().length == 0 || image.trim().length == 0 || description.trim().length == 0){

      formState = 'invalid';
      return;
    } 

    createdContacts = [...createdContacts,{
      name: name,
      jobTitle: title,
      imageUrl: image,
      desc: description
    }];


    formState = 'done';
  }


</script>

<style>
  #form {
    width: 30rem;
    max-width: 100%;
  }
</style>

<div id="form">
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
  <div class="form-control">
    <textarea rows="3" bind:value={formState} />
  </div>
</div>

<button on:click={addContact}>Add Contact Card</button>
  
{#if formState === 'invalid'}
  <p>Invalid Form</p>
{:else}
  <p>Please, add some data and press the button</p>
{/if}

{#each createdContacts as contact, index}
<h2>#{index + 1}</h2>
<ContactCard 
              userName={contact.name} 
              jobTitle={contact.jobTitle} 
              description={contact.desc} 
              userImage={contact.imageUrl} />
{:else}
<p>Please start adding some contact!</p>
{/each}