<template>
 <div class="text-center lg:w-1/4 md:w-1/3 w-4/5">
  <div class="rounded-xl p-5" id="glassmorphismic-card">
   <div
    class="flex items-center pr-4 bg-white border-2 rounded-full border border-gray-400 text-sm"
   >
    <input
     type="text"
     v-model="city"
     class="p-2 px-4 w-4/5 rounded-full outline-none"
     placeholder="Enter a city..."
     @keyup.enter="getWeather"
    />
    <input
     class="w-1/5 text-right outline-none rounded-full"
     readonly
     v-model="country"
    />
   </div>

   <div class="pt-12">
    <span class="text-gray-600">
     Feels like: <b>{{ feelsLike }} <sup>o</sup></b>
    </span>
   </div>

   <div id="display" class="pt-12">
    <div
     class="rounded-full relative w-40 h-40 mx-auto flex justify-center items-center text-6xl font-bold shadow-2xl"
    >
     <span
      class="absolute -top-4 -left-4 text-sm w-20 h-20 flex justify-center items-center"
     >
      <span class="text-gray-600">
       <img
        v-if="weather == 'Clear'"
        src="https://icon-library.com/images/sun-icon-png/sun-icon-png-27.jpg"
       />
       <img
        v-else-if="weather == 'Rain'"
        src="https://icon-library.com/images/rain-icon-png/rain-icon-png-2.jpg"
       />
       <img
        v-else-if="weather == 'Snow'"
        src="https://icons.iconarchive.com/icons/google/noto-emoji-travel-places/512/42672-cloud-with-snow-icon.png"
       />
       <img
        v-else-if="weather == 'Clouds'"
        src="https://icon-library.com/images/cloud-icon-png/cloud-icon-png-6.jpg"
       />
      </span>
     </span>
     {{ temp }}<sup class="text-sm pb-10">o</sup>
    </div>
   </div>

   <div class="py-6 text-xl">
    {{ weather }}
   </div>

   <div class="flex justify-between border-t-2 pt-6 text-sm">
    <span class="flex flex-nowrap">
     <img class="pr-1" src="../assets/Wind.svg" /> {{ wind }} km/h
    </span>

    <span class="flex flex-nowrap">
     <img class="pr-1" src="../assets/Drop.svg" /> {{ humidity }} %
    </span>

    <span class="flex flex-nowrap">
     <img class="pr-1" src="../assets/Cloud.svg" /> {{ clouds }} %
    </span>
   </div>

   <!-- github link -->
  </div>
  <div class="flex justify-center items-center pt-4">
   <a
    href="https://github.com/murodjon-umar0v"
    target="_blank"
    class="flex flex-row justify-center"
   >
    <svg
     xmlns="http://www.w3.org/2000/svg"
     width="1em"
     height="1em"
     viewBox="0 0 24 24"
     fill="none"
     stroke="currentColor"
     stroke-width="2"
     stroke-linecap="round"
     stroke-linejoin="round"
     class="feather feather-github"
    >
     <path
      d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"
     ></path>
    </svg>
    <span class="pl-1">Github Repository</span>
   </a>
  </div>
 </div>
</template>

<script>
export default {
 name: "WeatherCard",
 data() {
  return {
   apiKey: "a34f80c8bbcc79e06c1ad993edec04d7",
   city: "Tashkent",
   country: "UZ",
   feelsLike: "",
   temp: "",
   wind: "",
   humidity: "",
   clouds: "",
   weather: "",
  };
 },

 watch: {
  temp: function (val) {
   this.temp = Math.round(val);
  },
  feelsLike: function (val) {
   this.feelsLike = Math.round(val);
  },
  weather: function (val) {
   this.weather = val;
   var bg = document.getElementById("app");
   if (this.weather == "Clouds") {
    bg.style.backgroundImage =
     "url('https://img.freepik.com/free-photo/clouds_328046-27567.jpg?w=740')";
   } else if (this.weather == "Clear") {
    bg.style.backgroundImage =
     "url('https://img.freepik.com/free-photo/clouds-blue-sky-wallpaper_53876-71443.jpg?t=st=1655117639~exp=1655118239~hmac=76502eecc2460db254d8b05ad283ef04f237078cc59a87ca63ebd55d7dd15995&w=740')";
   } else if (this.weather == "Rain") {
    bg.style.backgroundImage =
     "url('https://img.freepik.com/free-photo/view-glass-wet-from-rain_611712-2412.jpg?w=740')";
   } else if (this.weather == "Snow") {
    bg.style.backgroundImage =
     "url('https://img.freepik.com/free-photo/3d-snowy-winter-landscape_1048-11056.jpg?t=st=1655118614~exp=1655119214~hmac=7f8ee619f9a88cc0b649721157e8f33b2849bd8c8abfa9a841791b6ce8f39ad5&w=740')";
   } else if (this.weather == "Mist") {
    bg.style.backgroundImage =
     "url('https://img.freepik.com/free-photo/mesmerizing-shot-skyscrapers-city-covered-mist-night_181624-45438.jpg?t=st=1655119060~exp=1655119660~hmac=13a236865e4c4e011b6e6c9dec9d5e2fff5ee21bb301c33206aaef8a0b2d9dfd&w=740')";
   }
  },
 },

 mounted() {
  this.getWeather();
 },

 methods: {
  getWeather() {
   const url = `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${this.apiKey}&units=metric`;
   fetch(url)
    .then((response) => response.json())
    .then((data) => {
     if (data.cod == 200) {
      this.country = data.sys.country;
      this.feelsLike = data.main.feels_like;
      this.temp = data.main.temp;
      this.wind = data.wind.speed;
      this.humidity = data.main.humidity;
      this.clouds = data.clouds.all;
      this.weather = data.weather[0].main;
      console.log(data);
     } else {
      alert("City not found");
     }
    });
  },
 },
};
</script>
