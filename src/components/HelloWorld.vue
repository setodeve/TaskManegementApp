<template>
  <div>
    <v-row>
      <v-col
        cols="12"
        sm="2"
        md="3"
      >
        <v-text-field filled v-model="inputSection" type="text"></v-text-field>
      </v-col>
      <v-col
        cols="12"
        sm="2"
        md="3"
      >
        <v-btn
          target="_blank"
          text
          @click="createTodo()"
        >
        <span class="mr-2">Add Section</span>
        </v-btn>
      </v-col>
    </v-row>
    <div v-for="(section,key, index) in Sections" :key="key">
      <div class="card w-50 my-1">
        <div class="card-body">
            <h5 class="card-title">Section {{index+1}} : {{ section }}</h5>
            <a @click="deleteTodo(index)" class="btn btn-primary mt-2">Delete</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'HelloWorld',
    data() {
      return{
        inputSection:'',
        Sections :[],
      };
    },
    methods:{
      createTodo(){
        if(this.inputSection=="") return ;
        this.Sections.push(this.inputSection);
        this.inputSection = '' ;
      },
    },
  }
</script>
