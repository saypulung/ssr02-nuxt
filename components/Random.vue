<template>
  <div>
    <h3>Random data</h3>
    <div
      v-for="(ran, id) in random"
      :key="id">
      {{ ran }}
    </div>
  </div>
</template>
<script>

export default {
  name: 'Random',
  data: () => ({
    random: [],
  }),
  created() {
    this.loadRand()
  },
  methods: {
    async loadRand() {
      const resp = await this.$axios.get('random');
      if (resp) {
        this.random = resp.data.random
      }
    }
  }
}
</script>