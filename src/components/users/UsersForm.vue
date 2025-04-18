<template>
  <form @submit.prevent="$emit('submit', user)">
    <div class="form-group">
      <div class="form">
        <label>ФИО</label>
        <input v-model.trim="user.FIO" type="text" class="formInput" />
      </div>

      <div class="form">
        <label>Компания</label>
        <input v-model.trim="user.company" type="text" class="formInput" />
      </div>

      <div class="form">
        <label>Группа</label>
        <select id="group" v-model="user.group" name="group" class="formInput">
          <option value="stranger">Прохожий</option>
          <option value="client">Клиент</option>
          <option value="partner">Партнер</option>
        </select>
      </div>

      <div v-bind:value="user.presence" class="form">
        <label>Присутствие</label>
        <label class="custom-checkbox">
          <input
            type="checkbox"
            class="custom-checkbox"
            v-model="user.presence"
          />
        </label>
      </div>
    </div>
    <add-button class="btn_add" type="submit">Добавить</add-button>
    <button class="btn_close" @click.prevent="$emit('close')">Закрыть</button>
  </form>
</template>

<script>
import AddButton from "@/components/UI/AddButton.vue";
export default {
  components: { AddButton },
  props: {
    user: {
      type: Object,
      required: true,
    },
  },
  methods: {
    handleSubmit() {
      this.$emit("submit", this.user);
    },
  },
};
</script>

<style>
.form-group {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.formInput {
  width: 502px;
  height: 52px;
  border: 1px gray;
  box-shadow: 0 0 6px rgba(167, 163, 163, 0.3);
  padding-left: 19px;
  outline: none;
  margin-top: 15px;
  font-size: 25px;
}

.form {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  margin-top: 20px;
  font-size: 25px;
  color: #4e3000;
  font-weight: 600;
}

.form input {
  margin-left: 100px;
}

.custom-checkbox {
  display: inline-block;
  position: relative;
  padding-left: 35px;
  cursor: pointer;
  margin-left: 100px;
}
.custom-checkbox {
  width: 30px;
  height: 30px;
  position: relative;
  right: 302px;
}

.btn_close {
  width: 273px;
  height: 52px;
  background-color: #737373;
  border-radius: 10px;
  color: white;
  outline: none;
  border: none;
  cursor: pointer;
  font-weight: 400;
  font-size: 24px;
  margin-top: 44px;
  margin-left: 20px;
}
.btn_close:hover {
  background-color: #575656;
}
</style>
