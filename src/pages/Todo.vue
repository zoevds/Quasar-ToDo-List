<template>
  <q-page class="bg-grey-3 column">
<div class="row q-pa-sm bg-orange-3">
  <q-input
   v-model="NewTask"
   @keyup.enter="addTask"
   placeholder="Add Task"
   square
   class=col
   dense>
        <template v-slot:append>
          <q-btn
          @click="addTask"
          round
          dense
          flat
          icon="add" />
        </template>
      </q-input>
</div>
    <q-list class="bg-white" separator bordered>
      <q-item
      v-for="(task, index) in tasks"
      :key="task.title"
      @click="task.done = !task.done"
      :class="{ 'done bg-orange-3' : task.done }"
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
        side>
        <q-btn
        @click.stop="deleteTask(index)"
         flat
        round
        dense
        color="primary"
        icon="delete" />

        </q-item-section>
      </q-item>

    </q-list>
<div
v-if="!tasks.length"
 class="no-tasks absolute-center">
  <q-icon
  name="check"
  size="100px"
  color="orange-5"></q-icon>
  <div class="text-h5 text-orange-5 text-center">
No Tasks
  </div>
</div>
  </q-page>
</template>

<script>


export default {
data(){
  return {
     NewTask:'',
    tasks: [
      {
        title: 'Get Money',
        done: false
      },
      {
        title: 'Invest',
        done: false
      },
      {
        title: 'Sell ur mom for more money',
        done: false
      },
      {
        title: 'Buy a new mom',
        done: false
      },
    ]
  }
},
methods: {
  deleteTask(index){
    this.$q.dialog({
        title: 'Confirm',
        message: 'Really want to delete?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index, 1)
        this.$q.notify('Task Deleted')
      })
  },
  addTask(){
    this.tasks.push({
      title: this.NewTask,
      done:false
    })
    this.NewTask = ''
  }
}
}
</script>
<style lang="scss">
.done{
  .q-item__label{
    text-decoration: line-through;
    color:#abb
  }
}
.no-tasks{
  opacity:0.5;
}
</style >
