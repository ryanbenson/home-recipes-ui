<template>
  <div class="step">
    <div class="field">
      <div class="control">
        <input
          v-model="details"
          type="text"
          name="details"
          placeholder="Step details"
          class="input"
        />
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
  emits: ["step:update"],
  setup(props, { emit }) {
    const details = ref(null);

    watchEffect(() => {
      emit("step:update", {
        index: props.index,
        details: details.value,
      });
    });

    return {
      details,
    };
  },
};
</script>
