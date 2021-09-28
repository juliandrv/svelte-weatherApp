<script lang="ts">
  import Loading from "./Loading.svelte";
  import WeatherData from "./WeatherData.svelte";
  import Alert from "./Alert.svelte";

  const url: string = `https://api.openweathermap.org/data/2.5/weather`;
  const apiKey: string = `1e7ed95560959e71b42ef08745cf892f`;
  let city: string = "";

  const getWeatherData = async (city: string = "itagui") => {
    if (city.trim() === "") {
      throw new Error("It is necessary to fill the search input");
    }

    try {
      const res = await fetch(`${url}?q=${city}&units=metric&appid=${apiKey}`);
      const data = await res.json();
      return data;
    } catch (error) {}
  };

  let promise = getWeatherData();

  const handleSubmit = () => {
    promise = getWeatherData(city);
    city = "";
    // document.getElementById("query").focus();
  };
</script>

<div class="container ">
  <form on:submit|preventDefault={handleSubmit}>
    <label>
      Search: <input
        bind:value={city}
        id="query"
        class="form-control"
        type="text"
        placeholder="Enter a city"
      />
    </label>
    <button type="submit" class="btn btn-primary">Check</button>
  </form>

  {#await promise}
    <Loading />
  {:then weather}
    <div class="mt-5 animate__animated animate__fadeIn">
      {#if weather.cod === "404"}
        <Alert err="City not found!" />
      {:else}
        <WeatherData {weather} />
      {/if}
    </div>
  {:catch err}
    <Alert {err} />
  {/await}
</div>

<style>
  button {
    margin-top: -3px;
  }
</style>
