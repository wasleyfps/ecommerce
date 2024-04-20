<template>
  <div class="container">
    <div class="row">
      <div class="col-12 text-center">
        <h3 class="pt-3">Adicionar Categoria</h3>
      </div>
    </div>
    <div class="row">
      <div class="col-3"></div>
      <div class="col-6">
        <form>
          <div class="form-group">
            <label> Nome da Categoria</label>
            <input type="text" class="form-control" v-model="categoryName" />
          </div>
          <div class="form-group">
            <label>Descrição</label>
            <textarea
              type="text"
              class="form-control"
              v-model="description"
            ></textarea>
          </div>
          <div class="form-group">
            <label>Imagem</label>
            <input type="text" class="form-control" v-model="imageUrl" />
          </div>
          <button type="button" class="btn btn-primary" @click="addCategory()">
            Enviar
          </button>
        </form>
      </div>
      <div class="col-3"></div>
    </div>
  </div>
</template>
<script>
const axios = require("axios");
const sweetalert = require("sweetalert");
export default {
  data() {
    return {
      categoryName: "",
      description: "",
      imageUrl: "",
    };
  },
  methods: {
    addCategory() {
      console.log(this.categoryName, this.description);
      const newCategory = {
        categoryName: this.categoryName,
        description: this.description,
        imageUrl: this.imageUrl,
      };

      const baseURL = "https://limitless-lake-55070.herokuapp.com";

      axios({
        method: "post",
        url: `${baseURL}/category/create`,
        data: newCategory,
        headers: { "Content-Type": "application/json" },
      })
        .then(() => {
          sweetalert({
            text: "Categoria adicionada com sucesso!",
            icon: "success",
          });
        })
        .catch((error) => {
          console.log("Erro ao adicionar categoria:", error);
        });
    },
  },
};
</script>
