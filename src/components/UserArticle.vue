<template>
  <article class="user">
    <button class="user__trigger" @click="viewDetails">
      <div class="user__image"><img :src="user.img" alt="user" /></div>
      <div class="user__info" v-if="!user.active">
        <h2>{{ user.firstName + " " + user.lastName }}</h2>
        <p class="user__age">{{ user.age }}</p>
      </div>
      <div class="user__extra-info" v-else>
        <p>{{ user.details }}</p>
      </div>
    </button>
  </article>
</template>

<script>
export default {
  name: "UserArticle",
  props: {
    user: Object,
  },
  methods: {
    viewDetails() {
      this.$eventBus.$emit("viewDetails", this.user);
    },
  },
};
</script>


<style scoped>
h2 {
  font-weight: bold;
  font-size: 1.2rem;
  margin-bottom: 5px;
}

.user__image {
  flex-basis: 50px;
  margin-right: 10px;
  flex-shrink: 0;
  width: 50px;
  height: 50px;
  overflow: hidden;
  border-radius: 50%;
}

.user__image img {
  object-fit: cover;
  width: 100%;
  height: 100%;
  display: block;
}

.user__trigger {
  display: flex;
  width: 100%;
  align-items: center;
  background: transparent;
  border: 0;
  padding: 0;
  text-align: left;
  margin-bottom: 15px;
  cursor: pointer;
}
.user__trigger:focus {
  outline: none;
}

.user__age {
  font-size: 0.8rem;
  color: gray;
  font-weight: bold;
  letter-spacing: 1px;
}

.user__extra-info {
  height: 78px;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
}
</style>
