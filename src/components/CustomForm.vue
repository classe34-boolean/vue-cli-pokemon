<template>
  <form @submit.prevent>
      <input 
        type="text" 
        :placeholder="inputPlaceholder"
        v-model.trim="searchText"
        >
      <input 
        type="submit" 
        value="Cerca"
        @click="$emit('sendForm', searchText)"
        > 
  </form>
</template>

<script>
export default {
    name: "CustomForm",
    data() {
        return {
            searchText: ''
        }
    },
    props: [ "inputPlaceholder" ],
    methods: {
        
    }
}
</script>

<style lang="scss" scoped>
    form {
       margin: 20px 0;  

       input {
            padding: 5px;
            margin-right: 10px;

            &[type="text"] {
                width: 300px;
            }
        }  
    } 
</style>