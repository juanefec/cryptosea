<template>
  <nb-container>
    <nb-header>
      <nb-body :style="{ marginLeft: 100 }">
        <nb-title>Cryptowatch</nb-title>
      </nb-body>
      <nb-right>
        <nb-button transparent :onPress="handleOptions">
          <nb-icon name="menu" />
        </nb-button>
      </nb-right>
    </nb-header>

    <nb-container v-if="!modifingCoins">
      <nb-tabs :renderTabBar="getScollableTabComp">
        <nb-tab v-for="coin in coins" :key="coin" :heading="coin">
          <CoinInfo :coinid="coin" @delete="handleDeleteCoin" />
        </nb-tab>
      </nb-tabs>
    </nb-container>
    <nb-container v-if="modifingCoins">
      <AddCoinInfo v-if="clicked == 0" @add="handleAddCoin"/>
    </nb-container>
  </nb-container>
</template>

<script>
import React from "react";
import { ScrollableTab, ActionSheet } from "native-base";
import CoinInfo from "./coin/index.vue";
import AddCoinInfo from "./coin/add.vue";
export default {
  components: { CoinInfo, AddCoinInfo },
  data() {
    return {
      modifingCoins: false,
      coins: ["ADA", "BTC", "ETH"],
      btnOptions: ["Add coin", "Cancel"],
      optionCancelIndex: 1,
      optionDestructiveIndex: 1,
      clicked: 0,
    };
  },
  methods: {
    getScollableTabComp() {
      return <ScrollableTab />;
    },
    handleAddCoin(coin) {
      this.coins.push(coin)
    },
    handleDeleteCoin(coin) {
      this.modifingCoins = true
      this.coins = this.coins.map(e => e !== coin ? e : false)
      this.modifingCoins = false
    },
    handleOptions() {
      ActionSheet.show(
        {
          options: this.btnOptions,
          cancelButtonIndex: this.optionCancelIndex,
          destructiveButtonIndex: this.optionDestructiveIndex,
          title: "Options",
        },
        (buttonIndex) => {
          this.clicked = this.btnOptions[buttonIndex];
          if (this.clicked === "Add coin") {
            this.modifingCoins = true
          }
          if (this.clicked === "Cancel") {
            this.modifingCoins = false
          }
        }
      );
    },
  },
};
</script>