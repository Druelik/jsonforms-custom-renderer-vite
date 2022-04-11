<template>
  <div v-if="layout.visible" :class="layoutClassObject.root">
    <div
      v-for="(element, index) in layout.uischema.elements"
      :key="`${layout.path}-${index}`"
      :class="layoutClassObject.item"
    >
      <dispatch-renderer
        :schema="layout.schema"
        :uischema="element"
        :path="layout.path"
        :enabled="layout.enabled"
        :renderers="layout.renderers"
        :cells="layout.cells"
      />
    </div>
  </div>
</template>

<script>
import { isLayout, rankWith } from "@jsonforms/core";
import { defineComponent } from "@vue/composition-api";
import {
  DispatchRenderer,
  rendererProps,
  useJsonFormsLayout,
} from "@jsonforms/vue2";
import { useVanillaLayout } from "@jsonforms/vue2-vanilla";
const layoutRenderer = defineComponent({
  name: "layout-renderer",
  components: {
    DispatchRenderer,
  },
  props: {
    ...rendererProps(),
  },
  setup(props) {
    return useVanillaLayout(useJsonFormsLayout(props));
  },
  computed: {
    layoutClassObject() {
      return this.layout.direction === "row"
        ? this.styles.horizontalLayout
        : this.styles.verticalLayout;
    },
  },
});
export default layoutRenderer;
export const entry = {
  renderer: layoutRenderer,
  tester: rankWith(1, isLayout),
};
</script>
