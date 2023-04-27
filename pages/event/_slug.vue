<template>
  <div>event</div>
</template>
<script>
export default {
  data: () => ({
    event: {}
  }),
  head() {
    if (!this.event.avatar) {
      this.event.avatar = `https://ui-avatars.com/api/?name=${this.event.name.replace(' ', '+')}`;
    }
    return {
      title: this.event.name,
      meta: [
        { hid: 'ssr-description', name: 'description', content: this.event.bio },
        { hid: 'ssr-avatar', name: 'avatar', content: this.event.avatar },
      ]
    }
  },
  async asyncData(context) {
    console.log(context.params.slug)
    try {
      const response=await context.$axios.get(`parties/event/${context.params.slug}`)
      console.log(response)
      return {
        event: response.data.data
      }
    } catch(e) {
      console.log(e)
      context.error({ statusCode: 404, message: 'User not found' })
    }
  },
}
</script>