<template>
  <v-parallax
    dark
    src="https://warnerwave.com/image/26919-full_blue-polygon-wallpapers-top-free-blue-polygon-backgrounds.jpg">
    <v-layout
      align-center
      justify-center>
      <v-flex
        xs12
        sm12
        md6
        lg6>
        <v-card
          light
          class="elevation-10 card-style"> 
          <v-card-title class="card-title grey--text">
            LOGIN
          </v-card-title> 
          <v-layout
            align-center
            justify-center>
            <v-flex
              md11
              lg11
              ml-3
              mr-3>
              <v-flex
                xs12
                sm12
                md10
                lg11
                ml-5
                mr-5>
                <v-text-field
                  :rules="[rules.required, rules.min]"
                  :type="show1 ? 'text' : 'cro'"
                  name="input-10-2"
                  label="CRO"
                  hint="Apenas números!z"
                  value=""
                  class="input-group--focused"
                  @click:append="show1 = !show1" />
              </v-flex>
              <v-flex
                xs12
                sm12
                md10
                lg11
                ml-5
                mr-5>
                <v-text-field
                  :rules="[rules.required, rules.min]"
                  :type="show2 ? 'text' : 'password'"
                  name="input-10-2"
                  label="Senha"
                  hint="Mínimo 8 caracteres"
                  value=""
                  class="input-group--focused"
                  @click:append="show2 = !show2">
                  </v-text-field>
                  <a href="" class="link">Esqueceu a Senha</a>
              </v-flex>
              <v-card-actions>
                <v-spacer />
                <v-btn
                  class=" elevation-2"
                  dark
                  large
                  min-width="25%"
                  rounded 
                  label="LOGIN"
                  color="primary"
                  nuxt
                  to="/register">
                  LOGIN
                </v-btn>
              </v-card-actions>
            </v-flex>
          </v-layout>
        </v-card>
      </v-flex>
    </v-layout>
  </v-parallax>
</template>

<script>
import Logo from '~/components/Logo.vue'
import VuetifyLogo from '~/components/VuetifyLogo.vue'

export default {
  layout: 'dental',
  data () {
    return {
      show1: true,
      show2: true,
      password: 'Password',
      email:'Email',
      rules: {
        required: value => !!value || 'Required.',
        min: v => v.length >= 8 || 'Min 8 characters',
        emailMatch: () => ('The email and password you entered don\'t match')
      }
    }
  },

  methods: {
    loginEnter () {
      if(this.$refs.formLogin.validate() ){
        this.loadind = true
        setTimeout(() => this.$router.push('/') , 3000)
    
      }
    }
  }
}
</script>

<style>
.card-style {
 border-radius: 10px;
}

.card-title {
  background-color: #f0f0f5 !important
}
.link {
  text-decoration:none;
  font-size: 12px !important;
}
</style>
