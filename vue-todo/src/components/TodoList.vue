<template>
  <transition-group name="list" tag="p">
    <li v-for="(todoItem,index) in this.storedTodoItems" v-bind:key="todoItem.item">
    <i class="checkBtn fas fa-check" v-on:click="checkTodo({todoItem,index})" v-bind:class="{checkBtnCompleted : todoItem.completed}"></i>
    <span v-bind:class="{textCompleted : todoItem.completed}">{{ todoItem.item }}</span>
    <span class="removeBtn" v-on:click="removeTodo({todoItem,index})">
        <i class="far fa-trash-alt"></i>
    </span>
    </li>
  </transition-group>
</template>

<script>
import { mapGetters, mapMutations } from 'vuex'

export default {
    methods : {
        ...mapMutations({
            removeTodo : 'removeOneItem', 
            checkTodo : 'checkOneItem'
            //!!인자는 따로 안 넘겨줘도 된다!! 
            // 다만, vuex를 쓸 때는 template단에서 인자를 두 개 보내주고, store.js에 보낼 때는 하나로 묶었으므로 헬퍼 쓸 때는 template인자를 하나로 묶어줘야한다.
        }),
        // removeTodo : function(todoItem, index){

        //     this.$store.commit('removeOneItem', {todoItem, index})
        //     // this.$emit('removeItem', todoItem, index);
        // },
        // checkTodo : function(todoItem, index){
        //     this.$store.commit('checkOneItem', {todoItem, index})
        //     // this.$emit('checkItem', todoItem, index)
        // }
    },
    computed : {
       ...mapGetters(['storedTodoItems'])
    }
}
</script>

<style scoped>
ul {
    list-style-type: none;
    padding-left: 0px;
    margin-top: 0;
    text-align: left;
}
li {
    display: flex;
    min-height: 50px;
    height: 50px;
    line-height: 50px;
    margin: 0.5rem 0;
    padding: 0 0.9rem;
    background: white;
    border-radius: 5px;
}
.checkBtn {
    line-height: 45px;
    color : #62acde;
    margin-right: 5px;
}
.checkBtnCompleted {
    color : #b3adad;
}
.textCompleted {
    text-decoration: line-through;
    color : #b3adad;
}
.removeBtn {
    margin-left: auto;
    color : #de4343;
}

.list-enter-active, .list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}
</style>