<template>
  <section class="user-filter-section">
    <Card>
      <label for="input-field">Filter Users by Name</label>
      <input
        type="text"
        :value="filterValue"
        @input="$emit('input', $event.target.value)"
        id="input-field"
      />
      <button class="filter-button" @click="$emit('sort')">
        Sort by Age (the youngest first)
      </button>
    </Card>
  </section>
</template>

<script>
import Card from "../components/Card.vue";
export default {
  name: "UserFilter",
  components: {
    Card,
  },
  props: {
    filterValue: String,
  },
};
</script>

<style scoped>
.user-filter-section {
  width: 50%;
  display: inline-block;
  padding: 20px 40px;
  box-sizing: border-box;
}

label {
  font-weight: bold;
  font-size: 15px;
  display: block;
  cursor: pointer;
}

#input-field {
  padding: 10px 15px;
  margin-top: 10px;
  width: 200px;
  box-sizing: border-box;
  border-radius: 5px;
}

#input-field:focus {
  outline: none;
}

.filter-button {
  display: block;
  margin-top: 20px;
  padding: 12px 5px;
  box-sizing: border-box;
  width: 200px;
  color: white;
  background-color: rgb(24, 42, 59);
  border-radius: 5px;
  cursor: pointer;
}

/* MEDIA QUERIES */
@media only screen and (max-width: 768px) {
  .user-filter-section {
    width: 100%;
    display: block;
    padding: 20px;
  }

  #input-field {
    width: 100%;
  }
}
</style>
