<template>
  <aside
    id="sidenav-main"
    class="sidenav navbar navbar-vertical navbar-expand-xs border-0 border-radius-xl my-3 ms-3"
    :class="`${
      isRTL ? 'me-3 rotate-caret fixed-end' : 'fixed-start ms-3'
    } ${sidebarType}`"
  >
    <div class="sidenav-header">
      <i
        id="iconSidenav"
        class="top-0 p-3 cursor-pointer fas fa-times text-secondary opacity-5 position-absolute end-0 d-none d-xl-none"
        aria-hidden="true"
      ></i>
      <router-link class="m-0 navbar-brand d-flex align-items-center" to="/">
        <i class="material-icons-round text-white opacity-10">speed</i>
        <span class="ms-1 font-weight-bold text-white"
          >Monitoreo y pruebas</span
        >
      </router-link>
    </div>
    <hr class="horizontal light mt-0 mb-2" />
    <sidenav-list />
  </aside>
</template>
<script>
import SidenavList from "./SidenavList.vue";
import logo from "@/assets/img/logo-ct.png";
import logoDark from "@/assets/img/logo-ct-dark.png";
import { mapState } from "vuex";
export default {
  name: "Index",
  components: {
    SidenavList,
  },
  data() {
    return {
      logo,
      logoDark,
    };
  },
  computed: {
    ...mapState(["isRTL", "sidebarType", "isDarkMode"]),
  },
};
</script>
