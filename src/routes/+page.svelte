<script>
 let meals = [];
 const getMeals = async()  => {
  const res = await fetch("https://www.themealdb.com/api/json/v1/1/search.php?f=b")
  const data = await res.json();
  meals = data.meals;
  return meals;
 }
 
</script>

{#await getMeals()}
  <p>Loading...</p>
{:then meals} 
  {#each meals as meal}
    <div class="card">
      <img src="{meal.strMealThumb}" alt="{meal.strMeal}" style="width:100%">
      <div class="container">
        <h4><b>{meal.strMeal}</b></h4>
        <p>{meal.strInstructions}</p>
      </div>
    </div>
  {/each}
{/await}



<style>
  .card {
    box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
    transition: 0.3s;
    width: 40%;
  }

  .card:hover {
    box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
  }

  .container {
    padding: 2px 16px;
  }
</style>

