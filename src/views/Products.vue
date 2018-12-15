<template>
    <div class="container">
        <h1 class="text-center" style="margin; 10px;">Product List</h1>
        <b-table striped hover :items="products" :fields="fields" :per-page="pageSize" :current-page="pageIndex"></b-table>
        <b-pagination :total-rows="products.length" :per-page="pageSize" v-model="pageIndex"  align="center"/>
    </div>
</template>

<script>
import axios from "axios";
export default {
  name: "products",
  data() {
    return {
      message: "Project 2",
      products: [],
      pageSize: 10,
      pageIndex: 1,
      fields: [
        {
          key: "product_id",
          sortable: true
        },
        {
          key: "product_name",
          sortable: true
        },
        {
          key: "unit_price",
          sortable: true,
          variant: 'danger'
        }
      ]
    };
  },
  mounted() {
    var instance = this;
    axios
      .get("https://shielded-spire-43023.herokuapp.com/api/products/")
      .then(function(response) {
        console.log(response);
        instance.products = response.data.data;
      });
  }
};
</script>