<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-primary">
        <q-input 
          v-model="newTask"
          @keyup.enter="addTask"
          class="col" 
          square
          filled
          placeholder="Add Task" 
          dense
          bg-color="white">
          <template v-slot:append>
            <q-btn
              @click="addTask" 
              round 
              dense 
              flat 
              icon="add" 
            />
          </template>
      </q-input>
    </div>
    <q-list 
      class="bg-white"
      separator
      bordered>
      <q-item 
        v-for="(task, index) in tasks"
        :key="task.title"
        @click="task.done = !task.done"
        :class="{ 'done bg-blue-1' : task.done }"
        clickable
        v-ripple>
        <q-item-section avatar>
          <q-checkbox 
          v-model="task.done" 
          color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{task.title}}</q-item-label>
        </q-item-section>
        <q-item-section
          v-if="task.done"
          side>
          <q-btn 
            flat round color="primary"
            @click.stop="deleteTask(index)" 
            dense
            icon="delete" />
        </q-item-section>
      </q-item>
      </q-list>
      <div 
        v-if="!tasks.length"
        class="noTasks absolute-center">
        <q-icon 
          name="check"
          size ="100px"
          color="primary"/>

        <div class="text h5 text-primary text-center">
          No Tasks!
        </div>
      </div>
  </q-page>
</template>

<script>
import { METHODS } from 'http'
export default {
  data() {
    return {
      newTask: '',
      tasks: [
      ]
    }
  },
  methods: {
    deleteTask(index) {
      this.$q.dialog({
        title: 'Confirm',
        message: 'Do You really want to delete this task?',
        cancel: true,
        persistent: true
      }).onOk(() => {
          this.tasks.splice(index, 1)
          this.$q.notify('Done! Task deleted!')
      })
    },
    addTask(){
      this.tasks.push({
        title : this.newTask,
        done: false
      })
      this.newTask= ''
    } 
  }
}
</script>

<style lang="scss">
  .done {
    .q-item__label {
      text-decoration: line-through;
      color: #bbbbbb
    }
  }
  .noTasks {
    opacity: 0.5;
  }
</style>