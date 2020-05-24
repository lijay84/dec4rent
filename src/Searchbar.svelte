<script>
  let query = "";
  let result;
  let bro = {};

  function handleClick(event) {
    console.log("test", event.target.value);
    if (event.target.value != "") {
      getResult(event.target.value);
    } else {
      bro = {};
    }
  }
  function handleErrors(response) {
    if (!response.ok) {
      if (document.getElementsByClassName("pac-container").length == 0)
        getGmapsResults();
    }
    return response;
  }
  async function getResult(query) {
    let protectedUrl = `https://api-eu.preprod.decathlon.net/dktrent/api/v1/sites/full-text-search.json?fullTextToSearch=${query}`;

    await fetch(protectedUrl, {
      method: "GET",
      headers: {
        "content-type": "application/json",
        "x-api-key": "771e8ae7-04ae-498a-8141-5568016852c5"
      }
    })
      .then(handleErrors)
      .then(response => response.json())
      .then(result => checkResults(result, query))
      .then(getGmapsResults())
      .catch(err => {
        console.log("err", err);
      });
  }

  function getGmapsResults() {
    if (document.getElementsByClassName("pac-container").length == 0) {
      bro = {};
      var input = document.getElementById("searchGoogle");
      var options = {
        types: ["(cities)"],
        componentRestrictions: { country: "it" }
      };
      let autocomplete = new google.maps.places.Autocomplete(input, options);
    }
  }

  function checkResults(data, stringToSearch) {
    let stores = {};
    var re =
      stringToSearch != "" ? new RegExp(stringToSearch.toLowerCase(), "g") : "";

    if (data.length > 0) {
      stores = Object.values(data).filter(store =>
        store.city.toLowerCase().match(re)
      );
      if (stores.length != 0) {
        if (document.querySelector(".pac-container") != null) {
          document.querySelector(".pac-container").remove();
        }
        bro = stores;
        bro = stores;
      }
    }
  }
</script>

<style type="text/scss">
  .search-container {
    display: flex;
  }

  .container-stores {
    border-radius: 2px;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.3);
    position: absolute;
    background-color: white;
    width: 100%;
  }
  .item-store {
    text-transform: uppercase;
    font-family: "Roboto Condensed", serif;
    align-items: center;
    cursor: default;
    border: 0;
    font-size: 16px;
    min-height: 45px;
    padding-left: 10px;
    display: flex;
  }
  .search-container {
    display: flex;
    max-width: 950px;
    margin: auto;
    background-color: #fff !important;
    padding: 10px;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.3);
    margin-top: -20px;
  }
  .item {
    width: 33.33%;
    margin: 10px;
    position: relative;
    word-break: break-all;
  }
  input,
  select {
    padding: 6px 20px;
    text-transform: uppercase;
    width: 100%;
    font-family: "Roboto Condensed", serif;
    border: 1px solid #999;
    outline: 0;
    padding: 6px 20px;
    height: 45px;
    font-size: 16px;
    margin: 0;
    background-color: white;
  }
</style>

<div class="search-container">
  <div class="item">
    <input
      type="text"
      id="searchGoogle"
      placeholder="seleziona un luogo"
      on:input={handleClick} />
    {#if bro.length > 0}
      <div class="container-stores">
        {#each bro as item}
          <div class="item-store">{item.name}</div>
        {/each}
      </div>
    {/if}
  </div>
  <div class="item">
    <select>
      <option value="">seleziona uno sport</option>
      <option value="sci">sci</option>
      <option value="snowboard">snowboard</option>
    </select>
  </div>
  <div class="item">
    <input type="date" />
  </div>
</div>
