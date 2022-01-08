<template>
  <div class="ingredient">
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
      <div class="control control--name">
        <input
          v-model="name"
          type="text"
          name="name"
          placeholder="Ingredient name"
          class="input"
        />
      </div>
      <div class="control control--remove">
        <button class="button is-danger">
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
    index: Number,
  },
  emits: ["ingredient:update"],
  setup(props, { emit }) {
    const measurement = ref(null);
    const name = ref(null);
    const quantity = ref(0);

    watchEffect(() => {
      emit("ingredient:update", {
        index: props.index,
        measurement: measurement.value,
        name: name.value,
        quantitye: quantity.value,
      });
    });

    return {
      measurement,
      name,
      quantity,
    };
  },
};
</script>

<style scoped>
.control--quantity {
  max-width: 60px;
}
</style>
