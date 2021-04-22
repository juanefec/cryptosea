<template>
  <nb-container>
    <nb-item>
      <nb-icon active name="flask" />
      <nb-input v-model="coinID" placeholder="Crypto" />
      <nb-icon active name="coin" />
    </nb-item>
    <nb-button transparent :onPress="emitAdd">
      <nb-text>Search</nb-text>
    </nb-button>
  </nb-container>
</template>
<script>
export default {
    data: () => ({
        coinID: ""
    }),
    methods: {
        emitAdd() {
            this.$emit('add', this.coinID)
        }
    }
}
</script>