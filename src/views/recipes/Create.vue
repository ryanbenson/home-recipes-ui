<template>
  <div class="about">
    <h1>Create new recipe</h1>
    <div class="new-recipe">
      <div class="row">
        <label for="name">Name</label>
        <input
          v-model="name"
          type="text"
          name="name"
          placeholder="Recipe name"
        />
      </div>

      <button @click="onIngredientAdd">Add Ingredient</button>
      <div class="row">
        <ingredient
          v-for="(ingredient, index) in ingredients"
          :key="index"
          :index="index"
          @ingredient:update="onIngredientUpdate"
        />
      </div>

      <div class="row">
        <button @click="onSubmit">Save</button>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import Ingredient from "@/components/create/Ingredient";
export default {
  props: {},
  components: {
    Ingredient,
  },
  // You should avoid using this inside setup as it won't refer to the component instance. setup is called before data properties, computed properties or methods are resolved, so they won't be available within setup.
  // setup(props, { attrs, slots, emit, expose }) {},
  setup() {
    const ingredients = ref([]);
    const name = ref(null);

    function onIngredientAdd() {
      ingredients.value.push({
        measurement: null,
        name: null,
        quantity: 0,
      });
    }

    function onSubmit() {
      // submit to backend or whatever you like
      console.log(name.value, ingredients.value);
    }

    function onIngredientUpdate(data) {
      ingredients.value.splice(data.index, 1, data);
    }

    return {
      ingredients,
      name,
      onIngredientAdd,
      onIngredientUpdate,
      onSubmit,
    };
  },
};
</script>
