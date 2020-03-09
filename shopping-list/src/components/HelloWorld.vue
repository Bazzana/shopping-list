<template>
  <div class="meal-list"></div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

export type Meallist = Meal[];

export type Meal = {
  mealName: string;
  ingredients: Ingredient[];
};

export type Ingredient = {
  name: string;
  amount: string;
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.meal-list {
  width: 50%;
  height: 100%;
  display: inline-block;
}
</style>
