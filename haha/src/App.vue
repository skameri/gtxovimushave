<template>
  <div class="navbar">
    <img src="./line-art-car-with-swoosh-5986ld-removebg-preview.png"  class="logo">
    <input  class="filter" v-model = "search" placeholder="Search">
    <button @click="showCart" class="cart">Cart</button>
    <button  @click = "startSelling" class="sell-car">Sell</button>
  </div>
  <div class="gela" v-bind:style="{ display: showSelling }  ">
    <p>Sell</p>
    <input class="myInputt" v-model = "newName" placeholder="name">  
  <input class="myInputt" v-model = "newPrice" placeholder="price (in $)">
    <input class="myInputt" v-model = "newImage" placeholder="image(src)">
    <button class="gilaki" @click="addit">add to listing</button>
  </div>
  <div v-if = "isVisible" class="myCart">
    <ul>
      <li v-for = "i in favorites ">
        <p class="item-in-cart">{{ i  }}</p>
      </li>
      <button class="cart" @click="removeItem">Clear cart</button>
    </ul>
  </div>
  <div class="cards-background">
    <div class="car" v-for = "a in pagedCars">
      <img v-bind:src="a.img.cover">
      <p class="car-name">{{ a.name + " "  }}  </p>
      <p class="myPrice">{{ a.price + "GEL" }}</p>
      <button @click="addToCart" :id= a.name class="purchase">Add to cart</button>
    </div>
    
  </div>
  <div class="pagination">
      <button @click="prevPage">Previous</button>
      <span>{{ page }} / {{ totalPages }}</span>
      <button @click="nextPage">Next</button>
  </div>
</template>
  <script>
  import axios from "axios"
  export default {
    data() {
      return {
        isVisible: false,
        showSelling: "none",
        newName:"",
        newYear: null,
        newImage:"",
        search: "",
        car: [
        ],
        favorites: [],
        page: 1,
        itemsPerPage: 6,
      }
      
    },
    mounted(){
    axios.get("https://items.magischer.de/api/products")
        .then((response) => {
          this.car = response.data.data
          console.log(this.car.id)
        })
        .catch(console.log(""))
      },
    methods:{
      showCart(){
        this.isVisible = !this.isVisible
      },
      removeItem(e){
        this.favorites.splice(e.target.id)
      },
      addToCart(e){
        this.favorites.push(e.target.id)
      },
      startSelling(){
        this.showSelling = "flex"
      },
      addit(){
        this.car.push({price:this.newPrice,name:this.newName,year:this.newYear,img:this.newImage})
      },
      prevPage() {
        if (this.page > 1) {
          this.page--;
        }
      },
      nextPage() {
        if (this.page < this.totalPages) {
          this.page++;
        }
      },
      
    },
    computed: {
      filterCars: function(){
        return this.car.filter((a) => {
          return a.name.toLowerCase().match(this.search.toLowerCase())
        })
      },
      totalPages() {
        return Math.ceil(this.filterCars.length / this.itemsPerPage);
      },
      pagedCars() {
        let start = (this.page - 1) * this.itemsPerPage;
        let end = start + this.itemsPerPage;
        return this.filterCars.slice(start, end);
      },
    },
  }
  </script>

  <style>
  .item-in-cart{
    
    color: black;
    font-family: Arial, Helvetica, sans-serif

  }
  li{
    list-style:none;
  }
  .pagination {
    display: flex;
    justify-content: center;
    margin-bottom: 0px;
  }
  .pagination button {
    padding: 10px 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
    margin: 0 10px;
    cursor: pointer;
  }
  .myCart{
    width: 500px;
    height: 500px;
    background-color:#7B8FA1;
    margin-left: 500px;
  }
  .cart{
    margin-left: 50px;
    width: 100px;
    height: 40px;
    border: none;
    border-radius: 10px;
  
    cursor: pointer;
  }
  .myCart .cart{
   
    margin-left: 70%;
  }

  .sell-car{
    margin-left: 450px;
    width: 100px;
    height: 30px;
    border: none;
    border-radius: 10px;
    cursor: pointer;
  }

  .year{
    font-size: 30px;
    margin-top: 260px;
    
  }
  .car-name{
    font-weight: bold;
    color:chocolate;
    font-family: Arial, Helvetica, sans-serif;
    font-size: 20px;
    margin-top: 150px;
    margin-left: -50%;
  }

  img:not(.logo){
    width: 150px;
    height: 150px;
    margin-top: -120px;
    
    
    border-radius: 50%;
  }

  .cards-background{
    border-radius: 10px;
    margin-left: 90px;
    width: 90%;
    height: 100%;
    background-color: #CFB997;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
  }
  .car{
    border-radius: 13px;
    margin-top: 50px;
    margin-left: 100px;
    background-color: #7B8FA1;
    width: 280px;
    height: 300px;
    display: flex;
    align-items: center;
    justify-content: center;
  }


  .logo{
    width: 200px;
    margin-top: -20px;
    margin-left: -30px;

  }
  .navbar{
    display: flex;
    align-items: center;
  }
  .card{
    background-color: aliceblue;
    
  }
  .filter{
    margin-left: 27%;
    width: 300px;
    height: 40px;
    border-radius: 8px;
    padding-left: 10px;
    border: none;
    
  }
  .filter:hover{
    box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
  }
  .filter:focus {
    outline: none;
}

.cards-background {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    background-color:#7B8FA1;
    padding: 20px;
  }
  
  .car {
    width: 300px;
    height: 400px;
    background-color:#CFB997;
    margin: 20px;
    text-align: center;
    box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.1);
  }
  
 
  
  .car-name {
    font-size: 18px;
    font-weight: bold;
    margin-top: 100px;
  }
  
  .myPrice {
    font-size: 20px;
    color: green;
    margin-top: 200px;
  }
  
  .purchase {
    width: 60%;
    height: 40px;
    background-color: green;
    color: white;
    font-size: 16px;
    margin-top: 20px;
    margin-left: -50px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }

  .gela{
    width: 500px;
    background-color: #f2f2f2;
    padding: 20px;
    text-align: center;
    box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.1);
  }
  
  p {
    font-size: 18px;
    font-weight: bold;
    margin-bottom: 20px;
  }
  
  .myInputt{
    width: 80%;
    height: 40px;
    margin-bottom: 20px;
    padding: 10px;
    font-size: 16px;
    border: 1px solid lightgray;
    border-radius: 5px;
  }
  
  .gilaki{
    width: 80%;
    height: 40px;
    background-color: green;
    color: white;
    font-size: 16px;
    margin-top: 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }

</style>
  
