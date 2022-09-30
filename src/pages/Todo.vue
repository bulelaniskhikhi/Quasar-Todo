<template>
  <q-page class="q-pa-lg">
    <div class="row q-pa-sm bg-gray">
      <q-input 
        @keyup.enter="addTask"
        color="black" 
        bottom-slots 
        v-model="newTask" 
        placeholder="Add Task" 
        :dense="dense" 
        style="width: 100%; color: black;"
        >
        <template v-slot:append>
          <q-btn 
          @click="addTask"
          name="close" 
          flat
          class="cursor-pointer" 
          icon="add"
          />
        </template>
      </q-input>
      <div 
        v-if="!tasks.length"
        class="no-tasks absolute-center">
        <q-icon
        name="check"
        size="100px"
        color="black"
        />
        <div class="text-h5 text-black text-center">
          No Tasks
        </div>
      </div>
    </div>
    <q-list class="bg-white"
    seperator>
      <q-item 
      v-for="(task, index) in tasks"
      :key="task.id"
      @click="task.done = !task.done"
      :class="{'done bg-black' : task.done}"
      clickable
      v-ripple>
        <q-item-section avatar>
          <q-checkbox 
          v-model="task.done" 
          class="no-pointer-events" 
          color="black" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{task.title}}</q-item-label>
        </q-item-section>

        <q-item-section
        v-if="task.done"
        side
        >
        <q-btn 
        flat 
        round 
        color="white" 
        icon="delete" 
        @click.stop="deleteTask(index)"
        />      
        </q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
 data() {
  return {
    newTask: '',
    tasks: [
      // {
      //   id: 1,
      //   title: 'go to your house',
      //   done: false,
      // },
      // {
      //   id: 2,
      //   title: 'keep your room',
      //   done: false,
      // },
      // {
      //   id: 3,
      //   title: 'lay on the bed',
      //   done: false,
      // },
    ]
  }
 },
 methods: {
  deleteTask(index) {
      this.$q.dialog({
        color: 'black',
        title: 'Confirm',
        message: 'Are you sure you want to delete this?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index, 1)
        this.$q.notify('Task Deleted')
      })
  }, 
  addTask() {
    this.tasks.push({
      title: this.newTask,
      done: false
    })
    this.newTask = ''
  }
 }
})
</script>

<style>
.done > .q-item__section > .q-item__label { 
    text-decoration: line-through;
    color: white;
}

.no-tasks {
  opacity: 0.5
}
</style>