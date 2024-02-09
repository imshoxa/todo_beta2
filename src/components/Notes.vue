<template>
  <div class="notes" >
    <div class="container">
        <div class="notes__top">
            <h2 class="notes__title">
                {{ notes.length > 0 ? 'All To-Dos' : 'No notes'}}
            </h2>
            <button class="notes__btn" @click="list = !list">
                <img v-if="list" src="../assets/img/menu.svg" alt="" />
                <img v-else src="../assets/img/setka.svg" alt="">
                <span>{{ list ? 'List' : 'Grid' }}</span>
            </button>
        </div>
        <div class="notes__list" :class="{active: !list}">
            <Noteitem 
            :list="list"
            v-for="note in notes" 
            :key="note.id"
            :note="note"
            @delNote="$emit('delNote', note.id)"
            @changeNote="$emit('changeNote', note.id)"
            />
        </div>
    </div>
  </div>
</template>

<script>


import Noteitem from '@/components/Noteitem.vue';
export default {
    components: {
        Noteitem
    },
    data(){
        return{
            list: true
        }
    },
    inject:['words'],
    props: {
        notes:{
            lang: String,
            typeof: Array,
            required: true
        }
    },
};
</script>

<style>
.notes{
    margin-top: 30px;
}
.notes__top{
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.notes__title{
    font-size: 22px;
    line-height: 28px;
    color: #323232;
}
.notes__btn{
    background: linear-gradient(
        0deg,
        rgba(80, 164, 116, 0.11),
        rgba(80, 164, 116, 0.11) 
    ),
    #fffbfe;
    box-shadow: 0px 4px 8px 3px rgba(0, 0, 0, 0.15),
    0px 1px 3px rgba(0, 0, 0, 0.3);
    border-radius: 16px;
    width: 120px;
    height: 56px;
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 15px;
}
.notes__btn span{
    font-family: 'RM';
    font-size: 14px;
    line-height: 20px;
    color: #323232;
}
.notes__list{
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 24px;
    margin-top: 40px;
}
.notes__list.active{
    grid-template-columns: 1fr;
}
</style>