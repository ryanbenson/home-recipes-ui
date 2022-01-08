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

              <h2 v-if="ingredients.length > 0" class="subtitle is-4">
                Ingredients
              </h2>
              <ingredient
                v-for="ingredient in ingredients"
                :key="ingredient.key"
                :k="ingredient.key"
                @ingredient:update="onIngredientUpdate"
                @ingredient:remove="onIngredientRemove"
              />

              <h2 v-if="steps.length > 0" class="subtitle is-4">Steps</h2>
              <step
                v-for="s in steps"
                :key="s.key"
                :k="s.key"
                @step:update="onStepUpdate"
                @step:remove="onStepRemove"
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
import { ref, reactive, toRefs } from "vue";
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
    const state = reactive({
      ingredients: [],
      steps: [],
    });
    const name = ref(null);
    const description = ref(null);

    function onIngredientAdd() {
      state.ingredients.push({
        measurement: null,
        name: null,
        quantity: 0,
        key: randomString(),
      });
    }

    function onStepAdd() {
      state.steps.push({
        details: null,
        key: randomString(),
      });
    }

    function onSubmit() {
      // submit to backend or whatever you like
      console.log(
        name.value,
        description.value,
        state.ingredients,
        state.steps
      );
    }

    function onIngredientUpdate(data) {
      const i = state.ingredients.findIndex(
        (ingredient) => ingredient.key === data.key
      );
      state.ingredients.splice(i, 1, data);
    }

    function onIngredientRemove(data) {
      state.ingredients = state.ingredients.filter((ingredient) => {
        return ingredient.key !== data.key;
      });
    }

    function onStepUpdate(data) {
      const i = state.steps.findIndex((step) => step.key === data.key);
      state.steps.splice(i, 1, data);
    }

    function onStepRemove(data) {
      const updatedSteps = state.steps.filter((step) => {
        return step.key !== data.key;
      });
      state.steps = updatedSteps;
    }
    function randomString() {
      const chars =
        "0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";
      const length = 12;
      let result = "";
      for (let i = length; i > 0; --i) {
        result += chars[Math.floor(Math.random() * chars.length)];
      }
      return result;
    }

    return {
      ...toRefs(state),
      name,
      description,
      onIngredientAdd,
      onIngredientUpdate,
      onIngredientRemove,
      onStepAdd,
      onStepUpdate,
      onStepRemove,
      onSubmit,
    };
  },
};
</script>
