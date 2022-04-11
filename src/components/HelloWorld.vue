<template>
  <div>
    {{ claims }}
    <json-forms
      :data="claims"
      :schema="jsonSchema"
      :uischema="uiSchema"
      :renderers="renderer"
      @change="onChange"
    />
  </div>
</template>
<script>
import { defineComponent, ref } from "@vue/composition-api";
import { JsonForms } from "@jsonforms/vue2";
import { entry as StringRenderer } from "./Stringrenderer.vue";
import { entry as LayoutRenderer } from "./VerticalLayoutRenderer.vue";
export default defineComponent({
  props: {
    msg: String,
  },
  components: { JsonForms },
  setup() {
    const claims = ref({});
    const uiSchema = {
      type: "VerticalLayout",
      elements: [{ type: "Control", scope: "#/properties/name" }],
    };
    const renderer = [StringRenderer, LayoutRenderer];
    const jsonSchema = {
      properties: {
        name: {
          type: "string",
        },
      },
    };
    const onChange = (e) => {
      console.log(e);
      claims.value = e.data;
    };
    return { claims, uiSchema, jsonSchema, onChange, renderer };
  },
});
</script>
