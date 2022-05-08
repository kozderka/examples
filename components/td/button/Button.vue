<template>
  <button :class="buttonClass">
    <slot />
  </button>
</template>

<script setup>
const props = defineProps({
  color: { type: String, default: "default" },
  small: { type: Boolean, default: false },
  large: { type: Boolean, default: false },
});

let buttonClass = "";

if (props.small) {
  buttonClass += "py-1 px-3 ";
} else if (props.large) {
  buttonClass += "py-3 px-5 ";
} else {
  buttonClass += "py-2 px-4 ";
}

buttonClass += "border border-primary ";

if (props.color === "primary") {
  buttonClass += "bg-primary hover:bg-primary-dark text-gray-50";
} else {
  buttonClass += "bg-white hover:bg-primary-light text-primary-dark";
}

buttonClass +=
  " hover:border-primary-dark rounded text-sm font-bold transition duration-200";
</script>
