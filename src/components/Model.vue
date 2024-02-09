<template>
    <Transition name="model">
        <div class="model" @click="closeModel"> 
    <div class="model__block" @click.stop="">
        <h2 class="model__title">
            {{ edit ? 'Edit note' : 'Add a note' }}
        </h2>
        <div class="model__inputs">
            <label>
                <span>Title</span>
                <input type="text" v-model="title">
            </label>
            <label>
                <span>Content</span>
                <textarea v-model="descr"></textarea>
            </label>
        </div>
        <div class="model__btns">
            <button class="model__btn cancel" @click="closeModel">Cancel</button>
            <button class="model__btn add" @click="addNote" v-if="!edit">Add</button>
            <button class="model__btn add" @click="changeNote" v-else>Edit</button>
        </div>
    </div>
  </div>
    </Transition>
</template>

<script>
export default {
    data(){
        return{
            title: '',
            descr: '',
            id: this.currentId
        }
    },
    props:{
        currentId: Number,
        edit: Boolean,
        editNote: Object
    },
    methods:{
        closeModel(){
            this.$emit('closeModel', false)
            this.title = ''
            this.descr = ''
        },
        addNote(){
            if(this.title !='' && this.descr !=''){
                const item = {
                id: this.id++,
                title: this.title,
                descr: this.descr,
                date: new Date().toLocaleDateString()
            }
            this.$emit('addNote', item)
            // this.$emit('close', false)
            this.title = '',
            this.descr = ''
            }
        },
        changeNote(){
            if(this.title !='' && this.descr !=''){
                const editNotes = {
                    id: this.editNote.id,
                    title: this.title,
                    descr: this.descr,
                    date: new Date().toLocaleString()
                }
                this.$emit('editedNote', editNotes)
                this.closeModel()
            }
        }
    }
}
</script>

<style>
.model{
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.35);
    z-index: 999;
    display: flex;
    justify-content: center;
    align-items: center;
}
.model__block{
    background: linear-gradient(
        0deg,
        rgba(80, 164, 116, 0.11),
        rgba(80, 164, 116, 0.11) 
    ),
    #fffbfe;
    border-radius: 28px;
    max-width: 312px;
    width: 100%;
    padding: 24px;
}
.model__title{
    color: #1C1B1F;
    font-size: 24px;
    line-height: 32px;
    margin-bottom: 16px;
}
.model__inputs{
    display: flex;
    flex-direction: column;
    gap: 16px;
}
.model__inputs label{
    position: relative;
}
.model__inputs span{
    position: absolute;
    top: 8px;
    left: 16px;
    font-size: 12px;
    line-height: 16px;
    color: #69a450;
}
.model__inputs input,
.model__inputs textarea{
    background: #e0ece0;
    border-radius: 4px 4px 0px 0px;
    width: 100%;
    border: none;
    outline: none;
    resize: none;
    padding: 23px 0px 9px 16px;
    height: 56px;
    overflow: hidden;
    font-size: 16px;
    line-height: 24px;
    color: #4f4945;
    border-bottom: 1px solid #1C1B1F;
}
.model__btns{
    display: flex;
    justify-content: flex-end;
    gap: 8px;
    margin-top: 24px;

}
.model__btn{
    font-family: 'RM';
    font-size: 14px;
    line-height: 20px;
    letter-spacing: 0.1px;
    text-transform: uppercase;
    padding: 10px 12px;
    transition: background .5s;
}
.cancel{
    color: #CF1b1B;
}
.cancel:hover{
    /* transition: .4s; */
    background: #bda6a6;
}
.add{
    color: black;
}
.add:hover{
    background: #cfa02b;
    /* transition: .4s; */
}


.model-enter-active,
.model-leave-active {
  transition: .2s linear;
}

.model-enter-from,
.model-leave-to {
  opacity: 0;
  transform: scale(1.5);
}
</style>