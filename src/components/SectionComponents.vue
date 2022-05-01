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
    <div v-for="(section, parent_index) in Sections" :key="parent_index">
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
              <div v-if="section.editFlg" @dblclick="changeSectionFlg(parent_index,'start')">
                {{ section.title }}              
              </div>
              <div v-else>
                <v-text-field v-model="editing" @keyup.enter="changeSectionFlg(parent_index,'end')" :value="section.title" ></v-text-field>
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

                <div v-if="task.editTFlg" @dblclick="changeTaskTitleFlg(parent_index,index,'start')">
                  <v-list-item-title class="text-h5 mb-1">
                    {{ task.title }}
                  </v-list-item-title>
                </div>
                <div v-else>
                  <v-text-field v-model="editing" @keyup.enter="changeTaskTitleFlg(parent_index,index,'end')" :value="task.title" ></v-text-field>
                </div>
              </v-card>
              <v-card-subtitle>Section Name : {{ section.title }}</v-card-subtitle>
              <div v-if="task.editCFlg" @dblclick="changeTaskContentsFlg(parent_index,index,'start')">
                <v-card-text>{{ task.contents }}</v-card-text>
              </div>
              <div v-else>
                <v-text-field v-model="editing" @keyup.enter="changeTaskContentsFlg(parent_index,index,'end')" :value="task.contents" ></v-text-field>
              </div>
                <a @click="deleteTodo(index)" class="btn btn-primary mt-2">×</a>
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
        editing:'',
        for_section: 1
      };
    },
    methods:{
      createTodo(){
        if(this.inputSection=="") return ;
        this.for_section += 1 ;
        this.Sections.push({title: this.inputSection, 
                            editFlg:true,
                            tasks:[{
                                editTFlg:true,
                                title:"title",
                                editCFlg:true,
                                contents:"content"
                              }]
                            });

        this.inputSection = '' ;
      },
      changeSectionFlg(i,flg){
        if(flg=="start"){
          this.Sections[i].editFlg = false ;
          this.editing = this.Sections[i].title ;
        }else{
          this.Sections[i].editFlg = true ;
          this.Sections[i].title = this.editing ;
        }
      },
      changeTaskContentsFlg(parent_i,i,flg){
        if(flg=="start"){
          this.Sections[parent_i].tasks[i].editCFlg = false ;
          this.editing = this.Sections[parent_i].tasks[i].contents ;
        }else{
          this.Sections[parent_i].tasks[i].editCFlg = true ;
          this.Sections[parent_i].tasks[i].contents = this.editing ;
        }
      },
      changeTaskTitleFlg(parent_i,i,flg){
        if(flg=="start"){
          this.Sections[parent_i].tasks[i].editTFlg = false ;
          this.editing = this.Sections[parent_i].tasks[i].title ;
        }else{
          this.Sections[parent_i].tasks[i].editTFlg = true ;
          this.Sections[parent_i].tasks[i].title = this.editing ;
        }
      },
    },
  }
</script>
