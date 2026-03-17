<template>
  <div class="contenedor">
    <h2>Sistema de Registro de Vehículos</h2>

    <form class="formulario" @submit.prevent="agregarVehiculo">
      <div class="campo">
        <label for="cliente">Cliente</label>
        <input id="cliente" v-model="cliente" type="text" placeholder="Ingrese el cliente" />
      </div>

      <div class="campo">
        <label for="placa">Placa</label>
        <input id="placa" v-model="placa" type="text" placeholder="Ingrese la placa" />
      </div>

      <div class="campo">
        <label for="servicio">Servicio</label>
        <select id="servicio" v-model="servicio">
          <option value="">Seleccione un servicio</option>
          <option value="Cambio de aceite">Cambio de aceite</option>
          <option value="Diagnóstico">Diagnóstico</option>
          <option value="Frenos">Frenos</option>
          <option value="Suspensión">Suspensión</option>
        </select>
      </div>

      <div class="campo">
        <label for="prioridad">Prioridad</label>
        <select id="prioridad" v-model="prioridad">
          <option value="">Seleccione prioridad</option>
          <option value="Alta">Alta</option>
          <option value="Media">Media</option>
          <option value="Baja">Baja</option>
        </select>
      </div>

      <div class="acciones">
        <button
          type="submit"
          :disabled="cliente.trim() === '' || placa.trim() === ''"
        >
          Agregar vehículo
        </button>
      </div>
    </form>

    <p v-if="mensaje" class="mensaje-exito">{{ mensaje }}</p>

    <ul v-if="errores.length > 0" class="lista-errores">
      <li v-for="(error, index) in errores" :key="index">
        {{ error }}
      </li>
    </ul>

    <div class="campo busqueda">
      <label for="busqueda">Buscar por placa</label>
      <input id="busqueda" v-model="busqueda" type="text" placeholder="Ejemplo: 140A" />
    </div>

    <p v-if="vehiculos.length === 0" class="sin-registros">
      No hay vehículos registrados.
    </p>

    <p v-else-if="vehiculosFiltrados.length === 0" class="sin-registros">
      No se encontraron resultados.
    </p>

    <div v-else class="tabla-contenedor">
      <table class="tabla">
        <thead>
          <tr>
            <th>#</th>
            <th>Cliente</th>
            <th>Placa</th>
            <th>Servicio</th>
            <th>Prioridad</th>
            <th>Acción</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(vehiculo, index) in vehiculosFiltrados" :key="index">
            <td>{{ index + 1 }}</td>
            <td>{{ vehiculo.cliente }}</td>
            <td>{{ vehiculo.placa }}</td>
            <td>{{ vehiculo.servicio }}</td>
            <td>
              <span
                class="badge"
                :class="{
                  alta: vehiculo.prioridad === 'Alta',
                  media: vehiculo.prioridad === 'Media',
                  baja: vehiculo.prioridad === 'Baja'
                }"
              >
                {{ vehiculo.prioridad }}
              </span>
            </td>
            <td>
              <button class="btn-eliminar" @click="eliminarVehiculo(index)">
                Eliminar
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
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
      errores: [],
      busqueda: ''
    }
  },
  computed: {
    vehiculosFiltrados() {
      return this.vehiculos.filter((v) =>
        v.placa.toLowerCase().includes(this.busqueda.toLowerCase())
      )
    }
  },
  methods: {
    agregarVehiculo() {
      this.errores = []
      this.mensaje = ''

      if (!this.cliente.trim()) {
        this.errores.push('El nombre del cliente es obligatorio.')
      }

      if (!this.placa.trim()) {
        this.errores.push('La placa es obligatoria.')
      } else if (this.placa.trim().length < 3) {
        this.errores.push('La placa ingresada es incorrecta.')
      }

      if (!this.servicio) {
        this.errores.push('Debe seleccionar un servicio.')
      }

      if (!this.prioridad) {
        this.errores.push('Debe seleccionar una prioridad.')
      }

      if (this.errores.length > 0) {
        return
      }

      this.vehiculos.push({
        cliente: this.cliente.trim(),
        placa: this.placa.trim(),
        servicio: this.servicio,
        prioridad: this.prioridad
      })

      this.mensaje = 'Vehículo agregado correctamente.'
      this.cliente = ''
      this.placa = ''
      this.servicio = ''
      this.prioridad = ''
    },

    eliminarVehiculo(index) {
      this.vehiculos.splice(index, 1)
      this.mensaje = 'Vehículo eliminado correctamente.'
    }
  }
}
</script>

<style scoped>
.contenedor {
  max-width: 950px;
  margin: 30px auto;
  padding: 25px;
  background: #ffffff;
  border-radius: 14px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.08);
  font-family: Arial, sans-serif;
}

h2 {
  text-align: center;
  color: #1f2937;
  margin-bottom: 25px;
}

.formulario {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 18px;
  margin-bottom: 20px;
}

.campo {
  display: flex;
  flex-direction: column;
}

.campo label {
  margin-bottom: 6px;
  font-weight: bold;
  color: #374151;
}

.campo input,
.campo select {
  padding: 10px 12px;
  border: 1px solid #cbd5e1;
  border-radius: 8px;
  font-size: 14px;
}

.campo input:focus,
.campo select:focus {
  outline: none;
  border-color: #2563eb;
  box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.15);
}

.acciones {
  grid-column: 1 / -1;
}

.acciones button {
  padding: 12px 18px;
  background: #2563eb;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-weight: bold;
}

.acciones button:hover {
  background: #1d4ed8;
}

.acciones button:disabled {
  background: #94a3b8;
  cursor: not-allowed;
}

.mensaje-exito {
  background: #dcfce7;
  color: #166534;
  padding: 12px;
  border-radius: 8px;
  margin-bottom: 15px;
}

.lista-errores {
  background: #fee2e2;
  color: #991b1b;
  padding: 12px 18px;
  border-radius: 8px;
  margin-bottom: 15px;
}

.busqueda {
  margin-bottom: 18px;
}

.sin-registros {
  text-align: center;
  color: #6b7280;
  margin-top: 20px;
}

.tabla-contenedor {
  overflow-x: auto;
}

.tabla {
  width: 100%;
  border-collapse: collapse;
  margin-top: 10px;
}

.tabla th,
.tabla td {
  padding: 12px;
  border-bottom: 1px solid #e5e7eb;
  text-align: center;
}

.tabla th {
  background: #1f2937;
  color: white;
}

.tabla tr:hover {
  background: #f9fafb;
}

.badge {
  display: inline-block;
  padding: 6px 10px;
  border-radius: 999px;
  color: white;
  font-size: 12px;
  font-weight: bold;
}

.alta {
  background: #dc2626;
}

.media {
  background: #f59e0b;
}

.baja {
  background: #16a34a;
}

.btn-eliminar {
  background: #ef4444;
  color: white;
  border: none;
  padding: 8px 12px;
  border-radius: 7px;
  cursor: pointer;
}

.btn-eliminar:hover {
  background: #dc2626;
}

@media (max-width: 700px) {
  .formulario {
    grid-template-columns: 1fr;
  }
}
</style>