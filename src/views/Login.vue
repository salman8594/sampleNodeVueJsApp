<template>
  <div>
    
   <b-container>
    <b-row align-h="center" class="mt-5">
      <b-col cols="5">
        <b-card class="p-3">
          <h3 class="mb-4">Login</h3>
          <b-form @submit="onSubmit" @reset="onReset" v-if="show">
      <b-form-group id="exampleInputGroup1"
                    label="Email address:"
                    label-for="exampleInput1"
                    >
        <b-form-input id="exampleInput1"
                      type="email"
                      v-model="form.email"
                      required
                      placeholder="Enter email">
        </b-form-input>
      </b-form-group>
      <b-form-group id="exampleInputGroup2"
                    label="Password:"
                    label-for="exampleInput2">
        <b-form-input id="exampleInput2"
                      type="password"
                      v-model="form.password"
                      required
                      placeholder="Enter password">
        </b-form-input>
      </b-form-group>

      <b-form-group id="exampleGroup4">
        <b-form-checkbox-group v-model="form.checked" id="exampleChecks">
          <b-form-checkbox value="remember">Remember me</b-form-checkbox>
        </b-form-checkbox-group>
      </b-form-group>
      <div class="d-flex justify-content-between">
        <div>
          <b-button type="submit" variant="primary">Submit</b-button>&nbsp;
          <b-button type="reset" variant="danger">Reset</b-button>
        </div>
        <div>
          <a href="#" v-b-modal.modal1>Forgot Password</a>
        </div>
      </div>
    </b-form>
        </b-card>
      </b-col>
    </b-row>
  </b-container>


  <b-modal id="modal1" title="Forgot Password">
      
    </b-modal>
  </div>
</template>

<script>
// @ is an alias to /src

import router from '../router'
import { mapMutations } from 'vuex'

export default {
  name: 'login',
   data() {
      return {
        form: {
          email: '',
          password: '',
          checked: []
        },
        foods: [{ text: 'Select One', value: null }, 'Carrots', 'Beans', 'Tomatoes', 'Corn'],
        show: true,
      }
    },
    methods: {
        ...mapMutations([
      'UPDATE_USERLOGIN'
    ]),
      onSubmit(evt) {
        evt.preventDefault()
       this.UPDATE_USERLOGIN(true);
        router.push({ name: "home" });
       // alert(JSON.stringify(this.form))
      },
      onReset(evt) {
        evt.preventDefault()
        // Reset our form values
        this.form.email = ''
        this.form.password = ''
        this.form.checked = []
        // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      }
    }
  
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css?family=Lato:400,700');
  body {
    background: #EEF1F4 !important;
    font-family: 'Lato', sans-serif !important;
  }
  .nav-background {
    background: #353535;
  }
</style>
