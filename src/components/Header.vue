<template>
  <div>
    <div class="title flex justify-center text-h2">AF1 Tracker</div>
    <div class="flex justify-center q-gutter-md">
      <q-select
        class="filter-input"
        v-model="company"
        label="Company Filter"
        :options="companyOptions"
      />
      <q-select
        class="filter-input"
        v-model="gender"
        label="Gender Filter"
        :options="genderOptions"
      />
      <q-select
        class="filter-input"
        v-model="size"
        label="Size Filter"
        :options="sizeOptions"
      />
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  setup(_,{emit}) {
    const companyOptions = ["Nike", "Footlocker"];
    const genderOptions = ["Men", "Women", "Boys", "Girls"];
    const sizeOptions = [
      4, 5.5, 5, 5.5, 6, 6.5, 7, 7.5, 8, 8.5, 9, 9.5, 10, 10.5, 11, 11.5, 12,
      12.5, 13, 13.5, 14, 14.5,
    ];
    const company = ref();
    const gender = ref();
    const size = ref();
    return {
      companyOptions,
      genderOptions,
      sizeOptions,
      company,
      gender,
      size,
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
