<template>
  <div class="numbers">
    <div class="container">
      <h2>{{ data.title }}</h2>
      <h3><span class="number-before" v-html="data.numbers.before"></span>
      <span class="numbers-number" id="numbers-number"></span>
      <span class="number-after" v-html="data.numbers.after"></span></h3>
      <p>{{ data.text }}</p>
      <div class="companies-list">
        <ul>
          <li :key="index" v-for="(item, index) in data.companies" >
            <img 
            :src="item.image.url" 
            :alt="item.image.description.length > 0 ? item.image.description : item.image.title" 
            :width="item.image.width"
            :height="item.image.height"
          />
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>
<script>
import { CountUp } from 'countup.js'
export default {
  name: 'NumberBlock',
  data: () => ({
    countUp: null
  }),
  props: {
    data: {
      type: Object,
      required: true
    },
    start: {
      type: Boolean,
      required: true
    }
  },
  watch: {
    start (value) {
      if(value === true) {
        let countUp = new CountUp('numbers-number', parseInt(this.data.numbers.number, 10), {
          decimalPlaces: 0,
          separator: ".",
          decimal: ",",
          prefix: "$",
          duration: 8,
          startVal: 0,
          endVal: parseInt(this.data.numbers.number, 10)
        })
        countUp.start()
      }
    }
  }
}
</script>
<style lang="stylus">
@import '~assets/css/functions.styl'
.numbers
  margin-top 33px
  .container
    width calc(100% - 128px)
    max-width 1164px
    margin 0 auto
    text-align center
  h2
    margin-bottom 40px
    color #0096FF
    font-size 36px
    line-height 150%
    font-weight 700
  h3
    margin-bottom 40px
    color #00417F
    font-size 24px
    line-height 150%
    font-weight 700
    .big
      font-size 40px
  p
    font-size 24px
    color #606266
.numbers-number
  font-size 40px
.companies-list
  max-width 1040px
  width calc(100% - 32px)
  margin 40px auto 0
  ul
    padding 0
    margin 0
    list-style-type none
    width 100%
    display flex
    justify-content space-between
    align-items center
    li
      margin-left 30px
      &:first-child
        margin-left 0
    img
      max-width 100%
      display block
      height auto
  
@media all and (max-width: 1250px)
  .numbers
    .container
      width calc(100% - 64px)
    h2
      font-size: clamp(24px, calc(1.5rem + (36 - 24) * ((100vw - 340px) / (1250 - 340))), 36px)
    h3
      font-size: clamp(16px, calc(1rem + (24 - 16) * ((100vw - 320px) / (1250 - 320))), 24px)
      .big
        font-size: clamp(28px, calc(2rem + (40 - 32) * ((100vw - 320px) / (1250 - 320))), 40px)
    p
      font-size: clamp(18px, calc(1.125rem + (24 - 18) * ((100vw - 320px) / (1250 - 320))), 24px)
@media all and (max-width: 1100px)
  .numbers
    .container
      width calc(100% - 32px)
  .companies-list
    flex-flow: row nowrap
    img
      width auto
      display block
@media all and (max-width: 600px)
  .numbers
    .container
      width calc(100% - 20px)
  .numbers-number
    margin 10px 0
    display block
  .companies-list
    ul li
      margin-left 20px
</style>