<template>
  <v-container fluid fill-heigth>
    <v-layout align-center justify-center>
      <v-flex xs12 sm8 md6>
        <v-card class="elevation-12">
          <v-toolbar dark color="primary">
            <v-toolbar-title>Регистрация</v-toolbar-title>
          </v-toolbar>
          <v-card-text>
              <v-alert
                  :value="error"
                  type="warning">
                  {{error}}
              </v-alert>
            <v-form v-model="valid">
              <v-text-field
                v-model="email"
                prepend-icon="mdi-account"
                name="Login"
                label="E-mail"
                type="email"
                :rules="[(v) => !!v || 'Email is required']"
                required
              ></v-text-field>
              <v-text-field
                v-model="password"
                id="password"
                prepend-icon="mdi-lock"
                name="password"
                label="Пароль"
                type="password"
                :rules="[(v) => !!v || 'Password is required']"
                reqired
              ></v-text-field>
            </v-form>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="primary" @click.prevent="signup" :disabled="processing">Зарегистрироваться</v-btn>
          </v-card-actions>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      email: null,
      password: null,
      valid: false
    }
  },
  computed:{
      error(){
          return this.$store.getters.getError
      },
      processing(){
          return this.$store.getters.getProcessing
      },
      isUserAuthenticated(){
          return this.$store.getters.isUserAuthenticated
      }  

  },
  watch:{
      isUserAuthenticated(val){
          if(val === true)
          this.$router.push("/")
      }
  },

  methods:{
        signup(){
            this.$store.dispatch('SIGNUP',{email:this.email, password: this.password})
        }
    }
}
</script>

<style>
</style>