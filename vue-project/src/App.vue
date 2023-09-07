<script>
import { RouterLink, RouterView } from 'vue-router'
import { ref, reactive, computed } from 'vue';
export default {
  name: "App",
  data: () => ({
    showProductList: true,
    productList: [
      {
        title: "GLASSES",
        price: 150,
        count: 0,
        img: "src/assets/1.png",
      },
      {
        title: "BACKPACK",
        price: 50,
        count: 0,
        img: "src/assets/2.png",
      },
      {
        title: "BACKPACK",
        price: 50,
        count: 0,
        img: "src/assets/2.png",
      },
      {
        title: "BACKPACK",
        price: 50,
        count: 0,
        img: "src/assets/2.png",
      },
      {
        title: "BACKPACK",
        price: 50,
        count: 0,
        img: "src/assets/3.png",
      },
      {
        title: "BACKPACK",
        price: 50,
        count: 0,
        img: "src/assets/3.png",
      },
      {
        title: "BACKPACK",
        price: 50,
        count: 0,
        img: "src/assets/2.png",
      },
      {
        title: "BACKPACK",
        price: 50,
        count: 0,
        img: "src/assets/2.png",
      },
      {
        title: "BACKPACK",
        price: 50,
        count: 0,
        img: "src/assets/2.png",
      },
      {
        title: "BACKPACK",
        price: 50,
        count: 0,
        img: "src/assets/2.png",
      },
      {
        title: "BACKPACK",
        price: 50,
        count: 0,
        img: "src/assets/2.png",
      },

    ],
  }),
  computed: {
    total() {
      let sum = 0;
      this.productList.forEach((item) => {
        sum += item.count * item.price;
      });
      return sum;
    },
    cartList() {
      return this.productList.filter((item) => item.count > 0);
    },
  },
  methods: {
    handleAdd(index) {
      this.productList[index].count += 1;
    },
    handleSub(index) {
      this.productList[index].count -= 1;
    },
    toggleView() {
      this.showProductList = !this.showProductList;
    },
  },
};
</script>

<template>
  <header>
    <h1>VueSHOP The Shopping Mall</h1>
    <div class="wrapper">
      <HelloWorld msg="You did it!" />
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">Recommend</RouterLink>
      </nav>
    </div>
  </header>
  <section>
    <button @click="toggleView">{{ showProductList ? 'GO TO CART' : 'SHOW PRODUCT' }}</button>
  </section>
  <section v-if="showProductList" class="product">
    <ul class="list">
      <li v-for="(item, index) in productList" :key="index">
        <img :src="item.img" alt="" />
        <div class="title">{{ item.title }}</div>
        <div class="price">PRICE: {{ item.price }}</div>
        <div class="btn" @click="handleAdd(index)" v-if="!item.count">
          ADD TO CART
        </div>
        <div class="btn-box" v-else>
          <div class="btn" @click="handleSub(index)">-</div>
          <div>{{ item.count }}</div>
          <div class="btn" @click="handleAdd(index)">+</div>
        </div>
      </li>
    </ul>
  </section>
  <!-- Cart Table -->
  <section v-else class="cart">
    <ul class="list-header">
      <li>NO.</li>
      <li>NAME</li>
      <li>PICTURE</li>
      <li>QUANTITY</li>
      <li>PRICE</li>
    </ul>
    <ul class="list-body">
      <li v-for="(item, index) in cartList" :key="index">
        <div>{{ index }}</div>
        <div>{{ item.title }}</div>
        <div><img :src="item.img" alt="" /></div>
        <div>{{ item.count }}</div>
        <div>{{ item.count * item.price }}</div>
      </li>
    </ul>
  </section>
  <p>information</p>
  <section class="total"><span>TOTAL PRICE:</span>${{ total }}</section>
  <RouterView />
</template>

<style scoped>
.btn {
  text-align: center;
  width: 200px;
  background-color: #4897dd;
  border-radius: 8px;
  height: 32px;
  line-height: 32px;
  color: #fff;
  cursor: pointer;
}
.btn:hover {
  background-color: lightblue;
}
header {
  line-height: 1.5;
  max-height: 100vh;
  background-color: aquamarine;
  text-align: center;
  font-size: 40px;
  border: 1px solid aquamarine;
  border-radius: 16px;
}
.product {
  margin-bottom: 24px;
}
.product .list {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}
.product .list li {
  width: calc(25% - 12px); /* 25% width for each item (4 items in a row). Subtracting margin. */
  margin-bottom: 12px;
}
.product .list li .title {
  font-size: 24px;
  font-weight: bold;
  margin-bottom: 8px;
}
.product .list li .price {
  font-size: 20px;
  margin-bottom: 8px;
}
.product .list li img {
  width: 220px;
  height: 220px;
}
.product .list li .btn-box {
  display: flex;
}
.product .list li .btn-box .btn {
  width: 40px;
}
.product .list li .btn-box > div {
  flex: 1;
  text-align: center;
  line-height: 32px;
}
.cart .list-header {
  display: flex;
}
.cart .list-header li {
  flex: 1;
  border-top: 1px solid #c6c6c6;
  border-left: 1px solid #c6c6c6;
  border-bottom: 1px solid #c6c6c6;
  text-align: center;
  height: 50px;
  line-height: 50px;
  font-weight: bold;
  font-size: 25px;
}
.cart .list-body li {
  display: flex;
  border-top: 1px solid #c6c6c6;
  height: 60px;
  line-height: 44px;
  text-align: center;
  font-size: 20px;
}
.cart .list-body li:first-child {
  border-top: none;
}
.cart .list-body li:last-child {
  border-bottom: 1px solid #c6c6c6;
}
.cart .list-body li > div {
  flex: 1;
  border-left: 1px solid #c6c6c6;
  padding: 8px;
}
.cart .list-header li:last-child,
.cart .list-body li > div:last-child {
  border-right: 1px solid #c6c6c6;
}
.cart .list-body li > div img {
  width: 45px;
  height: 45px;
}
.total {
  text-align: right;
  margin-top: 24px;
  font-size: 32px;
}
.total span {
  margin-right: 12px;
}
</style>
