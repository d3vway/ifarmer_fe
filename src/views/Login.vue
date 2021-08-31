<template>
  <div class="row justify-content-md-center">
    <div class="col-md-6">
      <div class="card">
        <div class="card-header">Login</div>
        <div class="card-body">
          <form>
            <div class="form-group">
              <input
                type="email"
                class="form-control"
                placeholder="Email"
                v-model="formData.email"
              />
            </div>
            <div class="form-group mt-2">
              <input
                type="password"
                class="form-control"
                placeholder="Password"
                v-model="formData.password"
              />
            </div>

            <button type="button" class="btn btn-primary mt-3" @click="login">Submit</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import axios, { AxiosPromise } from "axios";

@Component
export default class Login extends Vue {
  readonly url = "http://localhost/api/login";
  public formData = {
    email: "",
    password: "",
  };

  setHeaderToken(token: string): void {
    axios.defaults.headers.common["Authorization"] = "Bearer " + token;
  }

  removeHeaderToken(): void {
    delete axios.defaults.headers.common["Authorization"];
  }

  login(): AxiosPromise {
    const data = this.formData;
    return new Promise((resolve, reject) => {
      axios
        .post(this.url, data)
        .then((response) => {
          const token = response.data.access_token;
          localStorage.setItem("token", token);
          this.setHeaderToken(token);
          //  dispatch('get_user')
          console.log("token:", token);
          resolve(response);
        })
        .catch((err) => {
          console.error("Cannot login!");
          //  commit('reset_user')
          localStorage.removeItem("token");
          reject(err);
        });
    });
  }
}
</script>
