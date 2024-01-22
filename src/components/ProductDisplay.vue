<template>
  <div class="container" :style="{ color: isWomenClothing ? '#720060' : '' }">
    <div class="product" v-if="product">
      <div class="card">
        <div class="content">
          <div class="image">
            <img :src="product.image" alt="Product Image" />
          </div>
          <div class="text">
            <h2 :style="{ color: isWomenClothing ? '#720060' : '' }">
              {{ product.title }}
            </h2>
            <p>{{ product.category }}</p>
            <hr />
            <p>{{ product.description }}</p>
          </div>
        </div>
        <div class="text2">
          <hr />
          <h2
            class="price"
            :style="{ color: isWomenClothing ? '#720060' : '' }"
          >
            ${{ product.price }}
          </h2>
          <p>Rating: {{ product.rating }}</p>
          <div class="btn">
            <button
              class="btn-buy"
              :style="{
                cursor: 'pointer',
                backgroundColor: isWomenClothing ? '#720060' : '',
              }"
            >
              Buy now
            </button>

            <button
              class="btn-next"
              @click="nextProduct"
              :style="{
                cursor: 'pointer',
              }"
            >
              Next product
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [],
      currentIndex: 0,
    };
  },

  computed: {
    product() {
      return this.products[this.currentIndex];
    },

    isWomenClothing() {
      return this.product && this.product.category === "women's clothing";
    },
  },

  mounted() {
    this.getData();
  },

  methods: {
    getData() {
      fetch("https://fakestoreapi.com/products")
        .then((response) => response.json())
        .then((data) => {
          const filteredProducts = data.filter((product) => {
            return (
              product.category === "men's clothing" ||
              product.category === "women's clothing"
            );
          });

          filteredProducts.forEach((product) => {
            product.rating = Math.floor(Math.random() * 5) + 1;
          });

          this.products = filteredProducts;
        })
        .catch((error) => {
          console.log(error);
        });
    },

    nextProduct() {
      this.currentIndex = (this.currentIndex + 1) % this.products.length;
    },
  },

  created() {
    this.getData();
  },
};
</script>

<style scoped></style>
