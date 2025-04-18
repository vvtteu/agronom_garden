<template>
  <button>
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: "addButton",
};
</script>

<style>
.btn_add {
  width: 273px;
  height: 52px;
  background-color: #4caf50;
  border-radius: 10px;
  color: white;
  outline: none;
  border: none;
  cursor: pointer;
  font-weight: 400;
  font-size: 24px;
}

.btn_add:hover {
  background-color: #45a049;
}
</style>
