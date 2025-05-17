<script>
import { useAuthenticationStore } from "../services/authentication.store.js";
import { SignUpRequest } from "../model/sign-up.request.js";
import ToolbarHome from "../../public/component/toolbar-home.component.vue";

export default {
  name: "sign-up",
  components: { ToolbarHome },
  data() {
    return {
      authenticationStore: useAuthenticationStore(),
      username: "",
      password: "",
      role: "",
      passwordValidations: {
        length: false,
        upper: false,
        lower: false,
        number: false,
        special: false,
      }
    };
  },
  computed: {
    isPasswordValid() {
      return Object.values(this.passwordValidations).every(v => v === true);
    }
  },
  watch: {
    password(value) {
      this.passwordValidations.length = value.length >= 8;
      this.passwordValidations.upper = /[A-Z]/.test(value);
      this.passwordValidations.lower = /[a-z]/.test(value);
      this.passwordValidations.number = /[0-9]/.test(value);
      this.passwordValidations.special = /[^A-Za-z0-9]/.test(value);
    }
  },
  methods: {
    onSignUp() {
      if (!this.isPasswordValid) return;
      const signUpRequest = new SignUpRequest(this.username, this.password, this.role);
      this.authenticationStore.signUp(signUpRequest, this.$router);
    }
  }
}
</script>

<template>
  <toolbar-home></toolbar-home>
  <div>
    <h3>Sign Up</h3>
  </div>
  <p class="p-fluid mb-5">Please enter the required information to sign up.</p>
  <div>
    <form @submit.prevent="onSignUp">
      <div class="p-fluid">
        <!-- Username -->
        <div class="field mt-5">
          <pv-float-label>
            <label for="username">Username</label>
            <pv-input-text id="username" v-model="username" :class="{'p-invalid': !username }"/>
            <small v-if="!username" class="p-invalid">Username is required.</small>
          </pv-float-label>
        </div>

        <!-- Password -->
        <div class="field mt-5">
          <pv-float-label>
            <label for="password">Password</label>
            <pv-input-text id="password" v-model="password" type="password" :class="{'p-invalid': !isPasswordValid}"/>
          </pv-float-label>
          <ul class="validation-list">
            <li :class="{ valid: passwordValidations.length }">At least 8 characters</li>
            <li :class="{ valid: passwordValidations.upper }">At least one uppercase letter</li>
            <li :class="{ valid: passwordValidations.lower }">At least one lowercase letter</li>
            <li :class="{ valid: passwordValidations.number }">At least one number</li>
            <li :class="{ valid: passwordValidations.special }">At least one special character (!, @, #, etc.)</li>
          </ul>
        </div>

        <!-- Role -->
        <div class="field mt-5">
          <pv-float-label>
            <label for="role">Role</label>
            <pv-dropdown id="role" v-model="role" :options="['Winemaker']"/>
            <small v-if="!role" class="p-invalid">Role is required.</small>
          </pv-float-label>
        </div>

        <!-- Buttons -->
        <div class="p-field mt-5">
          <pv-button type="submit" :disabled="!username || !role || !isPasswordValid">Sign Up</pv-button>
          <router-link to="/home">
            <pv-button class="ml-2">Home</pv-button>
          </router-link>
        </div>
      </div>
    </form>
  </div>
</template>

<style scoped>
.ml-2 {
  margin-left: 0.5rem;
}
.validation-list {
  list-style-type: none;
  padding-left: 0.5rem;
  margin-top: 0.5rem;
}
.validation-list li {
  font-size: 0.85rem;
  color: red;
}
.validation-list li.valid {
  color: green;
}
</style>
