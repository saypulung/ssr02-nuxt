<template>
  <div>
    {{ event.name }}
    <random/>
  </div>
</template>
<script>
import Random from '@/components/Random'
export default {
  components: { Random },
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
      return {
        event: response.data.data
      }
    } catch(e) {
      console.log(e)
      context.error({ statusCode: 404, message: 'Event not found' })
    }
  },
}
</script>