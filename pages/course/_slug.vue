<template>
  <div>
    {{ course.name }}
  </div>
</template>
<script>
export default {
  data: () => ({
    course: {}
  }),
  head() {
    if (!this.course.avatar) {
      this.course.avatar = `https://ui-avatars.com/api/?name=${this.course.name.replace(' ', '+')}`;
    }
    return {
      title: this.course.name,
      meta: [
        { hid: 'ssr-description', name: 'description', content: this.course.bio },
        { hid: 'ssr-avatar', name: 'avatar', content: this.course.avatar },
      ]
    }
  },
  async asyncData(context) {
    console.log(context.params.slug)
    try {
      const response=await context.$axios.get(`parties/course/${context.params.slug}`)
      console.log(response)
      return {
        course: response.data.data
      }
    } catch(e) {
      console.log(e)
      context.error({ statusCode: 404, message: 'User not found' })
    }
  },
}
</script>