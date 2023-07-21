<script>
import AppNav from "./AppNav.vue";
export default {
  components: {
    AppNav,
  },
};
</script>

<template>
  <header class="fixed-top container-fluid">
    <div class="row row-cols row-cols-md row-cols-sm">
      <div class="contents d-flex justify-content-between px-4 z-1">
        <div class="logo d-flex">
          <router-link
            class="logo d-flex text-decoration-none"
            :to="{ name: 'home' }"
          >
            <img src="../../public/favicon-32x32.png" alt="logo-nav" />
            <div class="text-center text-light fs-4 pt-3 fw-bold logo_text">
              MIXTALES
            </div>
          </router-link>
        </div>

        <AppNav />
      </div>
    </div>
  </header>
</template>

<style lang="scss" scoped>
$primary-color: #da00ff;

header {
  height: 4.5rem;
  img {
    height: 2.5rem;
    position: relative;
    top: 12px;
    margin-right: 5px;
  }
  .logo_text {
    color: $primary-color !important;
  }
}
</style>
