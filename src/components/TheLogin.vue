<script>
import axios from "axios";
import Swal from "sweetalert2/dist/sweetalert2.js";
const baseUrl = "http://localhost:3000";
// const baseURL = "https://restaurant-server-fikar.herokuapp.com";

export default {
  name: "TheLogin",
  props: ["isLogin", "currentPage"],
  emits: ["goRegister", "loginHandle", "goHome"],
  data() {
    return {
      objLogin: {
        email: "",
        password: "",
      },
    };
  },
  methods: {
    goRegister() {
      this.$emit("goRegister");
    },
    loginHandle() {
      this.$emit("loginHandle", this.objLogin);
    },
    buttonGoHome() {
      this.$emit("goHome");
    },
    handleCredentialResponse(response) {
      axios({
        method: "POST",
        url: baseUrl + "/user/login-google",
        data: {
          credential: response.credential,
        },
      })
        .then((response) => {
          // console.log(response);
          localStorage.setItem("access_token", response.data.access_token);
          localStorage.setItem("id", response.data.dataUser.id);
          localStorage.setItem("role", response.data.dataUser.role);

          this.buttonGoHome();

          Swal.fire({
            icon: "success",
            text: "Login Success",
          }).then(() => {
            this.buttonGoHome()
          });
        })
        .catch((err) => {
          // console.log(err);
          Swal.fire({
            icon: "error",
            text: error.response.data.error.message,
          });
        });
    },
  },
  mounted() {
    const cb = this.handleCredentialResponse;

    window.onload = function () {
      google.accounts.id.initialize({
        client_id:
          "97034013937-4ojhlo9i1gv9q66li46jkfqajvf1tbt6.apps.googleusercontent.com",
        callback: cb,
      });
      google.accounts.id.renderButton(
        document.getElementById("buttonDiv"),
        { theme: "outline", size: "large" } // customization attributes
      );
    };
  },
};
</script>

<template>
  <!-- LOGIN FORM -->
  <div class="login-form text-center mt-5">
    <form action="" method="post" style="max-width: 480px; margin: auto">
      <img
        class="mt-4 mb-4"
        src="https://getbootstrap.com/docs/5.2/assets/brand/bootstrap-logo.svg"
        alt="bootstrap-logo"
        height="72"
      />
      <h1 class="h3 mb-3 font-weight-normal">Sign In</h1>
      <label class="sr-only">Email Address</label>
      <input
        type="email"
        id="email-login"
        class="form-control"
        placeholder="Email Address"
        required
        autofocus
        v-model="objLogin.email"
      />
      <label class="sr-only">Password</label>
      <input
        type="password"
        id="password-login"
        placeholder="Password"
        class="form-control"
        v-model="objLogin.password"
      />
      <div class="mt-3">
        <button
          class="btn btn-lg btn-primary btn-block col-12"
          id="signin-button"
          type="submit"
          v-on:click.prevent="loginHandle"
        >
          Sign In
        </button>
      </div>
      <div class="mt-3">
        <p>
          Don't have account yet?
          <a href="#" id="signup-anchor" v-on:click.prevent="goRegister"
            >Sign Up</a
          >
        </p>
      </div>
      <div id="buttonDiv"></div>
    </form>
  </div>
  <!-- BATAS LOGIN FORM -->
</template>
