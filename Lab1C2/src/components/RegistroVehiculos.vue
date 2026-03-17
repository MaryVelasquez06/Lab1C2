<template>
  <div>
    <h2>Registro de Vehículos</h2>

    <form @submit.prevent="agregarVehiculo">
      <input v-model="cliente" placeholder="Cliente" />
      <input v-model="placa" placeholder="Placa" />

      <button>Agregar</button>
    </form>

    <p v-if="mensaje">{{ mensaje }}</p>

    <ul>
      <li v-for="(v, i) in vehiculos" :key="i">
        {{ v.cliente }} - {{ v.placa }}
        <button @click="eliminarVehiculo(i)">X</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      cliente: '',
      placa: '',
      vehiculos: [],
      mensaje: ''
    };
  },
  methods: {
    agregarVehiculo() {
      if (!this.cliente || !this.placa) {
        this.mensaje = "Campos obligatorios";
        return;
      }

      this.vehiculos.push({
        cliente: this.cliente,
        placa: this.placa
      });

      this.mensaje = "Agregado correctamente";
      this.cliente = '';
      this.placa = '';
    },

    eliminarVehiculo(i) {
      this.vehiculos.splice(i, 1);
    }
  }
};
</script>