<template>
  <div class="mb-3">
    <h1>餐廳後台</h1>
    <router-link :to="{name: 'admin-restaurants'}" class="btn btn-link">Restaurants</router-link> |
    <router-link :to="{name: 'admin-categories'}" class="btn btn-link">Categories</router-link> |
    <router-link :to="{name: 'admin-users'}" class="btn btn-link">Users</router-link>
  </div>
</template>

<script>
export default {
 name: 'AdminNav'

}
</script>