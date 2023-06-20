
<script>
  function submitForm() {
    console.log();
  }
</script>

<style>
   button {
    margin-top: 1rem;
    border: 1px solid #cf0056;
    background: #cf0056;
    padding: 0.5rem 1rem;
    color: white;
    border-radius: 5px;
    box-shadow: 1px 1px 3px rgba(0, 0, 0, 0.26);
    cursor: pointer;
    text-decoration: none;
  }
  input {
    display: block;
    width: 100%;
    text-align: auto;
    border: none;
    border-bottom: 2px solid #ccc;
    border-radius: 3px 3px 0 0;
    background: white;
    padding: 0.15rem 0.25rem;
    transition: border-color 0.1s ease-out;
  }

  input:focus {
    border-color: #e40763;
    outline: none;
  }

  div {
    margin-top: 30px;
    margin: auto;
    width: 50%;
    padding: 10px;
  }
</style>

<div >
  <form on:submit|preventDefault={submitForm}>
    <label for="fname">First name:</label><br>
    <input type="text" required name="fname"><br>
    <label for="lname">Last name:</label><br>
    <input type="text" required name="lname">
    <label for="phoneNumber">Phone Number:</label>
    <input type="number" name="phoneNumber" required>
    <label for="email">Email</label>
    <input type="email" name="email" required>
    <button type="button" on:click={submitForm}>Submit</button>
  </form>
</div>
