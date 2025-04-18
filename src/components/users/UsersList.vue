<template>
  <div class="table">
    <table class="custom-table">
      <thead>
        <tr>
          <th>Номер</th>
          <th>ФИО</th>
          <th>Компания</th>
          <th>Группа</th>
          <th>Присутствие</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users" :key="user.number" @click="editUser(user)">
          <td>{{ user.number }}</td>
          <td>{{ user.FIO }}</td>
          <td>{{ user.company }}</td>
          <td>{{ groupNames[user.group] || user.group }}</td>
          <td>
            <img
              v-if="user.presence"
              class="circle"
              src="@/assets/green-circle.png"
              alt="Присутствует"
            />
            <img
              v-else
              class="circle"
              src="@/assets/red-circle.png"
              alt="Не присутствует"
            />
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import DialogBox from "../UI/DialogBox.vue";

export default {
  data() {
    return {
      groupNames: {
        stranger: "Прохожий",
        client: "Клиент",
        partner: "Партнер",
      },
    };
  },

  components: {
    DialogBox,
  },
  props: ["users"],
  methods: {
    editUser(user) {
      this.$emit("edit-user", user);
    },
  },
};
</script>

<style scoped>
.table {
  display: flex;
  justify-content: center;
  margin-top: 34px;
}

.custom-table {
  width: 95%;
  border-collapse: collapse;
}

.custom-table thead {
  height: 34px;
  border-bottom: 3px solid #e9e9e9;
  color: #4e3000;
  font-size: 20px;
}

.custom-table th:last-child,
.custom-table td:last-child {
  text-align: right;
  padding-right: 20px;
  width: 10px;
}

.custom-table th,
.custom-table td {
  padding: 8px 12px;
  text-align: left;
}

.custom-table td {
  font-size: 30px;
}

.circle {
  width: 59px;
  height: 59px;
}
</style>
