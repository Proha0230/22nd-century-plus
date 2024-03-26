<template>
  <div class="child_main">
    <h3>{{valueForm.name}}</h3>
    <div v-for="(item, index) in valueForm.items">
      <component :is="`form-${item.type}`"
                 :namePost="item.name"
                 :label="item.label"
                 :type="item.type"
                 :options="item.additional ? item.additional.options : ''"
                 :indexRadio="valueIndex"
                 @clearError="clearErrorPass"
                 ref="ComponentsForm"></component>
    </div>
          <div class="form-builder__form--error">
            <h3 v-if="!validatePass" class="error__pass">Введеные пароли не совпадают</h3>
          </div>
  </div>


</template>

<script>
import FormInput from "@/components/form-items/FormInput.vue";
import FormRadio from "@/components/form-items/FormRadio.vue";
import FormSelect from "@/components/form-items/FormSelect.vue";
import FormPassword from "@/components/form-items/FormPassword.vue";
export default {
  props: ["valueForm", "valueIndex"],
  name: "ChildComponents",
  data() {
    const inputValueForms = {}
    let validatePass = true
    return {inputValueForms,validatePass}
  },
  methods: {
    clearErrorPass() {
      this.validatePass = true
    },
    getValueChild() {
      this.$refs.ComponentsForm.forEach(item => {
        this.inputValueForms[item.namePost] = item.value
      })
      if(this.inputValueForms.pass !== this.inputValueForms['repeat-pass']) this.validatePass = false
    }
  },
  components: {FormInput, FormRadio, FormSelect, FormPassword}

}
</script>

<style scoped>

.child_main {
  display: flex;
  flex-flow: column;
  align-items: center;
  width: 200px;
  height: 300px;
  border: solid 2px darkgray;
  border-radius: 20px;
  background-color: darkgray;
}

.error__pass {
  background-color: red;
  color: white;
  padding: 7px;
  border-radius: 10px;
  margin-top: 20px;
}

</style>