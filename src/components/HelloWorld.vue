<template>
  <div class="hello">
    <div class="left">
      <h1>{{ title }}</h1>
      <form @submit.prevent="addLink">
        <input
          type="text"
          class="link-input"
          placeholder="Add a Link"
          v-model="newLink"
        />
      </form>
      <ul>
        <li v-for="(link, index) in links" :key="index">{{ link }}</li>
      </ul>
    </div>
    <div class="right">
      <stats />
    </div>
  </div>
</template>

<script>
import Stats from "@/components/Stats.vue";
import { mapState, mapMutations } from "vuex";

export default {
  name: "HelloWorld",
  components: {
    // DGG: Se va a borrar
    Stats
  },
  data() {
    return {
      newLink: ""
    };
  },
  methods: {
    ...mapMutations(["ADD_LINK"]),
    addLink() {
      this.ADD_LINK(this.newLink);
      this.newLink = "";
    }
  },
  computed: {
    // DGG: Se va a borrar
    ...mapState(["title", "links"])
  }
};
</script>

<style lang="scss">
html,
#app,
.home {
  height: 100%;
}
body {
  background-color: #f4f4f4;
  margin: 0;
  height: 100%;
}

.hello {
  display: grid;
  grid-template-columns: repeat(2, 50%);
  grid-template-rows: 100%;
  grid-template-areas: "left right";
  height: 100%;
}

.left,
.right {
  padding: 30px;
}

ul {
  list-style-type: none;
  padding: 0;
  li {
    padding: 20px;
    background: white;
    margin-bottom: 8px;
  }
}

.right {
  grid-area: right;
  background-color: #e9e9e9;
}
</style>
