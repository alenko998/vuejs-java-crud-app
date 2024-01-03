<template>
  <div class="container mt-5">
    <div class="card">
      <div class="card-header">
        <h4>Students</h4>
        <RouterLink to="/students/create" class="btn btn-primary float-end">Add Student</RouterLink>
      </div>
      <div class="card-body">
        <table class="table table-bordered">
          <thead>
            <tr>
              <th>#</th>
              <th>Name</th>
              <th>Course</th>
              <th>Email</th>
              <th>Email</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody v-if="this.students.length > 0">
            <tr v-for="(student,index) in this.students" :key="index">
              <td>{{ index+1 }}</td>
              <td>{{ student.name }}</td>
              <td>{{ student.course }}</td>
              <td>{{ student.email }}</td>
              <td>{{ student.phone }}</td>
              <td class="buttons">
                <RouterLink :to="{path: '/students/' + student.id + '/edit'}" class="btn btn-success">Edit</RouterLink>
                <button class="btn btn-danger" @click="deleteStudent(student.id)">Delete</button>
              </td>
            </tr>
          </tbody>
          <tbody v-else>
            <tr>
              <td colspan="7">No students...</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>    
</template>
  
<style scoped>
  .card-header{
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
  }
  .buttons{
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-evenly;
  }
</style>

<script>
import axios from 'axios';
  export default {
    name: 'students',
    data(){
      return {
        students: []
      }
    },
    mounted(){
      // console.log('I am here');
      this.getStudents();
    },
    methods:{
      getStudents(){
        axios.get('http://localhost:8080/api/v1/students').then(res=> {
          this.students = res.data;
          this.students.sort((a, b) => a.id - b.id);
          console.log(this.students);
        });
      },
      deleteStudent(studentId){
        axios.delete(`http://localhost:8080/api/v1/students/${studentId}`)
          .then(
            res=>{
              console.log(res);
              // alert('deleted student!')
              this.getStudents();
            }
          )
          .catch(error=>{
            console.log(error);
          })
      }
    }
  }
</script>
  