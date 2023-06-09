<template>
  <div>
    <h2 class="titulo">Crear Cliente</h2>
    <q-form @submit.prevent="crearCliente" class="form-container">
      <q-input
        outlined
        v-model="nuevoCliente.compañia"
        label="Compañía"
        required
      ></q-input>
      <q-input
        outlined
        v-model="nuevoCliente.contacto"
        label="Contacto"
        required
      ></q-input>
      <q-input
        outlined
        v-model="nuevoCliente.correo"
        label="Correo"
        type="email"
        required
      ></q-input>
      <q-input
        outlined
        v-model="nuevoCliente.telefono"
        label="Teléfono"
        type="tel"
        required
      ></q-input>
      <q-input
        outlined
        v-model="nuevoCliente.direccion"
        label="Dirección"
        required
      ></q-input>
      <q-input
        outlined
        v-model="nuevoCliente.ciudad"
        label="Ciudad"
        required
      ></q-input>
      <q-input
        outlined
        v-model="nuevoCliente.pais"
        label="País"
        required
      ></q-input>
      <q-btn type="submit" color="primary" label="Crear"></q-btn>
    </q-form>
  </div>
</template>

<style scoped>
.titulo {
  text-align: center;
}

.form-container {
  max-width: 400px;
  margin: 0 auto;
}

.q-input {
  margin-bottom: 20px;
}
</style>

<script>
export default {
  data() {
    return {
      clientes: [],
      nuevoCliente: {
        id: '',
        compañia: '',
        contacto: '',
        correo: '',
        telefono: '',
        direccion: '',
        ciudad: '',
        pais: ''
      },
      identity: 1
    };
  },
  mounted() {
    // Obtener la lista de clientes almacenada en el LocalStorage al cargar la página
    const storedClientes = localStorage.getItem('clientes');
    if (storedClientes) {
      this.clientes = JSON.parse(storedClientes);
    }
  },
  methods: {
    crearCliente() {
      // Asignar el ID único al nuevo cliente
      this.nuevoCliente.id = ` ${this.identity}`;

      // Incrementar el valor de identity para el próximo cliente
      this.identity++;

      // Agregar el nuevo cliente a la lista de clientes
      this.clientes.push(this.nuevoCliente);

      // Guardar la lista de clientes en el LocalStorage
      localStorage.setItem('clientes', JSON.stringify(this.clientes));

      this.$emit('cliente-creado');

      // Restablecer el objeto nuevoCliente para el siguiente cliente
      this.nuevoCliente = {
        id: '',
        compañia: '',
        contacto: '',
        correo: '',
        telefono: '',
        direccion: '',
        ciudad: '',
        pais: ''
      };

      // Redirigir a la página principal
      this.$router.push('/');
    }
  }
};
</script>

