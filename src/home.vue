<template>
  <div class="container">
    <div class="todo">
      <div class="todo__title">Vue3 TodoList</div>
      <div class="todo-search">
        <div class="todo-search-input">
          <input placeholder="请输入" v-model="value" />
        </div>
        <div class="todo-search-btn" @click="add">添加</div>        
      </div>
      <div class="todo-list">
        <div class="todo-list__item" v-for="(item , index) in list" :key="index">
          <div class="todo-list__item-content">{{ item }}</div>
          <div class="todo-list__item-btn" @click="remove(index)">删除</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue'
export default {
  props: {
    user: {
      type: String,
      required: true
    }
  },
  setup(props) {
    onMounted(()=>{
      console.log('onMounted');      
    })
    const msg = ref('组件消息')
    const value = ref('')
    const list = ref(["背单词","去西藏"])
    const remove = (index) => {
      list.value.splice(index,1)
    }
    const add = () => {
      if(!value.value){
        return
      }
      list.value.push(value.value)
      value.value = ""
    }
    return {msg,list,value,add,remove} // 这里返回的任何内容都可以用于组件的其余部分
  }
}

</script>

<style lang="scss">
.container{
  padding: 20px 20px 0;
  box-sizing: border-box;
  .todo{
    &__title{
      margin-bottom: 20px;
      font-weight: bold;
    }
    &-search{
      display: flex;
      align-items: center;
      margin-bottom: 20px;
      &-input{
        margin-right: 10px;
      }
    }
    &-list{
      &__item{
        display: flex;
        margin-bottom: 8px;
        &-content{
          flex: 1;
        }
        &-btn{
          flex: 0 1 50px;
        }
      }
    }
  }
}
</style>