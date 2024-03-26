<template>
  <div>
    <p>{{ label }}</p>
    <input
        v-bind="$attrs"
        v-model="value"
        :type="type"
        required
    />
  </div>
</template>

<script>
export default {
  name: "FormInput",
  props: {
    label: {
      type: String,
      default: ''
    },
    type: {
      type: String,
      default: 'text'
    },
    namePost: {
      type: String,
      default: ''
    }
  },
  data() {
    const value = ""
    return {value}
  }
}
</script>

<style scoped>

</style>
