<template>
  <nb-content padder>
    <nb-card :style="{ marginBottom: 15 }">
      <nb-card-item header bordered>
        <nb-text>{{ coinid }}</nb-text>
      </nb-card-item>

      <nb-card-item>
        <nb-left>
          <nb-text> Rank: {{ coin.rank }} </nb-text>
        </nb-left>
      </nb-card-item>

      <nb-card-item>
        <nb-left>
          <nb-text> Price: U$D {{ coin.price }} </nb-text>
        </nb-left>
      </nb-card-item>

      <nb-card-item>
        <nb-left>
          <nb-text> Timestamp: {{ coin.price_timestamp }} </nb-text>
        </nb-left>
      </nb-card-item>

      <nb-card-item>
        <nb-left>
          <nb-text> ATH: {{ coin.high }} </nb-text>
        </nb-left>
      </nb-card-item>

      <nb-card-item>
        <nb-button block info :onPress="updateCoin">
          <nb-text>Update</nb-text>
        </nb-button>
      </nb-card-item>
       <nb-card-item>
        <nb-button error info :onPress="deleteCoin">
          <nb-text>Delete</nb-text>
        </nb-button>
      </nb-card-item>
    </nb-card>
  </nb-content>
</template>
<script>
import axios from "axios";
import { Toast } from "native-base";
export default {
  name: "CoinInfo",
  props: ["coinid"],
  data() {
    return {
      coin: {},
      loading: true,
    };
  },
  mounted() {
    this.updateCoin();
  },
  methods: {
    updateCoin() {
      this.loading = true;
      axios
        .get("https://api.nomics.com/v1/currencies/ticker", {
          params: {
            key: "de723035914f911c98af92cd0ab3e5ba",
            ids: this.coinid,
            interval: "1d",
            convert: "USD",
          },
        })
        .then((res) => {
          console.log(res.status);
          this.coin = res.data[0];
        })
        .catch((e) => {
          Toast.show({
            text: e,
            buttonText: "K",
          });
          console.error(e);
        })
        .finally((_) => (this.loading = false));
    },
    deleteCoin() {
      this.$emit('delete', this.coinid)
    },
  },
};
</script>