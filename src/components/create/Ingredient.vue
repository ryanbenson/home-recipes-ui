<template>
  <div class="ingredient">
    <div class="row">
      <label for="name">quantity</label>
      <input
        v-model="quantity"
        type="number"
        name="quantity"
        placeholder="How many"
      />
    </div>
    <div class="row">
      <label for="measurement">Measurement</label>
      <input
        v-model="measurement"
        type="text"
        name="measurement"
        placeholder="Recipe name"
      />
    </div>
    <div class="row">
      <label for="name">Name</label>
      <input
        v-model="name"
        type="text"
        name="name"
        placeholder="Ingredient name"
      />
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
