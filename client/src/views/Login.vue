<template>
  <section id="login-page">
        <div class="flex items-center min-h-screen dark:bg-gray-900">
          <div class="container mx-auto">
              <div class="max-w-md mx-auto my-10">
                  <div class="text-center">
                      <h1 class="my-3 text-3xl font-semibold text-gray-700 dark:text-gray-200">Sign in</h1>
                  </div>
                  <div class="m-7">
                      <form @submit.prevent="login">
                          <div class="mb-6">
                              <label for="email" class="block mb-2 text-sm text-gray-600 dark:text-gray-400">Email Address</label>
                              <input v-model="email" type="email" name="emailLogin" id="emailLogin"
                              placeholder="example@mail.com"
                              class="w-full px-3 py-2 placeholder-gray-300 border
                              border-gray-300 rounded-md focus:outline-none
                              focus:ring focus:ring-indigo-100 focus:border-indigo-300
                              dark:bg-gray-700 dark:text-white dark:placeholder-gray-500 dark:border-gray-600 dark:focus:ring-gray-900 dark:focus:border-gray-500" />
                          </div>
                          <div class="mb-6">
                              <div class="flex justify-between mb-2">
                                  <label for="password" class="text-sm text-gray-600 dark:text-gray-400">Password</label>
                              </div>
                              <input v-model="password" type="password" name="passwordLogin" id="passwordLogin" placeholder="Password"
                              class="w-full px-3 py-2 placeholder-gray-300 border border-gray-300 rounded-md
                              focus:outline-none focus:ring focus:ring-indigo-100 focus:border-indigo-300
                              dark:bg-gray-700 dark:text-white dark:placeholder-gray-500 dark:border-gray-600 dark:focus:ring-gray-900 dark:focus:border-gray-500" />
                          </div>
                          <div class="mb-6">
                              <button type="submit" class="w-full px-3 py-4 text-white bg-indigo-500 rounded-md focus:bg-indigo-600 focus:outline-none">Sign in</button>
                          </div>
                          <p class="text-sm text-center text-gray-400">Don&#x27;t have an account yet?
                              <a @click.prevent="toRegister" href="" class="text-indigo-400 focus:outline-none focus:underline
                              focus:text-indigo-500 dark:focus:border-indigo-800">Sign up</a></p>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
export default {
  name: 'Login',
  data () {
    return {
      email: '',
      password: ''
    }
  },
  methods: {
    login () {
      const input = {
        email: this.email,
        password: this.password
      }

      this.$store.dispatch('login', input)
    },
    toRegister () {
      this.$router.push({ name: 'RegisterCust' })
    }
  }
}
</script>

<style>

</style>
