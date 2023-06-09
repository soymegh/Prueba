<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <!-- Encabezado de la barra -->
      </q-toolbar>
    </q-header>

    <q-page-container>
      <!-- Botón "Crear Cliente" -->
      <q-btn
        v-if="!mostrarCrearCliente && !mostrarEditarClienteFlag"
        color="primary"
        label="Crear Cliente"
        className="q-mb-md q-ml-md q-mt-md q-fixed-bottom q-fixed-left"
        @click="mostrarCrearCliente = true"
      />

      <!-- Componente "Crear" -->
      <crear v-if="mostrarCrearCliente" @cancelar="mostrarCrearCliente = false"/>

      <!-- Componente "ListaDatos" -->
      <lista-datos
        v-if="!mostrarCrearCliente && !mostrarEditarClienteFlag"
        :clientes="clientes" @update:clientes="actualizarClientes"
        @editar="mostrarEditarCliente"

      />

      <!-- Componente "Actualizar" -->
      <actualizar
        v-if="mostrarEditarClienteFlag"
        :cliente="clienteSeleccionado"
        @cancelar="mostrarEditarClienteFlag = false"
        @actualizar="actualizarCliente"
      />
    </q-page-container>
  </q-layout>
</template>

<script>
import ListaDatos from "pages/ListaDatos.vue";
import Crear from "pages/Crear.vue";
import Actualizar from "pages/Actualizar.vue";

export default {
  name: 'MainLayout',
  components: {
    ListaDatos,
    Crear,
    Actualizar
  },
  data() {
    return {
      leftDrawerOpen: false,
      mostrarCrearCliente: false,
      mostrarEditarClienteFlag: false,
      clienteSeleccionado: null,
      clientes: []
    };
  },
  methods: {
    mostrarEditarCliente(cliente) {
      this.clienteSeleccionado = cliente;
      this.mostrarEditarClienteFlag = true;
    },
    actualizarClientes() {
      const clientesData = localStorage.getItem('clientes');
      if (clientesData) {
        this.clientes = JSON.parse(clientesData);
      }
    },
    cargarDatosDesdeLocalStorage() {
      const clientesGuardados = localStorage.getItem('clientes');

      if (clientesGuardados) {
        this.clientes = JSON.parse(clientesGuardados);
      }
    }
  },
  mounted() {
    this.cargarDatosDesdeLocalStorage();


    // Cargar los clientes al montar el componente
    this.actualizarClientes();
  }
};
</script>
