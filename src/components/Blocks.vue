<template>
  <div class="allblocks">
    <div class="block-list" v-for="list of dataLists" v-bind:key="list.name">
      <div class="block-header">
        <span class="block-list-name">{{ list.name }}</span>
        <button
          class="block-button"
          v-on:click="randomHandler(list.random, list.id)"
        >
          {{ list.random ? "Перемешать" : "Сортировать" }}
        </button>
      </div>
      <div class="container" v-bind:class="{ notcontain: !list.random }">
        <div
          class="block-item"
          v-for="item of list.items"
          v-bind:key="item.name"
          v-bind:class="{ noblock: !item.checked }"
        >
          <div
            class="simple-block"
            v-for="n in item.count"
            v-on:click="deleteBlock(list.id, item.name)"
            v-bind:key="{ n }"
            v-bind:style="{ backgroundColor: item.color }"
          ></div>
        </div>
      </div>
      <div class="random-container" v-bind:class="{ notcontain: list.random }">
        <div
          class="random-block"
          v-for="randomblock of this.generatRandomArr(list.id)"
          v-bind:key="randomblock.name + Math.random()"
          v-on:click="deleteBlock(randomblock.id, randomblock.name)"
          v-bind:style="{
            backgroundColor: randomblock.color,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "Blocks",
  emits: ["randomHandler", "deleteBlock"],
  props: ["dataLists", "id"],
  components: {},
  methods: {
    deleteBlock(id, name) {
      this.$emit("deleteBlock", id, name);
    },
    randomHandler(random, id) {
      random = !random;
      this.$emit("randomHandler", random, id);
    },
    generatRandomArr(id) {
      let randomArr = [];
      if (this.dataLists[id].checked) {
        this.dataLists[id].items.forEach((item) => {
          if (item.checked) {
            randomArr = randomArr.concat(
              Array(item.count).fill({
                color: item.color,
                id: id,
                name: item.name,
              })
            );
          }
        });
      }
      function makeRandomArr() {
        return Math.random() - 0.5;
      }
      randomArr.sort(makeRandomArr);
      return randomArr;
    },
  },
};
</script>

<style >
.block-list {
  margin: 10px;
  border: black 1px solid;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.block-header {
  display: flex;
  justify-content: space-between;
}
.block-item {
  margin: 0 20px 0 20px;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
.block-list-name {
  margin: 10px 0 10px 30px;
}
.block-button {
  margin: 5px;
  border-radius: 5px;
  background-color: #25a1f2;
  box-shadow: none;
}
.noblock {
  display: none;
}

.simple-block {
  width: 10px;
  margin: 5px;
  height: 10px;
}
.random-container {
  display: flex;
  flex-direction: row;
  gap: 10px;
  flex-wrap: wrap;
  margin: 10px 25px 20px 25px;
}
.notcontain {
  display: none;
}
.random-block {
  width: 10px;
  height: 10px;
}
</style>