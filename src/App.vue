<script>
import axios from "axios";
import Swal from "sweetalert2/dist/sweetalert2.js";

import TheNavBar from "./components/TheNavBar.vue";
import TheRegister from "./components/TheRegister.vue";
import TheLogin from "./components/TheLogin.vue";
import TheHome from "./components/TheHome.vue";
import TheCategory from "./components/TheCategory.vue";
import TheHistory from "./components/TheHistory.vue";
import TheAddFood from "./components/TheAddFood.vue";
import TheEditFood from "./components/TheEditFood.vue";

const baseURL = "http://localhost:3000";
// const baseURL = "https://restaurant-server-fikar.herokuapp.com"

export default {
  components: {
    TheNavBar,
    TheRegister,
    TheLogin,
    TheHome,
    TheCategory,
    TheHistory,
    TheAddFood,
    TheEditFood
  },

  data() {
    return {
      isLogin: false, // kondisi sebelum login
      currentPage: "login-form",
      dataFood: [],
      dataHistory: [],
      dataCategory: [],
      dataDetailFood: [],
      foodId: 0,
      status: "",
    };
  },

  methods: {
    goHome: function () {
      this.currentPage = "list-food";
      this.getDataFood();
      this.getDataCategory();
    },
    goAddFood: function () {
      this.currentPage = "add-food";
      this.getDataCategory();
    },
    goEditFood: function (id) {
      this.currentPage = "edit-food";
      this.getDataCategory();
      this.foodId= +id
      this.getDetailFood()

    },
    goCategory: function () {
      this.currentPage = "list-category";
      this.getDataCategory();
    },
    goHistory: function () {
      this.currentPage = "list-history";
      this.getDataHistory();
    },
    goLogin: function () {
      this.currentPage = "login-form";
    },
    goRegister: function () {
      this.currentPage = "register-form";
    },

    loginHandle: function (objLogin) {
      axios
        .post(`${baseURL}/user/login`, {
          email: objLogin.email,
          password: objLogin.password
        })
        .then((response) => {
          // console.log(response.data, "ini response dari loginHandle");
          localStorage.setItem("access_token", response.data.access_token);
          localStorage.setItem("id", response.data.payload.id);
          localStorage.setItem("role", response.data.payload.role);

          this.isLogin = true;
          this.currentPage = "list-food";

          Swal.fire({
            icon: 'success',
            text: "Login Success"
          })

        })
        .catch((error) => {
          // console.log(error.response.data.error.message);
          Swal.fire({
            icon: 'error',
            text: error.response.data.error.message
          })
        });
    },

    registerHandle: function (objRegister) {
      axios
        .post(`${baseURL}/user/register`, {
          username: objRegister.username,
          email: objRegister.email,
          password: objRegister.password,
          phoneNumber: objRegister.phoneNumber,
          address: objRegister.address,
        })
        .then((response) => {
          // console.log(response.data, "ini response dari registerHandle");
          this.currentPage = "login-form";
          Swal.fire({
            icon: 'success',
            text: "Register Success, now Please Login"
          })
        })
        .catch((error) => {
          // console.log(error.response.data.error.message);
          Swal.fire({
            icon: 'error',
            text: error.response.data.error.message
          })
        });
    },

    addNewFood: function (objAddFood, foodId) {
      axios
        .post(`${baseURL}/food`, {
          name: objAddFood.name,
          description: objAddFood.description,
          price: objAddFood.price,
          imgUrl: objAddFood.imgUrl,
          categoryId: objAddFood.categoryId,
        } , {
          headers: {
            access_token: localStorage.getItem("access_token"),
          },
        })
        .then((response) => {
          // console.log(response, "ini response dari addNewFood");
          this.currentPage = "list-food";
          Swal.fire({
            icon: 'success',
            text: response.data.message
          })
        })
        .catch((error) => {
          // console.log(error.response.data.error.message[0], "ini error");
          Swal.fire({
            icon: 'error',
            text: error.response.data.error.message[0]
          })
        });
    },

    editFood: function (objEditFood) {
      axios
        .put(`${baseURL}/food/${this.foodId}`, {
          name: objEditFood.name,
          description: objEditFood.description,
          price: objEditFood.price,
          imgUrl: objEditFood.imgUrl,
          categoryId: objEditFood.categoryId,
        } , {
          headers: {
            access_token: localStorage.getItem("access_token"),
          },
        })
        .then((response) => {
          // console.log(response.data.message, "ini response dari addNewFood");
          this.currentPage = "list-food";
          Swal.fire({
            icon: 'success',
            text: response.data.message
          })
        })
        .catch((error) => {
          // console.log(error.response.data.error.message[0], "ini error");
          Swal.fire({
            icon: 'error',
            text: error.response.data.error.message[0]
          })
        });
    },

    getDetailFood: function () {
      axios
        .get(`${baseURL}/food/${this.foodId}`, {
          headers: {
            access_token: localStorage.getItem("access_token"),
          },
        })
        .then((response) => {
          // console.log(response.data.data, "ini response dari getDetailFood");
          this.dataDetailFood = response.data.data;
        })
        .catch((error) => {
          // console.log(error.message);
          Swal.fire({
            icon: 'error',
            text: error.message
          })
        });
    },

    getDataFood: function () {
      axios
        .get(`${baseURL}/food`, {
          headers: {
            access_token: localStorage.getItem("access_token"),
          },
        })
        .then((response) => {
          // console.log(response.data.data, "ini response dari getDataFood");
          this.dataFood = response.data.data;
        })
        .catch((error) => {
          // console.log(error.message);
          Swal.fire({
            icon: 'error',
            text: error.message
          })
        });
    },

    getDataCategory: function () {
      axios
        .get(`${baseURL}/category`, {
          headers: {
            access_token: localStorage.getItem("access_token"),
          },
        })
        .then((response) => {
          // console.log(
          //   response.data.category,
          //   "ini response dari getDataCategory"
          // );
          this.dataCategory = response.data.category;
        })
        .catch((error) => {
          // console.log(error);
          Swal.fire({
            icon: 'error',
            text: error.message
          })
        });
    },

    getDataHistory: function () {
      axios
        .get(`${baseURL}/history`, {
          headers: {
            access_token: localStorage.getItem("access_token"),
          },
        })
        .then((response) => {
          // console.log(response, "ini response dari getDataHistory");
          this.dataHistory = response.data.history;
        })
        .catch((error) => {
          // console.log(error);
          Swal.fire({
            icon: 'error',
            text: error.message
          })
        });
    },

    updateStatus: function (foodId, status) {
      axios
        .patch(`${baseURL}/food/${foodId}`, {status}, {
          headers: {
            access_token: localStorage.getItem("access_token"),
          },
        })
        .then((response) => {
          // console.log(response.data.message, "ini response dari updateStatus");
          this.currentPage = "list-food"
          Swal.fire({
            icon: 'success',
            text: response.data.message
          })

        })
        .catch((error) => {
          // console.log(error.response.data.error.message);
          Swal.fire({
            icon: 'error',
            text: error.response.data.error.message
          })
        });
    },

    logoutHandle: function () {
      localStorage.clear();
      (this.isLogin = false), this.goLogin();
      Swal.fire({
            icon: 'success',
            text: "Logout Success"
          })
    },
  }, // INI BATAS METHOD

  created() {
    if (localStorage.getItem("access_token")) {
      this.isLogin = true;
      this.currentPage = "list-food";
    }
  },
};
</script>

