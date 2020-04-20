<template>
  <div v-if="displayText" class="card">
    <CopyButton :text="text" />
    {{ displayText }}
  </div>
</template>

<script>
import CopyButton from './CopyButton'

export default {
  props: {
    displayText: {
      type: String,
      required: true,
    },
    text: {
      type: String,
      required: true,
    },
  },
  components: {
    CopyButton,
  },
}
</script>

<style scoped></style>
