<template>
  <div>
    <Headbar></Headbar>
    <!-- Content -->
    <div id="content">
      <!-- Page Title -->
       <div class="page-title bg-light">
        <div class="container">
          <div class="row">
            <div class="col-lg-12">
              <h1 class="mb-0 text-center">Register</h1>
              <h4 class="text-muted mb-0 text-center">
                Some information about our restaurant
              </h4>
            </div>
          </div>
        </div>
      </div>

      <!-- Section -->
      <section class="sectionbg bg-white">
        <b-container>
          <b-form @submit.prevent="save" id="registerform">
            <b-row>
              <b-col cols="12"  md="6" class="mx-auto">
                <b-col cols="12">
                  <h2 class="font-weight-bold">Register Form</h2>
                </b-col>
                <b-col cols="12">
                  <b-form-group>
                    <b-form-input
                      v-model="form.name"
                      placeholder="Name"
                      :class="[(err !== ''?'border-danger':'')]"
                    ></b-form-input>
                  </b-form-group>
                </b-col>
                <b-col cols="12">
                  <b-form-group>
                    <b-form-group>
                      <b-form-input
                        v-model="form.phone"
                        placeholder="Phone"
                        :class="[(error.error !== ''?'border-danger':'') || (err !== ''?'border-danger':'')]"
                      ></b-form-input>
                    </b-form-group>
                  </b-form-group>
                </b-col>
                <div class="text-danger text-left">
                  <span v-if="error">
                  {{ error.error }}
                </span>
                </div>
                <b-col cols="12">
                  <b-form-group>
                    <b-form-group>
                      <b-form-input
                        v-model="form.email"
                        placeholder="Email"
                        type="email"
                        :class="[(error.error !== ''?'border-danger':'') || (err !== ''?'border-danger':'')]"
                      ></b-form-input>
                    </b-form-group>
                  </b-form-group>
                </b-col>
                <div class="text-danger text-left">
                  <span v-if="error.error">
                    {{ error.error }}
                  </span>
                </div>
                <b-col cols="12">
                  <b-form-group>
                    <b-form-group>
                      <b-form-input
                        v-model="form.password"
                        placeholder="Password"
                        type="password"
                        :class="[(err !== ''?'border-danger':'')]"
                      ></b-form-input>
                    </b-form-group>
                  </b-form-group>
                </b-col>
                <div class="text-danger text-center text-left">
                  <span class="text-lg" v-if="err">
                  {{ err }}
                </span>
                </div>
                <b-col cols="12" class="mt-3">
                  <b-form-group>
                    <b-button class="w-100" type="submit"><span>Submit</span></b-button>
                  </b-form-group>
                </b-col>
                <b-col cols="12" class="mt-3">
                  <p>
                    <router-link to="/login"
                      ><strong>Already have an account?</strong></router-link
                    >
                  </p>
                </b-col>
              </b-col>
            </b-row>
          </b-form>
        </b-container>
      </section>
    </div>
    <Footer></Footer>
  </div>
</template>
<script>
import Headbar from '@/views/layouts/Headbar.vue'
import Footer from '@/views/layouts/Footer.vue'
import { register } from '@/store/api'
import { saveLocalStorage } from '@/store/service'
import {
  BForm,
  BFormGroup,
  BButton,
  BRow,
  BFormInput,
  BCol,
  BContainer
} from 'bootstrap-vue'
export default {
  name: 'Register',
  data () {
    return {
      form: {
        name: '',
        email: '',
        phone: '',
        password: ''
      },
      err: '',
      error: {
        error: ''
      }
    }
  },
  components: {
    Headbar,
    Footer,
    BForm,
    BFormGroup,
    BFormInput,
    BButton,
    BRow,
    BCol,
    BContainer
  },
  methods: {
    save () {
      this.error.error = ''
      this.err = ''
      if (!this.form.name || !this.form.email || !this.form.phone || !this.form.password) {
        this.err = 'All fields are required.'
      } else {
        register(this.form).then(res => {
          console.log(res.data)
          if (res.data.success === true) {
            // localStorage.setItem('userData', res.data.data)
            saveLocalStorage('userData', JSON.stringify(res.data.data))
            saveLocalStorage('userDataVerify', false)
            this.$router.push('/otpverify?type=' + res.data.verification.type)
          } else if (res.data.email_phone_already_used === true) {
            this.error.error = 'this email/ phone already exists'
            this.$toast.error('this email/ phone already exists')
          } else {
            this.error.error = 'Registration failed'
            this.$toast.error('Registration failed')
          }
        })
      }
    }
  }
}
</script>
<style>
#registerform .form-control {
    /* box-shadow: inset 1px 1px 2px 0 rgb(40 43 46 / 6%); */
    /* -webkit-appearance: none; */
    -moz-appearance: none;
    appearance: none;
    font-weight: 400;
    padding: 1rem;
    border: 2px solid #e0e0e0;
    border-radius: 0;
    height: calc(3.25rem + 2px);
    color: #000000 !important;
    /* font-size: 20px; */
}
</style>
