<template>
  <q-card>
    <ModalHeader>Add Task</ModalHeader>

    <form @submit.prevent="submitForm">
      <q-card-section>
        
        <ModalTaskName 
          :name.sync="taskToSubmit.name"
          ref="modalTaskName" />

        <ModalDueDate 
          :dueDate.sync="taskToSubmit.dueDate"
          @clear="clearDueDate" />
        
        <ModalDueTime 
          v-if="taskToSubmit.dueDate"
          :dueTime.sync="taskToSubmit.dueTime" />
      </q-card-section>

      <ModalButtons />      
    </form>
  </q-card>
</template>

<script>
import ModalButtons from 'components/Tasks/Modals/Shared/ModalButtons'
import ModalDueDate from 'components/Tasks/Modals/Shared/ModalDueDate'
import ModalDueTime from 'components/Tasks/Modals/Shared/ModalDueTime'
import ModalHeader from 'components/Tasks/Modals/Shared/ModalHeader'
import ModalTaskName from 'components/Tasks/Modals/Shared/ModalTaskName'
import { mapActions } from "vuex";

export default {
  components: {
    ModalButtons, ModalDueDate, ModalDueTime, ModalHeader, ModalTaskName    
  },
  data() {
    return {
      taskToSubmit: {
        name: "",
        dueDate: "",
        dueTime: "",
        completed: false
      }
    };
  },
  methods: {
    ...mapActions("tasks", ["addTask"]),
    submitForm() {
      let $name = this.$refs.modalTaskName.$refs.name
      $name.validate();
      if (!$name.hasError) {
        this.submitTask();
      }
    },
    submitTask() {
      this.addTask(this.taskToSubmit);
      this.$emit("close");
    },
    clearDueDate() {
      this.taskToSubmit.dueDate = "";
      this.taskToSubmit.dueTime = "";
    }
  }
};
</script>

<style>
</style>