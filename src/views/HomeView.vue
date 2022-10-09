<template>
  <div class="home bg-dark">
    <div class="card bg-dark border-0 text-center">
      <img src="../assets/logo.png" class="card-img-top logo" alt="logo">
      <div class="card-body">
        <router-link to="/board" class="btn btn-primary">New sketch</router-link>
        <router-link to="" class="btn btn-primary">Open sketch</router-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HomeView',
};
</script>

<style lang="scss" scoped>
.home {
  width: 100vw;
  height: 100vh;
  max-width: 100vw;
  max-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  .card {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 50px;
    .logo {
      width: 100px;
    }
    .card-body {
      display: flex;
      flex-direction: column;
      gap: 10px;
      justify-content: center;
      align-items: center;
    }
  }
}
</style>