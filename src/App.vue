<template>
  <div id="app">
      <RegistrationForm :onSubmit="onSubmit"/>
      <SuccessRegistration v-show="view" :name="name" :onClose="onClose"/>
  </div>
</template>

<script>
  import RegistrationForm from "@/components/RegistrationForm";
  import SuccessRegistration from "@/components/SuccessRegistration";


  export default {
      name: 'App',
      components: {
          SuccessRegistration,
          RegistrationForm,

      },
      data() {
          return {
              name:'',
              view:false
          }
      },
      methods: {
          onSubmit(data) {
              this.name=data.name
              this.view=true
          },
          onClose(){
              this.view=false
          }
      }
  }
</script>

<style lang="sass">
    body
        margin: 0
        padding: 0
        min-width: 320px

    #app
        font-family: Avenir, Helvetica, Arial, sans-serif
        -webkit-font-smoothing: antialiased
        -moz-osx-font-smoothing: grayscale
        color: #2c3e50
        background: #f7f7f7
        display: flex
        justify-content: center
        box-sizing: border-box
</style>