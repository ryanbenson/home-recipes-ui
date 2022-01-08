<template>
  <section class="section">
    <div class="container">
      <div class="card about">
        <div class="card-content">
          <div class="content">
            <h1 class="title">Create new recipe</h1>
            <div class="new-recipe">
              <div class="field">
                <label for="name" class="label">Name</label>
                <div class="control">
                  <input
                    v-model="name"
                    type="text"
                    name="name"
                    placeholder="Recipe name"
                    class="input"
                  />
                </div>
              </div>

              <div class="field">
                <label for="description" class="label">Description</label>
                <div class="control">
                  <textarea
                    v-model="description"
                    type="text"
                    name="description"
                    placeholder="Recipe description"
                    class="textarea"
                  />
                </div>
              </div>

              <ingredient
                v-for="(ingredient, index) in ingredients"
                :key="index"
                :index="index"
                @ingredient:update="onIngredientUpdate"
              />

              <step
                v-for="(s, index) in steps"
                :key="index"
                :index="index"
                @step:update="onStepUpdate"
              />
            </div>
            <footer class="card-footer mt-5 pt-5">
              <div class="field is-grouped">
                <div class="control">
                  <button @click="onIngredientAdd" class="button">
                    Add Ingredient
                  </button>
                </div>
                <div class="control">
                  <button @click="onStepAdd" class="button">Add Step</button>
                </div>
                <div class="control">
                  <button @click="onSubmit" class="button is-link">Save</button>
                </div>
              </div>
            </footer>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { ref } from "vue";
import Ingredient from "@/components/create/Ingredient";
import Step from "@/components/create/Step";
export default {
  props: {},
  components: {
    Ingredient,
    Step,
  },
  // You should avoid using this inside setup as it won't refer to the component instance. setup is called before data properties, computed properties or methods are resolved, so they won't be available within setup.
  // setup(props, { attrs, slots, emit, expose }) {},
  setup() {
    const ingredients = ref([]);
    const steps = ref([]);
    const name = ref(null);
    const description = ref(null);

    function onIngredientAdd() {
      ingredients.value.push({
        measurement: null,
        name: null,
        quantity: 0,
      });
    }

    function onStepAdd() {
      steps.value.push({
        details: null,
      });
    }

    function onSubmit() {
      // submit to backend or whatever you like
      console.log(
        name.value,
        description.value,
        ingredients.value,
        steps.value
      );
    }

    function onIngredientUpdate(data) {
      ingredients.value.splice(data.index, 1, data);
    }

    function onStepUpdate(data) {
      steps.value.splice(data.index, 1, data);
    }

    return {
      ingredients,
      name,
      description,
      steps,
      onIngredientAdd,
      onIngredientUpdate,
      onStepAdd,
      onStepUpdate,
      onSubmit,
    };
  },
};
</script>
