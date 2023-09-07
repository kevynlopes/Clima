<template>
  <div class="flex flex-col gap-12">
    <transition appear>
      <div
        class="flex justify-center items-center bg-white bg-opacity-20 backdrop-blur-lg rounded-2xl drop-shadow-lg w-96 h-28"
      >
        <div class="flex items-center justify-between gap-4">
          <div class="flex gap-4">
            <img src="../assets/lock.png" width="25" alt="lock" />
            <input
              @keypress.enter="puxarApi"
              v-model="dados"
              class="text-lg"
              type="text"
              placeholder="Adicione sua Localização."
            />
          </div>
          <button @click="puxarApi">
            <img src="../assets/search.png" width="20" alt="search" />
          </button>
        </div>
      </div>
    </transition>
    <transition>
      <div
        v-if="dado.name"
        class="flex flex-col items-center text-2xl pt-4 bg-white bg-opacity-20 backdrop-blur-lg rounded-2xl drop-shadow-lg gap-8 w-96 h-96"
      >
        <div class="flex items-center gap-3">
          {{ dado.name }}
          <img :src="`https://flagsapi.com/${dado.sys.country}/flat/32.png`" />
        </div>
        <p class="text-7xl">{{ parseInt(dado.main.temp) }} °C</p>
        <div class="flex items-center gap-2">
          <p class="descricao">{{ dado.weather[0].description }}</p>
          <img
            :src="`https://openweathermap.org/img/wn/${dado.weather[0].icon}.png`"
            alt=""
          />
        </div>
        <div class="flex gap-12">
          <div class="flex gap-2">
            <img src="../assets/humidity.png" alt="humidity" width="25" />
            <p>{{ dado.main.humidity }}%</p>
          </div>
          <div class="flex gap-2">
            <img src="../assets/wind.png" alt="humidity" width="25" />
            <p>{{ dado.wind.speed.toFixed(1) }}km/h</p>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dados: "",
      dado: "",
    };
  },
  methods: {
    puxarApi() {
      const api = `https://api.openweathermap.org/data/2.5/weather?q=${this.dados}&units=metric&appid=8922ca389fd95c0ffe26ee8d97751108&lang=pt_br`;

      fetch(api)
        .then((r) => r.json())
        .then((data) => {
          console.log(data);
          this.dado = data;
        });
    },
  },
};
</script>

<style>
.v-enter-active {
  transition: opacity 0.5s;
}

.v-enter {
  opacity: 0;
}
input {
  all: unset;
}
input {
  background-color: initial;
  border: initial;
  box-shadow: none;
}

.descricao {
  text-transform: capitalize;
}
</style>
