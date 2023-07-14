<template>
  <input v-model="state.firstName" /><br />
  <input v-model="state.contact[0].email" /><br />
  <input v-model="state.contact[0].password" /><br />
  <button @click="v$.$validate()">Validate</button><br />
  Password errors {{ v$.contact.$errors[0]?.$response.$errors }} <br />
</template>

<script setup>
import { reactive } from "vue"; // "from '@vue/composition-api'" if you are using Vue <2.7
import { useVuelidate } from "@vuelidate/core";
import { required, email, helpers } from "@vuelidate/validators";

const state = reactive({
  firstName: "",
  contact: [
    {
      email: "",
      password: "",
    },
  ],
});
const rules = {
  firstName: { required }, // Matches state.firstName
  contact: {
    $each: helpers.forEach({
      email: { required },
      password: { required },
    }),
  },
};

const v$ = useVuelidate(rules, state);
</script>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
