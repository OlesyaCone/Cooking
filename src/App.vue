
<script>
import AddDish from './components/AddDish.vue';
import DishCatalog from './components/DishCatalog.vue';
import CookingInProgress from './components/CookingInProgress.vue';
import axios from 'axios';

axios.defaults.baseURL = 'http://localhost:3005';

export default {
  components: {
    AddDish,
    DishCatalog,
    CookingInProgress
  },
  data() {
    return {
      dishes: [],
      cooking: []
    };
  },
  computed: {
    countDishes() {
      return this.dishes.length;
    }
  },
  mounted() {
    this.loadDishes();
    this.updateCooking();
    setInterval(() => {
      this.updateCooking();
    }, 3000);
  },
  methods: {
    async loadDishes() {
      try {
        let response = await axios.get('/dishes');
        this.dishes = response.data;
      } catch (error) {
        console.error('Ошибка при загрузке блюд:', error);
      }
    },
    async addDishToCatalog(dish) {
      try {
        let response = await axios.post('/dishes', dish);
        this.dishes.push(response.data);
      } catch (error) {
        console.error('Ошибка при добавлении блюда:', error);
      }
    },
    async startCooking(id) {
      try {
        let response = await axios.post('/cooking/cook', { id });
        this.cooking.push(response.data);
        this.startTimer(id);
      } catch (error) {
        console.error('Ошибка при начале приготовления блюда:', error);
      }
    },
    startTimer(id) {
      const dish = this.cooking.find(item => item.id === id);
      if (dish) {
        dish.preparingTime = 0;
        dish.isCooked = false;
        dish.timer = setInterval(() => {
          dish.preparingTime++;
          if (dish.preparingTime >= dish.timeToCook) {
            clearInterval(dish.timer);
            dish.isCooked = true;
          }
        }, 1000);
      }
    },
    async updateCooking() {
      try {
        let response = await axios.get('/cooking');
        this.cooking = response.data;
      } catch (error) {
        console.error('Ошибка при обновлении данных о готовке:', error);
      }
    }
  }
};
</script>
<template>
  <div>
    <header class="mb-5">
      <nav class="navbar">
        <div class="container-fluid">
          <p class="fs-1 text-white">В каталоге {{ dishes.length }} блюда</p>
        </div>
      </nav>
    </header>

    <AddDish @add-dish="addDishToCatalog" />

    <DishCatalog :dishes="dishes" @start-cooking="startCooking" />

    <CookingInProgress :cooking="cooking" />

  </div>
</template>