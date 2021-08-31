<template>
  <div class="container py-5">
    <!-- AdminNav Component -->
    <AdminNav />

    <table class="table">
      <thead class="thead-dark">
        <tr>
          <th scope="col">#</th>
          <th scope="col">Email</th>
          <th scope="col">Role</th>
          <th scope="col" width="140">Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users" :key="user.id">
          <th scope="row">{{ user.id }}</th>
          <td>{{ user.email }}</td>
          <td v-if="user.Admin">Admin</td>
          <td v-else>User</td>
          <td>
            <template v-if="user.id!==currentUser.id || !currentUser.isAdmin">
            <button
              v-if="user.Admin"
              type="button"
              class="btn btn-link"
              @click.stop.prevent="ChangeRole(user.id)"
            >
              set as User
            </button>
            <button
              v-else
              type="button"
              class="btn btn-link"
              @click.stop.prevent="ChangeRole(user.id)"
            >
              set as Admin
            </button>
            </template>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import AdminNav from "@/components/AdminNav";
const dummyData = {
  users: [
    {
      id: 1,
      name: "root123",
      email: "root@example.com",
      password: "$2a$10$K2x6pQHkzPEKzw86x8Tc0.bfW7QVdA2Ls4AXBFkFu7xHG3UgA4Mli",
      isAdmin: true,
      image: "https://i.imgur.com/WMsHuNP.jpeg",
      createdAt: "2021-07-05T09:58:39.000Z",
      updatedAt: "2021-08-27T08:16:04.000Z",
    },
    {
      id: 2,
      name: "user1",
      email: "user1@example.com",
      password: "$2a$10$knlgkc6iz7TSC1RADrSjmukYkaQgIc8JSVp1ltz614/F9SK.h/pqa",
      isAdmin: false,
      image: null,
      createdAt: "2021-07-05T09:58:39.000Z",
      updatedAt: "2021-08-21T14:30:09.000Z",
    },
    {
      id: 3,
      name: "user2",
      email: "user2@example.com",
      password: "$2a$10$1UaQ5KZLbMCJztUGRWP/uOtIaKel7TQFHIbozRf4LPysvFLu3UOO6",
      isAdmin: false,
      image: null,
      createdAt: "2021-07-05T09:58:39.000Z",
      updatedAt: "2021-08-21T02:03:29.000Z",
    },
    {
      id: 11,
      name: "root3",
      email: "ryan@gmail.com",
      password: "$2a$10$RlVjZ25mKa8aULENpsmZK.OBFxGUjicjsv2FVnmOXkdtn.yW14oRu",
      isAdmin: false,
      image: null,
      createdAt: "2021-07-05T10:20:05.000Z",
      updatedAt: "2021-07-05T10:32:11.000Z",
    },
    {
      id: 21,
      name: "hans",
      email: "hans@yahoo.com",
      password: "$2a$10$x1t6Xd/2gpTd2VjJHGoBd.NsmIZhv57MvwjMBVsB67qFh0ueCa2ja",
      isAdmin: false,
      image: null,
      createdAt: "2021-07-16T03:24:28.000Z",
      updatedAt: "2021-07-16T03:24:28.000Z",
    },
    {
      id: 31,
      name: "dd",
      email: "dd@dd",
      password: "$2a$10$iWJT2aS0M1DD5IqV2bo.quSOQibm8AHy/mztGRFTBlNz1ep0Vz4XO",
      isAdmin: false,
      image: null,
      createdAt: "2021-08-09T06:02:14.000Z",
      updatedAt: "2021-08-09T06:02:14.000Z",
    },
    {
      id: 41,
      name: "a",
      email: "a@a",
      password: "$2a$10$qPHPuJRtyeuvXclCo1x9nOGhXY140wMbaES5mdwTByqN81Wr/jy1K",
      isAdmin: false,
      image: null,
      createdAt: "2021-08-09T06:05:10.000Z",
      updatedAt: "2021-08-09T06:05:10.000Z",
    },
    {
      id: 51,
      name: "hello",
      email: "hello@example.com",
      password: "$2a$10$050DEPCXf./NI7dEOK7xHeXWiFYD0mZ4Ni99WfV18Uvuz2ujbKyVq",
      isAdmin: false,
      image: null,
      createdAt: "2021-08-22T05:57:25.000Z",
      updatedAt: "2021-08-22T05:57:25.000Z",
    },
    {
      id: 61,
      name: "888",
      email: "888@gmail.com",
      password: "$2a$10$jQbtulJ32N/nk4.1dU44TOzYLQWC7ES169fX49yiDLTNS4Jf0qusa",
      isAdmin: false,
      image: null,
      createdAt: "2021-08-22T06:08:19.000Z",
      updatedAt: "2021-08-22T06:08:19.000Z",
    },
    {
      id: 71,
      name: "424449435",
      email: "424449435@qq.com",
      password: "$2a$10$ubFRYFKcva9dKrYzg9W39OEZIjWwCHrOEILXk7a0oZpcDSTZvmLsG",
      isAdmin: false,
      image: null,
      createdAt: "2021-08-23T07:45:26.000Z",
      updatedAt: "2021-08-23T07:45:26.000Z",
    },
    {
      id: 81,
      name: "test",
      email: "test@example.com",
      password: "$2a$10$w5bcczmxLzWr/lE9a6fgz.toso5IO1oetOBMHZJK/fM3mGAEtsrAK",
      isAdmin: false,
      image: null,
      createdAt: "2021-08-25T11:13:24.000Z",
      updatedAt: "2021-08-25T11:13:24.000Z",
    },
    {
      id: 91,
      name: "cindy",
      email: "cindy@ddd.ddd",
      password: "$2a$10$QXnfafi0Ehr8k3wMdxF.0ufBlHXO7TcZ4rni9wuDrcaybgYe4KkbK",
      isAdmin: false,
      image: null,
      createdAt: "2021-08-31T00:04:19.000Z",
      updatedAt: "2021-08-31T00:04:19.000Z",
    },
  ],
};
const dummyUser = {
  currentUser: {
    id: 1,
    name: "管理者",
    email: "root@example.com",
    image: "https://i.imgur.com/58ImzMM.png",
    isAdmin: true,
  },
  isAuthenticated: true,
};

export default {
  components: {
    AdminNav,
  },
  data() {
    return {
      users: [],
      currentUser:dummyUser.currentUser
    };
  },
  methods: {
    fetchUser() {
      const { users } = dummyData;
      this.users = users.map((user) => ({
        id: user.id,
        email: user.email,
        Admin: user.isAdmin,
      }));
    },
    ChangeRole(UserId) {
      this.users = this.users.map((user) => {
        if (user.id === UserId) {
          return {
            ...user,
            Admin: !user.Admin,
          };
        }
        return user;
      });
    },
  },

  created() {
    this.fetchUser();
  },
};
</script>