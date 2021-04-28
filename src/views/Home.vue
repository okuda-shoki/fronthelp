<template>
  <div class="home">
    <input type="text" v-model="test">
    <button @click="send()">送信</button>
    <div v-for="data in list" :key="data.id">
      <p>{{data.name}}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data(){
    return{
      test:"",
      list:[]
    }
  },
  methods:{
     async getContact() {
      const resData = await axios.get("http://127.0.0.1:8000/api/");
      this.list= resData.data.data;
    },
    async send(){
      const sendData = {
        name:this.test
      };
      await axios.post("http://127.0.0.1:8000/api/", sendData);
      await this.getContact();
  }
},
created() {
    this.getContact();
  },
}
</script>
