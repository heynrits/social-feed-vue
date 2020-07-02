<template>
  <div
    class="overlay"
    v-on:click="
      e => {
        // Close modal if click target is the overlay element
        if (e.target === e.currentTarget) {
          onCancelEditClick();
        }
      }
    "
  >
    <div class="edit-tweet-modal">
      <div class="modal-header">
        <span class="title">Edit Tweet</span>
        <button v-on:click="onCancelEditClick">&times;</button>
      </div>
      <div class="modal-body">
        <textarea
          name="updatedText"
          id="updatedText"
          rows="4"
          v-model="updatedText"
          maxlength="280"
          placeholder="Edit tweet"
        ></textarea>
      </div>
      <div class="modal-footer">
        <span class="character-count">{{ updatedText.length }}/280</span>
        <button
          :class="updatedText.length === 0 ? 'disabled' : ''"
          v-on:click="updateTweet"
        >
          Save
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    tweet: Object,
    onCancelEditClick: Function,
    onSaveEditClick: Function,
  },
  data() {
    return {
      updatedText: this.tweet.text,
    };
  },
  methods: {
    updateTweet() {
      const updatedTweet = {
        ...this.tweet,
        text: this.updatedText,
      };

      this.onSaveEditClick(updatedTweet);
    },
  },
};
</script>

<style lang="scss" scoped>
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 100;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;

  .edit-tweet-modal {
    border-radius: 4px;
    display: flex;
    flex-direction: column;
    margin-top: 40px;
    @media screen and (max-width: 992px) {
      margin-top: initial;
      position: absolute;
      bottom: 0;
    }
    width: 100%;
    max-width: 600px;
    background-color: #fff;
    height: fit-content;

    .modal-header {
      padding: 24px 24px 12px 24px;
      display: flex;
      align-items: center;
      justify-content: space-between;

      .title {
        font-weight: bold;
      }

      button {
        border: none;
        background-color: transparent;
        font-size: 1.5rem;
        font-weight: bold;
      }
    }

    .modal-body {
      padding: 12px 24px 12px 24px;
      flex-grow: 1;

      textarea {
        padding: 8px;
        font-size: 1.125rem;
        box-sizing: border-box;
        width: 100%;
        height: 100%;
        border: 2px solid #ccc;
        border-radius: 4px;
        background-color: #fff;
        /* box-shadow: inset 0px 2px 4px rgba(0, 0, 0, 0.16); */

        &:focus {
          outline-color: #1da1f2;
        }
      }
    }

    .modal-footer {
      padding: 0px 24px 24px 24px;
      display: flex;
      align-items: center;
      justify-content: flex-end;

      span.character-count {
        color: #aaa;
        margin-right: 10px;
      }

      button {
        cursor: pointer;
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
    }
  }
}
</style>
