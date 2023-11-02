<template>
    <div>
      <input v-model="input" type="text" placeholder="ім'я студента" required />
      <button @click="login">Ввійти</button>
    </div>
  </template>
  <script>
  export default {
    data() {
      return {
        input: '',
      };
    },
    methods: {
      async login() {
        try {
          const response = await this.axios.get(`http://34.82.81.113:3000/students/name/${this.input}`);
          const data = response.data;
          if (data === null || data.name === "CastError") {
            return;
          }
          this.$store.commit('setUser', data);
          this.$router.push('/');
        } catch (error) {
          console.error('Ошибка при выполнении запроса:', error);
        }
      },
    },
  };
  </script>  