<template>
  <div>
    <nav-bar></nav-bar>
    <div
      :style="bgImage"
      class="w-full text-center bg-blue-900 bg-cover bg-center bg-no-repeat"
    >
      <h2
        class="text-white text-5xl font-bold w-8/12 mx-auto pt-16 leading-normal"
      >
        The Data Commerce Platform that makes it easy to buy and sell
      </h2>
      <button
        class="bg-white text-blue-800 my-12 rounded text-white px-32 py-4 text-center font-semibold text-lg hover:text-white hover:bg-blue-800"
      >
        Create Buy Order
      </button>
    </div>
    <section
      class="py-16 flex justify-center flex-col px-20 w-8/12 mx-auto relative"
    >
      <input
        type="text"
        placeholder="Search by name"
        class="rounded py-5 border border-gray-100 shadow pl-10 placeholder:text-lg placeholder:text-gray-600 focus:outline-none border border-blue-500/50"
      />
      <img
        src="@/assets/search.png"
        alt=""
        class="absolute w-4 h-4 top-24 left-24 -mt-2"
      />
      <div class="pt-5 flex items-center">
        <h3 class="text-blue-800 font-semibold mr-6">Featured Searches</h3>
        <div
          class="rounded-full border border-blue-600 text-blue-800 font-semibold cursor-pointer py-2 px-4 w-auto text-center flex mr-4"
          v-for="(item, index) in searchOptions"
          :key="index"
        >
          {{ item.value }}
        </div>
      </div>
    </section>
    <div class="flex justify-between items-center px-24 py-6">
      <h2 class="text-blue-900 font-semibold text-2xl">
        Featured Data Streams
      </h2>
      <p class="text-lg font-semibold text-gray-700">
        Showing Top {{ allOrders.length }} Results
      </p>
    </div>
    <section class="px-24 py-16 grid grid-cols-4 gap-8">
      <div v-for="order in allOrders" :key="order.id">
        <card-component class="" :cardDetails="order"></card-component>
      </div>
    </section>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import NavBar from "@/components/NavBar.vue";
import CardComponent from "@/components/CardComponent.vue";
import orders from "@/data";

export default Vue.extend({
  name: "Home",
  components: { NavBar, CardComponent },
  data: () => ({
    allOrders: orders,
    bgImage: {
      backgroundImage: `url(${"https://cdn.narrative.io/cdn-cgi/image/w=2048,h=637,q=100,f=auto/images/data-stream/images/landing-bg-header.png"})`,
      backgroundColor: "rgb(1, 10, 40)",
    },
    searchOptions: [
      {
        value: "Device Location",
        label: "devive_location",
      },
      {
        value: "Device Behavior",
        label: "devive_behavior",
      },
      {
        value: "ID Mapping",
        label: "id_mapping",
      },
    ],
  }),
});
</script>
