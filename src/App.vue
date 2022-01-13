<template>
  <!-- The typeof condition here is changing the background of the temperature if is greater 16 -->
  <div
    id="app"
    :class="
      typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : ''
    "
  >
    <!-- The Loading Component is Preloader 1 -->
    <Preloader />

    <main>
      <div class="title">
        <h1>Weather App</h1>
      </div>

      <div class="title-sub">
        <p>Developed by dicetheDev</p>
      </div>

      <div class="search-box">
        <span class="las la-search"></span>
        <input
          type="search"
          class="search-bar"
          placeholder="Search here..."
          v-model="query"
          v-on:keypress="fetchWeather"
        />
      </div>

      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">
            {{ weather.name }}, {{ weather.sys.country }}
          </div>
          <div class="date">{{ dateBuilder() }}</div>
        </div>

        <div class="weather-box">
          <div class="temp">{{ Math.round(weather.main.temp) }}°C</div>
          <div class="weather">{{ weather.weather[0].main }}</div>
        </div>
      </div>
    </main>
  </div>
</template>


<script>
import Preloader from "./components/Preloader.vue";
export default {
  name: "app",
  data() {
    return {
      api_key: "a13e3e73e679d0cb0236ece180176e71",
      url_base: "https://api.openweathermap.org/data/2.5/",
      query: "", // this query here is bond to the Search in the template above
      weather: {},
    };
  },
  components: {
    Preloader,
  },
  methods: {
    //in case i don't want to call this function every single time or method that is why i created a condition inside fetchWeather
    fetchWeather(e) {
      if (e.key == "Enter") {
        //fetch is a javascript API that allow us to make request
        fetch(
          `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
        )
          .then((respond) => {
            return respond.json();
          })
          .then(this.setResults);
      }
    },
    setResults(results) {
      this.weather = results;
    },
    dateBuilder() {
      let d = new Date();
      let months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return `${day} ${date} ${month} ${year}`;
    },
  },
};
</script>


<style>
@import url("https://fonts.googleapis.com/css2?family=Rubik:wght@300;400;500;600&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: "Rubik", sans-serif;
}

#app {
  background-image: url("./assets/blurred-cold.jpg");
  background-size: cover;
  background-position: bottom;
  transition: 0.5s;
}

/*this image is changing the backgound when is warm */
#app.warm {
  background-image: url("./assets/warm-bg.jpg");
}

main {
  min-height: 100vh;
  padding: 25px;

  background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.25),
    rgba(0, 0, 0, 0.75)
  );
}

.title {
  display: flex;
  justify-content: center;
  align-items: center;
}
.title h1 {
  margin: 18px;
  padding: 14px;
  font-size: 40px;
  font-style: normal;
  color: #fff;
}

.title-sub p {
  display: flex;
  margin-bottom: 40px;
  font-size: 18px;
  justify-content: center;
  align-items: center;
  color: #fff;
}

.search-box {
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;

  color: #313131;
  font-size: 16px;

  appearance: none;
  border: none;
  outline: none;
  background: none;

  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 16px;
  transition: 0.5s;
}

.search-box .search-bar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px;
}

.location-box .location {
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.location-box .date {
  color: #fff;
  font-size: 18px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}

.weather-box {
  text-align: center;
}

.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 102px;
  font-weight: 900;

  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(0, 140, 255, 0.493);
  border-radius: 16px;
  margin: 30px 0px;

  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.weather-box .weather {
  color: #fff;
  font-size: 48px;
  font-weight: 600;
  font-style: italic;
}
</style>
