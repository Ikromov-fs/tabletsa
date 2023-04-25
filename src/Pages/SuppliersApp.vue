<template>
    <div>
        <appModal v-model="addsup">
          <div class="text-center">
            <h2>Add Suppliers</h2>
            <form id="form" @submit="(e)=>submitForm(e)">
             <input @change="(e)=>changeUsername(e)" type="text" placeholder="enter your username">
             <input @change="(e)=>changeLastname(e)" type="text" placeholder="enter your lastname">
             <input @change="(e)=>changeFirstname(e)" type="text" placeholder="enter your firstname">
             <input @change="(e)=>changeEmail(e)" type="email" placeholder="enter your email">
             <input @change="(e)=>changeAddress(e)" type="address" placeholder="enter your address">
             <input @change="(e)=>changeNumber(e)" type="number" placeholder="enter your phone number">
             <input @change="(e)=>changeImage(e)" type="file" placeholder="choose your img"/>
            </form>
            <button class="btn submit-btn" form="form">Submit</button>
          </div>
        </appModal>
        <appModal v-model="editsup">
          <div class="text-center">
            <h2>Edit Suppliers</h2>
            <form id="forme" @submit="(e)=>submitForme(e)">
             <input @change="(e)=>changeUsernamee(e)" type="text" placeholder="enter your username">
             <input @change="(e)=>changeLastnamee(e)" type="text" placeholder="enter your lastname">
             <input @change="(e)=>changeFirstnamee(e)" type="text" placeholder="enter your firstname">
             <input @change="(e)=>changeEmaile(e)" type="email" placeholder="enter your email">
             <input @change="(e)=>changeAddresse(e)" type="address" placeholder="enter your address">
             <input @change="(e)=>changeNumbere(e)" type="number" placeholder="enter your phone number">
             <input @change="(e)=>changeImagee(e)" type="file" placeholder="choose your img"/>
            </form>
            <button class="btn submit-btn" form="forme">Submit</button>
          </div>
        </appModal>
      <h2>Suppliers</h2>
       <div class="col-md-6 text-center mx-auto m-5">
        <button @click="addsup=true" class="btn btn-info ">Add Suppliers</button>
       </div>
      <table class="table">
        <thead>
                <th v-for="(item,index) in headers" :key="index">{{ item.title }}</th>
        </thead>
        <tbody>
            <tr v-for="(item , index) in suppliers">
                <td>{{ index +1}}</td>
                <td>{{ item.username }}</td>
                <td>{{ item.last_name }}</td>
                <td>{{ item.first_name }}</td>
                <td>{{ item.email }}</td>
                <td>{{ item.address }}</td>
                <td>{{ item.phone_number }}</td>
                <td><img :src="item.image" alt="image" width="20" height="20"></td>
                <td>
                    <button @click="()=>deletClick(item.id)"  class="btn btn-danger">delet</button>
                    <button class="btn btn-info m-2" @click="()=>editSuppliers(item.id)">edit</button>
                </td>
            </tr>
        </tbody>
      </table>
    </div>
</template>

<script setup>
import http from '@/axios';
import { ref } from 'vue';
import appModal from '@/components/ui/app-modal.vue';
const addsup = ref(false)
const editsup =ref(false)
const editId = ref('')
const headers = ref([
    {title :'T/R' , value:'Tr'},
  {title: 'Username', value:'username'},
  {title :"Lastname" , value :'last_name'},
  {title:'Firstname' , value:"first_name"},
  {title:'Email' , value:'email'},
  {title:'Address' , value:'address'},
  {title:'Number' , value:'phone_number'},
  {title:'Image' },
  {title :'Action'}
])
const changeUsername =(e)=>{
    username.value=e.target.value
}
const changeUsernamee =(e)=>{
    usernamee.value=e.target.value
}
const changeLastname =(e)=>{
    lastname.value=e.target.value
}
const changeLastnamee =(e)=>{
    lastnamee.value=e.target.value
}
const changeFirstname =(e)=>{
    firstname.value=e.target.value
}
const changeFirstnamee =(e)=>{
    firstnamee.value=e.target.value
}
const changeEmail =(e)=>{
    email.value=e.target.value
}
const changeEmaile =(e)=>{
    emaile.value=e.target.value
}
const changeAddress =(e)=>{
    address.value=e.target.value
}
const changeAddresse =(e)=>{
    addresse.value=e.target.value
}
const changeNumber =(e)=>{
    number.value=e.target.value
}
const changeNumbere =(e)=>{
    numbere.value=e.target.value
}
const changeImage =(e)=>{
    image.value=e.target.files[0]
}
const changeImagee =(e)=>{
    image.value=e.target.files[0]
}
const submitForm =(e)=>{
    e.preventDefault()
    const form = new FormData()
    form.append('username' , username.value)
        form.append('first_name' , firstname.value)
        form.append('last_name' , lastname.value )
        form.append('email',email.value )
        form.append('address' , address.value)
        form.append('phone_number' , number.value)
        form.append('image' , image.value)
        http.post('/suppliers/' , form).then((res) =>{
            if(res.status === 201){
                window.location.reload()
            }
        })
        addsup.value = false
        console.log(form)
}
const submitForme =(e)=>{
    e.preventDefault()
    const form = new FormData()
    form.append('username' , usernamee.value)
        form.append('first_name' , firstnamee.value)
        form.append('last_name' , lastnamee.value )
        form.append('email',emaile.value )
        form.append('address' , addresse.value)
        form.append('phone_number' , numbere.value)
        form.append('image' , imagee.value)
        http.put(`/suppliers/${editId.value}`, form).then((res) =>{
           console.log(res.data);
        })
        
        console.log(form)
}

const username = ref('')
const firstname = ref('')
const lastname = ref('')
const email = ref('')
const address = ref('')
const number = ref('')
const image = ref({})
const suppliers = ref([])
const usernamee = ref('')
const firstnamee = ref('')
const lastnamee = ref('')
const emaile = ref('')
const addresse = ref('')
const numbere = ref('')
const imagee = ref({})

const getSuppliers = ()=>{
    http.get('/suppliers/').then((res)=>{
        console.log(res.data);
        suppliers.value = res.data
    })
}
const  deletClick =(id)=>{
    http.delete(`/suppliers/${id}`).then((res)=>{
        if(res.status === 204){
            window.location.reload()
        }
    })
    
}
const editSuppliers=(id)=>{
    editId.value=id
    console.log(id)
    editsup.value=true
}
getSuppliers()
</script>

<style  scoped>

  h2{
    text-align: center;
    margin: 20px 0 60px 0;
    font-size: 40px;
    font-weight: 700;
    font-family: sans-serif;
  }
  input{
    width: 80%;

    padding: 5px;
    border-radius: 7px;
 
    outline: none;
    margin-bottom: 10px;
 }
 .submit-btn{
    background-color: blue;
    color: white;
    padding: 10px 25px;
 }

 .router-link-active{
    color:red;
 }
</style>