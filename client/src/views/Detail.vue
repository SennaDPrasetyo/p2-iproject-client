<template>
    <section v-if="oneDesign" id="detail-page">
        <br>
        <div class="container mx-auto px-6">
            <div class="md:flex md:items-center">
                <div class="swiper flex overflow-x-scroll w-1/2">
                  <img class="w-full h-1/2 object-cover bg-gray-300" :src="`${oneDesign.image1}`" id="slide1">
                  <img class="w-full h-1/2 object-cover bg-gray-300" :src="`${oneDesign.image2}`" id="slide2">
                  <img class="w-full h-1/2 object-cover bg-gray-300" :src="`${oneDesign.image3}`" id="slide3">
                </div>
                <div class="w-full max-w-lg mx-auto mt-5 md:ml-8 md:mt-0 md:w-1/2">
                    <h3 class="text-gray-700 text-3xl">{{ oneDesign.name }}</h3><br>
                    <span class="text-gray-700 text-base">{{ oneDesign.description }}</span>
                    <hr class="my-3">
                    <div class="mt-2">
                        <label class="text-gray-500 text-sm" for="count">design by {{ oneDesign.User.email }}</label>
                    </div>
                    <div class="flex items-center mt-6">
                        <button @click.prevent="toSmsForm" v-if="isCustomer" class="px-8 py-2 bg-indigo-600 text-white text-sm font-medium
                        rounded hover:bg-indigo-500 focus:outline-none focus:bg-indigo-500">Send Me a Message</button>
                        <span v-if="isCustomer" class="ml-2 text-gray-500 text-sm"> or </span>
                        <button @click.prevent="toEmailForm" v-if="isCustomer" class="px-8 py-2 bg-indigo-600 text-white text-sm font-medium
                        rounded ml-2 hover:bg-indigo-500 focus:outline-none focus:bg-indigo-500">Email Me</button>
                        <button v-if="isCustomer" @click.prevent="addBookmark(oneDesign.id)" class="mx-2 text-gray-600 border rounded-md p-2 hover:bg-gray-200 focus:outline-none">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                                <path fill-rule="evenodd" d="M3.172 5.172a4 4 0 015.656 0L10 6.343l1.172-1.171a4 4 0 115.656 5.656L10 17.657l-6.828-6.829a4 4 0 010-5.656z" clip-rule="evenodd" />
                            </svg>
                        </button>
                        <button @click="toEdit(oneDesign.id)" v-if="isLoggedIn && !isCustomer" class="px-8 py-2 bg-indigo-600 text-white text-sm font-medium
                        rounded hover:bg-indigo-500 focus:outline-none focus:bg-indigo-500">Edit</button>
                        <button v-if="isLoggedIn && !isCustomer" @click.prevent="deleteDesign(oneDesign.id)" class="mx-2 text-gray-600 border rounded-md p-2 hover:bg-gray-200 focus:outline-none">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16" />
                            </svg>
                        </button>
                    </div>
                </div>
            </div>
        </div>
        <br>
    </section>
</template>

<script>
import swal from 'sweetalert'

export default {
  name: 'Detail',
  computed: {
    oneDesign () {
      return this.$store.state.oneDesign
    },
    isCustomer () {
      return this.$store.state.isCustomer
    },
    isLoggedIn () {
      return this.$store.state.isLoggedIn
    }
  },
  methods: {
    getOneDesign () {
      const id = this.$route.params.id
      this.$store.dispatch('getOneDesign', id)
    },
    addBookmark (id) {
      if (!localStorage.access_token) {
        this.$router.push({ name: 'Login' })
        swal('Please login first')
      } else {
        this.$store.dispatch('addBookmark', id)
      }
    },
    deleteDesign (id) {
      this.$store.dispatch('deleteDesign', id)
    },
    toEdit (id) {
      this.$router.push({ name: 'EditDesign', params: { id: id } }).catch(() => {})
    },
    toEmailForm () {
      if (!localStorage.access_token) {
        this.$router.push({ name: 'Login' })
        swal('Please login first')
      } else {
        const id = this.$route.params.id
        this.$router.push({ name: 'EmailForm', params: { id: id } }).catch(() => {})
      }
    },
    toSmsForm () {
      if (!localStorage.access_token) {
        this.$router.push({ name: 'Login' })
        swal('Please login first')
      } else {
        const id = this.$route.params.id
        this.$router.push({ name: 'SmsForm', params: { id: id } }).catch(() => {})
      }
    }
  },
  created () {
    this.getOneDesign()
  }
}
</script>

<style>

</style>
