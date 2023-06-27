<template>
  <div class="border">
    <div class="image">
      <div class="over">
        <h3 @click="setNombre">{{ Nombre }}</h3>
        <h4>Subtitle</h4>
      </div>
      <img :src="image2" alt="img" />
    </div>
    <div class="content">
      <p class="proposito"></p>
      <div class="stats">
        <div v-for="item in stats(20)" class="stat-value">
          <h2>{{ item.stat }}</h2>
          <h2>
            {{ item.value }}
          </h2>
        </div>
      </div>
    </div>
  </div>
  <div class="accion">
    <button @click="setIntencion">Roll!!</button>
    <button @click="">Stats</button>
    <h1>{{ Intencion }}</h1>
  </div>
</template>

<script setup>
import { ref, compile } from "vue";

import image2 from "../../assets/images/Dorothy.webp";
import { CombateAccion, Nombres } from "../../assets/data/db";

const ItemPick = (num) => {
  return Math.ceil(Math.random() * num);
};

const tableItem = (array) => {
  return array[ItemPick(array.length)];
};

const Intencion = ref(tableItem(CombateAccion).resultado);
const setIntencion = () => {
  Intencion.value = ref(tableItem(CombateAccion).resultado);
};

const Nombre = ref(tableItem(Nombres).resultado);
const setNombre = () => {
  Nombre.value = ref(tableItem(Nombres).resultado);
};

const stats = (num) => {
  const max = num / 4;
  const keys = ["Fort", "Dest", "Inte", "Cord"];
  const result = [];
  for (let index = 0; index < 4; index++) {
    let temp = Math.ceil(Math.random() * max);
    num = num - temp;
    result.push({ stat: keys[index], value: temp });
  }
  console.log(result);
  return result;
};
</script>

<style scoped>
.border {
  position: relative;
  border: 4px solid black;
  height: 600px;
  width: 400px;
  border-radius: 20px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
}

.over {
  position: absolute;
  margin: 0;
  top: 5px;
  left: 35px;
}

.over h3,
h4 {
  margin: 0.5rem;
  padding: 0.25rem;
  background: gray;
  border-radius: 7px;
}

.image {
  width: 90%;
  margin: 1rem;
  border-radius: 20px;
  overflow: hidden;
}

.image img {
  width: 100%;
}

.stats {
  display: flex;
  justify-content: space-around;
  margin: 2rem auto;
}

.stats * {
  margin: auto 1rem;
  text-align: center;
}

.stat-value {
  border: 2px gray solid;
  border-radius: 20px;
}
</style>
