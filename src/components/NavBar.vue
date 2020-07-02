<template>
  <nav>
    <ul class="container">
      <li>
        <img id="profile-icon" src="../assets/img/default_profile.png" alt="" />
      </li>
      <li id="title">
        <h1><router-link to="/">Home</router-link></h1>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: 'NavBar',
};
</script>

<style lang="scss" scoped>
nav {
  height: 54px;
  box-sizing: border-box;
  position: sticky;
  top: 0;

  background: #fff;
  border-bottom: 1px solid #aaa;

  display: flex;
  align-items: center;

  ul {
    width: 100%;
    margin: 0;
    padding: 0 20px;
    list-style: none;

    &.container {
      max-width: 992px;
      box-sizing: border-box;
      margin-left: auto;
      margin-right: auto;
      display: flex;
      align-items: center;
    }

    li {
      display: flex;
      align-items: center;
    }

    li:not(:last-of-type) {
      margin-right: 12px;
    }

    #profile-icon {
      width: 24px;
      height: 24px;
      border-radius: 100%;
    }

    #title {
      h1 {
        font-size: 1rem;
        font-weight: 900;
      }

      a {
        color: #212121;
      }
    }
  }
}
</style>
