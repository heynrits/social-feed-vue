<template>
  <div id="composer">
    <img id="avatar" :src="avatar" alt="User Avatar" />
    <div id="main">
      <textarea
        name="compose-tweet-body"
        id="compose-tweet-body"
        rows="2"
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
        <button type="button">Tweet</button>
      </div>
    </div>
  </div>
</template>

<script>
import composerAvatar from '@/assets/img/default_profile.png';

export default {
  data() {
    return {
      avatar: composerAvatar,
    };
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

      button {
        cursor: pointer;
      }

      button:not(:last-of-type) {
        /* class="border-0 rounded-circle btn-compose-tweet-advanced" */
        background: transparent;
        border: none;
        border-radius: 100%;

        img {
          width: 23px;
          height: 23px;
        }
      }

      button:last-of-type {
        /* class="btn btn-primary py-2 px-3 rounded-pill font-weight-bold send-tweet-btn ml-auto" */
        background: #1da1f2;
        border: none;
        border-radius: 25px;

        padding: 8px 18px;
        margin-left: auto;

        font-weight: bold;
        color: #fff;
      }
    }
  }
}
</style>
