<template>
  <div>
      <div class="bg_container">
            <div class="bg_image"></div>
        </div>
        <div class="HomePageSignupForm">
            <div class="titleapp">
                <h1>AuthVueExpress</h1>
            </div>
            <h2 class="tagline">Tempat berbagi pengetahuan dan memahami dunia lebih baik</h2>
            <div class="container">
                <div class="content_inner">
                    <div class="signup_login">
                        <div class="signup">
                            <h2>Register</h2>
                            <form @submit.prevent="regist()">
                                <div class="stacked_form">
                                    <div class="form_row">
                                        <label for="">Full name</label>
                                        <input v-model="register.fullname" @change="rgsubmit()" class="text" type="text">
                                    </div>
                                    <div class="form_row">
                                        <label for="">email</label>
                                        <input v-model="register.email" @change="rgsubmit()" class="text" type="email">
                                    </div>
                                    <div class="form_row">
                                        <label for="">password</label>
                                        <input v-model="register.password" @change="rgsubmit()" class="text" type="password">
                                    </div>
                                </div>
                                <span class="ToDisclimer">
                                    Dengan melanjutkan, Anda menunjukkan bahwa Anda telah membaca dan menyetujui Persyaratan Layanan dan Kebijakan Privasi.
                                </span>
                                <div class="form_button">
                                    <span>
                                        <!-- jika semua sudah ada value/v-modelnya maka submit_button_disabled di hapus -->
                                        <input :class="{'submit_button_disabled': notsubmitrg}" class="submit_button left" type="submit" value="Register">
                                    </span>
                                </div>
                            </form>
                        </div>
                        <div class="login">
                            <h2>Login</h2>
                            <form @submit.prevent="logi()">
                                <div class="form_inputs">
                                    <div class="form_column">
                                        <input v-model="login.email" @change="lgsubmit()" type="email" class="text login_text_box" placeholder="Email">
                                    </div>
                                    <div class="form_column">
                                        <input v-model="login.password" @change="lgsubmit()" type="password" class="text login_text_box" placeholder="Password">
                                    </div>
                                </div>
                                <div class="form_button">
                                    <span>
                                        <input :class="{'submit_button_disabled': notsubmitlg}" class="submit_button left" type="submit" value="Login">
                                    </span>
                                </div>
                            </form>
                        </div>
                    </div>
                </div>
                <div class="FooterNav">
                    <span>Designed by Miftakh Ali Said</span>
                </div>
            </div>
        </div>
  </div>
</template>

<script>
import { mapActions } from 'vuex'
export default {
  data () {
    return {
      register: {
        fullname: '',
        email: '',
        password: ''
      },
      login: {
        email: '',
        password: ''
      },
      notsubmitrg: true,
      notsubmitlg: true
    }
  },
  methods: {
    ...mapActions({
      actionLogin: 'auth/login',
      actionRegister: 'auth/register'
    }),
    rgsubmit () {
      const rg = this.register
      if (rg.fullname !== '' && rg.email !== '' && rg.password !== '') {
        this.notsubmitrg = false
      } else {
        this.notsubmitrg = true
      }
    },
    lgsubmit () {
      const lg = this.login
      if (lg.email !== '' && lg.password !== '') {
        this.notsubmitlg = false
      } else {
        this.notsubmitlg = true
      }
    },
    regist () {
      this.actionRegister(this.register)
        .then((response) => {
          alert(response)
        }).catch((err) => {
          alert(err)
        })
    },
    logi () {
      this.actionLogin(this.login)
        .then((response) => {
          if (response === 'Activation needed!') {
            alert(response)
          } else {
            alert(response)
            window.location.href = '/'
          }
        }).catch((err) => {
          alert(err)
        })
    }
  },
  mounted () {
  }
}
</script>

