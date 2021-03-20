<template>
  <section class="user-list-section">
    <Card>
      <div v-if="users.length">
        <p class="users-found">{{ users.length }} Users found</p>
        <transition-group
          name="user-list"
          tag="ul"
          :css="false"
          v-on:before-enter="beforeEnter"
          v-on:enter="enter"
          v-on:leave="leave"
        >
          <li v-for="(user, index) in users" :key="user.id" :data-index="index">
            <UserArticle :user="user" />
          </li>
        </transition-group>
      </div>
      <div v-else>
        <slot></slot>
      </div>
    </Card>
  </section>
</template>

<script>
import Card from "../components/Card.vue";
import UserArticle from "../components/UserArticle.vue";
import Velocity from "velocity-animate";

export default {
  name: "UserList",
  components: {
    Card,
    UserArticle,
  },
  props: {
    users: Array,
  },
  methods: {
    beforeEnter(el) {
      el.style.opacity = 0;
      el.style.height = 0;
    },
    enter(el, done) {
      var delay = el.dataset.index * 150;
      setTimeout(function () {
        Velocity(el, { opacity: 1, height: "70px" }, { complete: done });
      }, delay);
    },
    leave(el, done) {
      var delay = el.dataset.index * 150;
      setTimeout(function () {
        Velocity(el, { opacity: 0, height: 0 }, { complete: done });
      }, delay);
    },
  },
};
</script>

<style scoped>
.user-list-section {
  display: inline-block;
  width: 50%;
  vertical-align: top;
  padding: 20px 40px;
  box-sizing: border-box;
}

.user-list-section ul {
  list-style: none;
  padding: 0px 10px;
}

.user-list-section li {
  height: 70px;
}

.users-found {
  text-align: center;
}

.user-list-move {
  transition: transform 1s;
}

/* MEDIA QUERIES */
@media only screen and (max-width: 768px) {
  .user-list-section {
    width: 100%;
    display: block;
    padding: 20px;
  }
}
</style>
