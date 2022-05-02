<template>
  <div>
      <a @click="NewTask()" class="btn btn-primary mt-2"><font-awesome-icon :icon="['fa', 'plus']" /></a>
  </div>
</template>

<script>
  export default {
    props: ["parent_index"],
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
