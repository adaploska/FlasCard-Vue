<template>
  <div class="searchwrapper">
    <p>Search card</p>
    <input v-model="search" placeholder="Search" @keyup="searchCards" />
  </div>
</template>
<script>
export default {
  name: "SearchCard",
  methods: {
    searchCards() {
      this.$emit("searchCards", this.search);
    },
  },
};
</script>
<style lang="scss">
.searchwrapper {
  display: flex;
  flex-direction: column;
  border: 5px solid #2d7f70;
  padding: 20px;
  border-radius: 27px 7px 27px 7px;
  p {
    font-size: 25px;
  }
}
</style>
