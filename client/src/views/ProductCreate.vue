<template>
  <div>
    <h1>This is a product create page</h1>
  </div>
</template>

<script>
export default {
  name: "ProductCreate",
  computed: {
    user() {
      return this.$store.state.user;
    }
  },
  mounted() {
    if(this.user.email == undefined) {
      alert("로그인을 해야 이용할 수 있습니다.");
      this.$router.push({path:'/'});
    }
  }
}
</script>

<style scoped>

</style>