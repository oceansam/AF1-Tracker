<template>
  <div>
    <q-card class="my-card shadow-3" bordered rounded>
      <q-img :src="product.images.portraitURL" />

      <q-card-section>
        <div class="text-overline text-orange-9">
          {{ product.productType }} - {{ brand }}
        </div>
        <div class="text-h5 q-mt-sm q-mb-xs">
          {{ product.title.substring(0, 25) }}
          {{ product.title.length >= 25 ? "..." : "" }}
        </div>
        <div class="text-h6 text-grey">
          <div v-if="product.price.discounted">
            <span class="text-strike">${{ product.price.fullPrice }}</span>
            <span> ${{ product.price.currentPrice }}</span>
            <span>{{ product.price.currency }}</span>
          </div>
          <div v-else class="text-h6 text-grey">
            ${{ product.price.currentPrice }}
            <span>{{ product.price.currency }}</span>
          </div>
        </div>
      </q-card-section>
      <q-card-section class="row q-gutter-xs q-py-none">
        <q-icon
          :name="product.inStock ? 'check' : 'close'"
          size="1.5rem"
          :color="product.inStock ? 'green' : 'red'"
        >
          <q-tooltip>
            {{ product.inStock ? "In stock" : "Not in stock" }}
          </q-tooltip>
        </q-icon>
        <q-icon
          v-if="product.price.discounted"
          name="percent"
          size="1.5rem"
          color="green"
        >
          <q-tooltip> On sale </q-tooltip>
        </q-icon>
      </q-card-section>
      <q-card-actions>
        <a :href="`//www.nike.com${transferUrl}`" target="_blank">
          <q-btn flat color="dark" label="Go to page" />
        </a>
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
    brand: String,
  },
  setup(props) {
    const transferUrl = props.product.url.substring(13);
    return {
      transferUrl,
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
