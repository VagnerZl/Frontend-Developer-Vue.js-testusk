<template>
  <li v-for="item of items" v-bind:key="item.name" class="item">
    <label>
      <input
        type="checkbox"
        v-model="item.checked"
        v-on:change="checkHandler(id)"
      />
      {{ item.name }}
    </label>
    <div class="inputs">
      <input
        class="number"
        type="number"
        v-model.number="item.count"
        min="0"
        v-on:change="countChange(item.count, id, item.name)"
      />
      <input
        class="color"
        type="color"
        v-model="item.color"
        v-on:change="colorChange(item.color, id, item.name)"
      />
    </div>
  </li>
</template>

<script>
export default {
  name: "Items",
  emits: ["countChange", "colorChange", "onItemCheck"],
  props: ["items", "id"],
  methods: {
    countChange(count, id, itemName) {
      if (count < 0) {
        count = 0;
      }
      this.$emit("countChange", count, id, itemName);
    },
    colorChange(color, id, itemName) {
      this.$emit("colorChange", color, id, itemName);
    },
    checkHandler(id) {
      this.$emit("onItemCheck", id);
    },
  },
  data() {
    return {};
  },
};
</script>

<style >
.item {
  display: flex;
  justify-content: space-around;
  align-items: center;
  margin: 5px;
}
.inputs {
  display: flex;
  align-items: center;
  gap: 5px;
}
.color {
  box-sizing: border-box;
  width: 28px;
  height: 28px;
  padding: 0;
}
.number {
  width: 40px;
  height: 20px;
}
</style>
