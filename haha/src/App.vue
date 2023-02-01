<template>
  <div class="navbar">
    <input  class="filter" v-model = "search" placeholder="Search">
    <button @click="showCart" class="cart">Cart</button>
    <button  @click = "startSelling" class="sell-car">Sell</button>
  </div>
  <div class="gela" v-bind:style="{ display: showSelling }  ">
    <p>Sell</p>
    <input class="myInputt" v-model = "newName" placeholder="name">  
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
import { ref, computed, onMounted } from "vue";
import axios from "axios";

export default {
  setup() {
    const isVisible = ref(false);
    const showSelling = ref("none");
    const newName = ref("");
    const newYear = ref(null);
    const newImage = ref("");
    const search = ref("");
    const car = ref([]);
    const favorites = ref([]);
    const page = ref(1);
    const itemsPerPage = ref(6);

    onMounted(() => {
      axios
        .get("https://items.magischer.de/api/products")
        .then((response) => {
          car.value = response.data.data;
          console.log(car.value.id);
        })
        .catch(console.log(""));
    });

    const showCart = () => {
      isVisible.value = !isVisible.value;
    };

    const removeItem = (e) => {
      favorites.value.splice(e.target.id);
    };

    const addToCart = (e) => {
      favorites.value.push(e.target.id);
    };

    const startSelling = () => {
      showSelling.value = "flex";
    };

    const addit = () => {
      car.value.push({
        name: this.newName.value,
        year: this.newYear.value,
        img: this.newImage.value,
      });
    };

    const prevPage = () => {
      if (page.value > 1) {
        page.value--;
      }
    };

    const nextPage = () => {
      if (page.value < totalPages) {
        page.value++;
      }
    };

    const filterCars = computed(() => {
      return car.value.filter((a) => {
        return a.name.toLowerCase().match(search.value.toLowerCase());
      });
    });

    const totalPages = computed(() => {
      return Math.ceil(filterCars.value.length / itemsPerPage.value);
    });

    const pagedCars = computed(() => {
      let start = (page.value - 1) * itemsPerPage.value;
      let end = start + itemsPerPage.value;
      return filterCars.value.slice(start, end);
    });

    return {
      isVisible,
      showSelling,
      newName,
      newYear,
      newImage,
      search,
      car,
      favorites,
      page,
      itemsPerPage,
      showCart,
      removeItem,
      addToCart,
      startSelling,
      addit,
      prevPage,
      nextPage,
      filterCars,
      totalPages,
      pagedCars,
    };
  },
};
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
  
