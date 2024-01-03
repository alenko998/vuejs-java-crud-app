<template>
  <div class="container mt-5">
    <div class="card">
      <div class="card-header">
        <h4>Add Students</h4>
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
          <button type="button" class="btn btn-primary" @click="saveStudent">Save</button>
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
    methods:{
        saveStudent(){
            axios.post('http://localhost:8080/api/v1/students', this.model.student)
                .then(res => {
                    console.log(res);
                    this.model.student = {name: '', course: '', email: '', phone:''};
                    this.$router.push('/students');
                    // alert("You added student");
                })
                .catch(function(error){
                    if(error.response){
                        console.log(error.response.data);
                        console.log(error.response.status);
                        console.log(error.response.header);
                    } else if (error.request){
                        console.log(error.request);
                    } else {
                        console.log("Error: " , error.message);
                    }
                })
        }
    }
    
  }
</script>

<style lang="scss" scoped>
  
</style>