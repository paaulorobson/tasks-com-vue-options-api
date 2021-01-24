<template>
 <div>
 <h1>{{title}}</h1>
 
 <input type="text" v-focus v-model="currentTask"  @keyup.enter="addTask" />
 <br>
 <br>
 <button @click="handleShowHideList">Ver minha lista</button>
 <br>
 <ul v-if="showList">
   <li @dblclick="complete(task)" 
        v-for="(task, index) in tasks" 
        :key="`${task}-${index}`"
        class="cursor-text"
        :class="{
          'line-through': task.isDone
          }"
    >
        {{task.name}} 

    <button @click="remove(task)">&times;</button>

   </li>
 </ul>
 

 <p v-else>Lista de tarefas escondidas</p>
 <!-- <a :href="curso">Link para curso</a>  data-binding-->
 </div>
</template>

<script>
const focus = {
   inserted:(el) => {
    el.focus();  
   }
 }


export default {
  name: 'Tasks',
  directives: {
    focus
  },
  
  data: () => ({
    title: 'Minha lista de tarefas',
    showList: false,
    tasks: [
      {name: 'Fazer uma tarefa', isDone: false}
    ],
    currentTask: ''
  }),

  methods: {
    remove(task) {
      this.tasks = this.tasks.filter(t => t.name !== task.name)
    },

    handleShowHideList() {
      this.showList = !this.showList
    },

    complete(task) {
      this.tasks = this.tasks.map(t=> {
        if(t.name === task.name) {
          return {...t, isDone: !t.isDone}
        }
          return {...t}
        
      })
    },
    
    addTask() {
      this.tasks.push({
        name: this.currentTask,
        isDone: false,
      })
      this.currentTask = ''

    }
  }
 
}
</script>


<style scoped>
.line-through {
  text-decoration: line-through;
}

.cursor-text {
  cursor: pointer;
}


</style>
