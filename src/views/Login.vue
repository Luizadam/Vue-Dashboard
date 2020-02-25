<template>
  <div class="row justify-content-center">
    <div class="col-lg-5 col-md-7">
      <div class="card bg-secondary shadow border-0" style="margin-top:-6rem">
        <div class="card-header bg-transparent pb-3">
          <div class="text-muted text-center mt-2 mb-3">
            <small></small>
          </div>
          <div class="btn-wrapper text-center">
            <!-- <a href="#" class="btn btn-neutral btn-icon">
                                <span class="btn-inner--icon"><img src="img/icons/common/github.svg"></span>
                                <span class="btn-inner--text">Github</span>
                            </a>
                            <a href="#" class="btn btn-neutral btn-icon">
                                <span class="btn-inner--icon"><img src="img/icons/common/google.svg"></span>
                                <span class="btn-inner--text">Google</span>
            </a>-->
            <img src="../assets/logobaru.png" style="width:50%" />
          </div>
        </div>
        <div class="card-body px-lg-5 py-lg-5">
          <form role="form" @submit.prevent="validate">
            <base-input
              class="input-group-alternative mb-3"
              placeholder="Email"
              addon-left-icon="ni ni-email-83"
              v-model="model.email"
            ></base-input>

            <base-input
              class="input-group-alternative"
              placeholder="Password"
              type="password"
              addon-left-icon="ni ni-lock-circle-open"
              v-model="model.password"
            ></base-input>

            <base-checkbox class="custom-control-alternative">
              <span class="text-muted">Remember me</span>
            </base-checkbox>
            <div class="text-center">
              <base-button type="primary" nativeType="submit" class="my-4">Sign in</base-button>
            </div>
          </form>
        </div>
      </div>
      <div class="row mt-3">
        <div class="col-6">
          <router-link to="/forgotpass" class="text-light">
            <small>Forgot password?</small>
          </router-link>
        </div>
        <div class="col-6 text-right">
          <router-link to="/register" class="text-light">
            <small>Create new account</small>
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "login",
  data() {
    return {
      model: {
        email: "",
        password: ""
      }
    };
  },
/*eslint-disable*/
  methods: {
    async login(email, password) {
      const credentials = {
        email,
        password
      };
      try {
        const response = await axios({
          method: "post",
          url: "https://x-user-api.mindzzle.com/registrations/api/login/",
          params: {
            email: credentials.email,
            password: credentials.password
          },
          // watch: {
          //   users: {
          //     handler() {
          //       localStorage.setItem('email', JSON.stringify(this.params.email));
          //       localStorage.setItem('password', JSON.stringify(this.params.password))
          //     },
          //     deep: true
          //   }
          // },
          headers: {
            Accept: "application/json",
            "Content-Type": "application/json;charset=UTF-8"
          }


          // credentials.email + "&&password=",
          //   JSON.stringify(credentials)}
        });
        
        const user = response.data;
        
          // console.log('respons data', response.data);

        if (
          user.email == credentials.email &&
          user.password == credentials.password
        ) {
          // console.log({
          //   status: "success",
          //   name: user.name,
          //   username: user.username,
          //   email: user.email
          // });
          alert('email dan password sesuai')
        } else {
          // return { status: "failed" };
          // console.log('credentials password ' + credentials.password)
          console.log(user)
          alert('email dan password tidak sesuai')

          // console.log(user)
        }
      } catch (error) {
        console.error("whoops " + error);
      }
    },
    async validate() {
      let response = await this.login(this.model.email, this.model.password);

      if (response.api_status === "failed") {
        return alert("Failed to login");
      }
      

      await alert("Success login!");
    }
  }
};
</script>
<style>
</style>