<template>
  <TheNavBar 
    v-if="isLogin === true"
    v-on:logoutHandler="logoutHandle"
    v-on:goHome="goHome"
    v-on:goCategory="goCategory"
    v-on:goAddFood="goAddFood"
    v-on:goHistory="goHistory"
  />

  <TheLogin
    v-if="isLogin === false && currentPage === 'login-form'"
    v-bind:isLogin="isLogin"
    v-bind:currentPage="currentPage"
    v-on:goHome="goHome"
    v-on:goRegister="goRegister" 
    v-on:loginHandle="loginHandle"
  />

  <TheRegister 
    v-if="isLogin === false && currentPage === 'register-form'"
    v-on:goLogin="goLogin"
    v-on:registerHandle="registerHandle"
  />

  <TheHome 
    v-if="isLogin === true && currentPage === 'list-food'" 
    v-bind:dataFood="dataFood"
    v-on:updateStatus="updateStatus"
    v-on:getDataFood="getDataFood"
    v-on:goEditFood="goEditFood"
  />

  <TheCategory 
    v-if="isLogin === true && currentPage === 'list-category'" 
    v-bind:dataCategory="dataCategory"
    v-on:getDataCategory="getDataCategory"
  />

  <TheHistory 
    v-if="isLogin === true && currentPage === 'list-history'"
    v-bind:dataHistory="dataHistory"
    v-on:getDataHistory="getDataHistory"
  />

  <TheAddFood 
    v-if="isLogin === true && currentPage === 'add-food'" 
    v-on:submitFood="addNewFood"
    v-bind:dataCategory="dataCategory"
  />

  <TheEditFood 
    v-if="isLogin === true && currentPage === 'edit-food'" 
    v-on:submitFood="editFood"
    v-bind:dataCategory="dataCategory"
    v-bind:dataDetailFood="dataDetailFood"
    v-bind:currentPage="currentPage"
  />

</template>

<style></style>
