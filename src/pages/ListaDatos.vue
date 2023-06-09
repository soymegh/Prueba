<template>
  <div>
    <table class="q-table">
      <thead>
      <tr>
        <th>ID</th>
        <th>Compañía</th>
        <th>Contacto</th>
        <th>Correo</th>
        <th>Teléfono</th>
        <th>Acciones</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="cliente in clientes" :key="cliente.id">
        <td>{{ cliente.id }}</td>
        <td>{{ cliente.compañia }}</td>
        <td>{{ cliente.contacto }}</td>
        <td>{{ cliente.correo }}</td>
        <td>{{ cliente.telefono }}</td>
        <td>
          <q-menu>
            <q-icon
              name="more_vert"
              class="q-mr-sm"
              slot="trigger"
              color="red"
              size="24px"
            />
            <q-list>
              <q-item clickable v-on:click="editarCliente(cliente.id)">
                <q-item-section>Editar Cliente</q-item-section>
              </q-item>
              <q-item clickable v-on:click="confirmarEliminacion(cliente.id)">
                <q-item-section>Eliminar</q-item-section>
              </q-item>
            </q-list>
          </q-menu>
        </td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    clientes: {
      type: Array,
      default: () => []
    }
  },
  methods: {
    editarCliente(clienteId) {
      const clienteSeleccionado = this.clientes.find(cliente => cliente.id === clienteId);
      if (clienteSeleccionado) {
        this.$emit('editar', clienteSeleccionado);
      }
    },
    confirmarEliminacion(clienteId) {
      if (confirm('¿Estás seguro de eliminar este cliente?')) {
        const clientesActualizados = [...this.clientes]; // Hacer una copia de la lista de clientes
        const index = clientesActualizados.findIndex(cliente => cliente.id === clienteId);
        if (index !== -1) {
          clientesActualizados.splice(index, 1);
          this.$emit('update:clientes', clientesActualizados); // Emitir evento para actualizar la prop "clientes" en el componente padre
        }
      }
    }

  }
};
</script>
