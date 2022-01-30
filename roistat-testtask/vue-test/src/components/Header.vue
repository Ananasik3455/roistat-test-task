<template>
  <header class="nav">
    <div class="nav__logo">
      <img class="nav__img" src="../assets/LOGO.svg" alt="">
    </div>
    <div class="nav__container">
      <button class="nav__button" @click="$emit('open')">Добавить пользователя</button>
    </div>
  </header>
</template>

<script>
export default {
  data () {
    return {
      modalVisible: false
    }
  },
  emits: ['open']
}
</script>

<style>
  .nav {
    max-width: 100%;
    display: flex;
    flex-direction: row;
    padding: 20px;
  }

  .nav__logo {
    display: flex;
    align-content: center;
    width: 10%;
  }

  .nav__img {
    width: 67px;
  }

  .nav__container {
    width: 90%;
    display: -webkit-box;
    justify-content: end;

  }

  .nav__link {
    padding-right: 30px;
    text-decoration: none;
    color: #05574f;
  }

  .nav__button {
    width: 220px;
    border: 2px solid #08786C;
    border-radius: 10px;
    background: #3fbd97;
    text-shadow: 0 1px 1px #2D2020;
    border-spacing: 0;
    transition: all 0.3s ease-in-out;
    color: #FFFFFF;
    text-decoration: none;
    padding: 5px 20px;
    cursor: pointer;
  }

  .nav__button:hover {
    border-color:#05574f;
    background: #0aa394;
    transition: all 0.3s ease-in-out;
  }
</style>
