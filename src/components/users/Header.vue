<template>
  <header>
    <div class="header">
      <img class="logo_img" src="@/assets/logo.png" alt="logo" />
      <div class="search">
        <div class="search-field">
          <input
            v-model="nameQuery"
            type="text"
            class="input"
            placeholder="Поиск по имени"
            @input="handleSearch"
          />
        </div>
        <div class="search-field">
          <input
            v-model="companyQuery"
            type="text"
            class="input"
            placeholder="Поиск по компании"
            @input="handleSearch"
          />
        </div>
        <AddButton class="btn_add" @click="$emit('open-dialog')"
          >Добавить</AddButton
        >
      </div>
      <div class="visitors">
        <p>Посетители</p>
        <span class="counters">
          <span class="green-text">{{ presentCount }} </span> /
          <span class="red-text">{{ absentCount }}</span>
        </span>
      </div>
    </div>
  </header>
</template>
<script>
import AddButton from "../UI/AddButton.vue";
import UsersForm from "./UsersForm.vue";

export default {
  props: {
    presentCount: Number,
    absentCount: Number,
  },
  data() {
    return {
      nameQuery: "",
      companyQuery: "",
    };
  },
  components: {
    UsersForm,
    AddButton,
  },
  methods: {
    handleSearch() {
      this.$emit("search", {
        name: this.nameQuery,
        company: this.companyQuery,
      });
    },
    created() {
      const savedSearch =
        JSON.parse(localStorage.getItem("searchParams")) || {};
      this.nameQuery = savedSearch.name || "";
      this.companyQuery = savedSearch.company || "";
    },
    clearName() {
      this.nameQuery = "";
      this.handleSearch();
    },
    clearCompany() {
      this.companyQuery = "";
      this.handleSearch();
    },
  },
};
</script>
<style scoped>
.header {
  display: flex;
}

.logo_img {
  max-width: 187px;
  height: 89px;
  margin-top: 24px;
  margin-left: 50px;
}

.search {
  margin-left: 32px;
  margin-top: 59px;
  display: flex;
}

.input {
  width: 394px;
  height: 52px;
  border: 1px gray;
  box-shadow: 0 0 6px rgba(167, 163, 163, 0.3);
  padding-left: 19px;
  outline: none;
  margin-left: 9px;
}

.btn_add {
  margin-left: 40px;
}
.visitors {
  margin-left: auto;
  margin-top: 40px;
  margin-right: 50px;
  color: #4e3000;
  font-size: 30px;
  line-height: 100%;
  font-weight: 700;
  display: flex;
  flex-direction: column;
  align-items: end;
}

.green-text {
  color: green;
}
.red-text {
  color: red;
}
</style>
