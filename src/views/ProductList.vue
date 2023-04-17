<template>
  <div id="ProductList">
    <!-- <Header v-if="categories" />
    <template v-if="products">
      <NewProductHint />
      <ProductItem />
      <ExhibitButton />
    </template> -->
    <div class="main-img">
      <!-- <div class="name">An</div> -->
    </div>
  </div>
</template>

<script setup lang="ts">
import Header from "@/components/Header/index.vue";
import NewProductHint from "@/components/ProductList/NewProductHint.vue";
import ProductItem from "@/components/ProductList/ProductItem.vue";
import ExhibitButton from "@/components/ProductList/ExhibitButton.vue";

import { storeToRefs } from "pinia";
import { useProduct } from "@/store";

const productStore = useProduct();
const { categories, products } = storeToRefs(productStore);
</script>

<style lang="scss" scoped>
// #ProductList {
//   @include position(relative);
//   margin-top: 1.25rem;
//   height: calc(100vh - 1.25rem);
//   border-bottom: 0.03rem solid #f0f0f0;
//   background: #eef0ec;
//   ::-webkit-scrollbar {
//     display: none;
//   }
// }
html {
  font-size: 80vmax / 1920 * 100;
  @media (max-width: 992px) {
    font-size: 80vmax / 992 * 100;
  }
}
body {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #000;
}
.main-img {
  position: relative;
  width: 19.2rem * 0.5;
  height: 10.8rem * 0.5;
  background: url(https://fakeimg.pl/300x300/000000/) no-repeat center / 100%
    auto;
  &:before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: inherit;
    animation: bgGlitch 1.5s both infinite alternate;
    opacity: 0.6;
  }
}

@mixin resetGlitch {
  left: 0;
  clip-path: none;
}

$pct-weight: 10, 30, 50, 70, 90;
@mixin randomGlitch($name: "", $shiftX: 0, $rdTop: 0, $rdBtm: 0) {
  @keyframes #{$name} {
    0%,
    100% {
      @include resetGlitch;
    }
    @each $w in $pct-weight {
      $pct: $w + random(5);
      #{$pct * 1%} {
        left: #{random($shiftX) - $shiftX/2}px;
        clip-path: inset(#{random($rdTop) * 1%} 0 #{random($rdBtm) * 1%} 0);
      }
      #{($pct + 5) * 1%},
      #{($pct - 5) * 1%} {
        @include resetGlitch;
      }
    }
  }
}

// @include randomGlitch(bgGlitch, 15, 30, 30);
</style>
