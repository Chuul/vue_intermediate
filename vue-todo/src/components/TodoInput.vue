<template>
  <div class="inputBox shadow">
      <input type="text" v-model="newTodo" v-on:keyup.enter="addTodo">
      <span class="addContainer" v-on:click="addTodo">
        <i class="addBtn fas fa-plus"></i>
      </span>

      <Modal v-if="showModal" @close="showModal = false">
        <h3 slot="header">
          경고!
          <i class="closeModalBtn fas fa-times" v-on:click="showModal = false"></i>
        </h3>
        <div slot="body">무엇이든 입력하세요!</div>
      </Modal>
  </div>
</template>

<script>
import Modal from './common/Modal.vue'

export default {
  data : function(){
    return {
      newTodo : "",
      showModal: false
    }
  },
  methods : {
    addTodo : function(){
      if(this.newTodo !== ""){
        this.$store.commit('addOneItem', this.newTodo)
        // this.$emit('addItem', this.newTodo)
        this.clearText();
      }else{
        this.showModal = !this.showModal;
      }
    },
    clearText : function(){
      this.newTodo = ""
    }
  },
  components : {
      Modal : Modal
  }
}
</script>

<style scoped>
input:focus {
  outline :none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
}
.addContainer {
  float : right;
  background: linear-gradient(to right, #6478FB, #8763FB);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color : white;
  vertical-align: middle;
}
.closeModalBtn {
  color : #42b983;
}
</style>