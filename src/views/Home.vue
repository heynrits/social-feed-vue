<template>
  <div class="home">
    <NavBar />
    <main class="container">
      <ComposeTweet />
    </main>
  </div>
</template>

<script>
// @ is an alias to /src
import NavBar from '@/components/NavBar.vue';
import ComposeTweet from '@/components/ComposeTweet.vue';

export default {
  name: 'Home',
  components: {
    NavBar,
    ComposeTweet,
  },
};
</script>

<style lang="scss" scoped>
.container {
  max-width: 992px;
  box-sizing: border-box;
  margin-left: auto;
  margin-right: auto;
  padding-left: 56px;
  padding-right: 56px;
}
</style>
