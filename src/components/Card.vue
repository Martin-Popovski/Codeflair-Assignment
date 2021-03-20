<template>
  <div class="card-body">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "Card",
};
</script>


<style>
.card-body {
  background-color: white;
  padding: 15px;
  box-shadow: 0px 2px 12px #b9b9b9;
  border-radius: 10px;
  width: 100%;
  box-sizing: border-box;
}
</style>
