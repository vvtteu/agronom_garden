<template>
  <div class="app">
    <Header
      @open-dialog="openDialog"
      @search="handleSearch"
      :present-count="presentCount"
      :absent-count="absentCount"
    />
    <UsersList :users="filteredUsers" @edit-user="openEditDialog" />
    <!-- <button @click="clearUsers">Очистить список</button> -->
    <DialogBox :show="isDialogOpen" @close="isDialogOpen = false">
      <UsersForm
        :user="selectedUser"
        @submit="handleSubmit"
        @close="isDialogOpen = false"
      />
    </DialogBox>
    <UsersFilter @filter-users="handleFilterChange" v-if="!isDialogOpen" />
  </div>
</template>

<script>
import Header from "@/components/users/Header.vue";
import UsersList from "@/components/users/UsersList.vue";
import UsersForm from "@/components/users/UsersForm.vue";
import DialogBox from "@/components/UI/DialogBox.vue";
import UsersFilter from "@/components/users/UsersFilter.vue";

export default {
  components: {
    Header,
    UsersList,
    DialogBox,
    UsersForm,
    UsersFilter,
  },
  data() {
    return {
      users: (JSON.parse(localStorage.getItem("users")) || []).map((user) => ({
        ...user,
        presence: user.presence !== undefined ? user.presence : false,
      })),
      isDialogOpen: false,
      selectedUser: null,
      presenceFilter: null,
      searchParams: { name: "", company: "" },
    };
  },

  computed: {
    filteredUsers() {
      let result = this.users;

      if (this.presenceFilter !== null) {
        result = result.filter((user) => user.presence === this.presenceFilter);
      }

      if (this.searchParams.name) {
        const nameQuery = this.searchParams.name.toLowerCase();
        result = result.filter((user) =>
          user.FIO.toLowerCase().includes(nameQuery)
        );
      }

      if (this.searchParams.company) {
        const companyQuery = this.searchParams.company.toLowerCase();
        result = result.filter((user) =>
          user.company.toLowerCase().includes(companyQuery)
        );
      }

      return result;
    },
    presentCount() {
      return this.users.filter((user) => user.presence).length;
    },
    absentCount() {
      return this.users.filter((user) => !user.presence).length;
    },
  },

  methods: {
    handleSearch(params) {
      this.searchParams = params;
    },
    handleFilterChange(filterValue) {
      console.log("Received filter:", filterValue);
      this.presenceFilter = filterValue;
    },

    openDialog() {
      console.log("Диалог открывается");
      this.selectedUser = this.getEmptyUser();
      this.isDialogOpen = true;
    },
    openEditDialog(user) {
      this.selectedUser = { ...user };
      this.isDialogOpen = true;
    },
    handleSubmit(user) {
      if (!user.FIO) return;
      if (user.number) {
        const index = this.users.findIndex((u) => u.number === user.number);
        this.users.splice(index, 1, user);
      } else {
        user.number =
          this.users.length > 0
            ? Math.max(...this.users.map((u) => u.number)) + 1
            : 1;
        this.users.push(user);
      }
      localStorage.setItem("users", JSON.stringify(this.users));
      this.closeDialog();
    },
    // clearUsers() {
    //   this.users = [];
    //   localStorage.removeItem('users');
    // },
    closeDialog() {
      this.isDialogOpen = false;
    },
    getEmptyUser() {
      return {
        FIO: "",
        company: "",
        group: "",
        presence: false,
        number: null,
      };
    },
  },
};
</script>

<style>
.app {
  font-family: "Open Sans", sans-serif;
}


</style>
