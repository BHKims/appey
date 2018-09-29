<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <br>
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <h2>Todos</h2>
    <br>
    <input @keyup.enter="submit" type="text" placeholder="What needs to be Done?" v-model="newItem.title">
    <ul>
      <li class="listitem" v-bind:item="item" v-for="(item, index) in items" >
          <input  type="checkbox" v-model="item.bool">
          <span >{{item.title}} - {{item.bool}}</span>
          <button v-if="item.bool" @click="deleteItem(index)">X</button>
      </li>
      <li>
        <span>{{items.length}} items left</span>
        <span class="tab">
          <button class="tabitem" @click="displayAll">All</button>
          <button class="tabitem" @click="displayActive">Active</button>
          <button class="tabitem" @click="displayComplete">Completed</button>
        </span>
      </li>
    </ul>



  </div>
</template>

<script lang="ts">

// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  data() {
    return {
      itemList:[],
      checkedItems:[],
      newItem: {
        title:'',
        bool:false
      },
      displayState: 'All',
      displayingItems: []
    }
  },
  created() {
    this.itemList;
    console.log("displayingItems: ", this.$data.displayingItems);
  },
  mounted() {
    this.itemList;
    console.log("displayingItems: ", this.$data.displayingItems);
  },

  watch: {
    
  },
  computed: {
    items: function() {
      var arr=[];
      if(this.$data.displayState == 'All'){
        arr = this.$data.itemList;
        return arr;
      } else if(this.$data.displayState == 'Active'){
        arr = this.$data.itemList.filter(x => x.bool == false);
        return arr;
      } else if(this.$data.displayState == 'Complete') {
        arr = this.$data.itemList.filter(x => x.bool == true);
        return arr;
      } else {
        console.error('displayState is not one of intended State!');
        return arr;
      }
      
    }
  },

  methods: {
  //   displayWhat(index){
  //    if(this.$data.displayState == 'All'){
  //      return true;
  //    } else if(this.$data.displayState == 'Active'){
  //       return !this.$data.itemList[index].bool;
  //    } else if(this.$data.displayState == 'Complete'){
  //      return this.$data.itemList[index].bool;
  //    } else {
  //      console.error('displayState is not one of intended State!');
  //    }
  //  },

   
    submit() {
      if(this.$data.newItem.title){
        this.$data.itemList.push(this.$data.newItem);
        this.$data.newItem = {title:'', bool:false};
      }
    },

    deleteItem(index) {
      this.$data.itemList.splice(index, 1);
    },

    displayAll(){
      this.$data.displayState = 'All';
    },
    displayActive() {
      this.$data.displayState = 'Active';
    },
    displayComplete(){
      this.$data.displayState = 'Complete';
    }
  }
}

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.listitem {
  
  left: 20px;
}
</style>
