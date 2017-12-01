<template>
  <div id="app">
  <h1>Register Here</h1>
    <form @submit.prevent="validateBeforeSubmit" v-if="!formSubmitted">
        <div class="form-group" :class="{'input': true,'has-error': errors.has('oranizationname') }">
            <label class="control-label" for="oranizationname">Organization Name</label>
            <input v-model="oranizationname" v-validate.initial="oranizationname" data-rules="required|alpha|min:3" class="form-control" type="text" placeholder="Oranization Name">
            <p class="text-danger" v-if="errors.has('oranizationname')">{{ errors.first('oranizationname') }}</p>
        </div>
        <div class="form-group" :class="{'input': true,'has-error': errors.has('email') }" >
            <label class="control-label" for="email">Email</label>
            <input v-model="email" v-validate.initial="email" data-rules="required|email" class="form-control" type="email" placeholder="Email">
            <p class="text-danger" v-if="errors.has('email')">{{ errors.first('email') }}</p>
        </div>
        <div class="form-group" :class="{'input': true,'has-error': errors.has('password') }">
            <label class="control-label" for="password">Password</label>
            <input v-model="password" name="password"  v-validate.initial="password" data-rules="required|min:6" class="form-control" type="password" placeholder="Password">
            <p class="text-danger" v-if="errors.has('password')">{{ errors.first('password') }}</p>
        </div>
      
        <div class="form-group" :class="{'input': true,'has-error': errors.has('confirmpassword') }">
            <label class="control-label" for="confirmpassword">Confirm Password</label>
            <input v-model="confirmpassword" v-validate.initial="confirmpassword"   data-rules="required|confirmed:password" name="confirmpassword" class="form-control" type="password" placeholder="Confirm Password">
            <p class="text-danger" v-if="errors.has('confirmpassword')">{{ errors.first('confirmpassword') }}</p>
        </div>

        <button class="btn btn-success btn-block" type="submit">Submit</button>
    </form>
    <div v-else>
      <h1 class="submitted">Form submitted successfully!</h1>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import VeeValidate from 'vee-validate';

Vue.use(VeeValidate);

export default {
  data () {
    return {
      oranizationname: '',
      email: '',
      password: '',
      confirmpassword: '',
      formSubmitted: false
    }
  },
  methods: {
    validateBeforeSubmit(e) {
        this.$validator.validateAll();

        if (!this.errors.any()) {
            this.submitForm()
        }
      },
    submitForm(){
      this.formSubmitted = true
    }
  }
}
</script>




<style>

body {
  font-family: Helvetica, sans-serif;
}
.container {
  width: 500px;
}
h1 {
  text-align: center
}
img {
  text-align: center
}

   .input:focus {
        border-bottom: 2px solid #green;
        box-shadow: none;
    }



.submitted {
  color: #4fc08d;
}
</style>
