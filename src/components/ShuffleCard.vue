<template>
  <button class="shuffleButton" @click="shuffleCards">shuffle cards</button>
</template>
<script>
export default {
  name: "ShuffleCard",
  methods: {
    shuffleCards() {
      this.$emit("shuffleCard");
    },
  },
};
</script>

<style lang="scss">
.shuffleButton {
  display: block;
  background: #40b59f;
  color: white;
  padding: 15px 20px;
  margin: 10px 10px;
  border-radius: 5px;
  text-decoration: none;
  border: none;
  font-size: 25px;
  &:hover {
    background: #2d7f70;
  }
}
</style>
