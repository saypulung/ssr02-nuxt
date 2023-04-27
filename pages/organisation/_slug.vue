<template>
  <div>organisation</div>
</template>
<script>
export default {
  data: () => ({
    organisation: {}
  }),
  head() {
    if (!this.organisation.avatar) {
      this.organisation.avatar = `https://ui-avatars.com/api/?name=${this.organisation.name.replace(' ', '+')}`;
    }
    return {
      title: this.organisation.name,
      meta: [
        { hid: 'ssr-description', name: 'description', content: this.organisation.bio },
        { hid: 'ssr-avatar', name: 'avatar', content: this.organisation.avatar },
      ]
    }
  },
  async asyncData(context) {
    console.log(context.params.slug)
    try {
      const response=await context.$axios.get(`parties/organisation/${context.params.slug}`)
      console.log(response)
      return {
        organisation: response.data.data
      }
    } catch(e) {
      console.log(e)
      context.error({ statusCode: 404, message: 'User not found' })
    }
  },
}
</script>