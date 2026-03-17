<template>
  <div>
    <h2>Registro de Vehículos</h2>

    <form @submit.prevent="agregarVehiculo">
      <label>Cliente:</label>
      <input v-model="cliente" type="text" placeholder="Cliente" />

      <label>Placa:</label>
      <input v-model="placa" type="text" placeholder="Placa" />

      <label>Servicio:</label>
      <select v-model="servicio">
        <option value="">Seleccione un servicio</option>
        <option value="Cambio de aceite">Cambio de aceite</option>
        <option value="Diagnóstico">Diagnóstico</option>
        <option value="Frenos">Frenos</option>
      </select>

      <label>Prioridad:</label>
      <select v-model="prioridad">
        <option value="">Seleccione prioridad</option>
        <option value="Alta">Alta</option>
        <option value="Media">Media</option>
        <option value="Baja">Baja</option>
      </select>

      <button :disabled="cliente.trim() === '' || placa.trim() === ''">
        Agregar
      </button>
    </form>

    <p v-if="mensaje">{{ mensaje }}</p>

    <ul v-if="errores.length > 0">
      <li v-for="(error, index) in errores" :key="index">
        {{ error }}
      </li>
    </ul>

    <p v-if="vehiculos.length === 0">No hay vehículos registrados.</p>

    <ul v-else>
      <li v-for="(v, i) in vehiculos" :key="i">
        {{ v.cliente }} - {{ v.placa }} - {{ v.servicio }} - {{ v.prioridad }}
        <button @click="eliminarVehiculo(i)">X</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'RegistroVehiculos',
  data() {
    return {
      cliente: '',
      placa: '',
      servicio: '',
      prioridad: '',
      vehiculos: [],
      mensaje: '',
      errores: []
    }
  },
  methods: {
    agregarVehiculo() {
      this.errores = []
      this.mensaje = ''

      if (!this.cliente.trim()) {
        this.errores.push('El cliente es obligatorio')
      }

      if (!this.placa.trim()) {
        this.errores.push('La placa es obligatoria')
      } else if (this.placa.trim().length < 3) {
        this.errores.push('La placa es incorrecta')
      }

      if (!this.servicio) {
        this.errores.push('Debe seleccionar un servicio')
      }

      if (!this.prioridad) {
        this.errores.push('Debe seleccionar una prioridad')
      }

      if (this.errores.length > 0) {
        return
      }

      this.vehiculos.push({
        cliente: this.cliente,
        placa: this.placa,
        servicio: this.servicio,
        prioridad: this.prioridad
      })

      this.mensaje = 'Agregado correctamente'

      this.cliente = ''
      this.placa = ''
      this.servicio = ''
      this.prioridad = ''
    },

    eliminarVehiculo(i) {
      this.vehiculos.splice(i, 1)
    }
  }
}
</script>