<template>
  <div>{{ institute.name }}</div>
</template>
<script>
export default {
  data: () => ({
    institute: {}
  }),
  head() {
    if (!this.institute.avatar) {
      this.institute.avatar = `https://ui-avatars.com/api/?name=${this.institute.name.replace(' ', '+')}`;
    }
    return {
      title: this.institute.name,
      meta: [
        { hid: 'ssr-description', name: 'description', content: this.institute.bio },
        { hid: 'ssr-avatar', name: 'avatar', content: this.institute.avatar },
      ]
    }
  },
  async asyncData(context) {
    console.log(context.params.slug)
    try {
      const response=await context.$axios.get(`parties/institute/${context.params.slug}`)
      return {
        institute: response.data.data
      }
    } catch(e) {
      console.log(e)
      context.error({ statusCode: 404, message: 'Institute not found' })
    }
  },
}
</script>