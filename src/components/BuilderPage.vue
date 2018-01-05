<template>
  <div class="page builder-page">
    <builder-form
      :init-width="width"
      :init-height="height"
      @rebuild="rebuildGrid"
      @mode="onToggleMode"
    />
    <builder-grid
      :grid-width="width"
      :grid-height="height"
      :blanks="blanks"
      :is-edit-blanks="isEditBlanks"
      @updateblanks="onBlanksUpdate"
    />
  </div>
</template>

<script>
import BuilderGrid from './BuilderGrid'
import BuilderForm from './BuilderForm'
  
export default {
  name: 'BuilderPage',

  components: { BuilderForm, BuilderGrid },

  data: () => ({
    width: 10,
    height: 10,
    blanks: [],
    isEditBlanks: true,
  }),

  methods: {
    rebuildGrid (payload) {
      this.width = payload.width
      this.height = payload.height
    },

    onToggleMode (payload) {
      this.isEditBlanks = payload
      document.body.style.background = payload ? '#222' : '#fff'
    },

    onBlanksUpdate (id) {
      if (!this.blanks.includes(id)) {
        return this.blanks.push(id)
      }

      this.blanks = this.blanks.filter(i => i !== id)
    },
  },
}
</script>