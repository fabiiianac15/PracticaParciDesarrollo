<script setup>
import { ref } from "vue";

const carSlots = ref([
  { active: true, value: 1000 },
  { active: true, value: 1100 },
  { active: true, value: 1200 },
  { active: true, value: 1300 },
  { active: true, value: 1400 },
  { active: true, value: 1500 },
]);

const bikeSlots = ref([
  { active: true, value: 200 },
  { active: true, value: 200 },
  { active: true, value: 200 },
]);

const total = ref(0);

const toggleCarSlot = (index) => {
  const car = carSlots.value[index];
  car.active = !car.active;
  total.value += car.active ? car.value : -car.value;
};

const toggleBikeSlot = (index) => {
  const bike = bikeSlots.value[index];
  bike.active = !bike.active;
  total.value += bike.active ? bike.value : -bike.value;
};

const restartTotal = () => {
  total.value = 0;
};
</script>

<template>
  <div class="container mx-auto p-6 bg-gradient-to-r from-blue-500 via-purple-500 to-pink-500 min-h-screen">
    <h1 class="font-bold mb-6 text-3xl text-center text-white">Parqueadero</h1>

    <div class="section mb-8">
      <h2 class="text-2xl font-semibold mb-4 text-white">Carriles de Autos</h2>
      <div class="grid grid-cols-3 gap-4">
        <div v-for="(car, index) in carSlots" :key="index">
          <div
            @click="toggleCarSlot(index)"
            :class="car.active ? 'bg-green-500 hover:bg-green-600' : 'bg-red-500 hover:bg-red-600'"
            class="slot w-24 h-24 flex justify-center items-center text-white rounded-lg cursor-pointer transition-transform transform hover:scale-105"
          >
            {{ car.active ? 'Libre' : 'Ocupado' }}
          </div>
        </div>
      </div>
    </div>

    <div class="section mb-8">
      <h2 class="text-2xl font-semibold mb-4 text-white">Carriles de Motos</h2>
      <div class="grid grid-cols-3 gap-4">
        <div v-for="(bike, index) in bikeSlots" :key="index">
          <div
            @click="toggleBikeSlot(index)"
            :class="bike.active ? 'bg-green-500 hover:bg-green-600' : 'bg-red-500 hover:bg-red-600'"
            class="slot w-24 h-24 flex justify-center items-center text-white rounded-lg cursor-pointer transition-transform transform hover:scale-105"
          >
            {{ bike.active ? 'Libre' : 'Ocupado' }}
          </div>
        </div>
      </div>
    </div>

    <div class="total-section text-center mt-12">
      <h2 class="text-2xl font-semibold mb-2 text-white">TOTAL A PAGAR</h2>
      <p class="text-3xl font-bold text-cyan-300">Total: {{ total }}</p>
    </div>

    <div class="text-center mt-6">
      <button @click="restartTotal" class="p-4 bg-yellow-500 rounded-lg text-white font-semibold hover:bg-yellow-600 transition-colors">
        Reiniciar
      </button>
    </div>
  </div>
</template>

<style scoped>
.container {
  max-width: 800px;
}

.section {
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
  padding-bottom: 2rem;
}

.slot {
  transition: transform 0.2s;
}
</style>