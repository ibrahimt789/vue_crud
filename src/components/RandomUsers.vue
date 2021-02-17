<template>
  <h2>Hello from Users Page</h2>
  <button @click="showUsers()" class="bg-green-500 active:bg-green-700">
    Random User
  </button>
  <template v-if="isUserAvailable">
    <figure class="md:flex bg-gray-100 rounded-xl p-8 md:p-0">
      <img
        class="w-32 h-32 md:w-48 md:h-auto md:rounded-none rounded-full mx-auto"
        :srcset="getPicture()"
        alt=""
        width="384"
        height="512"
      />
      <div class="pt-6 md:p-8 text-center md:text-left space-y-4">
        <figcaption class="font-medium">
          <div class="text-cyan-600">
            {{ getFullName }}
          </div>
          <div class="text-gray-500">
            <span class="">email - {{ user.email }}</span>
          </div>
        </figcaption>
      </div>
    </figure>
  </template>
</template>
<script>
import axios from "axios";
export default {
  name: "Users",
  data() {
    return {
      user: {},
    };
  },
  computed: {
    getFullName() {
      const user = this.user;
      console.log(user);
      if (user && Object.keys(user).length > 0) {
        const { name } = user;
        return `${name.title} ${name.first} ${name.last}`;
      } else {
        return "temp";
      }
    },
    isUserAvailable() {
      return this.user && Object.keys(this.user).length > 0 ? true : false;
    },
  },
  mounted() {
    this.getusers();
  },
  methods: {
    getPicture: function () {
      const { picture } = this.user;
      return `${picture.large}`;
    },
    showUsers: function () {
      this.getusers();
    },
    getusers: async function () {
      // fetch initially to have better UI transition
      const result = await axios.get("https://randomuser.me/api/", {
        params: { dataType: "json" },
      });
      console.log(this.user);
      if (result.data && result.status == 200) {
        // it will always return 1 data
        const { results } = result.data;
        this.user = results[0];
      }
    },
  },
};
</script>