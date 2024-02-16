<script setup>
import { ref } from 'vue';

let a = ref()
let actividad = ref("")
let fecha = ref("")
let arr = ref([])
function check() {
  let prioridad = a.value === true ? 'Alta' : 'Baja';
  arr.value.push({
    actividad: actividad.value,
    prioridad,
    fecha: fecha.value
  })
  actividad.value = ''
  fecha.value = ''
}

function ordenar() {
  arr.value.sort((z, b) => z.prioridad.localeCompare(b.prioridad))
}

function eliminar(i) {
  arr.value.splice(i, 1)
}

</script>

<template>
  <section class="papa">

    <section class="hijo">

      <input class="actividad" type="text" placeholder="  ✍🏼  Escribe tu asunto  ✍🏼" v-model="actividad">
      <input class="fecha" type="date" v-model="fecha">
      <section class="parted">
        <button @click="check()">+</button>
        <input type="checkbox" class="check" v-model="a">
        <button @click="ordenar()">Ordenar</button>
      </section>
    </section>

    <section class="hijoD">
      <table>
        <thead class="a">
          <tr class="tHead">
            <th>Actividad</th>
            <th>Prioridad</th>
            <th>Fecha</th>
            <th>Opciones</th>
          </tr>
        </thead>

        <tbody>
          <tr v-for="(item, i) in arr" :key="i" :style="item.prioridad === 'Alta' ? {backgroundColor:'rgba(255, 0, 0, 0.521)'} : ''">
            <td>{{ item.actividad }}</td>
            <td>{{ item.prioridad }}</td>
            <td>{{ item.fecha }}</td>
            <td>
              <button class="eliminar" @click="eliminar(i)">❌</button>
            </td>
          </tr>
        </tbody>

      </table>


    </section>

  </section>
</template>

<style scoped>
* {
  color: white;
}

.actividad {
  position: absolute;
  top: 7%;
  left: 5%;
  width: 50rem;
  height: 42px;
  padding-left: 20px;
}

.fecha {
  position: absolute;
  top: 17%;
  left: 5%;
  width: 240px;
  height: 40px;
  right: 400px;
  padding-left: 29px;
}

.papa {
  position: relative;
  background-color: white;
  padding: 300px;
  width: 650px;
  height: 170px;
}

.parted {
  position: relative;
  display: flex;
  gap: 20px;
  left: 95%;
  top: -130px;
}
/* Estilo del checkbox */
.check {
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  width: 40px;
  height: 40px;
  /* Ajuste del alto para que sea cuadrado */
  border: 4px solid black;
  /* Borde verde */
  background-color: #ffffff;
  /* Fondo blanco */
  border-radius: 4px;
  cursor: pointer;
  position: relative;
}

/* Estilo del chulo (tick) cuando está marcado */
.check:checked {
  border: 4px solid black;
  /* Borde verde */
  background-color: rgb(0, 132, 255);
  /* Fondo verde cuando está marcado */
  border-color: rgb(0, 132, 255);
  /* Borde verde cuando está marcado */
}

/* Estilo del chulo (tick) dentro del checkbox */
.check:checked::before {
  content: '\2713';
  /* Código unicode para el símbolo de chulo */
  display: block;
  width: 100%;
  height: 100%;
  font-size: 25px;
  /* Ajuste del tamaño del chulo para que sea más grande */
  font-weight: bold;
  /* Ajuste del peso del chulo */
  color: #ffffff;
  /* Color blanco del chulo */
  text-align: center;
  line-height: 35px;
  /* Ajuste del line-height para centrar verticalmente el chulo */
  position: absolute;
  /* Posiciona el chulo absolutamente dentro del checkbox */
  top: 0;
  left: 0;
}

table {
  border-collapse: collapse;
  width: 100%;
}

.hijoD {
  height: 400px;
  overflow-y: auto;
  position: absolute;
  width: 65rem;
  top: 64%;
  left: 50%;
  transform: translate(-50%, -50%);
}

td {
  font-weight: 500;
  color: black;
}
.tHead {
  background-color: rgb(0, 132, 255);
}

.eliminar {
  background-color: transparent;
}
</style>
