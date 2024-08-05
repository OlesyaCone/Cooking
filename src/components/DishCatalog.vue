<script>
export default {
  props: ["dishes"],
  methods: {
    startCooking(id) {
      this.$emit("start-cooking", id);
    },
  },
};
</script>
<template>
  <div>
    <h2>Каталог блюд:</h2>
    <div class="container">
      <div class="row g-2">
        <div
          class="col-6 col-md-4 col-lg-3"
          v-for="dish in dishes"
          :key="dish.id"
        >
          <div class="card" style="width: 18rem">
            <img :src="dish.image" class="card-img-top" alt="..." />
            <div class="card-body">
              <h5 class="card-title">{{ dish.title }}</h5>
              <p class="card-text">{{ dish.preparation }}</p>
              <div class="d-flex">
                <a
                  class="btn btn-warning form-control mt-3 mb-3"
                  @click="startCooking(dish.id)"
                  >Приготовить</a
                >
                <p class="text-end form-control mt-3 mb-3">
                  {{ dish.timeToCook }} мин
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
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
