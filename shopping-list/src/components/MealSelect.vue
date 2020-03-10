<template>
  <div class="meal-list">
    <form>
      <div
        class="meal-list__selector"
        @click="setActive(meal)"
        v-for="meal in meals"
        :key="meal.name"
      >{{meal.mealName}}</div>
    </form>
    {{active}}
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import axios from "axios";

export type Meallist = Meal[];

export type Meal = {
  mealName: string;
  ingredients: Ingredient[];
};

export type Ingredient = {
  name: string;
  amount: string;
};

@Component
export default class MealSelect extends Vue {
  meals: Meallist = [];
  active: Meallist = [];

  getMeals(): void {
    axios
      .get("meals.json")
      .then(response => {
        console.log(response.data);
        this.meals = response.data;
      })
      .catch(error => {
        console.log(error);
      });
  }

  setActive(meal: Meal) {
    this.active.push(meal);
    const activeUnique = [...new Set(this.active)];
    console.log(this.active);
    console.log(activeUnique);
  }

  mounted() {
    this.getMeals();
    this.active;
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.meal-list {
  width: 50%;
  height: 100%;
  display: inline-block;

  &__selector {
    text-align: left;
    font-weight: bold;
    background: #fafafa;
    height: 55px;
    line-height: 55px;
    padding-left: 20px;
    border: 2px solid #dedede;
    margin: 10px 0;
    max-width: 350px;
  }
}
</style>
