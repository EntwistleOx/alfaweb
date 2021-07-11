<template>
  <v-container fill-height>
    <v-row align="center" justify="center">
      <v-col>
        <v-card shaped>
          <v-card-title>Login de Usuario</v-card-title>
          <v-card-text>
            <form>
              <v-text-field
                v-model="email"
                :error-messages="emailErrors"
                label="Email"
                required
                @input="$v.email.$touch()"
                @blur="$v.email.$touch()"
              ></v-text-field>

              <v-text-field
                v-model="password"
                :error-messages="passwordErrors"
                label="Password"
                required
                @input="$v.password.$touch()"
                @blur="$v.password.$touch()"
                type="password"
              ></v-text-field>

              <v-btn color="success" class="mr-4" @click="submit">
                Login
              </v-btn>
              <v-btn color="warning" @click="clear"> Limpiar </v-btn>
            </form>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import { mapActions } from "vuex";
import { validationMixin } from "vuelidate";
import { required, email } from "vuelidate/lib/validators";

export default {
  data() {
    return {
      email: "",
      password: "",
    };
  },
  mixins: [validationMixin],
  validations: {
    email: { required, email },
    password: { required },
  },
  computed: {
    emailErrors() {
      const errors = [];
      if (!this.$v.email.$dirty) return errors;
      !this.$v.email.email && errors.push("Email debe ser valido");
      !this.$v.email.required && errors.push("Email es requerido");
      return errors;
    },
    passwordErrors() {
      const errors = [];
      if (!this.$v.password.$dirty) return errors;
      !this.$v.password.required && errors.push("Password es requerido.");
      return errors;
    },
  },
  methods: {
    ...mapActions(["login"]),
    submit() {
      this.$v.$touch();
      if (!this.$v.$invalid) {
        const formData = { email: this.email, password: this.password };
        this.login(formData);
      }
    },
    clear() {
      this.$v.$reset();
      this.email = "";
      this.password = "";
    },
  },
};
</script>
