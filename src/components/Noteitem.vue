<template>
  <div class="notes__item">
    <div class="notes__item-top" :class="{between: !list}">
        <h3 class="notes__item-title">{{ note.title }}</h3>
        <p class="notes__item-date">{{ note.date }}</p>
    </div>
    <p class="notes__item-text">{{ note.descr }}</p>
    <div class="notes__item-btns">
        <button class="notes__item-btn edit" @click="$emit('changeNote', note.id)" >
            <img src="../assets/img/pencil.svg" alt="">
            <span>EDIT</span>
        </button>
        <button class="notes__item-btn trash" @click="$emit('delNote', note.id)">
            <img src="../assets/img/trash.svg" alt="">
            <span>DELETE</span>
        </button>
    </div>
  </div>
</template>

<script>
export default {
    props: {
        list: Boolean,
        note: Object
    }
}
</script>

<style>
.notes__item{
    background: linear-gradient(
        0deg,
        rgba(80, 164, 116, 0.11),
        rgba(80, 164, 116, 0.11) 
    ),
    #fffbfe;
    box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.3), 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
    border-radius: 16px;
    padding: 16px 16px 26px 16px;
}
.notes__item-title{
    font-family: 'RM';
    color: #1C1B1F;
    font-size: 16px;
    line-height: 24px;
    
}
.notes__item-date{
    font-size: 14px;
    line-height: 20px;
    letter-spacing: 0.25px;
    color: #cfa02b;
    margin-bottom: 16px;
}
.notes__item-text{
    font-size: 16px;
    line-height: 20px;
    letter-spacing: 0.25px;
    color: #49454f;
    margin-bottom: 30px;
}
.notes__item-btns{
    display: flex;
    justify-content: flex-end;
}
.notes__item-btn{
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 12px;
    border-radius: 5px;
}
.notes__item-btn span{
    font-family: 'RM';
    font-size: 14px;
    line-height: 20px;
}
.edit{
    color: #1C1B1F;
    transition: .4s;
}
.edit:hover{
      background: #cfa02b;
}
.trash{
    color: #CF1B1B;
}
.trash:hover{
    background: #bda6a6;
}
.notes__item-top.between{
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 20px;
}
.notes__item-top.between .notes__item-date{
    margin-bottom: 0;
}
.notes__item-top.between .notes__item-text{
    margin-bottom: 0;
}
</style>