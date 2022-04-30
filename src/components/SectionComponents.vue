<template>
  <div>
    <v-row>
      <v-col
        cols="12"
        sm="3"
        md="3"
        dense
        class="ma-1"
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
          class="mt-3"
          elevation="2"
          depressed
          @click="createTodo()"
        >
        <span class="mr-2">Add Section</span>
        </v-btn>
      </v-col>
    </v-row>
    <div v-for="(section, index) in Sections" :key="index">
      <v-card
        max-width="200"
        outlined
        elevation="2"
      >
        <v-list-item three-line>
          <v-list-item-content>
            <v-card
            outlined
            class="mb-2"
            elevation="1"
            >
              <div v-if="section.editFlg" @dblclick="changeFlg(index)">
                {{ section.title }}              
              </div>
              <div v-else>
                <v-text-field v-model="editing" @keyup.enter="saveSection(index)" :value="section.title" ></v-text-field>
              </div>
              </v-card>
              <v-card
              max-width="150"
              outlined
              class="mb-2"
              elevation="1"
              v-for="(task, index) in section.tasks" :key="index" 
              >
              <TaskComponents/>

              <v-card
                outlined
                class="mb-2"
                elevation="1"
              >
                <v-list-item-title class="text-h5 mb-1">
                  {{ task }}
                </v-list-item-title>
              </v-card>
              <v-card
                outlined
                class="mb-2"
                elevation="1"
              >
                <v-card-subtitle>Section Name : {{ section.title }}</v-card-subtitle>
                <a @click="deleteTodo(index)" class="btn btn-primary mt-2">×</a>
              </v-card>
            </v-card>
          </v-list-item-content>
        <TaskNewComponents/>
        </v-list-item>
      </v-card>

    </div>
  </div>
</template>

<script>

import TaskComponents from './TaskComponents';
import TaskNewComponents from './TaskNewComponents';
  export default {
    name: 'SectionComponents',
    components: {
      TaskComponents,TaskNewComponents
    },
    data() {
      return{
        inputSection:'',
        Sections :[],
        editing:''
      };
    },
    methods:{
      createTodo(){
        if(this.inputSection=="") return ;
        this.Sections.push({title: this.inputSection, editFlg:true,tasks:[""]});
        this.inputSection = '' ;
      },
      changeFlg(i){
        this.Sections[i].editFlg = false ;
        this.editing = this.Sections[i].title ;
      },
      saveSection(i){
        this.Sections[i].editFlg = true ;
        this.Sections[i].title = this.editing ;
      }
    },
  }
</script>
