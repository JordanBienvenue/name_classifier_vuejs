<template>
  <div class="home">
    <h1>{{ currentName }}</h1>
    <h2>Pick one</h2>
    <div class="options-wrapper" v-if="currentName != end">

      <div class="options" @click="addToList(key, currentName)"  v-for="(option, key, index) in options" :key="index">
          {{ key}}
      </div>
    </div>

    <div class="lists-wrapper">
      <div v-for="(option, key, index) in options" :key="index">
        {{ key }}
        <div>{{ options[key].list }}</div>

        <a
          :href="'data:text/json;charset=utf-8,' + encodeURIComponent(JSON.stringify(options[key].list))"
          download
        >Download</a>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import names from "@/names.js"
export default {
  name: "home",
  data() {
    return {
      allNames: names,
      currentItem: 0,
      end: 'finish',
      options: {
        red: {
          list: []
        },
        blue: {
          list: []
        },
        green: {
          list: []
        }
      }
    }
  },
  computed: {
    currentName: function () {
      return this.allNames[this.currentItem] || "finish"
    }
  },
  methods: {
    next() {
      this.currentItem = this.currentItem + 1
    },
    prev() {
      this.currentItem = this.currentItem - 1
    },
    addToList(listName, item) {
      this.options[listName].list.push(item)
      this.next()
      console.log('adding ' + item + ' to ' + listName);
    }
  }
};
</script>

<style lang="scss" scoped>
.options-wrapper {
  display: flex;
  justify-content: center;
}

.options {
  display: block;
  padding: 30px;
  cursor: pointer;

  &:hover {
    background: grey;
    color: white;
  }
}
</style>
