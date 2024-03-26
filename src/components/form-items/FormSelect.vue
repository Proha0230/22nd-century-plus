<template>
  <div>
    <p>{{ label }}</p>
    <select v-model="value">
      <option
        v-for="option in options"
        :key="option.value"
        :selected="option.selected"
      >{{ option.text }}</option>
    </select>
  </div>
</template>

<script>
export default {
  name: "FormSelect",
  props: {
    label: {
      type: String,
      default: ''
    },

    options: {
      type: Object,
      required: true
    },
    namePost: {
      type: String,
      default: ''
    }
  },
  data() {
    const value = ""
    return {value}
  },
  methods: {
    defaultValueAge() {
      if(this.$props.options.filter(item => item.selected)[0] !== undefined) {
        this.value = this.$props.options.filter(item => item.selected)[0].text
      } else this.value = this.$props.options[0].text
    }
  },
  mounted() {
    this.defaultValueAge();
  }
}
</script>

<style scoped>

</style>
