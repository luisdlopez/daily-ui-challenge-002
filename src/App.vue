<template>
  <div id="app">
    <div class="credit-card-container">

      <credit-card-carousel
            :credit-cards="creditCards"
            :default-credit-card="defaultCreditCardIndex"
            @credit-card-changed="creditCardSelectionChanged">
      </credit-card-carousel>

      <credit-card-form
            :credit-card="currentlySelectedCreditCard || defaultCreditCard"
            @card-updated="creditCardDetailsChanged">
      </credit-card-form>

    </div>
  </div>
</template>

<script>
import CreditCardCarousel from './components/credit-card-carousel.vue'
import CreditCardForm from './components/credit-card-form.vue'

export default {
  name: 'app',
  components: {
    CreditCardCarousel,
    CreditCardForm
  },
  data: function () {
    return {
      creditCards: [
        {
          type: 'visa',
          name: 'John Doe',
          number: 5555555555555555,
          expirationDate: {
            month: 7,
            year: 2019
          },
          cvv: 123,
          default: true
        },
        {
          type: 'mastercard',
          name: 'John Doe',
          number: 3333333333333333,
          expirationDate: {
            month: 2,
            year: 2018
          },
          cvv: 987
        }
      ],
      currentlySelectedCreditCardIndex: -1
    }
  },
  computed: {
    defaultCreditCardIndex () {
      return this.creditCards.findIndex(creditCard => creditCard.default)
    },
    defaultCreditCard () {
      return this.creditCards[this.defaultCreditCardIndex]
    },
    currentlySelectedCreditCard () {
      return this.creditCards[this.currentlySelectedCreditCardIndex]
    }
  },
  methods: {
    creditCardSelectionChanged (index) {
      this.currentlySelectedCreditCardIndex = index
    },
    creditCardDetailsChanged (updatedCreditCard) {
      let index = this.currentlySelectedCreditCardIndex === -1 ? this.defaultCreditCardIndex : this.currentlySelectedCreditCardIndex
      this.creditCards.splice(index, 1, updatedCreditCard)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.credit-card-container {
  width: 450px;
  height: 700px;
  margin: 50px auto;
  box-shadow: 0px 0px 25px #AAA;
}
</style>
