<template>
  <q-card>
    <ModalHeader>Edit Task</ModalHeader>
    <form @submit.prevent="submitForm">
      <q-card-section>
        <ModalTaskName 
          :name.sync="taskToSubmit.name"
          ref="modalTaskName"
          />

        <ModalDueDate
          :dueDate.sync="taskToSubmit.dueDate"
          @clear="clearDueDate" 
          />

        <ModalDueTime 
          v-if="taskToSubmit.dueDate"          
          :dueTime.sync="taskToSubmit.dueTime"
          />
      </q-card-section>

      <ModalButtons />
      <!-- <pre>{{ taskToSubmit }}</pre> -->
    </form>
  </q-card>  
</template>

<script>
import ModalButtons from "components/Tasks/Modals/Shared/ModalButtons";
import ModalDueDate from "components/Tasks/Modals/Shared/ModalDueDate";
import ModalDueTime from "components/Tasks/Modals/Shared/ModalDueTime";
import ModalHeader from "components/Tasks/Modals/Shared/ModalHeader";
import ModalTaskName from "components/Tasks/Modals/Shared/ModalTaskName";
import { mapActions } from "vuex";

export default {
  props: ["task", "id"],
  components: {
    ModalButtons, ModalDueDate, ModalDueTime, ModalHeader, ModalTaskName
  },
  data() {
    return {
      taskToSubmit: {}
    };
  },
  methods: {
    ...mapActions('tasks', ['updateTask']),
    submitForm(){      
      let $name = this.$refs.modalTaskName.$refs.name
      $name.validate()
      if(!$name.hasError){
        this.submitTask()
      }
    },
    submitTask(){
      this.updateTask({
        id: this.id,
        updates: this.taskToSubmit
      })
      this.$emit('close')
    },
    clearDueDate(){
      this.taskToSubmit.dueDate = ''
      this.taskToSubmit.dueTime = ''
    }
  },
  mounted(){
    let v = this
    v.taskToSubmit = Object.assign({}, this.task)
  }
};
</script>

<style>
</style>