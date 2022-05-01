<template>
  <div>
      <a @click="NewTask()" class="btn btn-primary mt-2">＋</a>
  </div>
</template>

<script>
  export default {
    props: ["Sections", "parent_index"],
    name: 'TaskNewComponents',
    data() {
      return{

      };
    },
    methods:{
      NewTask(){
        this.$emit('AddTodo',this.parent_index)
      }
    }
  }
</script>
