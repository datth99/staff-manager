<template>

  <div class="container">
    <div class="row">
      <div class="mt-5" >
        <div class="row">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item active" aria-current="page"><h4>List Staff </h4></li>
            </ol>
            <hr>
          </nav>
        
        </div>
        <div>
            <div class="row mb-3">
              <div>
                <button type="button" class="btn btn-primary" @click="clickAdd()">Add Staff</button>
              </div>
            </div>
            <table class="table table-hover table-striped table-bordered text-center" >
          <thead>
            <tr>
              <th scope="col">ID</th>
              <th scope="col">Name</th>
              <th scope="col">Email</th>
              <th scope="col">Address</th>
              <th scope="col">Phone</th>
              <th scope="col">Edit</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="staff in staffs" :key="staff">
              <th scope="row">{{staff.id+1}}</th>
              <td>{{staff.name}}</td>
              <td>{{staff.email}}</td>
              <td>{{staff.address}}</td>
              <td>{{staff.phone}}</td>
              <td class="btn-edit">
                <button type="button" class="btn btn-primary" @click="clickEdit(staff)">Edit</button>
                <button type="button" class="btn btn-danger" @click="clickDelete(staff)">Delete</button>
              </td>
            </tr>
            
          </tbody>
            </table>
        </div>
      </div>
    </div>
    <div class="row">
         <editStaff v-if="isEdit" :staff="staff" @save="clickSave()"></editStaff>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import EditStaff from './components/EditStaff.vue'
export default {
  name: 'App',
  data(){
    return {
      staffs: {},
      isEdit: false,
      staff: null
    }
  },
  methods: {
    clickAdd(){
      let staff = {id: Math.floor(Math.random() * 100), name: '', email: '', address: '', phone: ''}
      this.staff = staff;
      this.isEdit = true;
    },
    clickSave(staff){
      let index = this.staffs.findIndex(item => item.id == staff.id)
      if(index >= 0){
        this.staffs.splice(index, 1, staff)
      }else{
        this.staffs.push(staff)
      }

      this.isEdit = false
    },
    clickEdit(staff){
      this.staff = JSON.parse(JSON.stringify(staff))
      this.isEdit = true
    },
    clickDelete(staff){
      let index = this.staffs.findIndex(item => item.id == staff.id)
      this.staffs.splice(index, 1)
    }
  },
  mounted () {
    axios
      .get('https://61100702c848c900171b3a53.mockapi.io/staffs')
      .then(res => {
        this.staffs = res.data
      })
  },
  components: {
    'editStaff': EditStaff,
  }
}
</script>

<style scoped>
  .btn-edit button{
    margin: 0 5px;
  }
</style>
