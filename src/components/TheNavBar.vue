<script>
export default {
  name: "TheNavBar",
  emits: ["logoutHandler", "goHome", "goCategory", "goAddFood", "goHistory" ],
  data() {
    return {
      role: localStorage.getItem("role")
    }
  },
  methods: {
    logoutHandler() {
      this.$emit("logoutHandler")
    },
    goHome() {
      this.$emit("goHome")
    },
    goCategory() {
      this.$emit("goCategory")
    },
    goAddFood() {
      this.$emit("goAddFood")
    },
    goHistory() {
      this.$emit("goHistory")
    }
  },
  computed: {
    currentRole () {
      if (this.role === "admin") {
        return "YOU SIGN AS ADMIN"
      } else {
        return "YOU SIGN AS STAFF"
      }
    }
  }
}
</script>

<template>
<!-- NAVBAR -->
    <nav class="navbar navbar-expand-lg bg-primary container-xxl mb-1">
      <div class="container-fluid">
        <a class="navbar-brand" href="#" v-on:click.prevent="goHome">Restaurant Fikar</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent"
          aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item" id="navListFood">
              <a class="nav-link active" aria-current="page" href="#" v-on:click.prevent="goHome">List Food</a>
            </li>
            <li class="nav-item" id="navListCategory">
              <a class="nav-link" href="#" v-on:click.prevent="goCategory">List Category</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#" id="navAddFood" v-on:click.prevent="goAddFood">Add Food</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#" id="navRegister" v-on:click.prevent="goHistory">History</a>
            </li>
          </ul>
          <div class="d-flex" role="search" id="role">
            <a class="nav-link" >{{ currentRole }} &emsp;</a>
          </div>
          <div class="d-flex" role="search" id="navLogout">
            <a class="nav-link" href="#" v-on:click.prevent="logoutHandler"><b>Logout</b></a>
          </div>
        </div>
      </div>
    </nav>
</template>