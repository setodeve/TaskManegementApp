<template>
  <div>
    <v-row>
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
    <v-container>
      <draggable  class="d-flex align-start">
        <div v-for="(section, parent_index) in Sections" :key="parent_index">
          <v-card
            max-width="200"
            outlined
            class="pa-3 ma-2"
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

                  <TaskComponents :section='section' :parent_index="parent_index" />
              </v-list-item-content>

            </v-list-item>
            <TaskNewComponents :parent_index="parent_index" @AddTodo="AddTodo"/>
          </v-card>
        </div>
      </draggable>
    </v-container>
  </div>
</template>

<script>

import TaskComponents from './TaskComponents';
import TaskNewComponents from './TaskNewComponents';
import draggable from 'vuedraggable'
  export default {
    name: 'SectionComponents',
    components: {
      TaskComponents,TaskNewComponents,draggable
    },
    data() {
      return{
        Sections :[],
        editing:''
      };
    },
    methods:{
      createTodo(){
        
        this.Sections.push({title: "Section Title", 
                            editFlg:true,
                            tasks:[{
                                favo:false,
                                complete:false,
                                editTFlg:true,
                                title:"title",
                                editCFlg:true,
                                contents:"content"
                              }]
                            });

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
      AddTodo(i){
        this.Sections[i].tasks.push({
                                    favo:false,
                                    complete:false,
                                    editTFlg:true,
                                    title:"title",
                                    editCFlg:true,
                                    contents:"content"
                              });
      },
    },
  }
</script>
