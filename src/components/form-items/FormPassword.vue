<template>
  <FormInput :label="label"
             @input="value = $refs.valuePass.value; $emit('clear-error')"
             ref="valuePass"
             type="password"
  />
</template>

<script>
import FormInput from "@/components/form-items/FormInput.vue";

export default {
  name: "FormPassword",
  props: {
    label: {
      type: String,
      default: ''
    },
    namePost: {
      type: String,
      default: ''
    },
  },
  data() {
    const value = ""
    return {value}
  },
  methods: {},
  components: {
    FormInput
  }
}
</script>

<style lang="scss" scoped>

</style>
