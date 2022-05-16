<template>
  <div class="container">
    <h1>Random Gif Cat</h1>
    <form @submit.prevent="obtenerGatito" class="form">
      <div class="container-form">
        <div class="input">
          <label for="title">Titulo: </label>
          <input type="text" name="title" v-model="title" />
        </div>
        <div class="input">
          <label for="filter">Filtro: </label>
          <select v-model="filtro">
            <option
              v-for="(filtro, index) in filtros"
              :key="index"
              :value="filtro"
              v-text="filtro"
            ></option>
          </select>
        </div>
        <div class="input">
          <label for="color">Color: </label>
          <select name="color" v-model="color">
            <option
              v-for="(color, index) in colors"
              :key="index"
              :value="color.value"
              v-text="color.nombre"
            ></option>
          </select>
        </div>
        <div class="input">
          <label for="size">Tamaño: </label>
          <input type="number" name="size" v-model="size" />
        </div>
      </div>
      <button type="submit">Obtener mi gatito</button>
    </form>
    <Imagen v-if="estadoDeCarga" :urlImagen="url" />
    <Cargando v-else />
  </div>
</template>

<script>
import Imagen from "./components/Imagen";
import Cargando from "./components/Cargando";

export default {
  name: "App",
  components: { Imagen, Cargando },
  data: () => ({
    url: "",
    title: "",
    filtro: "",
    filtros: ["", "blur", "mono", "sepia", "negative", "paint", "pixel"],
    color: "",
    colors: [
      { nombre: "rojo", value: "red" },
      { nombre: "azul", value: "blue" },
      { nombre: "amarillo", value: "yellow" },
    ],
    size: "",
    estadoDeCarga: false,
  }),
  methods: {
    obtenerGatito() {
      this.estadoDeCarga = false;
      this.url = `https://cataas.com/cat/gif/says/${this.title}?filter=${this.filtro}&color=${this.color}&size=${this.size}&type=or`;
      console.log(this.url);
      this.estadoDeCarga = true;
    },
  },
};
</script>

<style>
body {
  background-color: aquamarine;
}
h1 {
  text-align: center;
}
.input {
  display: flex;
  gap: 10px;
  margin-bottom: 10px;
}

.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 2rem;
}

.form {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  width: 100%;
  align-items: center;
}

.container-form {
  display: flex;
  width: 100%;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: darksalmon;
  margin: 0 auto;
  padding: 2rem;
  box-sizing: border-box;
}

button {
  max-width: 400px;
}

img {
  object-fit: cover;
}
</style>
