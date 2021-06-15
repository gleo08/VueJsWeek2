<template>
  <input @keyup="searchProduct">
  <div class="big">
    <ul class="detail">
      <li class="list" v-for="item in items" :key="item.id">
          <div class="product">
            <img class="image" v-bind:src="item.src"/>
            <p class="info">{{ item.name }} - {{priceUsd(item.price)}}</p>
          </div>
      </li>
    </ul>
  </div>

  <div class="input-group mb-3">
  <div class="input-group-prepend">
    <label class="input-group-text" for="inputGroupSelect01">Options</label>
  </div>
  <select v-model="selected" @change="optionSort(selected)" class="custom-select" id="inputGroupSelect01">
    <option selected disable value="">Choose...</option>
    <option value="1">Sort by A-Z</option>
    <option value="2">Sort by Z-A</option>
  </select>
  <p>Value selected: {{ selected }}</p>
</div>

</template>

<script>
import image1 from "./asset/1.jpg"
import image2 from "./asset/2.jpg"
import image3 from "./asset/3.jpg"
import image4 from "./asset/4.jpg"
import image5 from "./asset/5.jpg"
import image6 from "./asset/6.jpg"
import {ref} from "vue"

export default {
  name: "App",
  setup() {
    const selected = ref("")
    const items = ref([
      {
        id: 1,
        name: "Jordan 1",
        src: image1,
        price: 2500,
        sale: true,
      }, 
      {
        id: 2,
        name: "Jordan 1",
        src: image2,
        price: 2700,
        sale: true,
      },
      {
        id: 3,
        name: "Jordan 1",
        src: image3,
        price: 2800,
        sale: true,
      },
      {
        id: 4,
        name: "Jordan 1",
        src: image4,
        price: 2800,
        sale: false,
      },
      {
        id: 5,
        name: "Jordan 1",
        src: image5,
        price: 2800,
        sale: false,
      },
      {
        id: 6,
        name: "Jordan 1",
        src: image6,
        price: 3000,
        sale: true,
      },
  ])
    const priceUsd = (value) => {
      return '$' + value.toFixed(2).replace(/(\d)(?=(\d\d\d)+(?!\d))/g, "$1,");
    }

    const countProduct = () =>{
      return items.value.length
    }

    const countProductSale = () =>{
      return items.value.filter(items => items.sale).length
    }

    const valueOfProducts = () => {
      var sum = 0
      for (let i in items) {
        sum += items.value[i].price
      }
      return sum
    }
    
    const sort1 = () => {
      items.value.sort((p1, p2) => {
        return p1.price - p2.price
      })
    }

    const sort2 = () => {
      console.log(1)
      items.value.sort((p1, p2) => {
        return p2.price - p1.price;
      })
    }

    const optionSort = (value) => {
      if (value == 1) {
        sort1();
      }
      if (value == 2) {
        sort2();
      }
    }

    const searchProduct = (e) => {
      console.log(e.target.value)
      let regexValue = new RegExp(e.target.value)
      console.log(regexValue)
      items.value = items.value.filter((item) => {
        return item.name.match(regexValue)
      })
    }

    return {
      selected,
      searchProduct,
      items,
      optionSort,
      priceUsd,
      countProduct,
      countProductSale,
      valueOfProducts,
    }
  },
}
</script>

<style scoped>
.big {
  width: calc(100% - 160px);
  padding: 80px;
}
.detail {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  margin: 0px;
  padding: 0px;
}
.image {
  height: 300px;
  width: 100%;
}
.info {
  font-size: 30px;
  font-weight: bold;
}
.product {
  width: 100%;
}
.list {
  width: calc(100%/3);
}
.analyzer {
  font-size: 30px;
  font-weight: bold;
}
@media (max-width: 768px) {
  .list {
    width: calc(100%/2);
  }
}

</style>

