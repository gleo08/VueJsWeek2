<template>
  <div class="big">
    <ul class="detail">
      <li class="list" v-for="item in items" :key="item.id">
          <div class="product">
            <img class="image" v-bind:src="item.src"/>
            <p class="info">{{ item.name }} - {{priceUsd(item.price)}}</p>
          </div>
      </li>
    </ul>
    <p class="analyzer">Quantity of product: {{countProduct(items)}}</p>
    <p class="analyzer">Quantity of sale product: {{countProductSale(items)}}</p>
    <p class="analyzer">Value of all products: {{valueOfProducts(items)}}</p>
    <p class="analyzer">Average price of products: {{normalize(valueOfProducts(items) / countProduct(items))}}</p>

  </div>
</template>

<script>
import image1 from "./asset/1.jpg"
import image2 from "./asset/2.jpg"
import image3 from "./asset/3.jpg"
import image4 from "./asset/4.jpg"
import image5 from "./asset/5.jpg"
import image6 from "./asset/6.jpg"

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
    const priceUsd = (value) => {
      return '$' + value.toFixed(2).replace(/(\d)(?=(\d\d\d)+(?!\d))/g, "$1,");
    }

    const countProduct = (items) =>{
      return items.length
    }

    const countProductSale = (items) =>{
      return items.filter(items => items.sale).length
    }

    const valueOfProducts = (items) => {
      var sum = 0
      for (let i in items) {
        sum += items[i].price
      }
      return sum
    }

    const normalize = (value) => {
      return value.toFixed(2)
    }
    return {
      items,
      priceUsd,
      countProduct,
      countProductSale,
      valueOfProducts,
      normalize,
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

