<template>
  <div>
    <div class="container">
      <div class="productoContainer" v-for="(producto, index) in productos" :key="index">
        <div class="infoProducto">
          <div class="nombreProducto">
            <h2>{{ producto.nombre.toLocaleUpperCase() }}</h2>
          </div>
          <div class="descripcionProducto">
            <p>{{ producto.descripcion }}</p>
          </div>
          <div class="enStockProducto">
            <button v-if="producto.unidades > 0" @click="agregarAlCarrito(producto)">Agregar al carrito</button>
            <p v-else>Producto no disponible en stock</p>
          </div>
          <div class="unidadesProducto">
            <p>Quedan: {{ producto.unidades }}</p>
          </div>
        </div>
      </div>
    </div>
    <div class="carrito">
      <p>Carrito</p>
      <div v-if="carrito.length > 0">
        <div v-for="(articulo, index) in carrito" :key="index">
          {{ articulo.articulo }} ({{ articulo.unidades }})
          <button @click="quitarArticulo(index, articulo)">Eliminar</button>
        </div>
      </div>
      <div v-else>
        <p>No hay artículos en el carrito</p>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref } from 'vue';

const carrito = ref([])

const productos = ref([
  {
    nombre: "Zapatos deportivos",
    descripcion: 'Estos zapatos son perfectos para correr y hacer ejercicio',
    unidades: 5
  },
  {
    nombre: "Camiseta térmica",
    descripcion: 'Camiseta térmica imprescindible para hacer deporte en invierno',
    unidades: 2
  }
])

const agregarAlCarrito = (producto) => {
  carrito.value.push(
    {
      articulo: producto.nombre,
      unidades: 1
    }
  )
  producto.unidades--
}

const quitarArticulo = (index, articulo) => {
  carrito.value.splice(index, 1)

  productos.value.forEach(producto => {
    if (producto.nombre === articulo.articulo) {
      producto.unidades++
    }
  });
}

</script>
<style>
.container {
  display: flex;
}

.productoContainer {
  display: grid;
  background-color: lightblue;
  margin-right: 1rem;
  padding: 1rem;
}

.nombreProducto {
  justify-items: center;
  font-style: oblique;
}
</style>
