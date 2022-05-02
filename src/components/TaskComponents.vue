<template>
  <div>
    <v-card
    max-width="150"
    outlined
    class="mb-2"
    elevation="1"
    v-for="(task, index) in section.tasks" :key="index" 
    >
      <v-card
        outlined
        class="mb-2"
        elevation="1"
      >
        <div v-if="task.editTFlg" @dblclick="changeTaskTitleFlg(section,index,'start')">
          <v-list-item-title class="text-h5 mb-1">
            {{ task.title }}
          </v-list-item-title>
        </div>
        <div v-else>
          <v-text-field v-model="editing" @keyup.enter="changeTaskTitleFlg(section,index,'end')" :value="task.title" ></v-text-field>
        </div>
      </v-card>
    <v-card-subtitle>Section Name : {{ section.title }}</v-card-subtitle>
    <div v-if="task.editCFlg" @dblclick="changeTaskContentsFlg(section,index,'start')">
      <v-card-text>{{ task.contents }}</v-card-text>
    </div>
    <div v-else>
      <v-text-field v-model="editing" @keyup.enter="changeTaskContentsFlg(section,index,'end')" :value="task.contents" ></v-text-field>
    </div>
    <div class="d-flex justify-end mb-2">
      <div>
        <a @click="changeTaskContentsFlg(section,index,'start')" class="btn btn-primary pa-1"><font-awesome-icon :icon="['fa', 'pen']" :style="{ color: 'grey' }" /></a>
      </div>
      <div v-if="task.complete">
        <a @click="checkcomplete(section,index)" class="btn btn-primary pa-1"><font-awesome-icon :icon="['fa', 'check']" :style="{ color: 'green' }" /></a>
      </div>
      <div v-else>
        <a @click="checkcomplete(section,index)" class="btn btn-primary pa-1"><font-awesome-icon :icon="['fa', 'check']" :style="{ color: 'grey' }" /></a>
      </div> 

      <div v-if="task.favo">
        <a @click="checkstatus(section,index)" class="btn btn-primary pa-1"><font-awesome-icon :icon="['fa', 'star']" :style="{ color: 'yellow' }"/></a>
      </div>
      <div v-else>
        <a @click="checkstatus(section,index)" class="btn btn-primary pa-1"><font-awesome-icon :icon="['fa', 'star']" :style="{ color: 'grey' }"/></a>
      </div>
      <div>
        <a @click="deleteTodo(section,index)" class="btn btn-primary pa-1 mr-2"><font-awesome-icon :icon="['fa', 'trash']" :style="{ color: 'grey' }" /></a>
      </div>
    </div>
  </v-card>

  </div>
</template>

<script>

  export default {
    props: ["section"],
    emit:["changeTaskTitleFlg","changeTaskContentsFlg","deleteTodo","checkstatus"],
    name: 'TaskComponents',
    data() {
      return{
        
      };
    },
    methods:{
      changeTaskContentsFlg(section,i,flg){
        if(flg=="start"){
          section.tasks[i].editCFlg = false ;
          this.editing = section.tasks[i].contents ;
        }else{
          section.tasks[i].editCFlg = true ;
          section.tasks[i].contents = this.editing ;
        }
      },
      changeTaskTitleFlg(section,i,flg){
        if(flg=="start"){
          section.tasks[i].editTFlg = false ;
          this.editing = section.tasks[i].title ;
        }else{
          section.tasks[i].editTFlg = true ;
          section.tasks[i].title = this.editing ;
        }
      },
      deleteTodo(section,i){
        section.tasks.splice(i,1) ;
      },
      checkstatus(section,i){
        if(section.tasks[i].favo) section.tasks[i].favo = false ;
        else section.tasks[i].favo = true ;
      },
      checkcomplete(section,i){
        if(section.tasks[i].complete) section.tasks[i].complete = false ;
        else section.tasks[i].complete = true ;
      },
    },
  }
</script>
