<template>
  <div class="credi-card-carousel">
    <carousel-3d  :perspective="15" :controls-visible="true"
                  :clickable="false"
                  :space="550" :loop="false" :startIndex="view"
                  :onSlideChange="slideChanged">

      <slide v-for="(creditCard, i) in creditCards" :key="creditCard.type" :index="i" class="slide">
        <credit-card
              :type="creditCard.type"
              :number="creditCard.number"
              :name="creditCard.name"
              :expiration-date="creditCard.expirationDate">
        </credit-card>
      </slide>

    </carousel-3d>
  </div>
</template>

<script>
import { Carousel3d, Slide } from 'vue-carousel-3d'
import CreditCard from './credit-card.vue'

export default {
  components: {
    Carousel3d,
    Slide,
    CreditCard
  },
  props: {
    creditCards: Array,
    defaultCreditCard: Number
  },
  data: function () {
    return {
      view: this.defaultCreditCard
    }
  },
  methods: {
    slideChanged (index) {
      this.$emit('credit-card-changed', index)
    }
  }
}
</script>

<style lang="scss" rel="stylesheet/scss">
.credi-card-carousel {
  background-color: #83A0EC;
  width: 100%;
  height: 300px;

  .carousel-3d-slider {
    .carousel-3d-slide {
      background-color: #83A0EC;
      border: none;
    }
  }
}
</style>
