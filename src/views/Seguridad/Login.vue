<template>
  <div
    class="page-header align-items-start min-vh-100 bg-dark">
    <span class="mask bg-gradient-dark opacity-6"></span>
    <div class="container my-auto">
      <div class="row">
        <div class="col-lg-4 col-md-8 col-12 mx-auto">
          <div class="card z-index-0 fadeIn3 fadeInBottom">
            <div class="card-header p-0 position-relative mt-n4 mx-3 z-index-2">
              <div
                class="bg-gradient-dark shadow-dark border-radius-lg py-3 pe-1"
              >
                <h4 class="text-white font-weight-bolder text-center mt-2 mb-0">
                  Subsitema de Monitoreo y Pruebas
                </h4>
              </div>
            </div>
            <div class="card-body">
              <div class="mb-3">
                <label class="form-label">Usuario</label>
                <input
                  class="form-control border-secondary border p-2"
                  id="email"
                  type="text"
                  name="email"
                  v-model="user"
                />
              </div>
              <div class="mb-3">
                <label class="form-label">Contraseña</label>
                <input
                  class="form-control border-secondary border p-2"
                  id="password"
                  type="password"
                  name="password"
                  v-model="password"
                />
              </div>
              <material-switch id="rememberMe" name="Remember Me"
              >Remember me
              </material-switch
              >
              <div class="text-center">
                <div v-if="error"
                     class="bg-gradient-danger text-white p-3 d-flex align-items-center justify-content-center">
                  <i class="material-icons me-2">warning</i>
                  Credenciales Incorrectas
                </div>
                <button
                  @click="Login"
                  class="my-4 mb-2 btn bg-gradient-dark form-control"
                >Aceptar
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import MaterialInput from "@/components/MaterialInput.vue";
import MaterialSwitch from "@/components/MaterialSwitch.vue";
import MaterialButton from "@/components/MaterialButton.vue";
import { mapMutations } from "vuex";
import axios from "axios";
import MaterialAlert from "@/components/MaterialAlert.vue";

const LOGIN = `mutation TokenAuth($password:String!, $user:String!) {
    tokenAuth(password: $password, username: $user) {
        token
        success
        errors
        user {
            id
            lastLogin
            username
            firstName
            lastName
            email
            isStaff
            isActive
            dateJoined
            pk
            archived
            verified
            secondaryEmail
        }
    }
}
`;

export default {
  name: "SigninBasic",
  data() {
    return {
      user: "",
      password: "",
      error: false
    };
  },
  components: {
    MaterialAlert,
    Navbar,
    MaterialInput,
    MaterialSwitch,
    MaterialButton
  },
  beforeMount() {
    this.toggleEveryDisplay();
    this.toggleHideConfig();
  },
  beforeUnmount() {
    this.toggleEveryDisplay();
    this.toggleHideConfig();
  },
  methods: {
    ...mapMutations(["toggleEveryDisplay", "toggleHideConfig"]),
    Login() {
      if (this.user === "" || this.password === "") {
        this.error = true;
        return false;
      }
      axios.post(this.$store.state.url, {
        query: LOGIN,
        variables: {
          user: this.user,
          password: this.password
        }
      }).then(response => {
        if (response.data.data.tokenAuth.success) {
          this.$store.state.autorizado = true;
          this.$store.state.user = response.data.data.tokenAuth.user;
          this.$router.push("/");
        } else {
          this.error = true;
          return false;
        }
      }).catch(error => {
        alert(error);
        this.error = true;
      });
    }
  }
};
</script>
