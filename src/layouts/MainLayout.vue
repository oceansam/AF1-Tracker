<template>
  <div class="root">
    <Header class="q-my-xl" />
    <div class="row justify-center q-gutter-md q-py-md">
      <div v-for="(prod, index) in footlocker_list" :key="index">
        <shoe-display :product="prod" />
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
      "https://api.nike.com/product_feed/threads/v2?filter=language(en)&filter=marketplace(US)&filter=channelId(d9a5bc42-4b9c-4976-858a-f159cf99c647)&filter=productInfo.merchProduct.styleColor(CW2288-001,DD8959-100,DO6394-100,CI0919-100,DC9486-101,CT2302-002,CJ9179-200,DD8959-001,BQ6806-100,DO6394-001,DC4831-100,CT3839-104)";

    const footlocker_list = ref([]);
    onMounted(async () => {
      const res = await axios.get(reqUrl);
      const productList = res.data.objects.map((obj) => {
        return obj.productInfo[0];
      });
      footlocker_list.value = productList;
      console.log(footlocker_list);
    });

    return {
      footlocker_list,
    };
  },
});
</script>

<style lang="scss" scoped>
.root {
  background-color: "#E8998D";
}
</style>
