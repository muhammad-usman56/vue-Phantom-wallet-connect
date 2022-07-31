<template>
  <div>

    <div v-if="this.cars === null">

      <button type="button" @click="connectWallet">Wallet Connect</button>
    </div>
    <div v-else>
      <button type="button" @click="logout">Logout</button>
    </div>

  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {

    return {
      key: '',
      cars: '',
      new: ''
    }
  },

  beforeMount() {
    this.getUnits();
  },

  methods: {
    logout() {
      localStorage.removeItem("cars");



    },
    getUnits() {
      this.cars = localStorage.getItem("cars");
      console.log(this.cars)

    },


    async connectWallet() {
      const { solana } = window;

      if (solana) {
        const response = await solana.connect();
        console.log('Connected with Public Key:', response.publicKey.toString());
        this.key = response.publicKey.toString();
        localStorage.setItem("cars", this.key);

        console.log(this.key)
      }
    }
  }
}






</script>


