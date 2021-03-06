<template>
<v-container fluid>
    <v-layout align-center justify-center>
      <v-flex xs12 sm8 md8>
        <v-alert
          :value=show_message
          :color=message_type
          :icon=message_icon
          outline
        >
          {{message_text}}
        </v-alert>
        <v-card class="elevation-6">
          <v-toolbar dark color="blue-grey darken-3">
            <v-toolbar-title>Create New Office</v-toolbar-title>
          </v-toolbar>
          <v-card-text>
            <v-form>
              <v-text-field
                prepend-icon="person"
                name="office_name"
                label="Office Name"
                type="text"
                v-model="office_name"
                v-validate="'required'"
                :error-messages="errors.collect('office_name')"
                data-vv-name="office_name"
              ></v-text-field>

              <v-text-field
                prepend-icon="email"
                name="identification_code"
                label="Identification Code eg. DDO Code/IFSC/DISE Code alike"
                type="text"
                v-model="identification_code"
                v-validate="'required'"
                :error-messages="errors.collect('identification_code')"
                data-vv-name="identification_code"
              ></v-text-field>

              <v-text-field
                prepend-icon="email"
                name="officer_designation"
                label="Designation of Head of Office"
                type="text"
                v-model="officer_designation"
                v-validate="'required|alpha'"
                :error-messages="errors.collect('officer_designation')"
                data-vv-name="officer_designation"
              ></v-text-field>

              <v-text-field
                prepend-icon="email"
                name="office_address"
                label="Office Address"
                type="text"
                v-model="office_address"
                v-validate="'required|alpha'"
                :error-messages="errors.collect('office_address')"
                data-vv-name="office_address"
              ></v-text-field>

              <v-text-field
                prepend-icon="email"
                name="post_office"
                label="Post Office"
                type="text"
                v-model="post_office"
                v-validate="'required|alpha'"
                :error-messages="errors.collect('post_office')"
                data-vv-name="post_office"
              ></v-text-field>

              <v-text-field
                prepend-icon="email"
                name="pin"
                label="Pincode"
                type="text"
                v-model="pin"
                v-validate="'required|digits:6'"
                :error-messages="errors.collect('pin')"
                data-vv-name="pin"
              ></v-text-field>

              <subdivision-list
                v-model="subdivision_id"
                v-validate="'required'"
                data-vv-name="subdivision_id"
                :error="errors.collect('subdivision_id')"
              ></subdivision-list>

              <block-muni-list
                v-model="block_muni_id"
                v-validate="'required'"
                data-vv-name="block_muni_id"
                :error="errors.collect('block_muni_id')"
              ></block-muni-list>

              <police-station-list
                v-model="police_station_id"
                v-validate="'required'"
                data-vv-name="police_station_id"
                :error="errors.collect('police_station_id')"
              ></police-station-list>

              <assembly-list
                v-model="ac_id"
                v-validate="'required'"
                data-vv-name="ac_id"
                :error="errors.collect('ac_id')"
              ></assembly-list>

              <pc-list
                v-model="pc_id"
                v-validate="'required'"
                data-vv-name="pc_id"
                :error="errors.collect('pc_id')"
              ></pc-list>

              <category-list
                v-model="category_id"
                v-validate="'required'"
                data-vv-name="category_id"
                :error="errors.collect('category_id')"
              ></category-list>

              <institute-list
                v-model="institute_id"
                v-validate="'required'"
                data-vv-name="institute_id"
                :error="errors.collect('institute_id')"
              ></institute-list>

              <v-text-field
                prepend-icon="email"
                name="email"
                label="Email"
                type="text"
                v-model="email"
                v-validate="'required|email'"
                :error-messages="errors.collect('email')"
                data-vv-name="email"
              ></v-text-field>

              <v-text-field
                prepend-icon="email"
                name="phone"
                label="Phone No"
                type="text"
                v-model="phone"
                v-validate="'digits:11'"
                :error-messages="errors.collect('phone')"
                data-vv-name="phone"
              ></v-text-field>

              <v-text-field
                prepend-icon="email"
                name="mobile"
                label="Mobile of Head of Office"
                type="text"
                v-model="mobile"
                v-validate="'required|digits:10'"
                :error-messages="errors.collect('mobile')"
                data-vv-name="mobile"
              ></v-text-field>

              <v-text-field
                prepend-icon="email"
                name="fax"
                label="Fax"
                type="text"
                v-model="fax"
                v-validate="'numeric'"
                :error-messages="errors.collect('fax')"
                data-vv-name="fax"
              ></v-text-field>

              <v-text-field
                prepend-icon="email"
                name="male_staff"
                label="Male Staff (in count)"
                type="text"
                v-model="male_staff"
                v-validate="'required|numeric'"
                :error-messages="errors.collect('male_staff')"
                data-vv-name="male_staff"
              ></v-text-field>

              <v-text-field
                prepend-icon="email"
                name="female_staff"
                label="Female Staff (in count)"
                type="text"
                v-model="female_staff"
                v-validate="'required|numeric'"
                :error-messages="errors.collect('female_staff')"
                data-vv-name="female_staff"
              ></v-text-field>

              <v-text-field
                prepend-icon="email"
                name="total_staff"
                label="Total Staff"
                type="text"
                v-model="total_staff"
                v-validate="'required|digits:4'"
                :error-messages="errors.collect('total_staff')"
                data-vv-name="total_staff"
              ></v-text-field>

            </v-form>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="primary" @click="validateOffice" :disabled="disable_save">Save</v-btn>
          </v-card-actions>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>
