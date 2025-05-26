<template>

    <h1>CRYPTO</h1>
    <Input :changeAmount="changeAmount" :convert="convert" :favorite="favorite"/>
    <p v-if="error != ''">{{ error }}</p>
    <p className="result-text" v-if="result != ''">{{ result }}</p>
    <Favorite :favs="favs" v-if="favs.length > 0" :getFromFavs="getFromFavs" />
    
    <div className="selectors">
        <Selector :setCrypto="setCryptoFirst" :cryptoNow="cryptoFirst"/>
        <Selector :setCrypto="setCryptoSecond"  :cryptoNow="cryptoSecond"/>
    </div>
    
</template>

<script>
import { triggerRef } from 'vue';
import Input from './components/Input.vue';
import Selector from './components/Selector.vue';
import Favorite from './components/Favorite.vue'
import CryptoConvert from 'crypto-convert';

const convert = new CryptoConvert();

export default {
  components: { Input, Selector, Favorite },
  data() {
    return {
      amount: 0,
      cryptoFirst: '',
      cryptoSecond: '',
      error: '',
      result: 0,
      favs: []
    }
  },
  methods: {
    favorite() {
      this.favs.push({
        from: this.cryptoFirst,
        to: this.cryptoSecond
      });
    },
    getFromFavs(index){
        this.cryptoFirst = this.favs[index].from
        this.cryptoSecond = this.favs[index].to
    },
    changeAmount(val) {
      this.amount = val
    },
    setCryptoFirst(val) {
      this.cryptoFirst = val
    },
    setCryptoSecond(val) {
      this.cryptoSecond = val
    },
    async convert() {
      if (this.amount <= 0) {
        this.error = 'Enter the number more than null';
        return
      } else if (this.cryptoFirst == this.cryptoSecond) {
        this.error = 'Select another currency';
        return
      } else if (this.cryptoFirst == '' || this.cryptoSecond == '') {
        this.error = 'Select currency';
        return
      }
      this.error = '';

      await convert.ready();

      if (this.cryptoFirst == 'BTC' && this.cryptoSecond == 'ETH')
        this.result = convert.BTC.ETH(this.amount);
      else if (this.cryptoFirst == 'BTC' && this.cryptoSecond == 'USDT')
        this.result == convert.BTC.USDT(this.amount)
      else if (this.cryptoFirst == 'ETH' && this.cryptoSecond == 'BTC')
        this.result == convert.ETH.BTC(this.amount)
      else if (this.cryptoFirst == 'ETH' && this.cryptoSecond == 'USDT')
        this.result == convert.ETH.USDT(this.amount)
      else if (this.cryptoFirst == 'USDT' && this.cryptoSecond == 'BTC')
        this.result == convert.USDT.BTC(this.amount)
      else if (this.cryptoFirst == 'USDT' && this.cryptoSecond == 'ETH')
        this.result == convert.USDT.ETH(this.amount)
      
    }
  }
}

</script>


<style scoped>

.selectors {
    display: flex;
    justify-content: space-around;
    width: 700px;
    margin: 0 auto;
}

.error {
  color: #d03939;
}

.wrapper {
  width: 900px;
  height: 500px;
  border-radius: 50px;
  padding: 20px;
  background: #1f0f24;
  text-align: center;
  color: #fff;
}

.wrapper h1 {
  margin-top: 50px;
}

.wrapper p {
  margin-top: 20px;
}

.wrapper input {
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid #110813;
  color: #fcfcfc;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;
}

.wrapper input:focus {
  border-bottom-color: #6e2d7d;
}

.wrapper button:disabled {
  background: #746024;
  cursor: not-allowed;
}

.wrapper button {
  background: #e3bc4b;
  color: #fff;
  border-radius: 10px;
  border: 2px solid #b99935;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}

.wrapper button:hover {
  transform: scale(1.1) translateY(-5px);
}

.result-text {
  font-family: 'Nabla', cursive;
  font-size: 2em;
}
</style>

