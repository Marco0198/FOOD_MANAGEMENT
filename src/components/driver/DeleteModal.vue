<template>
    <div>
      <b-row class="mt-2 mb-3">
        <h6 class="text-secondary">
          Are you sure you want to delete this Driver ?
        </h6>
      </b-row>
      <b-row class="mt-2 mb-3">
        <p class="text-danger">
          This action is not reversible and may result in the loss if important
          data.
        </p>
      </b-row>
      <b-row class="mt-4">
        <b-col>
          <b-button variant="danger" @click="removeCustomerFromData"
            >Delete Driver</b-button
          >
        </b-col>
        <b-col>
          <b-button variant="warning" @click="triggerClose">Close</b-button>
        </b-col>
      </b-row>
    </div>
  </template>
  
  <script>
  import axios from "axios";
  
  export default {
    name: "DeleteCustomerModal",
    props: {
      customerId: String,
    },
    methods: {
      triggerClose() {
        this.$emit("closeDeleteModal");
      },
      removeCustomerFromData() {
        axios
          .delete(`http://localhost:8083/api/driver/delete/${this.customerId}`)
          .then(() => {
            this.$emit("reloadDataTable");
            this.$emit("showDeleteAlert");
            this.$emit("closeDeleteModal");
          })
          .catch((error) => {
            console.log(error);
          });
      },
    },
  };
  </script>