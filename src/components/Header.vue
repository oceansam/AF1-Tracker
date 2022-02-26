<template>
  <div>
    <div class="title flex justify-center text-h2">AF1 Tracker</div>
    <div class="flex justify-center q-gutter-md">
      <!-- <q-select
        class="filter-input"
        v-model="size"
        label="Size Filter"
        :options="sizeOptions"
        @change="updateFilter"
      /> -->
      <q-toggle
        label="On sale"
        size="4rem"
        v-model="sale"
        @update:model-value="updateFilter"
      />
    </div>
    <div class="flex justify-center text-h6">
      Showing {{ itemsShown }} of {{ totalItems }}
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  props: {
    itemsShown: Number,
    totalItems: Number,
  },
  setup(_, { emit }) {
    // const sizeOptions = [
    //   4, 5.5, 5, 5.5, 6, 6.5, 7, 7.5, 8, 8.5, 9, 9.5, 10, 10.5, 11, 11.5, 12,
    //   12.5, 13, 13.5, 14, 14.5,
    // ];
    // const size = ref();
    const sale = ref(false);
    function updateFilter() {
      emit("update", sale);
    }

    return {
      // sizeOptions,
      // size,
      sale,
      updateFilter,
    };
  },
};
</script>

<style lang="scss" scoped>
.filter-input {
  width: 200px;
}
.title {
  color: #a1683a;
}
</style>
