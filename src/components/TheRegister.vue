<script>
export default {
  name: "TheRegister",
  emits: ["goLogin", "registerHandle"],
  data() {
    return {
      objRegister: {
        username: "",
        email: "",
        password: "",
        phoneNumber: "",
        address: "",
      },
    }
  },
  methods: {
    goLogin() {
      this.$emit("goLogin")
    },
    registerHandle() {
      this.$emit("registerHandle", this.objRegister)
    }
  },
}
</script>

<template>
<!-- REGISTER-FORM -->
    <div class="register-form text-center mt-5 mb-5">
      <form action="" method="post" style="max-width: 480px; margin: auto">
        <img class="mt-4 mb-4" src="https://getbootstrap.com/docs/5.2/assets/brand/bootstrap-logo.svg"
          alt="bootstrap-logo" height="72" />
        <h1 class="h3 mb-3 font-weight-normal">Sign Up</h1>
        <label class="sr-only">Username</label>
        <input type="text" id="username-register" class="form-control" placeholder="Username"
          v-model="objRegister.username" required autofocus />
        <label class="sr-only">Email Address</label>
        <input type="email" id="email-register" class="form-control" placeholder="Email Address"
          v-model="objRegister.email" required autofocus />
        <label class="sr-only">Password</label>
        <input type="password" id="password-register" placeholder="Password" class="form-control"
          v-model="objRegister.password" />
        <label class="sr-only">Phone Number</label>
        <input type="number" id="phone-number-register" class="form-control" placeholder="Phone Number"
          v-model="objRegister.phoneNumber" required autofocus />
        <label class="sr-only">Address</label>
        <input type="text" id="address-register" class="form-control" placeholder="Address"
          v-model="objRegister.address" required autofocus />
        <div class="mt-3">
          <button class="btn btn-lg btn-primary btn-block col-12" id="signup-button" type="submit"
            v-on:click.prevent="registerHandle">
            Sign Up
          </button>
        </div>
        <div class="mt-3">
          <p>
            Already have account?
            <a href="#" id="signin-anchor" v-on:click.prevent="goLogin">Sign In</a>
          </p>
        </div>
      </form>
    </div>
    <!-- BATAS REGISTER FORM -->
</template>