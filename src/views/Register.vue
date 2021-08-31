<template>
  <div class="row justify-content-md-center">
    <div class="col-md-6">
      <div class="card">
        <div class="card-header">Register</div>
        <div class="card-body">
          <form>
            <div class="form-group">
              <input type="text" class="form-control" placeholder="Name.." />
            </div>
            <div class="form-group mt-1">
              <input type="email" class="form-control" placeholder="Email.." />
            </div>
            <div class="form-group mt-1">
              <input
                type="password"
                class="form-control"
                placeholder="Password.."
              />
            </div>
            <button type="submit" class="btn btn-primary mt-3">Submit</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class Register extends Vue {}
</script>
