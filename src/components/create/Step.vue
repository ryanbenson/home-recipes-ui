<template>
  <div class="step mb-3">
    <div class="field is-grouped">
      <div class="control is-expanded control--details">
        <input
          v-model="details"
          type="text"
          name="details"
          placeholder="Step details"
          class="input"
        />
      </div>
      <div class="control control--remove">
        <button class="button is-danger" @click="removeStep">
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
  emits: ["step:update", "step:remove"],
  setup(props, { emit }) {
    const details = ref(null);

    watchEffect(() => {
      emit("step:update", {
        key: props.k,
        details: details.value,
      });
    });

    function removeStep() {
      emit("step:remove", {
        key: props.k,
      });
    }

    return {
      details,
      removeStep,
    };
  },
};
</script>
