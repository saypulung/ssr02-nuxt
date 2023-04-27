<template>
  <div>
    <div>{{ user.name }}</div>
    <div>{{ user.description }}</div>
  </div>
</template>
<script>
export default {
  data: () => ({
    user: {}
  }),
  head() {
    if (!this.user.avatar) {
      this.user.avatar = `https://ui-avatars.com/api/?name=${this.user.name.replace(' ', '+')}`;
    }
    return {
      title: this.user.name,
      meta: [
        { hid: 'ssr-description', name: 'description', content: this.user.bio },
        { hid: 'ssr-avatar', name: 'avatar', content: this.user.avatar },
      ]
    }
  },
  async asyncData(context) {
    console.log(context.params.slug)
    try {
      const response=await context.$axios.get(`parties/user/${context.params.slug}`)
      console.log(response)
      return {
        user: response.data.data
      }
    } catch(e) {
      console.log(e)
      context.error({ statusCode: 404, message: 'User not found' })
    }
  },
}
</script>