<template>
    <v-select
      :items="pcs"
      item-text= "name"
      item-value= "id"
      prepend-icon="list"
      label="Parliamentary Constituency"
      :error-messages="error"
      @input="$emit('input',$event)"
    >
    </v-select>
</template>

<script>
export default {
  name: 'PcList',
  props: {
    error: {
      type: Array,
      required: false
    }
  },
  data(){
    return {
      pcs: [],
    }
  },

  methods:{

  },

  created(){
    axios.get('/pcs')
      .then((response, data) => {
       response.data.forEach(item => {
          this.pcs.push(item)
        });
      })
      .catch(error => {
        console.log(error)
      })
  }
}
</script>
