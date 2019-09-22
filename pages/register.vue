<template>
  <v-layout
   class=""
    wrap
    font-weight-bold
    row
    title
    align-center
    justify-center
    mt-10>
    <v-flex
      class="text-center"
      lg7
      md7
      xs12
      sm12>
      <h1>Cadastro</h1>
      <v-form>
        <v-text-field
          v-model="name"
          label="Nome"
          required />
        <v-text-field
          v-model="email"
          label="Email"
          required />
        <v-flex>
          <v-row>
            <v-col
              sm="6"
              cols="12"> 
              <v-flex>
<v-menu
                  ref="menu"
                  v-model="menu"
                  :close-on-content-click="false"
                  transition="scale-transition"
                  offset-y
                  full-width
                  min-width="290px">
                  <template v-slot:activator="{ on }">
                    <v-text-field
                      v-model="date"
                      label="Data de Nascimento"
                      readonly
                      v-on="on">
                      <v-icon>event</v-icon>
                    </v-text-field>
                  </template>
                  <v-date-picker
                    ref="picker"
                    v-model="date"
                    :max="new Date().toISOString().substr(0, 10)"
                    min="1950-01-01"
                    @change="save" />
                </v-menu>
              </v-flex>
            </v-col>
            <v-col
              sm="6"
              cols="12">
              <v-flex>
                <v-text-field
                  ref="age"
                  v-model="age"
                  type="number"
                  :rules="[() => !!age || 'Este campo é obrigatório']"
                  :items="age"
                  label="Idade"
                  required />
              </v-flex>
            </v-col>
          </v-row>
          <v-row>
            <v-col
              sm="6"
              cols="12"> 
              <v-flex>
                <v-text-field
                  label="Telefone"
                  required />
              </v-flex>
            </v-col>
            <v-col
              sm="6"
              cols="12">
              <v-flex>
                <v-text-field
                  v-model="cel"
                  label="Celular"
                  required />
              </v-flex>
            </v-col>
          </v-row>
        </v-flex>
        <v-autocomplete
          ref="country"
          v-model="country"
          :rules="[() => !!country || 'Este campo é obrigatório']"
          :items="countries"
          label="País"
          placeholder="Selecione..."
          required />
        <v-row>
          <v-col
            sm="6"
            cols="12"> 
            <v-flex>
          <v-checkbox
                v-if="!checkboxPaciente"
                v-model="checkboxDentista"
                value="1"
                label="Dentista"
                type="checkbox"
                required />
            </v-flex>
          </v-col>
          <v-col
            sm="6"
            cols="12">
            <v-flex>
              <v-checkbox
                v-if="!checkboxDentista"
                v-model="checkboxPaciente"
                value="1"
                label="Paciente"
                type="checkbox"
                required />
            </v-flex>
          </v-col>
        </v-row>
          
        <v-flex>
          <v-flex
            sm12
            xs12
            md6
            lg6>
            <v-text-field
              v-model="CRO"
              v-if="checkboxDentista"
              dark
              label="CRO"
              required />
          </v-flex>
          <v-row>
            <v-col
              sm="6"
              cols="12"> 
              <v-flex>
                 <v-text-field
              v-model="senha1"
              v-if="checkboxDentista"
              dark
              type="password"
              label="Digite uma Senha"
              required />
              </v-flex>
            </v-col>
            <v-col
              sm="6"
              cols="12">
              <v-flex>
                <v-text-field
              v-model="senha2"
              v-if="checkboxDentista"
              dark
              type="password"
              label="Repita a Senha"
              required />
              </v-flex>
            </v-col>
          </v-row>
        </v-flex>
        <v-btn
          large
          class="mr-4"
          @click="submit">
          Enviar
        </v-btn>
        <v-btn 
        large
        @click="clear">
          Limpar
        </v-btn>
      </v-form>
    </v-flex>
  </v-layout>
</template>


<script>

