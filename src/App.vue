<template>
  <div id="app">
    <NewStudentForm v-on:student-added = "newStudentAdded"></NewStudentForm>
    
    <StudentTable
      v-bind:students = "students"
      v-on:student-present = "studentArrivedOrLeft"
      v-on:delete-student = "studentDeleted">
    </StudentTable>
    
    <StudentMessage v-bind:message = "message" v-bind:name = "name"></StudentMessage>
  </div>
</template>

<script>
import NewStudentForm from './components/NewStudentForm.vue'
import StudentTable from './components/StudentTable.vue'
import StudentMessage from './components/StudentMessage.vue'



export default {
  name: 'App',
  components: {
    NewStudentForm,
    StudentTable,
    StudentMessage
  },
  data(){
    return {
      students: [],
      message: '',
      name: '',
      newStudentName: ''
    }
  },
  methods: {
    newStudentAdded(student){
      this.students.push(student)
      this.students.sort(function(s1, s2){
        return s1.name.toLowerCase() < s2.name.toLowerCase() ? -1 : 1
      })
    },
    studentArrivedOrLeft(student){
      this.newStudentName = this.newStudentName.toLowerCase() //make entire string lowercase
      this.newStudentName = this.newStudentName.charAt(0).toUpperCase() + this.newStudentName.slice(1) //capitalize first letter, concatenate rest of name
      this.student = { name: this.newStudentName, starID: this.newStarID, present: false }
      this.message = student.present? 'Welcome, ' : 'Goodbye'
      this.name = student.name
    },
    studentDeleted(student){
      this.students = this.students.filter( s => s != student)
    }
  }
}
</script>

<style>


</style>
