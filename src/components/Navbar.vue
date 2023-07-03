<template>
  <header class="header">
    <Transition name="header__change" mode="out-in">
      <div class="header__main" v-if="header">
      <button class="header__lang" @click="changeLang" v-if="lang == 'uz'">RU</button>
      <button class="header__lang" @click="changeLang" v-else>UZ</button>
      <h1 class="header__title">{{ words.appbartitle[lang] }}</h1>
      <button class="header__search" @click="header = false">
        <img src="../assets/img/search.svg" alt="searchIcon" />
      </button>
      </div>
      <div class="header__form" v-else>
      <button class="header__back" @click="header = true, search = ''">
          <img src="../assets/img/back.svg" alt="back">
      </button>
      <input type="text" placeholder="Поиск..." v-model="search">
      <button class="header__reset" @click="search = ''">
          <img src="../assets/img/reset.svg" alt="reset">
      </button>
      </div>
    </Transition>
  </header>
</template>
<script>
export default {
  props: ['lang'],
  inject: ['words'],
  data(){
    return {
      header: true,
      search: ''
    }
  },
  methods: {
    changeLang(){
      this.$emit('changeLang', this.lang == 'ru' ? 'uz' : 'ru')
    }
  },
  watch: {
    search(val){
      this.$emit('find', val)
    }
  }
};
</script>
<style lang="scss">
.header {
  background: #f3edf7;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25), 0px 1px 3px rgba(0, 0, 0, 0.3);
  padding: 18px 20px;
  height: 64px;
  &__main, &__form{
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  &__lang, &__search, &__back, &__reset{
    background: transparent;
    font-size: 20px;
    color: black;
    border: none;
    outline: none;
    cursor: pointer;
    font-weight: 700;
  }
  &__title {
    font-weight: 400;
    font-size: 22px;
  }
  input{
    width: 80%;
    display: block;
    background: transparent;
    outline: none;
    border: none;
    font-size: 16px;
  }
}
.header__change-enter-active,
.header__change-leave-active {
  transition: 0.3s linear;
}
.header__change-enter-from,
.header__change-leave-to {
  opacity: 0;
}

</style>