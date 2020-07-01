<template>
  <div class="tweet d-flex flex-row align-items-start">
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
        <span class="text-muted chevron"
          ><img src="../assets/img/ic-chevron-down.svg" alt="Options"
        /></span>
      </div>
      <div class="tweet-body">
        <span>{{ tweet.text }}</span>
      </div>
      <div class="tweet-actions">
        <a class="action" href="#"
          ><img src="../assets/img/ic-chat.svg" alt="Reply" />
        </a>
        <a class="action" href="#"
          ><img src="../assets/img/ic-arrow-left-right.svg" alt="Retweet"
        /></a>
        <a class="action" href="#"
          ><img src="../assets/img/ic-heart.svg" alt="Like"
        /></a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    tweet: Object,
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
        flex-shrink: 0;
        margin-left: auto;
      }
    }

    .tweet-body {
      margin-top: 8px;
      margin-bottom: 8px;
    }

    .tweet-actions {
      display: flex;
      align-items: center;
      justify-content: space-between;

      a.action {
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
