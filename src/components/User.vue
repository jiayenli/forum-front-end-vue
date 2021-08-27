<template>
  <div class="container py-5">
    <NavTabs />
   
    <div class="row text-center">
      <div v-for="user in users" class="col-3" :key="user.id">
        <router-link to="/">
          <img
            :src="
              user.image
                ? user.image
                : 'http://via.placeholder.com/300x300?text=No+Image'
            "
            width="140px"
            height="140px"
          />
        </router-link>
        <h2>User</h2>
        <span class="badge badge-secondary"
          >追蹤人數：{{ user.FollowerCount }}</span
        >
        <p class="mt-3">
          <button
            type="button"
            class="btn btn-danger"
            v-if="user.isFollowed"
            @click.stop.prevent="deleteFollowed(user)"
          >
            取消追蹤
          </button>
          <button
            type="button"
            class="btn btn-primary"
            v-else
            @click.stop.prevent="addFollowed(user)"
          >
            追蹤
          </button>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    initialUser: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      users: this.initialUser,
    };
  },
  methods: {
    addFollowed(user) {
      user.isFollowed = true
    },
    deleteFollowed(user) {
     user.isFollowed = false
    },
  },
};
</script>