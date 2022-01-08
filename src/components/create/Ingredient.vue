<template>
  <div class="ingredient mb-3">
    <div class="field is-grouped">
      <div class="control control--quantity">
        <input
          v-model="quantity"
          type="number"
          name="quantity"
          placeholder="How many"
          class="input"
        />
      </div>
      <div class="control control--measurement">
        <input
          v-model="measurement"
          type="text"
          name="measurement"
          placeholder="Measurement"
          class="input"
        />
      </div>
      <div class="control is-expanded control--name">
        <input
          v-model="name"
          type="text"
          name="name"
          placeholder="Ingredient name"
          class="input"
        />
      </div>
      <div class="control control--remove">
        <button class="button is-danger" @click="removeIngredient">
          <span class="icon is-small">
            <i class="fas fa-trash-alt"></i>
          </span>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, watchEffect } from "vue";
export default {
  props: {
    k: String,
  },
  emits: ["ingredient:update", "ingredient:remove"],
  setup(props, { emit }) {
    const measurement = ref(null);
    const name = ref(null);
    const quantity = ref(0);

    watchEffect(() => {
      emit("ingredient:update", {
        key: props.k,
        measurement: measurement.value,
        name: name.value,
        quantity: quantity.value,
      });
    });

    function removeIngredient() {
      emit("ingredient:remove", {
        key: props.k,
      });
    }

    return {
      measurement,
      name,
      quantity,
      removeIngredient,
    };
  },
};
</script>

<style scoped>
.control--quantity {
  max-width: 60px;
}
</style>
