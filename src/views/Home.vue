<template>
  <div class="home">
    <!-- Modals -->
    <EditTweetModal
      v-if="editTweet.editing"
      :tweet="editTweet.tweet"
      :onCancelEditClick="onCancelEditClick"
      :onSaveEditClick="onSaveEditClick"
    />
    <DeleteTweetModal
      v-if="deleteTweet.deleting"
      :tweetId="this.deleteTweet.id"
      :onCancelDeleteClick="onCancelDeleteClick"
      :onConfirmDeleteClick="onConfirmDeleteClick"
    />

    <NavBar />
    <main class="container">
      <ComposeTweet :saveTweet="this.saveTweet" />
      <div id="main-feed">
        <Tweet
          v-for="tweet in this.tweets"
          :key="tweet.id.toString()"
          v-bind:tweet="{ user, ...tweet }"
          :onEdit="onEditClick"
          :onDelete="onDeleteClick"
        />
      </div>
    </main>
  </div>
</template>

<script>
// @ is an alias to /src
import NavBar from '@/components/NavBar.vue';
import ComposeTweet from '@/components/ComposeTweet.vue';
import EditTweetModal from '@/components/EditTweetModal.vue';
import DeleteTweetModal from '@/components/DeleteTweetModal.vue';
import Tweet from '@/components/Tweet.vue';

import data from '../data/tweets.json';

export default {
  name: 'Home',
  components: {
    NavBar,
    ComposeTweet,
    Tweet,
    EditTweetModal,
    DeleteTweetModal,
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
      deleteTweet: {
        deleting: false,
        id: '',
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

    onDeleteClick(tweetId) {
      this.deleteTweet = {
        deleting: true,
        id: tweetId,
      };
    },

    onCancelDeleteClick() {
      this.deleteTweet = {
        deleting: false,
        id: '',
      };
    },

    onConfirmDeleteClick(tweetId) {
      this.tweets = this.tweets.filter((t) => t.id !== tweetId);

      this.onCancelDeleteClick();
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
