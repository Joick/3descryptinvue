<template>
<div>
  <textarea v-model="msg" ></textarea>
  <button @click="doEncrypt">加密</button>
  <textarea v-model="encryptResultTxt"></textarea>
  <button @click="doDecrypt">解密</button>
  <textarea v-model="decryptResultTxt"></textarea>
</div>
</template>

<script>
import CryptoJS from 'crypto-js'
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      encryptResultTxt: '',
      decryptResultTxt: '',
      key: '1234567890'
    }
  },
  methods: {
    doEncrypt () {
      this.encryptResultTxt = this.encryptByDES(this.msg, this.key)
    },
    doDecrypt () {
      this.decryptResultTxt = this.dencryptByDES(this.encryptResultTxt, this.key)
    },
    encryptByDES (message, key) {
      const keyHex = CryptoJS.enc.Utf8.parse(key)
      const encrypted = CryptoJS.DES.encrypt(message, keyHex, {
        mode: CryptoJS.mode.ECB,
        padding: CryptoJS.pad.Pkcs7
      })

      return encrypted.toString()
    },
    dencryptByDES (ciphertext, key) {
      const keyHex = CryptoJS.enc.Utf8.parse(key)
      // direct decrypt ciphertext
      const decrypted = CryptoJS.DES.decrypt({
        ciphertext: CryptoJS.enc.Base64.parse(ciphertext)
      }, keyHex, {
        mode: CryptoJS.mode.ECB,
        padding: CryptoJS.pad.Pkcs7
      })

      return decrypted.toString(CryptoJS.enc.Utf8)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
