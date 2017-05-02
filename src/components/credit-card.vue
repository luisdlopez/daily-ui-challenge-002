<template>
  <div class="credit-card" :class="type">
    <div class="logo"><i class="fa fa-4x" :class="logo" aria-hidden="true"></i></div>

    <div class="number">
      <div class="block" v-for="block in number.toString().match(/.{4}/g)">
        {{ block }}
      </div>
    </div>

    <div class="name-container">
      <div class="label">Name</div>
      <div class="value">{{ name }}</div>
    </div>

    <div class="expiration-date-container">
      <div class="label">Expiration Date</div>
      <div class="value">{{ expirationDate.month }} / {{ expirationDate.year }}</div>
    </div>

  </div>
</template>

<script>
export default {
  props: {
    type: String,
    number: Number,
    name: String,
    expirationDate: Object
  },
  computed: {
    logo: function () {
      return `fa-cc-${this.type}`
    }
  }
}
</script>

<style lang="scss">
.credit-card {
  box-shadow: 1px 1px 2px #444;
  width: 337px;
  height: 212px;
  margin: 40px auto 0 auto;
  border-radius: 10px;
  font-weight: bold;

  &.mastercard {
    background-color: #4A5CB9;
    color: #FFF;
  }

  &.visa {
    background-color: #EDCC58;
    color: #FFF;
  }

  .logo {
    float: right;
    margin: 10px 10px 0 0;
  }

  .number {
    position: relative;
    padding-top: 90px;
    font-size: 18px;

    .block {
      display: inline-block;
      margin-right: 20px;
    }
  }

  .name-container,
  .expiration-date-container {
    position: relative;
    padding: 30px 0 0 0;
    display: inline-block;
    text-align: left;
    float: left;

    .label {
      margin-left: 15px;
      font-size: 12px;
    }
    .value {
      margin-left: 15px;
      text-transform: uppercase;
      font-size: 16px;
    }
  }

  .name-container {
    width: 65%;
  }

  .expiration-date-container {
    width: 35%;
  }
}
</style>
