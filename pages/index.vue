<template>
  <v-layout
    column
    justify-center
    align-center
  >
    <v-flex
      xs12
      sm8
      md6
    >
      <div class="text-center">
        <logo />
       oooo
      </div>
      <v-card>
        <v-card-title class="headline">
          123123
          </v-card-title> 
        <v-card-text>
         456456
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn
            color="primary"
            nuxt
            to="/inspire"
          >
            Continue
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import Logo from '~/components/Logo.vue'
import VuetifyLogo from '~/components/VuetifyLogo.vue'

export default {
  layout: 'dental',


methods: {
  loginEnter() {
    if(this.$refs.formLogin.validate() ){
      this.loadind = true;
      setTimeout(() => this.$router.push('/') , 3000)
    
  }
}
}
}
</script>
