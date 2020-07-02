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
      <div class="attached-image" v-if="tweetImage.data">
        <img
          class="tweetImage"
          :src="tweetImage.data"
          :alt="tweetImage.altText"
        />
        <button class="btn-remove-img" v-on:click="removeImageAttachment">
          &times;
        </button>
      </div>
      <div id="actions">
        <input
          type="file"
          name="image-attachment"
          id="image-attachment"
          accept="image/png,image/jpeg,image/gif"
          v-on:input="previewImage"
        />
        <button>
          <img
            src="../assets/img/ic-image.svg"
            alt="Attach image"
            class="ic-compose-tweet-advanced"
            v-on:click="attachImageBtnClick"
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
            :disabled="tweetText.length === 0 && tweetImage.data === ''"
            id="btn-submit"
            :class="
              tweetText.length === 0 && tweetImage.data === '' ? 'disabled' : ''
            "
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
      tweetImage: {
        data: '',
        altText: '',
      },
    };
  },
  methods: {
    submitTweet() {
      const now = Date.now();
      const tweet = {
        created_at: new Date(now).toISOString(),
        id: now.toString(),
        text: this.tweetText,
        image: { ...this.tweetImage },
      };

      this.saveTweet(tweet);
      this.tweetText = '';
      this.tweetImage.data = '';
      this.tweetImage.altText = '';
    },
    attachImageBtnClick() {
      const imgInput = document.getElementById('image-attachment');
      imgInput.click();
    },
    previewImage(e) {
      const file = e.target.files[0];

      const reader = new FileReader();
      reader.onload = () => {
        this.tweetImage.data = reader.result;
        this.tweetImage.altText = file.name;
      };
      reader.readAsDataURL(file);
    },
    removeImageAttachment() {
      this.tweetImage.data = '';
      this.tweetImage.altText = '';
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

    .attached-image {
      display: inline-block;
      position: relative;

      .tweetImage {
        width: 100px;
        height: 100px;
        border: 2px solid #aaa;
        border-radius: 8px;
        box-shadow: 0px 0px 4px rgba(0, 0, 0, 0.25);
        object-fit: cover;
        object-position: center;
      }
      .btn-remove-img {
        cursor: pointer;
        position: absolute;
        top: -5px;
        right: -5px;
        width: 20px;
        height: 20px;
        border-radius: 50%;
        border: 0;
        background: red;
        color: #fff;

        &:hover {
          opacity: 0.5;
        }
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

      input#image-attachment {
        display: none;
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
