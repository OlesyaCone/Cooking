<script>
export default {
  data() {
    return {
      title: "",
      placeholder: "",
      image: "",
      timeToCook: "",
    };
  },
  methods: {
    addDish() {
      const dish = {
        title: this.title,
        preparation: this.placeholder,
        timeToCook: parseInt(this.timeToCook),
        image: this.image,
      };
      this.$emit("add-dish", dish);
      this.title = "";
      this.placeholder = "";
      this.image = "";
      this.timeToCook = "";
    },
  },
};
</script>
<template>
  <form @submit.prevent="addDish">
    <h2>Добавить рецепт:</h2>
    <input
      type="text"
      class="form-control mt-3 text-center"
      placeholder="Название"
      v-model="title"
    />
    <textarea
      class="form-control mt-3 text-center"
      placeholder="Рецепт"
      v-model="placeholder"
    ></textarea>
    <div class="d-flex">
      <div class="input-group mb-3 mt-3">
        <span class="input-group-text">Изображение</span>
        <input type="text" class="form-control" v-model="image" />
      </div>
      <input
        type="number"
        class="form-control mt-3 mb-3"
        placeholder="Время готовки (мин)"
        v-model="timeToCook"
      />
    </div>
    <button class="d-grid gap-2 col-6 mx-auto btn btn-success btn-lg">
      Добавить блюдо
    </button>
  </form>
</template>
<style>
body {
  margin: 0;
}

h2 {
  text-align: center;

  font-family: "Courier New", Courier, monospace;
}

.navbar {
  background-color: #146c43;
}

@media (max-width: 768px) {
  .col-6.col-md-4.col-lg-3 {
    flex: 0 0 100%;

    max-width: 100%;
  }
}
</style>
