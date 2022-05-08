<template>
  <div>
    <input v-model="localValue" :class="inputClass" type="text" />
    <div>
      <div v-for="error in errors">
        {{ error }}
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, watch, defineEmits, computed } from "vue";
import { isEqual } from "lodash/fp";

const props = defineProps({
  small: { type: Boolean, default: false },
  large: { type: Boolean, default: false },
  rules: { type: Array, default: () => [] },
  error: { type: Boolean, default: false },
  modelValue: { type: String, default: "" },
});

const emit = defineEmits(["update:modelValue"]);

let localValue = ref(props.modelValue);
let localError = ref(props.error);

watch(
  () => props.modelValue,
  (value) => {
    if (!isEqual(value, localValue.value)) {
      localValue.value = value;
    }
  }
);

watch(localValue, (value) => {
  emit("update:modelValue", value);
});

const inputClass = computed(() => {
  let inputClass =
    "w-full text-sm bg-white focus:outline-none border rounded text-gray-600 ";

  if (localError.value) {
    inputClass += "border-red-500 ";
  } else {
    inputClass += "focus:border-primary border-grey-700 ";
  }

  if (props.small) {
    inputClass += "py-1 px-3 ";
  } else if (props.large) {
    inputClass += "py-3 px-5 ";
  } else {
    inputClass += "py-2 px-4 ";
  }

  return inputClass;
});
</script>
