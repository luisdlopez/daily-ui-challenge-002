<template>
  <div class="credi-card-form">
    <form class="mui-form" @submit.prevent="update">
      <legend class="title">
        Card Details
        <i class="fa fa-pencil" aria-hidden="true" @click="edit"></i>
      </legend>

      <div class="mui-textfield mui-textfield--float-label">
        <input type="text" v-model="form.name" :disabled="!editing">
        <label>Name</label>
      </div>

      <div class="mui-textfield mui-textfield--float-label">
        <input type="text" v-model="form.number" :disabled="!editing">
        <label>Number</label>
      </div>

      <div class="mui-select">
        <select v-model="form.expirationDate.month" :disabled="!editing">
          <option v-for="(month, i) in 11">{{ month + 1 }}</option>
        </select>
        <label>Month</label>
      </div>

      <div class="mui-select">
        <select v-model="form.expirationDate.year" :disabled="!editing">
          <option v-for="(year, i) in [2017, 2018, 2019, 2020]">{{ year }}</option>
        </select>
        <label>Year</label>
      </div>

      <div class="mui-textfield mui-textfield--float-label cvv">
        <input type="text" v-model="form.cvv" :disabled="!editing">
        <label>CVV</label>
      </div>

      <div class="button-container" v-show="!editing">
        <button type="button"
                class="mui-btn mui-btn--large mui-btn--raised mui-btn--primary">
          Checkout
        </button>
      </div>

      <div class="button-container" v-show="editing" >
        <button type="button" @click="cancel"
                class="mui-btn mui-btn--large mui-btn--flat mui-btn--danger">
          Cancel
        </button>
        <button type="submit" @click="update"
                class="mui-btn mui-btn--large mui-btn--flat mui-btn--primary">
          Update Card
        </button>
      </div>
    </form>

  </div>
</template>

<script>
export default {
  props: {
    creditCard: Object
  },
  data: function () {
    return {
      form: JSON.parse(JSON.stringify(this.creditCard)),
      editing: false
    }
  },
  watch: {
    creditCard: function (newCreditCard) {
      this.form = Object.assign({}, newCreditCard)
    }
  },
  methods: {
    edit: function () {
      this.editing = true
    },
    cancel: function () {
      this.form = Object.assign({}, this.creditCard)
      this.editing = false
    },
    update: function () {
      this.editing = false
      this.$emit('card-updated', JSON.parse(JSON.stringify(this.form)))
    }
  }
}
</script>

<style lang="scss" rel="stylesheet/scss">
.credi-card-form {
  text-align: left;
  width: 100%;
  height: 400px;

  .mui-form {
    input, select {
      color: #7893E4;
      font-weight: bold;
    }

    .title {
      background-color: #E7EBF7;
      color: #B8C2DE;
      font-weight: bold;
      padding: 20px;
      margin-bottom: 40px;

      .fa.fa-pencil {
        margin-left: 20px;
        cursor: pointer;
      }
    }

    .mui-textfield.mui-textfield--float-label {
      margin-left: 20px;
      margin-right: 20px;
    }

    .mui-select {
      display: inline-block;
      margin-left: 20px;
      width: 80px;// 193px;
    }

    .cvv {
      display: inline-block;
      width: 170px;
      margin-left: 50px !important;
    }

    .button-container {
      position: relative;
      margin-top: 29px;
    }

    .mui-btn.mui-btn--flat.mui-btn--danger,
    .mui-btn.mui-btn--flat.mui-btn--primary {
      display: inline-block;
      width: 219px;
    }

    .mui-btn.mui-btn--raised {
      width: 100%;
      background-color: #6DD272;
    }
  }
}
</style>
