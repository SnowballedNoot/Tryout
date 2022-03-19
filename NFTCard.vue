<template>
  <div v-if="nft.onchainMetadata.data.creators[1].address === 'Boz8QjSACdbUkyjamdZAcocEfyA3DkkigaXCJ9mdppHd'"
    class="m-2 mt-6 card flex justify-start rounded-3"
    :class="{ 'card-selected': selected }"
    @click="toggleSelect"
  >
    <img
      :src="nft.externalMetadata.image"
      :alt="nft.onchainMetadata.data.name"
    />
    <div>
      <p class="text-danger text-center fs-6">{{ nft.onchainMetadata.data.name }}</p>
      <button class="btn btn-danger" @click="toggleSelect">
        Staking
      </button>
    </div>
  </div>
</template>

<script lang="ts">
import NftInfo from '@/components/NftInfo.vue';
import { defineComponent, ref } from 'vue';
export default defineComponent({
  components: { NftInfo },
  props: {
    nft: { type: Object, required: true },
  },
  emits: ['selected'],
  setup(props, ctx) {
    const selected = ref<boolean>(false);

    const toggleSelect = () => {
      selected.value = !selected.value;
      console.log('selected', props.nft.mint.toBase58());
      ctx.emit('selected', {
        nft: props.nft,
        selected: selected.value,
      });
    };

    return {
      selected,
      toggleSelect,
    };
  },
});
</script>

<style scoped>
img {
  max-width: 100%;
  max-height: 100%;
  height: auto;
  width: auto;
}

.card {
  width: 180px;
  height: 180px;
}

.card:hover {
  @apply border-4 border-solid border-gray-200;
}

.card-selected {
  @apply border-4 border-solid;
  border-color: red !important;
}

.mt-6,
.my-6 {
  margin-top: 5rem !important;
}

</style>
