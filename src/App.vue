<template>
  <div class="ss">
    <div class="input-group rounded">
      <input type="search" @keyup="searchProduct" class="form-control rounded" placeholder="Search" aria-label="Search"
    aria-describedby="search-addon" />
    </div>
    <select @change="optionSort" class="custom-select" id="inputGroupSelect01">
        <option selected disable value="">Choose...</option>
        <option value="1">Sort by A-Z</option>
        <option value="2">Sort by Z-A</option>
      </select>
  </div>
  <div class="big">
    <ul class="detail">
      <li class="list" v-for="item in itemsDisplay" :key="item.id">
          <div class="product">
            <img class="image" v-bind:src="item.src"/>
            <p class="info">{{ item.name }} - {{priceUsd(item.price)}}</p>
          </div>
      </li>
    </ul>
    <div class="analyzer">
      <p>Product quantity: {{countProduct()}}</p>
      <p>Value of all products: {{priceUsd(valueOfProducts())}}</p>
      <p>Sale product: {{countProductSale()}}</p>
    </div>
  </div>
</template>

<script>
import image1 from "./asset/1.jpg"
import image2 from "./asset/2.jpg"
import image3 from "./asset/3.jpg"
import image4 from "./asset/4.jpg"
import image5 from "./asset/5.jpg"
import image6 from "./asset/6.jpg"
import {ref, onMounted} from "vue"

export default {
  name: "App",
  setup() {
    const items = [
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
  ]

    const itemsDisplay = ref([])

    onMounted(() => {
      itemsDisplay.value = items
    })

    const priceUsd = (value) => {
      return '$' + value.toFixed(2).replace(/(\d)(?=(\d\d\d)+(?!\d))/g, "$1,");
    }

    const countProduct = () =>{
      return items.length
    }

    const countProductSale = () =>{
      return items.filter(items => items.sale).length
    }

    const valueOfProducts = () => {
      var sum = 0
      for (let i in items) {
        sum += items[i].price
      }
      return sum
    }
    
    const sort1 = () => {
      itemsDisplay.value = itemsDisplay.value.sort((p1, p2) => {
        return p1.price - p2.price
      })
    }

    const sort2 = () => {
      itemsDisplay.value = itemsDisplay.value.sort((p1, p2) => {
        return p2.price - p1.price;
      })
    }

    const optionSort = (e) => {
      if (e.target.value == 1) {
        sort1();
      } else {
        sort2();
      }
    }

    const searchProduct = (e) => {
      let regexValue = new RegExp(e.target.value, "i")
      itemsDisplay.value = items.filter((item) => {
        return item.name.match(regexValue)
      })
    }

    return {
      itemsDisplay,
      searchProduct,
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

.ss {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.input-group {
  width: 50%;
  height: 30px;
}
.form-control {
  height: 100%;
  width: 80%;
}

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
  height: auto;
  width: 100%;
  max-width: 100%;
}
.info {
  font-size: 20px;
  font-weight: bold;
}
.product {
  width: 100%;
}
.list {
  width: calc(100%/3);
  list-style-type: none;
}
.analyzer {
  font-size: 30px;
  font-weight: bold;
}
@media (max-width: 768px) {
  .list {
    width: calc(100%/2);
  }
  .info {
    font-size: 13px;
  }
}

</style>

