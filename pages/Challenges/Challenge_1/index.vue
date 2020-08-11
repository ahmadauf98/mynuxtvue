<template>
  <div class="b-theme container-fluid d-flex align-items-center">
    <div class="p-2 py-5 p-md-5">
      <div class="px-0 px-md-5 row align-items-center">
        <div class="text-white col-12 col-md-6 pr-md-5 mb-5 mb-md-0">
          <div class="title mb-4">
            <p class="display-4 font-weight-bolder text-center text-md-left">
              {{ title }}
            </p>
          </div>
          <div class="sub-title">
            <p class="lead text-center text-md-left">{{ subtitle }}</p>
          </div>
        </div>
        <div class="col-12 col-md-6">
          <div class="card card-promo mb-4">
            <div class="card-body text-center">
              <p
                class="card-title mb-n1 font-weight-normal text-white px-2 px-md-0"
              >
                <strong>Try it free 7 days</strong> then $20/mo. thereafter
              </p>
            </div>
          </div>
          <div class="card card-form">
            <div class="p-4">
              <div class="pt-3 px-0 px-md-3">
                <b-form ref="form" @submit.prevent="submit">
                  <b-form-group class="mb-4">
                    <b-form-input
                      class="input"
                      required
                      size="lg"
                      placeholder="First Name"
                      type="text"
                      v-model="form.firstName"
                    ></b-form-input>
                  </b-form-group>

                  <b-form-group class="mb-4">
                    <b-form-input
                      class="input"
                      required
                      size="lg"
                      placeholder="Last Name"
                      type="text"
                      v-model="form.lastName"
                    ></b-form-input>
                  </b-form-group>

                  <b-form-group class="mb-4">
                    <b-form-input
                      class="input"
                      required
                      size="lg"
                      placeholder="Email Address"
                      type="email"
                      v-model="$v.form.email.$model"
                      :state="validateState('email')"
                      aria-describedby="email-live-feedback"
                    ></b-form-input>
                    <b-form-invalid-feedback id="email-live-feedback"
                      >Email must be valid.</b-form-invalid-feedback
                    >
                  </b-form-group>

                  <b-form-group class="mb-4">
                    <b-form-input
                      class="input"
                      required
                      size="lg"
                      placeholder="Password"
                      type="password"
                      v-model="$v.form.password.$model"
                      :state="validateState('password')"
                      aria-describedby="password-live-feedback"
                    ></b-form-input>
                    <b-form-invalid-feedback id="password-live-feedback"
                      >Password must be at least 6
                      characters.</b-form-invalid-feedback
                    >
                  </b-form-group>

                  <b-button
                    class="btn text-uppercase font-weight-normal mb-4"
                    block
                    size="lg"
                    :disabled="Disabled"
                    >claim your free trial
                  </b-button>

                  <div class="col-12 mb-n2 text-center">
                    <p>
                      <small class="text-grey">
                        By clicking the button, you are agreeing to our
                        <a class="link" href="#"> Terms and Services</a>
                      </small>
                    </p>
                  </div>
                </b-form>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="col-12 text-center text-white mt-5">
        <p>
          <small>
            Challenge by
            <a
              class="bottom-link"
              href="https://www.frontendmentor.io?ref=challenge"
              target="_blank"
              rel="noopener"
              >Frontend Mentor</a
            >. Coded by
            <a
              class="bottom-link"
              href="https://twitter.com/aufnasa_"
              target="_blank"
              rel="noopener"
              >@aufnasa_</a
            >
          </small>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import { validationMixin } from 'vuelidate'
import { email, minLength } from 'vuelidate/lib/validators'

export default {
  layout: 'challenges.vue',
  head: {
    title: 'Challenge 1',
    meta: [
      {
        hid: 'description',
        name: 'description',
        content: 'Home page description',
      },
    ],
  },
  mixins: [validationMixin],
  data() {
    return {
      title: 'Learn to code by watching others',
      subtitle:
        'See how experienced developers solve problems in real-time. Watching scriptes tutorials is great, but understanding how developes think is invaluable.',
      form: {
        firstName: '',
        lastName: '',
        email: '',
        password: null,
      },
    }
  },
  computed: {
    Disabled() {
      return (
        !this.form.firstName,
        !this.form.lastName,
        !this.form.email,
        !this.form.password
      )
    },
  },
  validations: {
    form: {
      email: { email },
      password: {
        minLength: minLength(6),
      },
    },
  },
  methods: {
    validateState(email) {
      const { $dirty, $error } = this.$v.form[email]
      return $dirty ? !$error : null
    },
    validateState(password) {
      const { $dirty, $error } = this.$v.form[password]
      return $dirty ? !$error : null
    },
  },
}
</script>

<style scoped>
.b-theme {
  min-height: 100vh;
  background-color: #ff7978;
  background-image: url(~static/challenge_1/bg-intro.svg);
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
}

.mb-n1 {
  margin-top: -0.25rem !important;
}

.mb-n2 {
  margin-top: -0.5rem !important;
}

.card {
  border-radius: 10px;
}

.card-promo {
  background-color: #5d54a3;
  border: none;
}

.card-form {
  background-color: white;
  border: none;
}

.input {
  font-size: 16px;
  font-weight: 500;
  padding: 15px;
  padding-top: 25px;
  padding-bottom: 25px;
}

.btn {
  background-color: #37cc8a;
  border: none;
  font-size: 16px;
  padding: 12px;
}

.link {
  color: #ff7978;
  font-weight: bolder;
  text-decoration: none;
}

.text-grey {
  color: grey;
}

.bottom-link {
  color: white;
  font-weight: bolder;
  text-decoration: none;
}
</style>
