<template>
  <div class="container foo rounded-3">
    <p class="title text-white text-center">{{ title }}</p>
    <br>
    <slot />
    <div class="flex flex-wrap">
      <NFTCard
        v-for="nft in nfts"
        :key="nft"
        :nft="nft"
        @selected="handleSelected"
      />

      <NftInfo
        v-for="nft in nfts"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import NFTCard from '@/components/gem-bank/NFTCard.vue';

export default defineComponent({
  components: { NFTCard },
  emits: ['selected'],
  props: {
    title: String,
    nfts: Array,
  },
  setup(props, ctx) {
    const handleSelected = (e: any) => {
      ctx.emit('selected', e);
    };
    return {
      handleSelected,
    };
  },
});
</script>

<style scoped>
.foo {
 background-color: rgba(201,201,201,0.3);
}
</style>
