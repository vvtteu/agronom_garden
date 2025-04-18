<template>
  <div class="fixed-filter-container">
    <div class="users-filter">
      <span class="filter-label">Фильтровать по: </span>
      <span
        class="filter-option"
        :class="{ active: filterStatus === 'all' }"
        @click="setFilter('all')"
      >
        Без фильтра
      </span>
      <span
        class="filter-option"
        :class="{ active: filterStatus === 'present' }"
        @click="setFilter('present')"
      >
        Присутствующим
      </span>
      <span
        class="filter-option"
        :class="{ active: filterStatus === 'absent' }"
        @click="setFilter('absent')"
      >
        Отсутствующим
      </span>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      filterStatus: "all",
    };
  },
  methods: {
    setFilter(status) {
      this.filterStatus = status;
      const filterValue = status === "all" ? null : status === "present";
      this.$emit("filter-users", filterValue);
    },
  },
};
</script>

<style scoped>
.fixed-filter-container {
  position: fixed;
  bottom: 0;
  left: 0;
  background: white;
  padding: 15px 0;
  z-index: 1000;
}
.users-filter {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  gap: 15px;
  padding: 0 20px;
}

.filter-label {
  font-weight: bold;
  color: #4e3000;
  font-size: 25px;
}

.filter-option {
  padding: 5px 10px;
  cursor: pointer;
  border-radius: 4px;
  transition: all 0.3s;
  font-size: 20px;
}

.filter-option:hover {
  background: #e0e0e0;
  border-radius: 20px;
}

.filter-option.active {
  background: #c4c4c4;
  border-radius: 20px;
  color: white;
  font-weight: bold;
}
</style>
