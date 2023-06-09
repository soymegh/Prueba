<template>
  <div class="q-pa-md">
    <h2>Editar Cliente</h2>
    <q-form @submit="actualizarCliente" class="q-gutter-md">
      <q-input
        v-model="cliente.compañia"
        label="Compañía"
        dense
        required
      ></q-input>
      <q-input
        v-model="cliente.contacto"
        label="Contacto"
        dense
        required
      ></q-input>
      <q-input
        v-model="cliente.correo"
        label="Correo"
        type="email"
        dense
        required
      ></q-input>
      <q-input
        v-model="cliente.telefono"
        label="Teléfono"
        type="tel"
        dense
        required
      ></q-input>
      <q-input
        v-model="cliente.direccion"
        label="Dirección"
        dense
        required
        disabled
      ></q-input>
      <q-input
        v-model="cliente.ciudad"
        label="Ciudad"
        dense
        required
        disabled
      ></q-input>
      <q-input
        v-model="cliente.pais"
        label="País"
        dense
        required
        disabled
      ></q-input>
      <div class="q-mt-lg">
        <q-btn
          type="submit"
          label="Guardar"
          color="primary"
          class="full-width"
        ></q-btn>
      </div>
    </q-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      cliente: {
        id: null,
        compañia: '',
        contacto: '',
        correo: '',
        telefono: '',
        direccion: '',
        ciudad: '',
        pais: ''
      }
    };
  },
  created() {
    // Obtener el ID del cliente de la URL
    const clienteId = this.$route.params.clienteId;

    // Buscar el cliente en la lista de clientes
    this.cliente = this.clientes.find(c => c.id === parseInt(clienteId));
  },
  methods: {
    actualizarCliente(clienteId) {
      this.clienteId = clienteId;
      const rutaActual = this.$route.fullPath;
      const nuevaRuta = `/actualizar/${clienteId}`;
      console.log(nuevaRuta);

      if (rutaActual !== nuevaRuta) {
        this.$router.push(nuevaRuta);
      }
    }
  }
};
</script>

<style scoped>
.q-pa-md {
  max-width: 500px;
  margin: auto;
}

.full-width {
  width: 100%;
}
</style>