<style scoped>
a {
    text-decoration: none;
    color: #2b6dad;
    background: transparent;
}
h1, h2, h3, h4, h5, h6, ul, ol, li {
    margin: 0;
    padding: 0;
}
h2 {
    display: block;
    font-size: 1.5em;
    margin-block-start: 0.83em;
    margin-block-end: 0.83em;
    margin-inline-start: 0px;
    margin-inline-end: 0px;
    font-weight: bold;
}
input[type=text], input[type=email], input[type=password], input[type=number] {
    padding: 3px 5px;
    height: 15px;
    width: 150px;
}
input[type=text], input[type=email], input[type=number], input[type=password], textarea, .fake_editor, .qtext_editor_content {
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
    min-height: 27px;
    background: #fff;
    outline: 0;
    border: 1px solid #e2e2e2;
    border-radius: 3px;
    box-shadow: inset 0 1px 1px rgba(200,200,200,0.3);
    -webkit-transition: border-color .2s;
    transition: border-color .2s;
    -webkit-transition: border-color .2s 180ms ease-in-out 0s;
    -o-transition: border-color .2s 180ms ease-in-out 0s;
    transition: border-color .2s 180ms ease-in-out 0s;
}
.bg_container {
    position: absolute;
    height: 100%;
    width: 100%;
    background: #fff;
    overflow: hidden;
}
.bg_image {
    background: url(//qsf.fs.quoracdn.net/-4-images.home.illo_1920.png-26-e9e6fbe02d908942.png) no-repeat center center fixed;
    -webkit-background-size: cover;
    -moz-background-size: cover;
    -o-background-size: cover;
    background-size: cover;
    width: 100%;
    height: 100%;
    position: fixed;
}
.HomePageSignupForm {
    background: #fff;
    border: 1px solid #e2e2e2;
    box-shadow: 0 0 5px #888;
    border-radius: 4px;
    padding-top: 25px;
    width: 650px;
    position: absolute;
    bottom: initial;
    left: 0;
    right: 0;
    margin: auto;
    overflow-y: hidden;
    top: 10%;
}
.NetworkLogo {
    width: 224px;
    min-width: 224px;
    height: 140px;
    background-size: 224px 63px;
    background-image: url(//qsf.fs.quoracdn.net/-4-images.logo.wordmark_default.svg-26-74aca0454e71aad9.svg);
    background-repeat: no-repeat;
    background-position: center center;
    height: 82px;
    position: relative;
    margin: auto;
}
.hidden {
    display: none !important;
}
.tagline {
    font-size: 19px;
    font-weight: 400;
    font-family: -apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Oxygen-Sans,Ubuntu,Cantarell,"Helvetica Neue",sans-serif;
    margin: 8px 0 32px;
    color: #949494;
    text-align: center;
}
.container {
    margin-top: 0;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
    position: relative;
}
.container .content_inner {
    padding: 32px;
}
.container .signup_login {
    position: relative;
    *zoom: 1;
}
.container .signup_login h2 {
    font-size: 13px;
}
.container .signup_login::before {
    display: table;
    content: "";
    zoom: 1;
}
.container .signup_login::after {
    clear: both;
    display: table;
    content: "";
    zoom: 1;
}
.signup {
    padding-right: 32px;
    float: left;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
    width: 50%;
}
.signup::after {
    content: "";
    width: 1px;
    position: absolute;
    top: 0;
    bottom: 0;
    background-color: #e6e6e6;
    left: 50%;
}
.stacked_form {
    margin-top: 8px;
}
.stacked_form label {
    line-height: 27px;
}
.form_row {
    *zoom: 1;
    padding: 0 0 8px;
}
.form_row::before {
    display: table;
    content: "";
    zoom: 1;
}
.form_row::after {
    display: table;
    content: "";
    zoom: 1;
}
.form_row label {
    font-size: 11px;
    color: #666;
    text-transform: uppercase;
    letter-spacing: .5px;
    font-weight: bold;
}
.form_row input {
    display: block;
    width: 100%;
    background-color: #fafafa;
}
.form_row .text {
    float: right;
}
.ToDisclimer {
    color: #949494;
    font-size: 13px;
}
.form_button {
    margin-top: 16px;
    text-align: right;
    font-size: 13px;
}
.submit_button, .primary_button {
    -webkit-user-select: none;
    -webkit-touch-callout: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
    transition: opacity ease-in-out 100ms,color ease-in-out 100ms,background-color ease-in-out 100ms,border-color ease-in-out 100ms;
    border-radius: 3px;
    box-shadow: 0 1px 1px 0 rgba(200,200,200,0.2);
    display: inline-block;
    font-weight: 500;
    outline: 0;
    padding: 3px 7px 4px 7px;
    text-align: center;
    text-decoration: none;
    cursor: pointer;
    background: #3e78ad;
    color: #fff;
    border: 1px solid #3a66ad;
    box-shadow: 0 1px 1px 0 rgba(200,200,200,0.6);
}
.submit_button_disabled {
    opacity: .5;
    pointer-events: none;
}
.login {
    position: relative;
    padding-left: 32px;
    float: left;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
    width: 50%;
}
.form_column:after {
    clear: both;
}
.form_column:before, .form_column:after {
    display: table;
    content: "";
    zoom: 1;
}
.login .form_column .login_text_box {
    background-color: #EEE;
    width: 100%;
    font-size: 15px;
    line-height: 1.4;
    padding-left: 8px;
    padding-right: 8px;
    min-height: 32px;
    margin-bottom: 8px;
}
.form_column input[type=password] {
    margin-top: 16px;
}
.FooterNav {
    padding: 16px;
    border-top: 1px solid #e2e2e2;
    background: #fafafa;
    text-align: center;
}
.FooterNav span {
    color: #949494;
    font-size: 13px;
}
.titleapp {
    text-align: center;
    color: #B93328;
}
</style>
