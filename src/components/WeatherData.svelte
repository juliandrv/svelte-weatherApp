<script lang="ts">
  export let weather;
</script>

<img
  class="bg-secondary rounded-circle animate__animated animate__bounceIn animate__delay-1s"
  src={` http://openweathermap.org/img/wn/${weather.weather[0].icon}@2x.png`}
  alt={weather.weather[0].description}
/>
<h2>
  {weather.main.temp}°C
</h2>
<h4>
  City:
  <span class="fw-bold"> {weather.name}, {weather.sys.country} </span>
</h4>
<h4>
  Weather: <span class="fw-bold">{weather.weather[0].description}</span>
</h4>
<h4>
  Max. Temp:
  <span class="fw-bold text-danger">{weather.main.temp_max}°C </span>
</h4>
<h4>
  Min. Temp:
  <span class="fw-bold text-primary">
    {weather.main.temp_min}°C
  </span>
</h4>

<style>
  h4 {
    text-transform: capitalize;
  }
</style>
