<template>
  <header class="header">
    <Transition name="header__notes">
    <div class="header__nots" v-show="header === true">
        <button @click="changeLang" class="header__lang" v-if="lang == 'en'">RU</button>
        <button @click="changeLang" class="header__lang" v-else>EN</button>
        <h1 class="header__title"> To-Dos </h1>
        <button class="header__search" @click="header = false">
            <img src="@/assets/img/search.svg" alt=""  />
        </button>
    </div>
    </Transition>
    <Transition name="header__forms">
    <div class="header__form" v-show="header === false">
        <button class="header__back" @click="header = true">
            <img src="@/assets/img/back.svg" alt=""  />
        </button>
        <input 
        type="text" 
        class="header__input" 
        placeholder="Search.." 
        v-model="search" 
        />
        <button class="header__close" @click="search = '' ">
            <img src="@/assets/img/quit.svg" alt=""  />
        </button>
    </div>
    </Transition>
  </header>
</template>

<script>
export default {
    data(){
        return{
            header: true,
            search: ''
        };
    },
    inject:['words'],
    props: ['lang'],
    watch:{
        search(val){
            this.$emit('searchValue', val)
        },
    },
    methods:{
        changeLang(){
            this.$emit('changeLang', this.lang == 'en' ? 'ru' : 'en')
        }
    }
};
</script>

<style>
.header{
    background: #edf7ee;
    box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25), 0px 1px 3px rgba(0, 0, 0, 0.3);
    padding: 18px 20px;
    height: 70px;
    overflow: hidden;
}
.header__nots,
.header__form{
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.header__lang{
    font-size: 20px;
    font-weight: bold;
}
button{
    border: none;
    background: none;
    cursor: pointer;
}
.header__title{
    font-size: 22px;
    line-height: 28px;
    color: #1C1B1F;
}
.header__input{
    display: block;
    width: 90%;
    background: transparent;
    outline: none;
    border: none;
    font-size: 16px;
    line-height: 20px;
    color: #9D9D9D;
}

.header__notes-enter-active,
.header__notes-leave-active {
  transition: .5s linear;
}

.header__notes-enter-from,
.header__notes-leave-to {
  opacity: 0;
  transform: translateY(-200px);
}
.header__notes-enter-to,
.header__notes-leave-from {
  opacity: 1;
  transform: translateY(0px);
}
.header__forms-enter-active,
.header__forms-leave-active {
  transition: .5s linear;
}

.header__forms-enter-from,
.header__forms-leave-to {
  opacity: 0;
  transform: translateY(200px);
}
.header__forms-enter-to,
.header__forms-leave-from {
  opacity: 1;
  transform: translateY(0px);
}
</style>