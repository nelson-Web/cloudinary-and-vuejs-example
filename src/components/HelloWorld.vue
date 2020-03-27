<template>
  <div>
    <form @submit.prevent="GuardarImagen()" method="post">
      <input type="file" @change="processFile($event)" />
      <button type="submit">subir imagen</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
       CLOUDINARY_URL: "coloca tu url",
      CLOUDINARY_UPLOAD_PRESET: "coloca tu preset",
      imagen: []
    };
  },
  methods: {
    processFile(event) {
      this.imagen = event.target.files[0];
      console.log(this.imagen);
    },
    GuardarImagen() {
      let formData = new FormData();
      formData.append("file", this.imagen); // le damos los datos de la imagen luego que se lleno en la funcion processFile()
      formData.append("upload_preset", this.CLOUDINARY_UPLOAD_PRESET); // le damos nuestro preset

      //subiendo imagen con fetch
      fetch(this.CLOUDINARY_URL, { method: "POST", body: formData })
        .then(response => response.json()) //convertimos la respuesta en json
        .then(data => console.log(data.url))// obtenemos la url de la imagen guardada
        .catch(error => console.log("ocurrio un error " , error)); //capturamos un posible error
    }
  }
};
</script>