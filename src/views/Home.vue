<template>
  <div>
    <nav-bar></nav-bar>
    <div
      :style="bgImage"
      class="w-full text-center bg-blue-900 bg-cover bg-center bg-no-repeat"
    >
      <h2
        class="text-white text-xl md:text-5xl font-bold w-8/12 mx-auto pt-16 leading-normal"
      >
        The Data Commerce Platform that makes it easy to buy and sell
      </h2>
      <button
        @click="showCreateModal = true"
        class="w-64 md:w-80 mx-auto bg-white text-blue-800 my-12 rounded text-white py-4 text-center font-semibold text-lg hover:text-white hover:bg-blue-800"
      >
        Create Buy Order
      </button>
    </div>
    <section
      class="py-16 flex justify-center flex-col px-10 md:px-20 w-full md:w-8/12 mx-auto relative"
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
        class="absolute w-4 h-4 top-24 left-12 md:left-24 -mt-2"
      />
      <div
        v-show="searchQuery !== ''"
        @click="searchQuery = ''"
        class="absolute right-24 top-20 w-6 h-6 cursor-pointer"
      >
        x
      </div>
      <div class="pt-5 flex items-center flex-col md:flex-row">
        <h3 class="text-blue-800 font-semibold mr-6">Featured Searches</h3>
        <div
          class="rounded-full border border-blue-600 text-blue-800 font-semibold cursor-pointer py-2 px-4 w-auto text-center flex mr-4 my-2 md:my-0"
          v-for="(item, index) in searchOptions"
          :key="index"
          @click="setToSearchQuery(item.value)"
        >
          {{ item.value }}
        </div>
      </div>
    </section>
    <div class="flex justify-between items-center px-6 md:px-24 py-6">
      <h2 class="text-blue-900 font-semibold text-sm md:text-2xl">
        Featured Data Streams
      </h2>
      <p class="text-sm md:text-lg font-semibold text-gray-700">
        Showing Top {{ filteredOrders.length }} Results
      </p>
    </div>
    <section class="px-6 md:px-24 py-16">
      <div
        v-if="filteredOrders.length > 0"
        class="grid grid-cols-1 md:grid-cols-4 gap-5"
      >
        <div v-for="order in filteredOrders" :key="order.id">
          <card-component
            :cardDetails="order"
            @handleDelete="handleDelete"
            @openEditModal="openEditModal"
            @handleSelect="handleSelect"
          ></card-component>
        </div>
      </div>
      <h1
        v-else
        class="flex justify-center items-center text-4xl text-blue-800"
      >
        No Data Available
      </h1>
    </section>
    <add-buy-order-modal
      v-model="showCreateModal"
      @setOrders="setOrders"
    ></add-buy-order-modal>
    <update-buy-order-modal
      v-model="showUpdateModal"
      :selectedOrder="selectedOrder"
      @setOrders="setOrders"
    ></update-buy-order-modal>
  </div>
</template>

<script>
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
    selectedOrder: {},
    x: AllData,
    allOrders: [],
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
      return this.allOrders.filter((order) => {
        return (
          order.name.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
          order.data_package_type
            .toLowerCase()
            .includes(this.searchQuery.toLowerCase())
        );
      });
    },
  },
  created() {
    this.setOrders();
  },
  methods: {
    setToSearchQuery(value) {
      this.searchQuery = value;
    },
    handleSelect(x) {
      this.selectedOrder = x;
    },
    handleDelete(value) {
      this.$confirm(
        "This buy order will permanently deleted. Continue?",
        "Warning",
        { type: "warning", cancelButtonText: "Cancel" }
      )
        .then(() => {
          let orders = JSON.parse(localStorage.getItem("StoreOrders"));
          const index = orders.findIndex((item) => {
            return item.id === value;
          });
          orders.splice(index, 1);
          this.$message({
            type: "success",
            message: "Delete completed",
          });
          localStorage.setItem("StoreOrders", JSON.stringify(orders));
          this.setOrders();
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
    setOrders() {
      this.allOrders = JSON.parse(localStorage.getItem("StoreOrders")) || [];
    },
  },
});
</script>
