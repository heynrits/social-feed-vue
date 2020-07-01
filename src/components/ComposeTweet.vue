<template>
  <div id="composer">
    <img id="avatar" :src="avatar" alt="User Avatar" />
    <div id="main">
      <textarea
        v-model="tweetText"
        name="compose-tweet-body"
        id="compose-tweet-body"
        rows="2"
        maxlength="280"
        placeholder="What's happening"
      ></textarea>
      <div id="actions">
        <button>
          <img
            src="../assets/img/ic-image.svg"
            alt="Attach image"
            class="ic-compose-tweet-advanced"
          />
        </button>
        <button>
          <img
            src="../assets/img/ic-gif.svg"
            alt="Add animated GIF"
            class="ic-compose-tweet-advanced"
          />
        </button>
        <button>
          <img
            src="../assets/img/ic-bar-chart.svg"
            alt="Create poll"
            class="ic-compose-tweet-advanced"
          />
        </button>
        <button>
          <img
            src="../assets/img/ic-calendar-plus.svg"
            alt="Schedule tweet"
            class="ic-compose-tweet-advanced"
          />
        </button>
        <div class="left">
          <span class="character-count">{{ tweetText.length }}/280</span>
          <button
            :disabled="tweetText.length === 0"
            id="btn-submit"
            :class="tweetText.length === 0 ? 'disabled' : ''"
            v-on:click="submitTweet"
            type="button"
          >
            Tweet
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import composerAvatar from '@/assets/img/default_profile.png';

export default {
  props: {
    saveTweet: Function,
  },
  data() {
    return {
      avatar: composerAvatar,
      tweetText: '',
    };
  },
  methods: {
    submitTweet() {
      const now = Date.now();
      const tweet = {
        created_at: new Date(now).toISOString(),
        id: now.toString(),
        text: this.tweetText,
      };

      this.saveTweet(tweet);
      this.tweetText = '';
    },
  },
};
</script>

<style lang="scss" scoped>
#composer {
  display: flex;
  border-bottom: 1px solid #d0d0d0;
  padding-top: 24px;
  padding-bottom: 24px;

  #avatar {
    width: 49px;
    height: 49px;
    border-radius: 100%;

    margin-right: 20px;
  }

  #main {
    flex-grow: 1;

    textarea {
      width: 100%;
      padding-top: 12px;
      padding-bottom: 12px;

      border: none;

      font-family: inherit;
      font-size: 1rem;

      &:focus {
        outline: none;
      }
    }

    #actions {
      /* class="d-flex align-items-center mt-2" */
      display: flex;
      align-items: center;

      margin-top: 16px;

      @media screen and (max-width: 992px) {
        align-items: flex-end;
      }

      button {
        cursor: pointer;
      }

      button {
        /* class="border-0 rounded-circle btn-compose-tweet-advanced" */
        background: transparent;
        border: none;
        border-radius: 100%;

        img {
          width: 23px;
          height: 23px;
        }
      }

      #btn-submit {
        /* class="btn btn-primary py-2 px-3 rounded-pill font-weight-bold send-tweet-btn ml-auto" */
        background: #1da1f2;
        border: none;
        border-radius: 25px;

        padding: 8px 18px;

        font-weight: bold;
        color: #fff;

        &.disabled {
          opacity: 0.5;
          cursor: default;
        }
      }

      .character-count {
        color: #aaa;
        margin-right: 20px;

        @media screen and (max-width: 992px) {
          margin-right: 0;
          margin-bottom: 10px;
        }
      }

      .left {
        display: flex;
        align-items: center;
        margin-left: auto;

        @media screen and (max-width: 992px) {
          flex-direction: column;
          align-items: flex-end;
        }
      }
    }
  }
}
</style>
