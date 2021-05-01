<template>
 <div id="app">
   <div class="main-style">
     <div class="todo">
      <h1>Todo List</h1>
      <div class="newtodo">
         <input type="text" name="name" id="name" v-model="newTodo" class="newtext"/>
         <button @click="insertContact" class="newbutton">追加</button>
      </div>

      <div class="todolist">
        <table>
         <tr v-for="item in contactLists" :key="item.id">
           <div class="all">
            <td><input type="text" v-model="item.name" class="list"/></td>
            <div class="newupdel">
            <tr><button @click="updateContact(item.id,item.name)" class="updatebutton">更新</button></tr>
            <tr><button @click="deleteContact(item.id)" class="deletebutton">削除</button></tr>
            </div>
           </div> 
         </tr>
        </table>
       
      </div>
    </div>
   </div>  
 </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      newTodo: "",
      contactLists: [],
    };
  },
  methods: {
    async getContact() {
      const resData = await axios.get("http://127.0.0.1:8000/api/contact/");
      this.contactLists = resData.data.data;
    },
    async insertContact() {
      const sendData = {
        name: this.newTodo,
      };
      await axios.post("http://127.0.0.1:8000/api/contact/", sendData);
      await this.getContact();
    },
    async updateContact(id, name) {
      const sendData = {
        name: name,
      };
      await axios.put("http://127.0.0.1:8000/api/contact/" + id, sendData);
      await this.getContact();
    },
    async deleteContact(id) {
      await axios.delete("http://127.0.0.1:8000/api/contact/" + id);
      await this.getContact();
    },
  },
  created() {
    this.getContact();
  },
};
</script>

<style>
.main-style{
   background-color: rgb(45, 25, 124);
   min-height: 100vh;
   background: cover;
 }
  .todo{
   position:absolute;
   top: 50%;
   left: 50%;
   transform: translate(-50%, -50%);
   background-color: white;
   padding:30px;
   border-radius: 10px;
   width: 50vw
 }
 .newbutton{
  text-align: left;
    border: 2px solid #dc70fa;
    font-size: 12px;
    color: #dc70fa;
    background-color: #fff;
    font-weight: bold;
    padding: 8px 16px;
    border-radius: 5px;
    cursor: pointer;
    transition: 0.4s;
    outline: none;
 }
 .newbutton:hover{
  color:white;
  background-color:#dc70fa;
  transition: 0.5s;
 }
 .newtext{
   width:80%;
   font-size:20px;
   padding:5px;
 }
 .newtodo{
  display: flex;
  justify-content: space-between;
 }
 .newupdel{
   display:flex;
   float: right;
 }
 .all{
  display: flex;
  justify-content: space-between;
 }
 .todolist{
   justify-content: space-between;
 }
 .updatebutton{
   text-align: left;
    border: 2px solid #fa9770;
    font-size: 12px;
    color: #fa9770;
    background-color: #fff;
    font-weight: bold;
    padding: 8px 16px;
    border-radius: 5px;
    cursor: pointer;
    transition: 0.4s;
    outline: none;
 }
 .updatebutton:hover{
  color:white;
  background-color:#fa9770;
  transition: 0.5s;
 }
 .deletebutton{
   text-align: left;
    border: 2px solid #71fadc;
    font-size: 12px;
    color: #71fadc;
    background-color: #fff;
    font-weight: bold;
    padding: 8px 16px;
    border-radius: 5px;
    cursor: pointer;
    transition: 0.4s;
    outline: none;
 }
 .deletebutton:hover{
  color:white;
  background-color:#71fadc;
  transition: 0.5s;
 }
 .list{
   width:80%;
   font-size:20px;
   padding:5px;
 }
 *{
   margin:0px;
 }
</style>