export default {
  data () {
    return {
      autofocus: true,
      counter: 0,
      hint: '',
      label: '',
      loading: false,
      model: 'Área de Comentários',
      outlined: true,
      placeholder: '',
      rounded: true,
      rowHeight: 100,
      rows: 1,
      shaped: true,    
      menu: false,
      name: '',
      email: '',
      date:'',
      age: '',
      cel:'',
      select: null,
      country:'',
      countries: ['Afghanistan', 'Albania', 'Algeria', 'Andorra', 'Angola', 'Anguilla', 'Antigua &amp; Barbuda', 'Argentina', 'Armenia', 'Aruba', 'Australia', 'Austria', 'Azerbaijan', 'Bahamas', 'Bahrain', 'Bangladesh', 'Barbados', 'Belarus', 'Belgium', 'Belize', 'Benin', 'Bermuda', 'Bhutan', 'Bolivia', 'Bosnia &amp; Herzegovina', 'Botswana', 'Brazil', 'British Virgin Islands', 'Brunei', 'Bulgaria', 'Burkina Faso', 'Burundi', 'Cambodia', 'Cameroon', 'Cape Verde', 'Cayman Islands', 'Chad', 'Chile', 'China', 'Colombia', 'Congo', 'Cook Islands', 'Costa Rica', 'Cote D Ivoire', 'Croatia', 'Cruise Ship', 'Cuba', 'Cyprus', 'Czech Republic', 'Denmark', 'Djibouti', 'Dominica', 'Dominican Republic', 'Ecuador', 'Egypt', 'El Salvador', 'Equatorial Guinea', 'Estonia', 'Ethiopia', 'Falkland Islands', 'Faroe Islands', 'Fiji', 'Finland', 'France', 'French Polynesia', 'French West Indies', 'Gabon', 'Gambia', 'Georgia', 'Germany', 'Ghana', 'Gibraltar', 'Greece', 'Greenland', 'Grenada', 'Guam', 'Guatemala', 'Guernsey', 'Guinea', 'Guinea Bissau', 'Guyana', 'Haiti', 'Honduras', 'Hong Kong', 'Hungary', 'Iceland', 'India', 'Indonesia', 'Iran', 'Iraq', 'Ireland', 'Isle of Man', 'Israel', 'Italy', 'Jamaica', 'Japan', 'Jersey', 'Jordan', 'Kazakhstan', 'Kenya', 'Kuwait', 'Kyrgyz Republic', 'Laos', 'Latvia', 'Lebanon', 'Lesotho', 'Liberia', 'Libya', 'Liechtenstein', 'Lithuania', 'Luxembourg', 'Macau', 'Macedonia', 'Madagascar', 'Malawi', 'Malaysia', 'Maldives', 'Mali', 'Malta', 'Mauritania', 'Mauritius', 'Mexico', 'Moldova', 'Monaco', 'Mongolia', 'Montenegro', 'Montserrat', 'Morocco', 'Mozambique', 'Namibia', 'Nepal', 'Netherlands', 'Netherlands Antilles', 'New Caledonia', 'New Zealand', 'Nicaragua', 'Niger', 'Nigeria', 'Norway', 'Oman', 'Pakistan', 'Palestine', 'Panama', 'Papua New Guinea', 'Paraguay', 'Peru', 'Philippines', 'Poland', 'Portugal', 'Puerto Rico', 'Qatar', 'Reunion', 'Romania', 'Russia', 'Rwanda', 'Saint Pierre &amp; Miquelon', 'Samoa', 'San Marino', 'Satellite', 'Saudi Arabia', 'Senegal', 'Serbia', 'Seychelles', 'Sierra Leone', 'Singapore', 'Slovakia', 'Slovenia', 'South Africa', 'South Korea', 'Spain', 'Sri Lanka', 'St Kitts &amp; Nevis', 'St Lucia', 'St Vincent', 'St. Lucia', 'Sudan', 'Suriname', 'Swaziland', 'Sweden', 'Switzerland', 'Syria', 'Taiwan', 'Tajikistan', 'Tanzania', 'Thailand', 'Timor L\'Este', 'Togo', 'Tonga', 'Trinidad &amp; Tobago', 'Tunisia', 'Turkey', 'Turkmenistan', 'Turks &amp; Caicos', 'Uganda', 'Ukraine', 'United Arab Emirates', 'United Kingdom', 'United States', 'Uruguay', 'Uzbekistan', 'Venezuela', 'Vietnam', 'Virgin Islands (US)', 'Yemen', 'Zambia', 'Zimbabwe'],
      state:[''],
      CRO:'',
      items: [
        'Item 1',
        'Item 2',
        'Item 3',
        'Item 4'
      ],
      checkboxPaciente: null,
      checkboxDentista: null,
      dictionary: {
        attributes: {
          email: 'E-mail Address'
          // custom attributes
        },
        custom: {
          name: {
            required: () => 'Este campo é obrigatório',
            max: 'O campo nome não pode ter menos de 10 caracteres'
            // custom messages
          },
          select: {
            required: 'Este campo é obrigatório'
          }
        }
      },
      rules: {
        age: [val => val < 10 || `I don't believe you!`]
      }
    }
  },
  watch: {
    menu (val) {
      val && setTimeout(() => (this.$refs.picker.activePicker = 'YEAR'))
    }
  },
   
  methods: {
    clear () {
      this.name = ''
      this.email = ''
      this.select = null
      this.checkbox = null
      this.$refs.form.reset()
    },
    save (date) {
      this.$refs.menu.save(date)
    },
    submit () {
      
    }
  }
}
</script>
<style scoped>
.background-image {
  position: relative;
  width: 100%;
  height: 100%;
  background-image:
    linear-gradient(
      rgba(24, 23, 26, 0.75),
      rgba(24, 23, 26, 0.75)
    ),
    url(~assets/images/background-green.png);
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
}
</style>
