
<template>
  <button @click = "showHide" >
    <span v-if = "isHidden">Hide</span>
    <span v-if = "!isHidden">Show</span>
  
  </button>
  <ul v-if = this.isHidden>
    <li v-for = "a in list">{{a}}</li>
  </ul>
</template>


<script>





export default {

  data(){
        return{
            list: [
              "Home","Game","Download","About us"
            ],
            isHidden : true,
            
        }
    },

    methods: {
      showHide(){
        this.isHidden = !this.isHidden

        
      }
    }
 
 
}


</script>

<style >
li{
  padding: 30px;
  display: inline-block;
  list-style: none;
  color: blue;
}

</style>
