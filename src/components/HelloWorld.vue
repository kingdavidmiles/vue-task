<template>
  <div class="hello px-5">
    <div class="row">
      <div class="col-4" v-for="(user, index) in users" :key="index">
        <div>
          <b-card
            class="my-2 text text-capitalize shadow-md"
            @click="copyText(user.phone)"
          >
            <b-card-text>
              name: &nbsp;{{ user.name }} {{ user.username }}
            </b-card-text>

            <b-card-text>email: &nbsp; {{ user.email }}</b-card-text>
            <b-card-text>address: &nbsp; {{ user.address.street }}</b-card-text>
            <b-card-text>zipcode: &nbsp;{{ user.address.zipcode }}</b-card-text>
            <b-card-text>phone: &nbsp;{{ user.phone }}</b-card-text>
            <b-card-text>website:&nbsp; {{ user.website }}</b-card-text>
            <b-card-text>company: &nbsp;{{ user.company.name }}</b-card-text>
          </b-card>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Swal from 'sweetalert2'
export default {
  name: "HelloWorld",
  data() {
    return {
      apiUrl: "https://jsonplaceholder.typicode.com/users",
      users: [],
    };
  },
  methods: {
    copyText(text) {
      navigator.clipboard
        .writeText(text)
        .then(() => {
          console.log("Text copied to clipboard:", text);
          Swal.fire({
            position: "center",
            icon: "success",
            title: "phone number copied successfully",
            showConfirmButton: false,
            timer: 1500,
          });
        })
        .catch((error) => {
          console.error("Error copying text to clipboard:", error);
        });
    },
  },
  mounted() {
    axios
      .get(this.apiUrl)
      .then((response) => {
        this.users = response.data;
        console.log("API response:", this.posts);
      })
      .catch((error) => {
        console.error("Error fetching API data:", error);
      });
  },
};
</script>
<style scoped>
.text {
  text-align: left;
}
</style>