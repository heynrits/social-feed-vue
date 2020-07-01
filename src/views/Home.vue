<template>
  <div class="home">
    <NavBar />
    <main class="container">
      <ComposeTweet />
      <div>
        <div v-for="tweet in this.tweets" :key="tweet.id.toString()">
          <Tweet v-bind:tweet="{ user, ...tweet }" />
        </div>
      </div>
    </main>
  </div>
</template>

<script>
// @ is an alias to /src
import NavBar from '@/components/NavBar.vue';
import ComposeTweet from '@/components/ComposeTweet.vue';
import Tweet from '@/components/Tweet.vue';

import data from '../data/tweets.json';

export default {
  name: 'Home',
  components: {
    NavBar,
    ComposeTweet,
    Tweet,
  },
  data() {
    return {
      user: {
        name: 'John Doe',
        username: 'jdoe',
      },
      tweets: data.tweets,
    };
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

  @media screen and (max-width: 992px) {
    padding: 16px;
  }
}
</style>
