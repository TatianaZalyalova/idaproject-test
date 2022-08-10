<template>
  <div class="page">
    <div class="container">
      <div class="page__flex">
        <AddProductForm
          :addProduct="addProduct"
        />
        <ProductsList
          v-bind:products="this.products"
          :deleteProduct="deleteProduct"
          :sortProducts="sortProducts"
        />
      </div>
    </div>
  </div>
</template>

<script>
import AddProductForm from '../components/AddProductForm.vue'
import ProductsList from '../components/ProductsList.vue'

export default {
  name: 'App',
  components: {
    AddProductForm,
    ProductsList,
  },

  data() {
    return {
      products: [
        {
          id: 'zzyAB4TgGmJK',
          img: require(`~/assets/img/product.jpg`),
          title: 'Наименование товара',
          description:
            'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: '10 000',
        },
        {
          id: 'MLp2WqtlOHlk',
          img: require(`~/assets/img/product.jpg`),
          title: 'Наименование товара',
          description:
            'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: '10 000',
        },
        {
          id: '9HolMpMeUsN4',
          img: require(`~/assets/img/product.jpg`),
          title: 'Наименование товара',
          description:
            'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: '20 000',
        },
        {
          id: '4B3cE1cuKdr7',
          img: require(`~/assets/img/product.jpg`),
          title: 'Заголовок товара',
          description:
            'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: '10 000',
        },
        {
          id: '7hWYseczEqUBX',
          img: require(`~/assets/img/product.jpg`),
          title: 'Некий заголовок товара',
          description:
            'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: '10 000',
        },
        {
          id: 'fbu1fPDFklyff',
          img: require(`~/assets/img/product.jpg`),
          title: 'Наименование товара',
          description:
            'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: '50 000',
        },
        {
          id: 'QyKxh4c0udC5M',
          img: require(`~/assets/img/product.jpg`),
          title: 'Наименование товара',
          description:
            'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: '10 000',
        },
      ],
    }
  },

  methods: {
    addProduct(obj) {
      this.products.push(obj)
    },
    deleteProduct(id) {
      this.products = this.products.filter((product) => {
        return product.id !== id
      })
    },

    sortProducts(kindSorting) {
      const collator = new Intl.Collator('ru')
      switch (kindSorting) {
        case 'minPriceSort':
          this.products.sort(
            (a, b) =>
              Number(a.price.split(' ').join('')) -
              Number(b.price.split(' ').join(''))
          )
          break
        case 'maxPriceSort':
          this.products.sort(
            (a, b) =>
              Number(b.price.split(' ').join('')) -
              Number(a.price.split(' ').join(''))
          )
          break
        case 'nameSort':
          this.products.sort((a, b) => collator.compare(a.title, b.title))
          break
        case 'default':
          this.products.sort(() => Math.random() - 0.5)
          break
      }
    },
  },
}
</script>
<style lang="scss">
@font-face {
  font-family: 'Source Sans Pro';
  src: local('Source Sans Pro Regular'), local('Source-Sans-Pro-Regular'),
    url('../assets/fonts/SourceSansPro-Regular.woff2') format('woff2'),
    url('../assets/fonts/SourceSansPro-Regular.woff') format('woff'),
    url('../assets/fonts/SourceSansPro-Regular.ttf') format('truetype');
  font-weight: 400;
  font-style: normal;
}

@font-face {
  font-family: 'Source Sans Pro';
  src: local('Source Sans Pro Semi Bold'), local('Source-Sans-Pro-Semi-Bold'),
    url('../assets/fonts/SourceSansPro-SemiBold.woff2') format('woff2'),
    url('../assets/fonts/SourceSansPro-SemiBold.woff') format('woff'),
    url('../assets/fonts/SourceSansPro-SemiBold.ttf') format('truetype');
  font-weight: 600;
  font-style: normal;
}

@font-face {
  font-family: 'Inter';
  src: local('Inter Semi Bold'), local('Inter-Semi-Bold'),
    url('../assets/fonts/Inter-SemiBold.woff2') format('woff2'),
    url('../assets/fonts/Inter-SemiBold.woff') format('woff'),
    url('../assets/fonts/Inter-SemiBold.ttf') format('truetype');
  font-weight: 600;
  font-style: normal;
}

* {
  box-sizing: border-box;
}

body {
  background-color: #f5f5f5;
  margin: 0;
  font-family: 'Source Sans Pro';
}

.header {
  font-weight: 600;
  font-size: 28px;
  line-height: 35px;
  color: #3f3f3f;
  margin-top: 0;
  margin-bottom: 16px;
}

.container {
  max-width: 1376px;
  margin: 0 auto;
}

.page {
  margin-top: 32px;
  margin-bottom: 16px;
  .page__flex {
    display: flex;
    align-items: flex-start;
  }
}

@media (max-width: 1420px) {
  .page {
    margin-right: 20px;
    margin-left: 20px;
  }
}

@media (max-width: 1024px) {
  .page {
    .header {
      text-align: center;
    }
    .page__flex {
      display: block;
    }
  }
}
</style>
