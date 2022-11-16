<template>
  <button class="resetShuffleButton" @click="resetShuffleCards">
    reset shuffle
  </button>
</template>
<script>
export default {
  name: "ResetShuffleCard",

  methods: {
    resetShuffleCards() {
      this.$emit("resetShuffle");
    },
  },
};
</script>
<style lang="scss">
.resetShuffleButton {
  display: block;
  background: #2d7f70;
  color: white;
  padding: 15px 20px;
  margin: 10px 10px;
  border-radius: 5px;
  text-decoration: none;
  border: none;
  font-size: 25px;
  &:hover {
    background: #40b59f;
  }
}
</style>
