<script>
  let name = "";
  let lastname = "";
  let identification = null;
  let users = [];
  const fetchUrl = "http://localhost:8000/user";

  export async function getusers() {
    const response = await fetch("http://localhost:8000/user");
    const data = await response.json();
    users = data;
  }

  getusers();

  async function userPost() {
    const response = await fetch(fetchUrl, {
      method: "POST",
      body: JSON.stringify({
        name,
        lastname,
        identification,
      }),
      headers: {
        "content-type": "application/json",
      },
    });
  }
</script>

<form>
  <input placeholder="Nombre" bind:value={name} />
  <input placeholder="Apellido" bind:value={lastname} />
  <input placeholder="Identificacíon" bind:value={identification} />
  <button type="button" on:click={userPost} on:click={getusers}> SEND </button>
</form>

<div>
  <table class="userTable">
    <tr>
      <th>NAME</th>
      <th>LASTNAME</th>
      <th>IDENTIFICATION</th>
    </tr>
    {#each users as user}
      <tr>
        <td>{user.name}</td>
        <td>{user.lastname}</td>
        <td>{user.identification}</td>
      </tr>
    {/each}
  </table>
</div>