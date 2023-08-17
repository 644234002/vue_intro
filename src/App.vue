<template>
  <div class="cart"> {{ cart }} </div>

  <div class="product-display">
    <div class="product-container">
      <div class="product-image">

        <!-- attibute binding -->
        <img v-bind:src="image" :atl="description" :title="description" />
      </div>

      <div class="product-info">
        <h1>  {{title}}  </h1>
        <p> {{ description }} </p>

        <!-- Condition rendering (v-if) -->
        <p v-if="inventory > 10">In Stock</p>
        <p v-else-if="inventory <= 10 && inventory > 0">Almost sold out!</p>
        <p v-else>Out of Stock</p>

        <!-- Loop (v-for) -->
        <ul>
          <li v-for="d in details"> {{ d }} </li>
        </ul>

        <!-- v-on หรือ @ แทนได้ -->
        <div
          v-for="v in variants"
          class="color-circle"
          v-bind:style="{backgroundColor: v.color}"
          @mouseover="updateImage(v.image)"
        >

        </div>

        <!-- Class binding, Even Handler -->
        <div>
          <button
            class="button"
            :class="{disabledButton : inventory <= 0}"
            :disabled="inventory <= 0"
            v-on:click="addToCart"
          >
            Add to Cart
          </button>
        </div>

        <a v-bind:href="url">Made by Marshall</a>
      </div>
    </div>
  </div>
</template>

<script setup>

import {ref, computed} from 'vue'

const product = 'หูฟังไร้สาย Marshall Major IV'
const brand = 'Marshall'
const image = ref('./images/major4.webp')
const description = 'หูฟังจาก Marshall ในรุ่น Major IV เป็นหูฟังไร้สายชนิด on ear รุ่นที่ 4 แล้วครับ โดยในรุ่นนี้จะออกแบบให้สวมใส่สบายมากขึ้น พร้อมแบตเตอรี่ที่สามารถใช้งานได้นานสูงสุดถึง 80 ชั่วโมงเลยทีเดียว'
const url = 'https://www.marshallheadphones.com'
const inStock =  true
const inventory = ref(20)
const details = ['Wired', 'Wireless']
const variants = [
        {id: 239, color: 'Black', image: './images/major4.webp'},
        {id: 240, color: 'Brown', image: './images/major4.jpg'}
]
var cart = ref(0)

function addToCart(){
    //console.log(cart.value);
    //console.log(inventory.value)
    cart.value += 1
    inventory.value -= 1
  }

function  updateImage(variantImage) {
      image.value = variantImage
      //console.loge(image.value);
    }

const title=computed (() => brand + '-' + product)    

</script>

<style scoped>

</style>