<script>
  import SubdivisionList from '@/components/SubdivisionList'
  import BlockMuniList from '@/components/BlockMuniList'
  import PoliceStationList from '@/components/PoliceStationList'
  import AssemblyList from '@/components/AssemblyList'
  import PcList from '@/components/PcList'
  import CategoryList from '@/components/CategoryList'
  import InstituteList from '@/components/InstituteList'

  export default{
    name: 'Office',

    components: {
      'subdivision-list': SubdivisionList,
      'block-muni-list': BlockMuniList,
      'police-station-list': PoliceStationList,
      'assembly-list': AssemblyList,
      'pc-list': PcList,
      'category-list': CategoryList,
      'institute-list': InstituteList,
    },

    $_veeValidate: {
      validator: 'new'
    },

    data (){
      return {
        valid: true,
        office_name: '',
        identification_code: '',
        subdivision_id: '',
        block_muni_id: '',
        office_address: '',
        officer_designation: '',
        post_office: '',
        pin: '',
        police_station_id: '',
        ac_id: '',
        pc_id: '',
        category_id: '',
        institute_id: '',
        email: '',
        phone: '',
        mobile: '',
        fax: '',
        total_staff: 0,
        male_staff: 0,
        female_staff: 0,
        show_message: false,
        message_type: "",
        message_icon: "",
        message_text: "",
        disable_save: false,

        dictionary: {

          custom: {
            office_name: {
              required: 'Office Name can not be empty',
            },
            identification_code: {
              required: 'Identification Code is required'
            },
            subdivision_id: {
              required: 'Subdivision is required'
            },
            block_muni_id: {
              required: 'Block/Municipality is required'
            }
          }
        }

      }
    },
    mounted () {
      this.$validator.localize('en', this.dictionary)
    },
    methods: {
      validateOffice(){
        this.disable_save = true
        this.$validator.validate()
          .then(result => {
            result ? this.saveOffice() : this.showError()
            this.disable_save = false
          })
      },
      showError(){
        this.show_message = true
        this.message_type = 'error'
        this.message_icon = 'warning'
        this.message_text = 'Error Occurred!!!'
      },
      saveOffice(){
        axios.post('/office',{
          office_name: this.office_name,
          identification_code: this.identification_code,
          officer_designation: this.officer_designation,
          office_address: this.office_address,
          post_office: this.post_office,
          pin: this.pin,
          subdivision_id: this.subdivision_id,
          block_muni_id: this.block_muni_id,
          police_station_id: this.police_station_id,
          ac_id: this.ac_id,
          pc_id: this.pc_id,
          category_id: this.category_id,
          institute_id: this.institute_id,
          identification_code: this.identification_code,
          email: this.email,
          phone: this.phone,
          mobile: this.mobile,
          fax: this.fax,
          total_staff: this.total_staff,
          male_staff: this.male_staff,
          female_staff: this.female_staff,
        })
        .then(response => {
          this.show_message = true
          this.message_type = 'success'
          this.message_icon = 'check_circle'
          this.message_text = 'Office Added Successfully'
        })
        .catch(error => {
          this.show_message = true
          this.message_type = 'error'
          this.message_icon = 'warning'
          this.message_text = 'Error Occurred!!!'
          console.log(error.statusText)
        })
      }
    },
    computed: {

    }

  }
</script>
