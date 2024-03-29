<template>
  <div class="container">
    <div v-if="loader">
      <Loader />
    </div>

    <div
      class="body-bg"
      :class="
        products.data?.category !== `men's clothing` &&
        products.data?.category !== `women's clothing`
          ? `unav`
          : products.data?.category === `men's clothing`
          ? `men`
          : `women`
      "
    >
      <!-- for men's and women's clothing -->
      <div
        v-if="
          products.data?.category == `men's clothing` ||
          products.data?.category == `women's clothing`
        "
        class="card card__flex"
      >
        <img
          :src="products.data?.image"
          :alt="products.data?.title"
          class="card__image"
        />
        <main class="main__flex">
          <article>
            <h1 class="title">{{ products.data?.title }}</h1>
            <div class="caption__flex">
              <p class="category">{{ products.data?.category }}</p>
              <div class="rate__flex">
                <p class="rate">{{ products.data?.rating.rate }}/5</p>
                <div
                  v-for="rate in rates"
                  :key="rate"
                  class="circle"
                  :class="
                    Math.round(products.data?.rating.rate) >= rate
                      ? `bg-circle`
                      : ``
                  "
                ></div>
              </div>
            </div>
            <hr />
            <p class="desc">{{ products.data?.description }}</p>
          </article>

          <section>
            <hr />
            <h2 class="price">${{ products.data?.price }}</h2>
            <div class="button__flex">
              <button class="btn-buy">Buy now</button>
              <button class="btn-next" @click="showProduct()">
                Next product
              </button>
            </div>
          </section>
        </main>
      </div>

      <!-- unavailable class for category other than men's and women's clothing -->
      <div
        v-if="
          products.data?.category !== `men's clothing` &&
          products.data?.category !== `women's clothing`
        "
        class="card unavailable"
      >
        <div class="unav-content">
          <h2>This product is unavailable to show</h2>
          <button @click="showProduct()">Next product</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Loader from "../components/Loader.vue";

export default {
  components: {
    Loader,
  },

  data() {
    return {
      products: {},
      count: 0,
      loader: false,
      rates: [1, 2, 3, 4, 5],
    };
  },
  methods: {
    async fetchAPI() {
      try {
        const res = await fetch(
          `https://fakestoreapi.com/products/${this.count}`
        );
        const result = await res.json();
        return result;
      } catch (err) {
        console.log(err.message);
      }
    },

    async showProduct() {
      this.loader = true;

      if (this.count === 20) {
        this.count = 1;
      } else {
        this.count++;
      }

      const data = await this.fetchAPI();
      this.products = { data };

      this.loader = false;
    },
  },
  mounted() {
    this.showProduct();
  },
};
</script>

<style>
@import url("../assets/style/page.css");
</style>
