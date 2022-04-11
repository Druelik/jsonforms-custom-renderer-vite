<template>
  <input
    :id="control.id + '-input'"
    :class="styles.control.input"
    :value="control.data"
    :disabled="!control.enabled"
    :autofocus="appliedOptions.focus"
    :placeholder="appliedOptions.placeholder"
    @change="onChange"
    @focus="isFocused = true"
    @blur="isFocused = false"
  />
</template>

<script>
import {
  rankWith,
  isStringControl,
} from "@jsonforms/core";
import { defineComponent } from "@vue/composition-api";
import {
  rendererProps,
  useJsonFormsControl,
} from "@jsonforms/vue2";
import { useVanillaControl } from "@jsonforms/vue2-vanilla";
const controlRenderer = defineComponent({
  name: "string-control-renderer",
  props: {
    ...rendererProps(),
  },
  setup(props) {
    return useVanillaControl(useJsonFormsControl(props));
  },
});
export default controlRenderer;
export const entry = {
  renderer: controlRenderer,
  tester: rankWith(1, isStringControl),
};
</script>
