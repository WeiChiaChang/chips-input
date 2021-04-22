<template>
  <span contenteditable="true" @input="update" />
</template>

<script>
export default {
  name: 'Editable',
  props:['content'],
  methods: {
    update(event) {
      this.$emit('update', event.target.innerText)
    }
  },
  mounted() {
    this.$el.innerText = this.content
  },
}
</script>
