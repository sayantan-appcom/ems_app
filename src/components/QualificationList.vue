<template>
    <v-select
      :items="qualifications"
      item-text= "name"
      item-value= "id"
      prepend-icon="list"
      label="Qualification"
      :error-messages="error"
      @input="$emit('input',$event)"
    >
    </v-select>
</template>

<script>
export default {
  name: 'QualificationList',
  props: {
    error: {
      type: Array,
      required: false
    }
  },
  data(){
    return {
      qualifications: [],
    }
  },

  methods:{

  },

  created(){
    axios.get('/qualifications')
      .then((response, data) => {
       response.data.forEach(item => {
          this.qualifications.push(item)
        });
      })
      .catch(error => {
        console.log(error)
      })
  }
}
</script>
