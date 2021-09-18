<template>
  <header class="main-header">
    <nav>
      <span>Sort users App</span>
    </nav>
  </header>
</template>

<script>
export default {
  name: "Nav",
};
</script>

<style scoped>
.main-header {
  height: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgb(24, 42, 59);
}

.main-header nav {
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.main-header span {
  color: white;
  font-size: 24px;
}
</style>