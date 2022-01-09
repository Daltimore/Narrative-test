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
        @click="showCreateModal = true"
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
        v-model="searchQuery"
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
          @click="setToSearchQuery(item.value)"
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
        Showing Top {{ filteredOrders.length }} Results
      </p>
    </div>
    <section class="px-24 py-16 grid grid-cols-4 gap-8">
      <div v-for="order in filteredOrders" :key="order.id">
        <card-component
          class=""
          :cardDetails="order"
          @handleDelete="handleDelete"
          @openEditModal="openEditModal"
        ></card-component>
      </div>
    </section>
    <add-buy-order-modal v-model="showCreateModal"></add-buy-order-modal>
    <update-buy-order-modal v-model="showUpdateModal"></update-buy-order-modal>
  </div>
</template>

<script lang="ts">
/* eslint-disable @typescript-eslint/no-explicit-any */
import Vue from "vue";
import NavBar from "@/components/NavBar.vue";
import CardComponent from "@/components/CardComponent.vue";
import AddBuyOrderModal from "@/components/CreateBuyOrderModal.vue";
import UpdateBuyOrderModal from "@/components/UpdateBuyOrderModal.vue";
import AllData from "@/data";

export default Vue.extend({
  name: "Home",
  components: { NavBar, CardComponent, AddBuyOrderModal, UpdateBuyOrderModal },
  data: () => ({
    showCreateModal: false,
    showUpdateModal: false,
    searchQuery: "",
    x: AllData,
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
        value: "Device Behaviour",
        label: "devive_behaviour",
      },
      {
        value: "ID Mapping",
        label: "id_mapping",
      },
    ],
  }),
  computed: {
    filteredOrders() {
      return (this as any).allOrders.filter((order: any) => {
        return (
          order.name.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
          order.data_package_type
            .toLowerCase()
            .includes(this.searchQuery.toLowerCase())
        );
      });
    },
    allOrders: {
      get(): any {
        const data = JSON.parse(localStorage.getItem("StoreOrders") as string);
        return data;
      },
      set(data: any) {
        return data;
      },
    },
  },
  // mounted() {
  //   localStorage.setItem("StoreOrders", JSON.stringify(this.x));
  // },
  methods: {
    setToSearchQuery(value: string) {
      this.searchQuery = value;
    },
    handleDelete(value: any) {
      this.$confirm(
        "This buy order will permanently deleted. Continue?",
        "Warning",
        { type: "warning", cancelButtonText: "Cancel" }
      )
        .then(() => {
          const index = this.allOrders.findIndex((i: any) => i.id === value);
          this.allOrders = this.allOrders.splice(index, 1);
          this.$message({
            type: "success",
            message: "Delete completed",
          });
          localStorage.setItem("StoreOrders", JSON.stringify(this.allOrders));
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "Delete canceled",
          });
        });
    },
    openEditModal() {
      this.showUpdateModal = true;
    },
    closeEditModal() {
      this.showUpdateModal = false;
    },
  },
});
</script>
