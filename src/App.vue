<template>
  <input type="text" v-model="userName" placeholder="Name">
  <input type="password" v-model="userPass" placeholder="Password">
  <input type="email" v-model="userEmail" placeholder="Email">
  <button @click="sendData()">Send</button>
  
  <div v-if="users.length == 0">
    We dont have users
  </div>

  <div v-else-if="users.length == 1">
    Users has 1 element
  </div>
  <div v-else>
    Has more users
  </div>

  <p className="error">{{ error }}</p>
 <User v-for="(el, index) in users" :key="index" :user="el" :index="index" :deleteUser="deleteUser" />
</template>

<script>
import User from './components/User.vue';

export default {
  components: { User },

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
    },
    deleteUser(index) {
      this.users.splice(index, 1);
      alert('hi')
    }
  }
}
</script>

<style scoped>
  
</style>
