<template>
  <div class="tweet">
    <img
      class="tweet-avatar"
      src="../assets/img/default_profile.png"
      alt="User's Profile"
    />
    <div class="tweet-content">
      <div class="user-info">
        <span class="display-name">
          <span class="name">{{ tweet.user.name }}</span>
          <span class="text-muted username">@{{ tweet.user.username }}</span>
        </span>
        <span class="text-muted dot-separator">&middot;</span>
        <span class="text-muted time">{{ this.getFormattedDate() }}</span>
        <span class="text-muted chevron" v-on:click="toggleMenu">
          <img
            class="ic-chevron"
            src="../assets/img/ic-chevron-down.svg"
            alt="Options"
          />
          <ul
            :class="
              this.showContextualMenu
                ? 'contextual-menu show'
                : 'contextual-menu'
            "
          >
            <li><span v-on:click="() => onEdit(tweet)">Edit</span></li>
            <li><span v-on:click="() => onDelete(tweet.id)">Delete</span></li>
          </ul>
        </span>
      </div>
      <div :class="tweet.recentlyUpdated ? 'tweet-body updated' : 'tweet-body'">
        <span>{{ tweet.text }}</span>
      </div>
      <div class="tweet-actions">
        <span class="action">
          <a href="#">
            <img src="../assets/img/ic-chat.svg" alt="Reply" />
          </a>
        </span>
        <span class="action">
          <a href="#">
            <img src="../assets/img/ic-arrow-left-right.svg" alt="Retweet" />
          </a>
        </span>
        <span class="action">
          <a href="#">
            <img src="../assets/img/ic-heart.svg" alt="Like" />
          </a>
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    tweet: Object,
    onEdit: Function,
    onDelete: Function,
  },
  data() {
    return {
      showContextualMenu: false,
      editTweet: {
        editing: false,
        updatedTweet: '',
      },
    };
  },
  methods: {
    getFormattedDate() {
      return new Date(this.tweet.created_at)
        .toDateString() // 'Sat Jun 27 2020'
        .split(' ') // ['Sat', 'Jun', '27', '2020']
        .slice(1) // ['Jun', '27', '2020']
        .join(', ') // 'Jun, 27, 2020'
        .replace(',', ''); // 'Jun 27, 2020'
    },
    toggleMenu() {
      this.showContextualMenu = !this.showContextualMenu;
    },
  },
};
</script>

<style lang="scss" scoped>
.tweet {
  display: flex;
  padding-top: 1rem;
  padding-bottom: 1rem;
  width: 100%;
  box-sizing: border-box;

  .tweet-avatar {
    flex-shrink: 0;
    width: 49px;
    height: 49px;
    border-radius: 100%;
  }

  .tweet-content {
    width: inherit;
    flex-shrink: 1;
    display: flex;
    flex-direction: column;
    margin-left: 20px;

    .user-info {
      width: 100%;
      display: flex;

      .text-muted {
        color: #aaa;
      }

      .display-name {
        flex-shrink: 1;
        display: flex;
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;

        .name {
          flex-shrink: 1;
          display: inline-block;
          overflow: hidden;
          text-overflow: ellipsis;
          white-space: no-wrap;
          font-weight: bold;
        }

        .username {
          flex-shrink: 1;
          display: inline-block;
          overflow: hidden;
          margin-left: 12px;
          text-overflow: ellipsis;
          white-space: no-wrap;
        }
      }
      .dot-separator {
        flex-shrink: 0;
        margin-left: 8px;
        margin-right: 8px;
      }

      .time {
        flex-shrink: 0;
        margin-right: 12px;
      }

      .chevron {
        cursor: pointer;
        flex-shrink: 0;
        margin-left: auto;
        position: relative;

        .contextual-menu {
          background: #fff;
          box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.25);
          border-radius: 4px;
          margin: 0;
          padding: 0;
          display: none;
          height: 0;
          list-style: none;
          &.show {
            height: initial;
            display: flex;
            flex-direction: column;
            position: absolute;
            right: 0;
          }

          li span {
            cursor: pointer;
            display: block;
            padding: 8px 16px;
            text-decoration: none;
            color: #212121;

            &:hover {
              transition: background-color 0.5s ease;
              background-color: #eee;
            }
          }
        }
      }
    }

    .tweet-body {
      margin-top: 8px;
      margin-bottom: 8px;

      @keyframes updatedTweet {
        0% {
          border-radius: 4px;
          background-color: #bccbff;
        }
        100% {
          background-color: initial;
        }
      }

      &.updated {
        animation-name: updatedTweet;
        animation-duration: 3s;
        animation-timing-function: ease-in-out;
        animation-iteration-count: 1;
      }
    }

    .tweet-actions {
      display: flex;
      align-items: center;
      justify-content: space-between;

      span.action {
        flex: 1;
        text-decoration: none;
        color: #aaa;
        display: flex;
        align-items: center;

        img {
          margin-right: 12px;
          width: 18px;
          height: 18px;
        }
      }
    }
  }
}
</style>
