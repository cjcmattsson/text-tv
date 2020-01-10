<template lang="html">
  <div class="wrapper">
    <input
      type="text"
      pattern="[0-9]*"
      value=""
      @keyup="setPageToSearch($event)"
      @keydown.enter="searchPage"
    >
    <button type="button" name="button" @click="searchPage">Sök</button>
    <div v-if="searchResultContent" v-html="searchResultContent"></div>
  </div>
</template>

<script>
export default {
  name: "SearchField",
  data() {
    return {
      searchNumber: 100,
      searchResultContent: false,
    }
  },
  methods: {
    setPageToSearch: function(e) {
      this.searchNumber = e.target.value;
    },
    searchPage: function() {
      fetch(`http://api.texttv.nu/api/get/${this.searchNumber}?app=JustForFun`)
        .then((resp) => resp.json())
        .then((data) => {
          this.searchResultContent = data[0].content[0];
          console.log(this.searchResultContent);
        })
    }
  }
}
</script>

<style lang="css" scoped>
  input {
    font-size: 16px;
  }
</style>
