<template>
  <div id="app">
    <div>
      <h1>Random Gif Cat</h1>
    </div>
    <div class="form-style">
      <div>
        <label for="">Título:</label>
        <input class="input" type="text" v-model="titulo" />
      </div>
      <div>
        <label for="">Filtro:</label>
        <select class="input" @change="cambioFiltro($event)">
          <option
            v-for="(filtro, index) in filtros"
            :key="index"
            :value="filtro"
            v-text="filtro"
          ></option>
        </select>
      </div>
      <div class="row">
        <label>Color:</label>
        <select class="input" @change="cambioColor($event)">
          <option
            v-for="(item, index) in lista_color"
            :key="index"
            :value="item.color"
            v-text="item.texto"
          ></option>
        </select>
        <div class="redondo" :style="{backgroundColor: color}"></div>
      </div>
      <div>
        <label>Tamaño:</label>
        <input class="input" type="number" v-model="tamano" />
      </div>
    </div>
    <div>
      <p><button @click="descargarGato">Obtener mi gatito</button></p>
      <div><img :src="imagen" /></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      filtros: ["blur", "mono", "sepia", "negative", "paint", "pixel"],
      titulo: "hola",
      filtro: "blur",
      color: "green",
      tamano: 300,
      imagen: "",
      lista_color: [
        {color: "green", texto: "verde"},
        {color: "red", texto: "rojo"},
        {color: "blue", texto: "azul"},
        {color: "white", texto: "blanco"},
        {color: "yellow", texto: "amarillo"},
      ],
    };
  },
  methods: {
    descargarGato() {
      var url = `https://cataas.com/cat/gif/says/${this.titulo}?filter=${this.filtro}&color=${this.color}&size=${this.tamano}&type=or`;
      this.imagen = url;
    },
    cambioFiltro(event) {
      this.filtro = event.target.value;
    },
    cambioColor(event) {
      this.color = event.target.value;
    },
  },
};
</script>

<style>
body {
  background-color: skyblue;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.form-style {
  background: #f0807f;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: left;
}

.input {
  margin: 8px;
}
.redondo {
  height: 25px;
  width: 25px;
  border-radius: 50%;
  border: 1px solid black;
  margin-left: 15px;
}

.row {
  display: inline-flex;
}
</style>
