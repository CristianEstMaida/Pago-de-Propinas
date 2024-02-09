<template>
  <div class="encabezado">
    <h1>Pago de Propinas</h1>
  </div>
  <div class="total-propinas">
    <p>Total de Propinas</p>
    <label for="monto-total">$</label>
    <input type="number" id="monto-total" v-model="montoTotal" min="0" />
  </div>
  <div class="division-propinas">
    <label for="cantidad-personas">
      ¿Entre cuántos quieres dividir las propinas?
    </label>
    <input
      type="number"
      id="cantidad-personas"
      v-model="cantidadPersonas"
      min="1"
    />
    <p>${{ montoPersona }} por Persona</p>
  </div>
  <div class="metodo-pago">
    <label for="metodo-pago">Método de Pago:</label>
    <select id="metodo-pago" v-model="metodoPago">
      <option value="efectivo">Efectivo</option>
      <option value="tarjeta">Tarjeta</option>
    </select>
  </div>
  <div class="teclado-numerico">
    <label for="montoRealizarPago">$</label>
    <input
      type="number"
      id="monto-realizar-pago"
      v-model="montoRealizarPago"
      min="0"
    />
  </div>
  <div class="pagos">
    <p>Total Pagado ${{ totalPagado }}</p>
    <p>Restante por Pagar ${{ montoRestante }}</p>
    <button @click="realizarPago">
      Pagar ${{ montoRealizarPago }} en Propinas
    </button>
  </div>
  <div class="hello">
    <h1>{{ msg }}</h1>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";

@Options({
  props: {
    msg: String,
    totalPropinas: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      metodoPago: "efectivo",
      cantidadPersonas: this.cantidadPersonas,
      montoPersona: this.montoPersona,
    };
  },
  computed: {
    montoPersona() {
      return this.montoTotal / this.cantidadPersonas;
    },
  },
  watch: {
    cantidadPersonas() {
      this.montoPersona = this.montoTotal / this.cantidadPersonas;
      return this.montoPersona;
    },
    montoTotal() {
      if (this.montoTotal < this.totalPagado) {
        // Mostrar mensaje de error
        this.montoTotal = this.totalPagado; // Restablecer monto total
      }
      this.montoRestante = this.montoTotal - this.totalPagado;
      this.montoPersona = this.montoTotal / this.cantidadPersonas;
      return this.montoPersona;
    },
    montoRealizarPago() {
      return this.montoRealizarPago;
    },
  },
  methods: {
    realizarPago() {
      // Actualizar total pagado
      if (this.montoRealizarPago + this.totalPagado <= this.montoTotal) {
        this.totalPagado += this.montoRealizarPago;

        this.montoRestante = this.montoTotal - this.totalPagado;
      }
    },
  },
})
export default class HelloWorld extends Vue {
  msg!: string;
  montoTotal = 1500;
  cantidadPersonas = 5;
  montoPersona = 500;
  montoRealizarPago = 300;
  totalPagado = 0;
  montoRestante = 1500;
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.main-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}
.encabezado {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 80%;
  margin: 10px auto;
}

.encabezado h1 {
  font-size: 24px;
  font-weight: bold;
}

.encabezado p {
  font-size: 18px;
}

.total-propinas input {
  width: 200px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 10px;
}

.division-propinas {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 80%;
  margin: 10px auto;
}

.division-propinas label {
  font-size: 16px;
}

.division-propinas input {
  width: 40px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 10px;
}

.division-propinas p {
  font-size: 18px;
}

.metodo-pago {
  /* Estilos generales del componente */
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 5px;

  /* Estilos específicos de cada elemento dentro del componente */
  .titulo {
    font-weight: bold;
    font-size: 18px;
  }

  .opciones-pago {
    display: flex;
    flex-wrap: wrap;
  }

  .opcion-pago {
    margin: 10px;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }

  .imagen-tarjeta {
    width: 50px;
  }

  .numero-tarjeta {
    font-size: 16px;
  }

  .vencimiento-tarjeta {
    font-size: 14px;
  }

  /* ... y así sucesivamente para cada elemento del componente */
}

.resumen-pago {
  /* Estilos generales del componente */
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 5px;

  /* Estilos específicos de cada elemento dentro del componente */
  .titulo {
    font-weight: bold;
    font-size: 18px;
  }

  .tabla-resumen {
    width: 100%;
    border-collapse: collapse;
  }

  .fila-resumen {
    border-bottom: 1px solid #ddd;
  }

  .celda-resumen {
    padding: 5px;
    text-align: right;
  }

  .total-pago {
    font-weight: bold;
    font-size: 18px;
  }

  /* ... y así sucesivamente para cada elemento del componente */
}

.resumen-pago {
  /* Estilos generales del componente */
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 5px;

  /* Estilos específicos de cada elemento dentro del componente */
  .titulo {
    font-weight: bold;
    font-size: 18px;
  }

  .tabla-resumen {
    width: 100%;
    border-collapse: collapse;
  }

  .fila-resumen {
    border-bottom: 1px solid #ddd;
  }

  .celda-resumen {
    padding: 5px;
    text-align: right;
  }

  .total-pago {
    font-weight: bold;
    font-size: 18px;
  }

  /* ... y así sucesivamente para cada elemento del componente */
}

.teclado-numerico {
  /* Estilos generales del componente */
  margin: 10px auto;

  input {
    width: 200px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 10px;
  }

  /* Estilos específicos de cada elemento dentro del componente */
  .boton-numerico {
    width: 30px;
    height: 30px;
    margin: 5px;
    border: 1px solid #ddd;
    border-radius: 5px;
    text-align: center;
  }

  .boton-especial {
    background-color: #ccc;
  }

  /* ... y así sucesivamente para cada elemento del componente */
}

.pagos {
  /* Estilos generales del componente */
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 5px;

  /* Estilos específicos de cada elemento dentro del componente */
  .titulo {
    font-weight: bold;
    font-size: 18px;
  }

  .lista-pagos {
    list-style: none;
    padding: 0;
  }

  .item-pago {
    margin: 10px;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }

  .fecha-pago {
    font-size: 14px;
  }

  .monto-pago {
    font-weight: bold;
    font-size: 16px;
  }

  /* ... y así sucesivamente para cada elemento del componente */
}

h1 {
  width: 80%;
  margin: 10px auto;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
