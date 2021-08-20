<template>
  <div>
    <h2>
      Login
    </h2>

    <form @submit.prevent="onSubmit">
      <input v-model="form.email" class="border p-1" placeholder="Email Address">
      <input v-model="form.password" type="password" class="border p-1" placeholder="Password">
      <button type="submit" class="bg-blue-500 text-white py-1 px-3">
        Login
      </button>
    </form>

    <h3>Errors</h3>
    <code>{{ errors }}</code>
  </div>
</template>

<script>
export default {
  middleware: ['auth'],
  auth: 'guest',

  data () {
    return {
      form: {
        email: '',
        password: ''
      },

      errors: {}
    }
  },

  methods: {
    onSubmit () {
      this.$auth.loginWith('local', { data: this.form })
        .catch((error) => {
          this.errors = error.response.data.errors
        })
    }
  }
}
</script>
