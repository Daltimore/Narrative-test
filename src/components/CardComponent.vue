<template>
  <div
    class="border border-gray-200 rounded p-3 hover:shadow-md hover:border-none"
  >
    <div class="flex justify-end">
      <p class="text-xs bg-blue-600 py-1 px-2 rounded-full text-white">
        {{ cardDetails.data_package_type }}
      </p>
    </div>
    <div
      class="w-20 h-20 rounded-full flex justify-center items-center text-3xl"
      :style="{ background: getRandomCustomerNameBG() }"
    >
      {{ getNameInitials(`${cardDetails.name}`) }}
    </div>
    <div class="py-4">
      <h3 class="text-blue-900 font-semibold font-lg">
        {{ cardDetails.name }}
      </h3>
    </div>
    <div class="text-sm">
      <span
        class="text-sm bg-blue-100 text-blue-900 font-semibold rounded py-1 px-2.5 mr-2"
        >$ {{ cardDetails.max_bid_price }}</span
      >
      per 1k
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  props: {
    cardDetails: {
      type: Object,
    },
  },
  methods: {
    getRandomCustomerNameBG() {
      const colors = ["#EEBDB3", "#DFF8E7", "#D3DDF6", "#E6E7EC"];
      return colors[Math.floor(Math.random() * colors.length)];
    },
    getNameInitials(nameString: string): string {
      const result = nameString.substring(0, 2);
      return result.toUpperCase();
    },
  },
});
</script>

<style></style>
