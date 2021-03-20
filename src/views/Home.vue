<template>
  <div class="page-wrapper">
    <Nav />
    <UserFilter
      :filterTerm="filterTerm"
      @input="filterList"
      @sort="sortByAge"
    />
    <UserList :users="filteredUsers">
      <div class="no-users-found">
        <p>No users found</p>
      </div>
    </UserList>
  </div>
</template>

<script>
import Nav from "../components/Nav.vue";
import UserList from "../components/UserList.vue";
import UserFilter from "../components/UserFilter.vue";
import { usersData } from "../data/users";

export default {
  name: "Home",
  components: {
    Nav,
    UserList,
    UserFilter,
  },
  data() {
    return {
      filterTerm: "",
      activeUser: null,
      users: usersData,
    };
  },
  computed: {
    filteredUsers() {
      if (this.filterTerm.length >= 3) {
        return this.users.filter((user) => {
          const fullName = user.firstName + " " + user.lastName;
          return (
            fullName.toLowerCase().indexOf(this.filterTerm.toLowerCase()) !== -1
          );
        });
      } else {
        return this.users;
      }
    },
  },
  watch: {
    activeUser: function (activeUser) {
      for (const user of this.users) {
        if (user.id == activeUser.id) {
          this.$set(user, "active", true);
        } else {
          this.$set(user, "active", false);
        }
      }
    },
  },
  methods: {
    filterList(value) {
      this.filterTerm = value;
    },
    sortByAge() {
      this.users = this.users.sort((a, b) => a.age - b.age);
    },
  },
  created() {
    // Pub Sub
    this.$eventBus.$on("viewDetails", (user) => {
      this.activeUser = user;
    });
  },
  destroyed() {
    this.$eventBus.$off("viewDetails");
  },
};
</script>

<style scoped>
.no-users-found {
  min-height: 115px;
  text-align: center;
}
</style>
