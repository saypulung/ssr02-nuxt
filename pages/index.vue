<template>
  <Tutorial :parties="parties"/>
</template>

<script>
export default {
  name: 'IndexPage',
  data: () => ({
    parties: {
      users: [],
      organisations: [],
      events: [],
      institutes: [],
      courses: [],
    },
  }),
  async asyncData(context) {
    const response = await context.$axios.get('parties');
    if (response) {
      return {
        parties: response.data
      }
    }
  }
}
</script>
