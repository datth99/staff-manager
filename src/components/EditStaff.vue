<template>
    <div>
        <form action="#">
            <div class="mb-3">
            <label for="exampleFormControlInput1" class="form-label">Name</label>
            <input type="text" class="form-control" placeholder="Name" v-model="mutableList.name" >
            </div>
            <div class="mb-3">
            <label for="exampleFormControlTextarea1" class="form-label">Email</label>
            <input type="email" class="form-control" placeholder="Email" v-model="mutableList.email" > 
            </div>
            <div class="mb-3">
            <label for="exampleFormControlTextarea1" class="form-label">Address</label>
            <input type="text" class="form-control" placeholder="Address" v-model="mutableList.address" >
            </div>
            <div class="mb-3">
            <label for="exampleFormControlTextarea1" class="form-label">Phone</label>
            <input type="text" class="form-control" placeholder="Phone" v-model="mutableList.phone" >
            </div>
            <button type="button" class="btn btn-primary" @click="clickSave()">Save</button>
        </form>
    </div>
</template>

<script>
export default {
    name: 'EditStaff',
    props: ['staff'],
    data: function(){
        return {
            mutableList: this.staff
        }
    },
    methods: {
        clickSave(){
            this.$emit('save', this.staff);
        },
    },
}
</script>

<style>
    
</style>