<template>
  <div>
    <h1 class="text-center">Register</h1>
    <form @submit.prevent="onRegister">
      <div class="flex flex-col items-center">
        <div>
          <input class="input" type="text" placeholder="Meno" v-model="name" />
        </div>
        <div>
          <input
            class="input"
            type="email"
            placeholder="email"
            v-model="email"
          />
        </div>
        <div>
          <input class="input" type="number" placeholder="vek" v-model="age" />
        </div>
        <div>
          <input
            class="input"
            type="password"
            placeholder="heslo"
            v-model="password"
          />
        </div>
        <div>
          <input
            class="input"
            type="password"
            placeholder="zopakujte heslo"
            v-model="passwordConfirmation"
          />
        </div>
        <div class="submit-btn">
          <button>Registrovat sa</button>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      name: "",
      email: "",
      age: null,
      password: "",
      passwordConfirmation: "",
    };
  },
  methods: {
    onRegister() {
      axios
        .post(`/api/register`, {
          name: this.name,
          email: this.email,
          age: this.age,
          password: this.password,
          password_confirmation: this.passwordConfirmation,
        })
        .then((response) => {
          console.log(response);
        });
    },
  },
};
</script>

<style>
.input {
  @apply border rounded-lg border-black p-1 my-2;
}
.submit-btn {
  @apply bg-purple-primary text-gray-50 py-2 px-4 rounded-lg mt-4 cursor-pointer;
}
</style>
