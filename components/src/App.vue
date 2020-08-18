<template>
  <div id="app">
    <div class="title">Title</div>
    <Status />
    <h1>{{ message }}</h1>
    <Input :msg="message" @messageChanged="message = $event" />
    <router-view/>

    <app-registration @userRegistered="userRegistered" :users="unregisteredUsers"></app-registration>
    <app-registrations @userUnregistered="userUnregistered" :registrations="registrations"></app-registrations>
  </div>
</template>

<script>
import Status from './components/Button.vue'
import Input from './components/Input.vue'
import Registration from './components/Registration.vue';
import Registrations from './components/Registrations.vue';
export default {
  name: 'App',
  components: {
    Status,
    Input,
    Registrations,
    Registration
  },
  data(){
    return{
      message: "This is great Message",
      registrations: [],
      users: [
          {id: 1, name: 'Max', registered: false},
          {id: 2, name: 'Anna', registered: false},
          {id: 3, name: 'Chris', registered: false},
          {id: 4, name: 'Sven', registered: false}
      ]
    }
  },
    computed: {
        unregisteredUsers() {
            return this.users.filter((user) => {
                return !user.registered;
            });
        }
    },
    methods: {
      userRegistered(user) {
          const date = new Date;
          this.registrations.push({userId: user.id, name: user.name, date: date.getMonth() + '/' + date.getDay()})
      },
        userUnregistered(registration) {
          const user = this.users.find(user => {
              return user.id == registration.userId;
          });
          user.registered = false;
          this.registrations.splice(this.registrations.indexOf(registration), 1);
        }
    },
    components: {
        appRegistration: Registration,
        appRegistrations: Registrations
    }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
}
.title{
  color: red;
}
</style>
