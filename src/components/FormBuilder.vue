<template>
  <div class="form-builder">
    <form class="form-builder__form" @submit.prevent="onSubmit">
      <div class="form-builder__form--components">
        <div  v-for="(item, index) in dataForm" :key="index">
        <child-components ref="formChild"
                          :value-form="item"
                          :value-index="index"
        ></child-components>
        </div>
      </div>
      <div class="form-builder__form--buttons">
      <button class="buttons__submit" type="submit">Отправить</button>
      <button class="buttons__reset" type="reset">Стереть</button>
      </div>
    </form>
  </div>
</template>

<script>
import ChildComponents from "@/components/ChildComponents.vue";

import formConfig from "../../form-config.json"

export default {
  name: "FormBuilder",
  data() {
    let validatePass = true
    const dataForm = formConfig;
    const dataPost = {};

    return {dataForm,dataPost,validatePass}
  },

  methods: {
    async onSubmit() {
      this.validatePass = true
      for(let i = 0; i < this.$refs.formChild.length; i++) {
        await this.$refs.formChild[i].getValueChild()
        this.dataPost[this.$refs.formChild[i].valueIndex] = this.$refs.formChild[i].inputValueForms
        if(!this.$refs.formChild[i].validatePass) this.validatePass = false
      }

      if(this.validatePass) {
        const url = 'https://google.com/base'
        const data = this.dataPost
        const options = {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify(data)
        }
        fetch(url, options)
            .then(response => {
              if (!response.ok) {
                throw new Error('Ошибка с запросом к серверу');
              }
              return response.json();
            })
            .then(jsonResponse => {
              console.log('Успешный ответ от сервера:', jsonResponse);
            })
            .catch(error => {
              console.error('Произошла ошибка :', error);
            });


        alert('Submit')
      }
    },
  },
  components: {ChildComponents}
}
</script>

<style scoped>

.form-builder {
  display: flex;
  justify-content: center;
  margin-top: 30px;
  width: 100vw;
}

.form-builder__form {
  display: flex;
  flex-flow: column;
  align-items: center;
}

.form-builder__form--components {
  display: flex;
  width: 100%;
  justify-content: space-around;
}

.form-builder__form--buttons {
  margin-top: 65px;
  width: 50vw;
  display: flex;
  justify-content: center;
}

.buttons__reset {
  width: 100px;
  height: 50px;
  border-radius: 20px;
  background-color: darkgray;
  margin-left: 10px;
}

.buttons__submit {
  width: 100px;
  height: 50px;
  border-radius: 20px;
  background-color: darkgray;
}


</style>
