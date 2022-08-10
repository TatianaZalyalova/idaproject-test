<template>
  <nuxt />
</template>

<script>
export default {
  computed: {
    meta() {
      return [
        { charset: 'utf-8' },
        {
          name: 'viewport',
          content:
            'width=device-width, initial-scale=1, maximum-scale=1 shrink-to-fit=no',
        },
        {
          hid: 'description',
          name: 'description',
          content: 'Тестовое задание',
        },
      ]
    },
  },

  head() {
    return {
      meta: [...this.meta],
    }
  },
}
</script>
