<script>
// @ts-nocheck



 /**
   * @type {never[]}
   */
 import Modal from "../lib/Modal.svelte";
 let meals = [];

 let display = false;
 const getMeals = async()  => {
  const res = await fetch("https://www.themealdb.com/api/json/v1/1/search.php?f=b")
  const data = await res.json();
  meals = data.meals;
  return meals;
 }

 // @ts-ignore
 function delete1(mealid) {
    console.log(mealid);
    return meals.filter(i => i.idMeal !== mealid);
 }

 function edit() {
    display = true;
 }

 function cancel() {
    display = false;
 }

</script>


{#if display}
  <Modal on:cancel={cancel} idMeal={meals} />
{/if}

{#await getMeals()}
  <p>Loading...</p>
{:then meals} 
  {#each meals as meal}
    <div class="fcontainer">
      <div class="card">
        <h2 class="title"><b>{meal.strMeal}</b></h2>
        <img src="{meal.strMealThumb}" alt="{meal.strMeal}" style="width:100%">
        <div class="container">
          <h4 class="desc">{meal.strTags}</h4>
          <p class="ellipsis">{meal.strInstructions}</p>
        </div>
        <div class="buttons">
          <button class="edit" on:click={edit} >Edit</button>
          <button class="delete" on:click={() => {delete1(meal.idMeal)}} >Delete</button>
        </div>
      </div>
    </div>
  {/each}
{/await}



<style>
  .title, .desc {
    margin-left: 6rem;
  }

  .fcontainer {
    width: 80%;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
  }

  .card {
    box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
    transition: 0.3s;
    max-width: 25rem;
    height: 40rem;
    
    margin: 1rem;
  }

  .card:hover {
    box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
  }

  .ellipsis { 
    white-space: nowrap;
    width: 350px;
    text-overflow: ellipsis; 
    overflow: hidden;}

  .container {
    padding: 2px 16px;
  }

  .buttons {
    display: flex;
    justify-content: space-around;
    text-align: center;
    border: none;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    cursor: pointer;
  }

  .edit {
    background-color: #f7e30b;
    padding: 10px 16px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    cursor: pointer;
    border: none;
    color: white;
  }

  .delete {
    background-color: #f44336;
    padding: 10px 16px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    cursor: pointer;
    border: none;
    color: white;
  }
</style>

