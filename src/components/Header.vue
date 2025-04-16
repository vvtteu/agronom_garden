<template>
<header>
    <div class="header">
        <img class="logo_img" src="../assets/logo.png" alt="logo">
        <div class="search">
        <input type="text" class="input" placeholder="Поиск по имени">
        <input type="text" class="input" placeholder="Поиск по компании">
        <input @click="showForm = true" type="button" class="btn_add" value="Добавить">
        </div>
        <div class="visitors">
        <p>Посетители</p>
        <span>
            <span class="green-text">280</span> / <span class="red-text">35</span>
        </span>
        </div>
        <div v-if="showForm" class="modal-overlay">
            <div class="modal-content">
                <form @submit.prevent="addUser">
                    <div class="form-group">
                        <div class="formm">
                            <label>ФИО</label>
                            <input
                              v-model="user.FIO"
                              type="text"
                              class="formInput" />
                        </div>
                        
                        <div class="formm">
                            <label>Компания</label>
                            <input 
                              v-model="user.company"
                              type="text" 
                              class="formInput" />
                        </div>
                        
                        <div class="formm">
                            <label>Группа</label>
                            <select 
                            id="group" 
                            v-model="user.group" 
                            name="group" 
                            class="formInput">
                                <option value="stranger">Прохожий</option>
                                <option value="client">Клиент</option>
                                <option value="partner">Партнер</option>
                            </select>
                        </div>
                        
                        <div 
                        v-bind:value="user.presence"
                        
                        class="formm"
                        >
                            <label>Присутствие</label>
                            <input type="checkbox" v-model="user.presence"/>
                        </div>
                    </div>
                    <button type="submit">Добавить</button>
                    <button @click="showForm = false">Закрыть</button>
                </form>
                
                
            </div>
        </div>
    </div>

  
</header>
    
</template>

<script>
export default {
    props: {
            addUser: {
                type: Function,
                required: true
            }
        },
  data() {
    return {
      user: {
        FIO: '',
        company: '',
        group: '',
        presence: false,
        
      },
    showForm: false,
    };
},
    methods: {
        addUser() {
            this.$props.addUser({ ...this.user });
            this.user.number += 1;
            this.user.FIO = '';
            this.user.company = '';
            this.user.group = '';
            this.user.presence = false;
            this.showForm = false;
        },
        
    }
    }

</script>

<style scoped>
.modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0,0,0,0.5);
    display: flex;
    justify-content: center;
    align-items: center;
}

.modal-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 1461px;
    height: 581px;
    background: white;
    padding: 20px;
    border-radius: 8px;
    
}

.form-group {
    display: flex;
    flex-direction: column;
}

.formInput {
    width: 502px;
    height: 52px;
    border: 1px gray;
    box-shadow: 0 0 6px rgba(167, 163, 163, 0.3);
    padding-left: 19px;
    outline: none;
    margin-top: 15px;
}

.formm {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    margin-top: 20px;
}

.formm input {
    margin-left: 100px;

}

.header {
  display: flex;
}

.logo_img {
  width: 187px;
  height: 89px;
  margin-top: 24px;
  margin-left: 50px;
}

.search {
  margin-left: 32px;
  margin-top: 59px;
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
  width: 273px;
  height: 52px;
  margin-left: 40px;
  background-color: #4CAF50;
  border-radius: 10px;
  color: white;
  outline: none;
  border: none;
  cursor: pointer;
  font-weight: 400px;
  font-size: 24px;
}

.btn_add:hover {
  background-color: #45a049;
}

.visitors {
  margin-left: auto;
  margin-top: 28px;
  margin-right: 50px;
  color: #4E3000;
  font-size: 30px;
  line-height: 100%;
  font-family: Open Sans;
  font-weight: 700;
  gap: 5px;
}

.green-text {
color: green;
}
.red-text {
color: red;
}
</style>