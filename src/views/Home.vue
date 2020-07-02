<template>
  <div class="home">
    <!-- Modals -->
    <div v-if="editTweet.editing">
      <EditTweetModal
        :tweet="editTweet.tweet"
        :onCancelEditClick="onCancelEditClick"
        :onSaveEditClick="onSaveEditClick"
      />
    </div>

    <NavBar />
    <main class="container">
      <ComposeTweet :saveTweet="this.saveTweet" />
      <div>
        <div v-for="tweet in this.tweets" :key="tweet.id.toString()">
          <Tweet v-bind:tweet="{ user, ...tweet }" :onEdit="onEditClick" />
        </div>
      </div>
    </main>
  </div>
</template>

<script>
// @ is an alias to /src
import NavBar from '@/components/NavBar.vue';
import ComposeTweet from '@/components/ComposeTweet.vue';
import EditTweetModal from '@/components/EditTweetModal.vue';
import Tweet from '@/components/Tweet.vue';

import data from '../data/tweets.json';

export default {
  name: 'Home',
  components: {
    NavBar,
    ComposeTweet,
    Tweet,
    EditTweetModal,
  },
  data() {
    return {
      user: {
        name: 'John Doe',
        username: 'jdoe',
      },
      tweets: data.tweets,
      editTweet: {
        editing: false,
        tweet: {},
        updatedTweet: '',
        recentlyUpdatedId: '',
      },
    };
  },

  updated() {
    // Remove recently updated status
    // to allow succeeding updates
    // to have the updated animation indicators as well
    if (this.recentlyUpdatedId) {
      setTimeout(() => {
        this.tweets = this.tweets.map((t) => {
          if (t.id === this.recentlyUpdatedId) {
            this.recentlyUpdatedId = '';
            return { ...t, recentlyUpdated: undefined };
          }
          return t;
        });
      }, 3000);
    }
  },

  methods: {
    saveTweet(tweet) {
      this.tweets = [tweet, ...this.tweets];
    },

    onEditClick(tweet) {
      this.editTweet = {
        editing: true,
        tweet,
        updatedTweet: tweet.text,
      };
    },

    onCancelEditClick() {
      this.editTweet = {
        editing: false,
        tweet: {},
        updatedTweet: '',
      };
    },

    onSaveEditClick(updatedTweet) {
      this.tweets = this.tweets.map((t) => {
        if (t.id === updatedTweet.id) {
          this.recentlyUpdatedId = t.id;
          return { ...updatedTweet, recentlyUpdated: true };
        }

        return t;
      });

      this.onCancelEditClick();
    },
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
