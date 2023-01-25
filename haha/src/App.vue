
<template>
  <button @click = "showHide" >
    <span v-if = "isHidden">Hide</span>
    <span v-if = "!isHidden">Show</span>
  </button>
  <ul v-if = this.isHidden>
    <li v-for = "  a in list" :key = "a.id"><a :href="a.link">{{ a.name }}</a> </li>
  </ul>
</template>


<script>



export default {

  data(){
        return{
            list: [
              {id: 1 , name: "Home", link: "https://stackoverflow.com/questions/40899532/how-to-pass-a-value-from-vue-data-to-href"},
              {id: 2 , name: "Game",link: "https://github.com/skameri/gtxovimushave"},
              {id: 3 , name: "Download",link: "https://us06web.zoom.us/postattendee?mn=2kFMiXB3K5_1iia5Mq_eziO8Fks6e5f0m-tg.z8SxurzTCDMr21fh"},
              {id: 4 , name: "About us",link: "https://vuejs.org/guide/quick-start.html#creating-a-vue-application"},
              
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

button{
  margin-top: 40px;
  width: 60px;
  height: 21px;
}

</style>
