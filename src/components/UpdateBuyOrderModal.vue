<template>
  <div class="create_by_order">
    <el-dialog
      :visible.sync="showModal"
      :appendToBody="true"
      style=""
      :showClose="false"
      :beforeClose="closeModal"
      center
    >
      <span
        class="absolute -top-10 right-0 p-2 rounded-full bg-white cursor-pointer text-gray-600"
        @click="closeModal()"
      >
        <times-icon width="8" height="8" />
      </span>
      <template #title class="px-8 py-5">
        <div class="w-full flex gap-4">
          <span>
            <svg
              width="32"
              height="32"
              viewBox="0 0 32 32"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <rect
                width="32"
                height="32"
                rx="16"
                fill="#D2E6FC"
                fill-opacity="0.3"
              />
              <g clip-path="url(#clip0_1661_27715)">
                <path
                  d="M11.7922 12.0013C11.7922 9.95224 13.4531 8.29128 15.5022 8.29128C15.6225 8.29128 15.7388 8.299 15.8551 8.30672C14.611 7.33101 12.8856 7.25045 11.5561 8.10622C10.2268 8.96199 9.58544 10.566 9.95858 12.1023C10.3317 13.6387 11.6373 14.7699 13.211 14.9206C12.3151 14.2169 11.7919 13.1406 11.7922 12.0013Z"
                  fill="#D4E1F4"
                />
                <path
                  d="M15.4979 17.4102C15.9357 17.4097 16.3723 17.4552 16.8006 17.5459C15.8267 16.945 14.7038 16.6294 13.5595 16.6348C10.1442 16.6426 7.37999 19.368 7.38771 23.078L9.36487 23.0741C9.71772 19.7673 12.3268 17.4179 15.4979 17.4102Z"
                  fill="#D4E1F4"
                />
                <path
                  d="M18.0217 21.7559C18.0217 20.3377 18.7963 19.0324 20.0412 18.3531C21.2862 17.6736 22.803 17.7283 23.9959 18.4956C23.1996 17.2587 21.7722 16.5789 20.3102 16.7403C18.8481 16.9017 17.6034 17.8767 17.0962 19.2573C16.5891 20.6381 16.9069 22.1869 17.917 23.2563C18.1319 23.4841 18.3741 23.6847 18.638 23.8533C18.2341 23.2284 18.02 22.4999 18.0217 21.7559Z"
                  fill="#D4E1F4"
                />
                <path
                  d="M13.5636 15.3244C15.8266 15.3244 17.6613 13.4897 17.6613 11.2266C17.6613 8.96341 15.8266 7.12891 13.5636 7.12891C11.3005 7.12891 9.46582 8.96341 9.46582 11.2266C9.46794 13.4888 11.3012 15.3223 13.5636 15.3244ZM13.5636 7.90426C15.3985 7.90426 16.8859 9.39168 16.8859 11.2266C16.8859 13.0616 15.3985 14.549 13.5636 14.549C11.7286 14.549 10.2412 13.0616 10.2412 11.2266C10.2433 9.39259 11.7295 7.90638 13.5636 7.90426Z"
                  fill="#2357D1"
                />
                <path
                  d="M13.5595 17.0215H13.5712C15.0503 17.0138 16.4742 17.5826 17.5411 18.6071L18.0799 18.0489C16.8681 16.8852 15.2512 16.2386 13.5712 16.2462H13.5595C11.7841 16.2499 10.1364 16.94 8.91524 18.1962C7.67467 19.4639 6.99623 21.1968 7.00002 23.077C7.00077 23.1799 7.04106 23.2785 7.11253 23.3524C7.18537 23.4252 7.28457 23.4658 7.38769 23.4647L17.7 23.4453V22.67L7.78703 22.6894C7.86851 21.1658 8.45775 19.774 9.4695 18.739C10.5435 17.6341 11.9973 17.0253 13.5595 17.0215Z"
                  fill="#2357D1"
                />
                <path
                  d="M22.3052 20.2049H21.1228V19.0224C21.1228 18.8085 20.9493 18.6348 20.7351 18.6348C20.521 18.6348 20.3474 18.8085 20.3474 19.0224V20.2049H19.165C18.9509 20.2049 18.7773 20.3786 18.7773 20.5925C18.7773 20.8067 18.9509 20.9802 19.165 20.9802H20.3474V22.1626C20.3474 22.3768 20.521 22.5503 20.7351 22.5503C20.9493 22.5503 21.1228 22.3768 21.1228 22.1626V20.9802H22.3052C22.5194 20.9802 22.6929 20.8067 22.6929 20.5925C22.6929 20.3786 22.5194 20.2049 22.3052 20.2049Z"
                  fill="#2357D1"
                />
                <path
                  d="M20.7352 16.3282C18.38 16.3282 16.4707 18.2375 16.4707 20.5926C16.4707 22.9479 18.38 24.8571 20.7352 24.8571C23.0903 24.8571 24.9996 22.9479 24.9996 20.5926C25.0054 19.4599 24.5581 18.3718 23.757 17.5709C22.956 16.7699 21.8679 16.3224 20.7352 16.3282ZM20.7352 24.0818C18.8081 24.0818 17.2461 22.5197 17.2461 20.5926C17.2461 18.6658 18.8081 17.1035 20.7352 17.1035C22.6622 17.1035 24.2243 18.6658 24.2243 20.5926C24.2243 22.5197 22.6622 24.0818 20.7352 24.0818Z"
                  fill="#4CAF6E"
                />
              </g>
              <defs>
                <clipPath id="clip0_1661_27715">
                  <rect
                    width="18"
                    height="18"
                    fill="white"
                    transform="translate(7 7)"
                  />
                </clipPath>
              </defs>
            </svg>
          </span>
          <div class="flex flex-col w-9/12">
            <h4 class="text-payazablue-800 font-medium text-base">
              Edit buy order
            </h4>
            <span class="text-gray-500 text-xs"
              >Supply the details to edit a buy order</span
            >
            <el-form
              ref="editBuyOrderForm"
              :model="editBuyOrderForm"
              class="py-16"
            >
              <el-form-item prop="name">
                <CustomInput
                  placeholder="Name"
                  v-model="editBuyOrderForm.name"
                />
              </el-form-item>
              <el-form-item prop="max_bid_price">
                <el-tooltip
                  class="item"
                  effect="dark"
                  content="Maximum bid price is $10000"
                  placement="right"
                >
                  <CustomInput
                    placeholder="Max Bid Price"
                    v-model="editBuyOrderForm.max_bid_price"
                    :maxlength="5"
                  />
                </el-tooltip>
              </el-form-item>
              <el-form-item>
                <el-select
                  v-model="editBuyOrderForm.data_package_type"
                  placeholder="Select Data Package Type"
                  style="width: 100%; outline: none"
                >
                  <el-option
                    v-for="item in packageType"
                    :key="item.value"
                    :label="item.value"
                    :value="item.value"
                  >
                  </el-option>
                </el-select>
              </el-form-item>
              <button
                @click.prevent="handleCreate"
                class="bg-blue-600 text-white py-3 w-full rounded"
              >
                Submit
              </button>
            </el-form>
          </div>
        </div>
      </template>
    </el-dialog>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import TimesIcon from "@/assets/svg-ivons/TimesIcon.vue";
