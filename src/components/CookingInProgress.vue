<script>
export default {
  props: ["cooking"],
};
</script>
<template>
  <div>
    <h2>На готовке:</h2>
    <div class="container">
      <div class="row g-2">
        <div
          class="col-6 col-md-4 col-lg-3"
          v-for="item in cooking"
          :key="item.id"
        >
          <div class="card" style="width: 18rem">
            <img :src="item.image" class="card-img-top" alt="..." />
            <div class="card-body">
              <h5 class="card-title">{{ item.title }}</h5>
              <p class="card-text">{{ item.preparation }}</p>
              <div class="d-flex">
                <p class="text-end form-control mt-3 mb-3">
                  {{ item.preparingTime }} / {{ item.timeToCook }} мин
                </p>
                <p v-if="item.isCooked" class="text-success">Готово!</p>
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
