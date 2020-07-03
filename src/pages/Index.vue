<template>
  <q-page padding>
    <div class="row q-mb-lg">
      <q-input v-model="newTask" placeholder="Add new task" class="col" @keyup.enter="addTask"></q-input>
      <q-btn color="primary"
             size="sm"
             label="Add"
              @click.native="addTask"></q-btn>
    </div>

    <div class="row q-mb-lg">
      <q-list bordered padding class="col">
        <q-item-label header>Tasks</q-item-label>
        <q-item v-for="(task,index) in tasks" :key="index">
          <q-item-section>
            <q-item-label>{{task}}</q-item-label>
          </q-item-section>
          <q-item-section avatar>
            <q-icon color="primary" name="check" @click.native="moveToDone(index)" />
          </q-item-section>
        </q-item>
      </q-list>
    </div>

    <div class="row">
      <q-list bordered class="col" padding>
        <q-item-label header>Done</q-item-label>
        <q-item v-for="(task,index) in done" :key="index">
          <q-item-section>
            <q-item-label>{{task}}</q-item-label>
          </q-item-section>
          <q-item-section avatar>
            <q-icon color="red" name="close" @click.native="deleteTask(index)" />
          </q-item-section>
        </q-item>
      </q-list>
    </div>
  </q-page>
</template>

<script>
  export default {
    name: 'PageIndex',
    data(){
      return {
        tasks: [],
        done:[],
        newTask: ''
      }
    },
    methods:{
      addTask(){
        this.tasks.push(this.newTask)
        this.newTask = ''
      },
      moveToDone(index){
        this.done.push(this.tasks[index])
        this.tasks.splice(index, 1)
      },
      deleteTask(index){
        this.$q.dialog({
          title: 'Confirm',
          message: 'Really Delete?',
          ok:'Yes',
          cancel:'No'
        }).onOk(() => {
          this.done.splice(index,1)
          this.$q.notify({type: 'negative', message:'Deleted!'})
        }).onCancel(() => {
          // this.$q.notify('Disagreed!')
        }).onDismiss( () => {

        })
      }
    }
  }
</script>
