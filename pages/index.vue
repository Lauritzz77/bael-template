<template>
  <div
    :class="['l-section', 'theme--' + theme, { 'light-mode': stayInLightMode }]">
    <slot />
  </div>
</template>

<script setup>
import { computed } from "vue";
const props = defineProps({
  theme: {
    type: String,
    validator(value) {
      return ["white", "yellow", "green", "orange", "grey", "blue"].includes(value);
    },
  },
  noSpacingTop: {
    type: Boolean,
    default: false,
  },
  noSpacingBottom: {
    type: Boolean,
    default: false,
  },
});

const stayInLightMode = computed(() => {
  return (
    props.theme === "yellow" ||
    props.theme === "green" ||
    props.theme === "orange"
  );
});

let spacing = "";
if (props.noSpacingTop && props.noSpacingBottom) {
  spacing = "0";
} else if (props.noSpacingTop) {
  spacing = "0 0 var(--spacing-section-y)";
} else if (props.noSpacingBottom) {
  spacing = "var(--spacing-section-y) 0 0";
} else {
  spacing = "var(--spacing-section-y) 0";
}
</script>

<style lang="scss">
.l-section {
  padding: v-bind(spacing);
}
</style>
<preview lang="md">
## How to use 
### l-section component is used to create a section with a background color and spacing.

----------------------
```
- prop.theme: String -> white, yellow, green, orange, grey, blue
- prop.noSpacingTop: Boolean
- prop.noSpacingBottom: Boolean

<l-section theme="white" :noSpacingTop="false" :noSpacingBottom="false">
  ${slot}
</l-section>
```

<style>
.markdown-body {
  max-width: 640px;
  margin: 30px auto;
}
</style>

</preview>
