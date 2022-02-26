<template>
  <div class="root">
    <Header
      class="q-my-xl"
      @update="filterList"
      :itemsShown="forceList_nike.length"
      :totalItems="bulk_list.length"
    />
    <div class="row justify-center q-gutter-md q-py-md">
      <div v-for="(prod, index) in forceList_nike" :key="index">
        <shoe-display :product="prod" brand="Nike" />
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent, ref, onMounted } from "vue";
import axios from "axios";
// Components
import ShoeDisplay from "src/components/ShoeDisplay.vue";
import Header from "src/components/Header.vue";
export default defineComponent({
  name: "MainLayout",
  components: {
    ShoeDisplay,
    Header,
  },
  setup() {
    const reqUrl =
      "https://api.nike.com/cic/browse/v2?queryid=products&anonymousId=C04F3B67B5F256B29EBF08C129DA9AE6&country=us&endpoint=%2Fproduct_feed%2Frollup_threads%2Fv2%3Ffilter%3Dmarketplace(US)%26filter%3Dlanguage(en)%26filter%3DemployeePrice(true)%26filter%3DattributeIds(0f64ecc7-d624-4e91-b171-b83a03dd8550%2C8529ff38-7de8-4f69-973c-9fdbfb102ed2%2C16633190-45e5-4830-a068-232ac7aea82c)%26anchor%3D0%26consumerChannelId%3Dd9a5bc42-4b9c-4976-858a-f159cf99c647%26count%3D24&language=en&localizedRangeStr=%7BlowestPrice%7D%20%E2%80%94%20%7BhighestPrice%7D";
    const forceList_nike = ref([]);
    const bulk_list = ref([]);

    async function init() {
      // Request and Parse
      const res_nike = await axios.get(reqUrl);
      const shoeList = res_nike.data.data.products.products;
      bulk_list.value = shoeList;
      forceList_nike.value = shoeList;
    }

    function filterList(saleVal) {
      const copy = bulk_list.value;
      if (saleVal.value) {
        forceList_nike.value = copy.filter((shoe) => shoe.price.discounted);
      } else {
        forceList_nike.value = bulk_list.value;
      }
    }

    onMounted(async () => {
      await init();
      filterList();
    });

    return {
      forceList_nike,
      bulk_list,
      filterList,
    };
  },
});
</script>

<style lang="scss" scoped>
.root {
  background-color: "#E8998D";
}
</style>
