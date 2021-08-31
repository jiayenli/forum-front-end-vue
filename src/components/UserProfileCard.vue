<template>
  <div class="card mb-3">
    <div class="row no-gutters">
      <div class="col-md-4">
        <img
          :src="profile.image"
          width="300px"
          height="300px"
        />
      </div>
      <div class="col-md-8">
        <div class="card-body">
          <h5 class="card-title">{{ profile.name }}</h5>
          <p class="card-text">{{ profile.email }}</p>
          <ul class="list-unstyled list-inline">
            <li>
              <strong>{{ profile.CommentsLength }}</strong> 已評論餐廳
            </li>
            <li>
              <strong>{{ profile.FavoritedRestaurantsLength }}</strong>
              收藏的餐廳
            </li>
            <li>
              <strong>{{ profile.FollowingsLength }}</strong> followings
              (追蹤者)
            </li>
            <li>
              <strong>{{ profile.FollowersLength }}</strong> followers (追隨者)
            </li>
          </ul>
          <p>
            <router-link
              :to= "{name: 'user-edit', params: {id: profile.id}}"
              v-if="currentUser.id === profile.id"
            >
              <button type="submit" class="btn btn-primary">edit</button>
            </router-link>
            <template v-else>
              <button type="submit" class="btn btn-danger" v-if="isFollowed" @click.stop.prevent="deleteFollow">取消追蹤</button>
              <button type="submit" class="btn btn-primary" v-else @click.stop.prevent="addFollow">追蹤</button>
            </template>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    profile: {
      type: Object,
      required: true,
    },
    currentUser: {
      type: Object,
      required: true,
    },
    initialIsFollowed: {
      type: Boolean,
      required: true,
    }
  },
  data() {
    return {
      isFollowed: this.initialIsFollowed
    }
  },
  methods: {
    addFollow() {
      this.isFollowed = true
    },
    deleteFollow() {
      this.isFollowed = false
    }
  }
};
</script>