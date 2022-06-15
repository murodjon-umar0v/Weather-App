<template>
 <div
  id="app"
  class="w-screen h-screen bg-lime-600 flex justify-center items-center"
 >
  <WeatherCard />
  <Modal />
 </div>
</template>

<script>
import WeatherCard from "./components/WeatherCard.vue";
import Modal from "./components/Modal.vue";

export default {
 components: {
  WeatherCard,
  Modal,
 },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Jost:300,400,500,600,700");
</style>
