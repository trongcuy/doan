<template>
  <div class="create">
    <the-header />

    <div class="create__container">
      <content-left />
      <content-right />
    </div>
  </div>
</template>

<script>
import ContentLeft from './content/content-left.vue'
import ContentRight from './content/content-right.vue'
import TheHeader from './the-header.vue'
import { onBeforeUnmount } from 'vue'
import { useStore } from 'vuex'
export default {
  components: {
    TheHeader,
    ContentLeft,
    ContentRight
  },

  setup () {
    const store = useStore()

    onBeforeUnmount(() => {
      store.commit('supplier/setSupplier', {})
    })
  }

}
</script>

<style lang="scss" scoped>
.create {
  &__container {
    display: grid;
    grid-template-columns: 2fr 1fr;
    grid-column-gap: 24px;
  }
}
</style>
