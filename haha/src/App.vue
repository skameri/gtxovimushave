
<template>

  <button @click = "showHide" >
    <span v-if = "isHidden">Hide</span>
    <span v-if = "!isHidden">Show</span>
  </button>
  <ul v-if = this.isHidden>
    <li  v-for = "  a in list" key = "a.id" @click.prevent = "guka" ><a :href="a.link"  :id=a.info>{{ a.name }} </a> </li>
    <div >{{ info }}</div>
  </ul>
  
</template>


<script>



export default {

  data(){
        return{
            list: [
              {id: 1 , name: "Home", link: "https://stackoverflow.com/questions/40899532/how-to-pass-a-value-from-vue-data-to-href", info:"random information home"},
              {id: 2 , name: "Game",link: "https://github.com/skameri/gtxovimushave",info:"random information game"},
              {id: 3 , name: "Download",link: "https://us06web.zoom.us/postattendee?mn=2kFMiXB3K5_1iia5Mq_eziO8Fks6e5f0m-tg.z8SxurzTCDMr21fh",info:"random information download"},
              {id: 4 , name: "About us",link: "https://vuejs.org/guide/quick-start.html#creating-a-vue-application",info:"random information about us"},
              
            ],
            isHidden : true,
            info:"",
            
        }
    },

    methods: {
      showHide(){
        this.isHidden = !this.isHidden
      },
      guka(e){
        this.info = e.target.getAttribute("id")
     
        console.log(e.target.getAttribute("id"))
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
