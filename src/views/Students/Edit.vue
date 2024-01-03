<template>
  <div class="container mt-5">
    <div class="card">
      <div class="card-header">
        <h4>Edit Students</h4>
      </div>
      <div class="card-body">
        <div class="mb-3">
          <label for="">Name</label>
          <input type="text" class="form-control" v-model="model.student.name">
        </div>
        <div class="mb-3">
          <label for="">Course</label>
          <input type="text" class="form-control" v-model="model.student.course">
        </div>
        <div class="mb-3">
          <label for="">Email</label>
          <input type="email" class="form-control" v-model="model.student.email">
        </div>
        <div class="mb-3">
          <label for="">Phone</label>
          <input type="text" class="form-control" v-model="model.student.phone">
        </div>
        <div class="mb-3">
          <button type="button" class="btn btn-primary" @click="updateStudent(this.$route.params.id)">Update</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';
  export default{
    name: 'studentCreate',
    data(){
        return {
            model: {
                student: {
                    name: '',
                    course: '',
                    email: '',
                    phone: ''
                }
            }
        }
    },
    mounted(){
      console.log(this.$route.params.id);
      this.getStudentData(this.$route.params.id)
    },  
    methods:{
        getStudentData(studentId){
          axios.get(`http://localhost:8080/api/v1/students/${studentId}`)
            .then(res=>{
              this.model.student = res.data
              console.log(res.data);
            })
            .catch(error=>{
              console.log('no such student');
              console.log(error);
              alert('no such student')
            })

        },
        updateStudent(studentId){
          axios.put(`http://localhost:8080/api/v1/students/${studentId}`, this.model.student)
            .then(res=>{
              console.log(res.data);
              alert('updated!')
              this.$router.push('/students');
            })
            .catch(error=>{
              console.log(error);
            })
        }
    }
    
  }
</script>

<style lang="scss" scoped>
  
</style>