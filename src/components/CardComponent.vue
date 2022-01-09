<template>
  <div
    class="border border-gray-200 rounded p-3 hover:shadow-md hover:border-none"
  >
    <div class="flex justify-end">
      <div @click="handleOpen">
        <edit-icon
          class="text-blue-800 w-4 h-4 mr-1.5 cursor-pointer"
        ></edit-icon>
      </div>
      <div @click="deleteOrder(orderIndex)">
        <delete-icon class="text-red-500 w-4 h-4 cursor-pointer"></delete-icon>
      </div>
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
    <div class="text-sm flex justify-between items-center">
      <div>
        <span
          class="text-sm bg-blue-100 text-blue-900 font-semibold rounded py-1 px-2.5 mr-2"
          >$ {{ cardDetails.max_bid_price }}</span
        >
        per 1k
      </div>
      <p class="text-xs bg-blue-600 py-1 px-2 rounded-lg text-white">
        {{ cardDetails.data_package_type }}
      </p>
    </div>
  </div>
</template>

<script lang="ts">
/* eslint-disable @typescript-eslint/no-explicit-any */
import Vue from "vue";
import EditIcon from "@/assets/svg-ivons/EditIcon.vue";
import DeleteIcon from "@/assets/svg-ivons/DeleteIcon.vue";

export default Vue.extend({
  components: { EditIcon, DeleteIcon },
  props: {
    cardDetails: {
      type: Object,
    },
    orderIndex: {
      type: Number,
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
    deleteOrder(id: any) {
      this.$emit("handleDelete", id);
    },
    handleOpen() {
      this.$emit("openEditModal");
    },
  },
});
</script>

<style></style>
