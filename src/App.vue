<template>
  <input type="text" v-model="userName" placeholder="Name">
  <input type="password" v-model="userPass" placeholder="Password">
  <input type="email" v-model="userEmail" placeholder="Email">
  <button @click="sendData()">Send</button>
  <div v-for="el in ['f', 'd']">{{ el }}</div>
  <div v-if="users.length == 0">
    We dont have users
  </div>

  <p className="error">{{ error }}</p>
  <div v-for="(el, index) in users" :key="index">
    <h3>{{ el.name }}</h3>
    <p>{{ el.email }} - <b>{{ el.pass }}</b></p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      users: [],
      error: '',
      userName: '',
      userPass: '',
      userEmail: ''
    }
  },
  methods: {
    sendData(){
      if(this.userName == '') {
        this.error = 'Name didnt enter';
        return;
      } else if (this.userEmail == '') {
        this.error = 'Email didnt enter';
        return;
      } else if (this.userPass == '') {
        this.error = 'Password didnt enter';
        return;
      }

      this.error = '';
      
      this.users.push({
        name: this.userName,
        pass: this.userPass,
        email: this.userEmail
      })
    }
  }
}
</script>

<style scoped>
  
</style>
