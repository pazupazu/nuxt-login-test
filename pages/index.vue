<template>
  <div>
    <template v-if="!$store.state.authUser">
      <login></login>
    </template>
    <template v-else>
      <p>indexじゃ</p>
      <button>ログアウト</button>
    </template>
  </div>
</template>


<script>
import login from '@/components/login'

export default {
  components: {
    login
  },
  data() {
    return {
      error: null,
      formUsername: '',
      formPassword: ''
    }
  },
  methods: {
    async logout () {
      try {
        await this.$store.dispatch('logout')
      } catch (e) {
        this.error = e.message
      }
    }
  }
}
</script>

<style lang="scss">
  .login-form {
    min-height: 100vh;
    @apply bg-gray-100 py-20;
    .container {
      text-align: left;
      display: block;
      min-height: auto;
      @apply bg-white p-4 mx-auto max-w-md shadow-md rounded;
      .error-notice {
        @apply text-red-500 bg-red-100 p-2 rounded border border-red-400 text-sm font-bold mb-4
      }
      .input {
        @apply shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight;
        &:focus {
          @apply outline-none shadow-outline
        }
      }
      .button {
        @apply bg-blue-500 text-white font-bold py-2 px-4 text-center rounded;
        cursor: pointer;
        transition: 0.2s;
        &:hover {
          @apply bg-blue-600
        }
        &:focus {
          @apply outline-none shadow-outline;
        }
      }
    }
  }
</style>
