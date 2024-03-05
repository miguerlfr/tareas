<script setup>
import { ref } from 'vue';
import Swal from 'sweetalert2';

let a = ref()
let actividad = ref("")
let fecha = ref("")
let arr = ref([])

function check() {
  if (actividad.value.trim() === '' || fecha.value.trim() === '') {
    // Mostrar mensaje de error con SweetAlert2
    Swal.fire({
      icon: 'error',
      title: 'Oops...',
      text: 'Por favor, completa todos los campos.',
    });
    return;
  }

  let prioridad = a.value ? 'Alta' : 'Baja';
  arr.value.push({
    actividad: actividad.value,
    prioridad,
    fecha: fecha.value
  });
  actividad.value = '';
  fecha.value = '';
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
        <button class="buttonCheck" @click="check()">+</button>
        <input type="checkbox" class="check" v-model="a">
        <button class="ordenar" @click="ordenar()">Ordenar</button>
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
          <tr v-for="(item, i) in arr" :key="i" :style="item.prioridad === 'Alta' ? { backgroundColor: 'red', color: 'white' } : { backgroundColor: 'white', color: 'black' }">
            <td>{{ item.actividad }}</td>
            <td>{{ item.prioridad }}</td>
            <td>{{ item.fecha }}</td>
            <td>
              <button class="eliminar" :style="{ color: a.value ? 'white' : 'black' }" @click="eliminar(i)">x</button>
            </td>
          </tr>
        </tbody>

      </table>


    </section>

  </section>
</template>

<style scoped>
.actividad {
  position: absolute;
  top: 7%;
  left: 5%;
  width: 50rem;
  height: 42px;
  padding-left: 20px;
  background-color: #242424ec;
  color: white;
}

.fecha {
  position: absolute;
  top: 17%;
  left: 5%;
  width: 240px;
  height: 40px;
  right: 400px;
  padding-left: 29px;
  background-color: #242424ec;
  color: white;
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

.buttonCheck {
  background-color: #242424ec;
  color: white;
}
/* Estilo del checkbox */
.check {
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  width: 40px;
  height: 40px;
  /* Ajuste del alto para que sea cuadrado */
  border: 4px solid #242424ec;;
  /* Borde verde */
  background-color: #ffffff;
  /* Fondo blanco */
  border-radius: 4px;
  cursor: pointer;
  position: relative;
  color: white;
}

/* Estilo del chulo (tick) cuando está marcado */
.check:checked {
  border: 4px solid black;
  color: white;
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

.ordenar {
  background-color: #242424ec;
  color: white;
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
}
.tHead {
  background-color: rgb(0, 132, 255);
}

.eliminar {
  background-color: transparent;
  font-size: 15px;
}
</style>
