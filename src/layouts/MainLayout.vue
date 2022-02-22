<template>
  <div>
    <div class="flex justify-center">
      <h1>Vue + Quasar Boilerplate</h1>
    </div>
    <div class="flex justify-center">
      <div>
        <q-input v-model="inputField" label="Example Input" />
        <div>Your Input is: {{ inputField }}</div>
      </div>
    </div>
    <div class="flex justify-center q-mt-xl">
      <sample-component />
    </div>
  </div>
</template>

<script>
import { defineComponent, ref } from "vue";
// Components
import SampleComponent from "src/components/SampleComponent.vue";
export default defineComponent({
  name: "MainLayout",
  components: {
    SampleComponent,
  },
  setup() {
    const inputField = ref();

    return {
      inputField,
    };
  },
});
</script>
