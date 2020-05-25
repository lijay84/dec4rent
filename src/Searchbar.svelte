<script>
  let query = "";
  let result;
  let storeResult = {};
  let inputValue = "";
  let mapurl = `https://maps.googleapis.com/maps/api/js?key=${process.env.gmapsKey}&libraries=places`;

  function handleClick(event) {
    if (event.target.value != "") {
      getResult(event.target.value);
    } else {
      storeResult = {};
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

    let protectedUrl = `${process.env.dkrentUrl}full-text-search.json?fullTextToSearch=${query}`;

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
      storeResult = {};
      let input = document.getElementById("searchGoogle");
      let options = {
        types: ["(cities)"],
        componentRestrictions: { country: "it" }
      };
      let autocomplete = new google.maps.places.Autocomplete(input, options);
    }
  }

  function checkResults(data, stringToSearch) {
    let stores = {};
    let re = stringToSearch != "" ? new RegExp(stringToSearch.toLowerCase(), "g") : "";

    if (data.length > 0) {
      stores = Object.values(data).filter(store =>
        store.city.toLowerCase().match(re)
      );
      if (stores.length != 0) {
        if (document.querySelector(".pac-container") != null) {
          document.querySelector(".pac-container").remove();
        }
        storeResult = stores;
      }
    }
  }

  function chooseStore(store) {
    inputValue = store.name;
    storeResult = {};
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
    cursor: pointer;
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
  @media (max-width: 575px) {
    .search-container {
      flex-direction: column;
    }
    .item {
      width: 100%;
      margin: 10px 0 0 0;
    }
    .container-stores {
      z-index: 2;
    }
  }
</style>

<svelte:head>
  <script src={mapurl} async defer>

  </script>
</svelte:head>

<div class="search-container">
  <div class="item">
    <input
      type="text"
      id="searchGoogle"
      placeholder="seleziona un luogo"
      on:input={handleClick}
      value={inputValue || ''} />
    {#if storeResult.length > 0}
      <div class="container-stores">
        {#each storeResult as item}
          <div class="item-store" on:click={e => chooseStore(item)}>
            {item.name}
          </div>
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
