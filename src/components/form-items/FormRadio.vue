<template>
  <fieldset>
    <legend>{{ label }}</legend>
      <div
          v-for="option in options"
          :key="option.value"
      >
      <input required
             :type="type"
             :name="parentNameInput()"
             :id="parentIdInput(option.value)"
             :value="option.value" v-model="value"
             :checked="option.selected"
      />
      <label :for="parentIdInput(option.value)">{{ option.text }}</label>
    </div>
  </fieldset>
</template>

<script>
export default {
  name: "FormRadio",
  props: {
    label: {
      type: String,
      default: ''
    },
    options: {
      type: Object,
      required: {}
    },
    indexRadio: {
      type: String,
      default: ''
    },
    namePost: {
      type: String,
      default: ''
    },
    type: {
      type: String,
      default: 'radio'
    },
  },
  data() {
    const value = 0;
    return {value}
  },
  methods: {
    parentIdInput (value) {
      if(this.indexRadio) return `${this.indexRadio}-id-${value}`
      else return value
    },
    parentNameInput() {
      if(this.indexRadio) return `${this.indexRadio}-radio`
    },
    defaultValueAge() {
      if(this.options.filter(item => item.selected).length) {
        this.value = +this.options.filter(item => item.selected)[0].value
      }
    }
  },
  mounted() {
    this.defaultValueAge();
  }
}
</script>

<style scoped>

</style>
