<template>
  <div>
    <q-card class="my-card shadow-3" bordered rounded>
      <q-img :src="product.imageUrls.productImageUrl" />

      <q-card-section>
        <div class="text-overline text-orange-9">
          {{ product.merchProduct.brand }} -
          <span v-for="gender in product.merchProduct.genders" :key="gender">
            <q-chip>{{ gender }}</q-chip>
          </span>
        </div>
        <div class="text-h5 q-mt-sm q-mb-xs">
          {{ product.productContent.title }}
        </div>
        <div class="text-h6 text-grey">
          <div v-if="product.merchPrice.discounted">
            <span class="text-strike">${{ product.merchPrice.fullPrice }}</span>
            <span> ${{ product.merchPrice.currentPrice }}</span>
          </div>
          <div
            v-else
            class="text-h6 text-grey"
            :class="product.merchPrice.discounted"
          >
            ${{ product.merchPrice.currentPrice }}
          </div>
        </div>
      </q-card-section>
      <q-card-section class="row q-gutter-xs">
        <q-badge
          v-for="(sku, index) in product.skus"
          :key="index"
          outline
          :color="availableSkuIds.includes(sku.id) ? 'secondary' : 'grey'"
        >
          {{ sku.nikeSize }}
        </q-badge>
      </q-card-section>
      <q-card-actions>
        <q-btn flat color="dark" label="Go to page" />
      </q-card-actions>
    </q-card>
  </div>
</template>

<script>
import { defineComponent, ref } from "vue";
export default defineComponent({
  name: "ShoeDisplay",
  props: {
    product: Object,
  },
  setup(props) {
    const availableSkuIds = props.product.availableSkus.reduce(
      (filtered, freeSku) => {
        if (freeSku.available) {
          filtered.push(freeSku.id);
        }
        return filtered;
      },
      []
    );

    return {
      availableSkuIds,
    };
  },
});
</script>

<style lang="scss" scoped>
.my-card {
  width: 500px;
  max-width: 350px;
  height: 650px;
}
</style>
