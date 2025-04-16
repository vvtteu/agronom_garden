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
        <tbody v-for="user in users">
          <tr >
            <td>{{ user.number }}</td>
            <td>{{ user.FIO }}</td>
            <td> {{ user.company }}</td>
            <td> {{ user.group }}</td>
            <td> {{ user.presence }}</td>
          </tr>
        </tbody>
      </table>
    </div>
</template>

<script>
export default {
    props: {
        users: {
            type: Array,
            required: true
        }
    }
}
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
  border-bottom: 3px solid #E9E9E9;
  color: #4E3000;
  font-size: 20px;
}

.custom-table th, .custom-table td {
  padding: 8px 12px;
  text-align: left;
}
</style>