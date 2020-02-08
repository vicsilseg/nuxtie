<template>
  <div>
    <img style="width: 500px; height: 500px" src="~/assets/eye.png" alt="eye" />
    <div class="title">
      <h1>Oops, it is a {{ error.statusCode }}</h1>
      {{ message }}
    </div>
    <p v-if="statusCode === 404">
      <nuxt-link to="/">
        Return to homepage
      </nuxt-link>
    </p>
  </div>
</template>

<script>
export default {
  props: {
    error: {
      type: Object,
      default: null
    }
  },
  head() {
    return {
      title: this.message
    }
  },
  computed: {
    statusCode() {
      return (this.error && this.error.statusCode) || 500
    },
    message() {
      return this.error.message
    }
  }
}
</script>
