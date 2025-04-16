<template>
  <div class="app">
    <Header :addUser="addUser" />
    <UsersList :users="users" />
    
  </div>


</template>


<script>
import Header from './components/Header.vue';
import UsersList from './components/UsersList.vue';

export default {
  components: {
    Header,
    UsersList,

  },
  data() {
    return {
      users: [
        {number: 1, FIO: 'Зубенко Михаил Петрович', company: 'ООО "Ассоль"', group: 'Партнер', presence: 'Присутствую'},
      ],
    }
  },
  methods: {
    addUser(user) {
      this.users.push(user);
    },
 }
  
};
</script>


<style >
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}



</style>
