<template>
  <div>    
    <svg>
      <polygon class="item" v-for="(item, index) in items" :key="index" points="200,300 200,350 400,250" fill="tomato"
        @click="click($event)"
      />
    </svg>
  </div>
</template>

<script>
  

  export default {
    name: "app",
    
    data () {
      return {
        
        items: [
          { id: 1, name: 'name01' },
        ],
        methods: {
          click: function(e) {
            console.log("クリックした");
          }
        }
      }
    }
  }
</script>

<style>
  svg {
    height: 1000px;
    width: 1000px;
    background-color: lightgray;
  }
  .item:hover {
    cursor: grab;
  }
  .item:active {
    cursor: grabbing;
  }
</style>