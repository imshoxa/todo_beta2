<template>
  <button class="add__btn" @click="$emit('openModel')">
    <img src="../assets/img/pencil.svg" alt="">
  </button>
</template>

<script>
export default {

}
</script>

<style>
.add__btn{
    background: linear-gradient(
        0deg,
        rgba(80, 164, 116, 0.11),
        rgba(80, 164, 116, 0.11) 
    ),
    #fffbfe;
    box-shadow: 0px 4px 8px 3px rgba(0, 0, 0, 0.15),
    0px 1px 3px rgba(0, 0, 0, 0.3);
    border-radius: 16px;
    width: 56px;
    height: 56px;
    position: fixed;
    right: 30px;
    bottom: 30px;
}
</style>