import CustomInput from "@/components/CustomInput.vue";

export default Vue.extend({
  components: { TimesIcon, CustomInput },
  model: {
    prop: "visible",
    event: "updateVisibility",
  },
  props: ["visible"],
  data: () => ({
    showModal: false,
    editBuyOrderForm: {
      name: "",
      max_bid_price: "",
      data_package_type: "",
    },
    rules: {
      name: [
        {
          required: true,
          message: "Please enter order name",
        },
      ],
      max_bid_price: [
        {
          required: true,
          message: "Please enter your max bid price",
        },
      ],
      data_package_type: [
        {
          required: true,
          message: "Please confirm your data package type",
          trigger: "change",
        },
      ],
    },
    packageType: [
      {
        value: "Device Location",
      },
      {
        value: "Device Behaviour",
      },
      {
        value: "ID Mapping",
      },
    ],
  }),
  watch: {
    visible(val) {
      // this.$emit("updateVisibility", val)
      this.showModal = val;
    },
    showModal(val) {
      this.$emit("updateVisibility", val);
    },
  },
  methods: {
    closeModal() {
      this.$emit("updateVisibility", false);
    },
    handleCreate() {
      console.log("i got here");
      // eslint-disable-next-line @typescript-eslint/ban-ts-comment
      /// @ts-ignore
      this.$refs["editBuyOrderForm"].validate((valid) => {
        if (valid) {
          const payload = { ...this.editBuyOrderForm };
          const allOrders = JSON.parse(
            localStorage.getItem("StoreOrders") as string
          );
          allOrders.push(payload);
          localStorage.setItem("StoreOrders", JSON.stringify(allOrders));
          this.closeModal();
        }
      });
    },
  },
});
</script>

<style scoped>
* >>> .el-input__inner {
  height: 65px !important;
  padding: 0 15px !important;
}

* >>> .el-dialog {
  width: 416px !important;
  max-width: 95% !important;
  border-radius: 20px !important;
  border-radius: 8px !important;
  position: relative !important;
}
* >>> .el-dialog__header {
  padding-bottom: 20px;
}

* >>> .el-dialog__header,
* >>> .el-dialog__footer {
  text-align: left !important;
}

* >>> .el-dialog--center .el-dialog__body {
  text-align: initial;
  padding: 25px 25px 0px;
}

* >>> .el-dialog__body {
  /* padding-top: 0 !important;
  padding-bottom: 0 !important; */
  background: #fcfcfd;
}
</style>
