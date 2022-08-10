<template>
  <div class="products-wrap">
    <div class="select">
      <select
        class="select-sort"
        v-model="selected"
        @change="sortProducts(selected)">
        <option value="default">По умолчанию</option>
        <option value="minPriceSort">По цене min</option>
        <option value="maxPriceSort">По цене max</option>
        <option value="nameSort">По имени</option>
      </select>
    </div>
    <div class="products">
      <div
        v-for="product in this.products"
        class="products__item"
        :key="product.id">
        <button
          class="products__del"
          @click="deleteProduct(product['id'])">
        </button>
        <img v-bind:src="product['img']" class="products__img" />
        <h3 class="products__title">{{ product['title'] }}</h3>
        <p class="products__description">{{ product['description'] }}</p>
        <p class="products__price">{{ product['price'] }} руб.</p>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'ProductsList',
  props: {
    products: {
      id: Number,
      title: String,
      description: String,
      link: String,
      price: String,
    },
    sortProducts: Function,
    deleteProduct: Function,
  },
  data() {
    return {
      selected: 'default',
    }
  },
}
</script>
<style lang="scss" scoped>
.products-wrap {
  display: flex;
  flex-direction: column;
}
.select {
  position: relative;
  display: inline-block;
  margin-left: auto;
  margin-bottom: 15px;

  .select-sort {
    width: 122px;
    background: #fffefb;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    margin-left: auto;
    font-family: 'Source Sans Pro';
    font-style: normal;
    font-weight: 400;
    font-size: 12px;
    line-height: 15px;
    color: #b4b4b4;
    margin-left: auto;
    padding: 10px 23px 11px 16px;
    border: none;
    outline: none;
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
  }

  &:after {
    content: '';
    position: absolute;
    right: 16px;
    top: 16px;
    z-index: 1;
    width: 8px;
    height: 6px;
    display: block;
    pointer-events: none;
    box-sizing: border-box;
    background: url(../assets/img/arrow-down.png);
    background-repeat: no-repeat;
    background-position: center;
  }
}

.products {
  display: flex;
  flex-wrap: wrap;
  max-width: 1028px;

  .products__item {
    width: 332px;
    max-width: 332px;
    margin-right: 16px;
    background: #fffefb;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
      0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
    margin-bottom: 16px;
    position: relative;
    display: flex;
    flex-direction: column;

    &:nth-child(3n) {
      margin-right: 0;
    }

    &:hover {
      cursor: pointer;
      .products__del {
        display: block;
      }
    }

    .products__del {
      content: '';
      display: none;
      width: 32px;
      height: 32px;
      border-radius: 10px;
      background: #ff8484;
      box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
      background-image: url(../assets/img/basket.png);
      background-position: center;
      background-repeat: no-repeat;
      position: absolute;
      top: -8px;
      right: -8px;
      border: none;
    }

    .products__img {
      height: 200px;
      margin-bottom: 12px;
    }

    .products__title {
      font-weight: 600;
      font-size: 20px;
      line-height: 25px;
      color: #3f3f3f;
      margin-top: 0;
      margin-bottom: 16px;
      padding: 0 16px;
    }

    .products__description {
      font-weight: 400;
      font-size: 16px;
      line-height: 20px;
      color: #3f3f3f;
      margin-bottom: 32px;
      padding: 0 16px;
      margin-bottom: auto;
    }

    .products__price {
      font-weight: 600;
      font-size: 24px;
      line-height: 30px;
      color: #3f3f3f;
      padding: 0 16px;
    }
  }
}

@media (max-width: 1420px) {
  .products {
    .products__item {
      margin-right: 15px;
      width: calc(33.3% - 10px);
    }
  }
}

@media (max-width: 1200px) {
  .products {
    margin-right: auto;
    margin-left: auto;
    .products__item {
      width: calc(50% - 10px);

      &:nth-child(3n) {
        margin-right: 15px;
      }

      &:nth-child(2n) {
        margin-right: 0;
      }
    }
  }
}

@media (max-width: 1024px) {
  .select {
    margin-right: auto;
  }

  .products {
    justify-content: center;
  }
}

@media (max-width: 576px) {
  .products {
    .products__item {
      width: 100%;
      margin-left: auto;
      margin-right: auto;

      &:nth-child(2n) {
        margin-right: auto;
      }
      &:nth-child(3n) {
        margin-right: auto;
      }
    }
  }
}
</style>
