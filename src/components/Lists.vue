<template>
  <div class="allLists">
    <div class="List" v-for="list of dataLists" v-bind:key="list.name">
      <button v-on:click="dropHandler($event, list.id)">↓</button>
      <label>
        <input
          type="checkbox"
          v-model="list.checked"
          v-on:change="checkHandler(list.id, list.checked)"
        />
        {{ list.name }}
      </label>
      <ul v-bind:id="list.id" v-bind:class="{ notshow: !drop[list.id] }">
        <Items
          v-bind:items="list.items"
          v-bind:id="list.id"
          v-on:countChange="onCountChange"
          v-on:colorChange="onColorChange"
          v-on:onItemCheck="onItemCheck"
        />
      </ul>
    </div>
  </div>
</template>

<script>
import Items from "./Items";
export default {
  name: "Lists",
  emits: ["onCountChange", "onColorChange", "onListCheck", "onItemCheck"],
  props: ["dataLists"],
  data() {
    return {
      drop: Array(this.dataLists.length).fill(true),
    };
  },
  components: {
    Items,
  },
  methods: {
    dropHandler(event, id) {
      this.drop[id] = !this.drop[id];
      event.target.textContent = "→";
    },
    onCountChange(count, id, itemName) {
      this.$emit("onCountChange", count, id, itemName);
    },
    onColorChange(color, id, itemName) {
      this.$emit("onColorChange", color, id, itemName);
    },
    checkHandler(id, checked) {
      console.log(id, checked);
      this.$emit("onListCheck", id, checked);
    },
    onItemCheck(itemChecked, id, name) {
      this.$emit("onItemCheck", itemChecked, id, name);
    },
  },
};
</script>

<style>
.allLists {
  margin: 20px 10%;
  display: flex;
  flex-direction: column;
  gap: 20px;
}
.notshow {
  display: none;
}
</style>
