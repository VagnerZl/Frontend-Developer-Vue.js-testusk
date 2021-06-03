<template>
  <div class="app">
    <div class="leftpart">
      <Lists
        v-bind:dataLists="dataLists"
        v-on:onCountChange="onCountChange"
        v-on:onColorChange="onColorChange"
        v-on:onListCheck="onListCheck"
        v-on:onItemCheck="onItemCheck"
      />
    </div>
    <div class="rightpart">
      <Blocks
        v-on:randomHandler="randomHandler"
        v-on:deleteBlock="deleteBlock"
        v-bind:dataLists="dataLists"
      />
    </div>
  </div>
</template>

<script>
import Lists from "@/components/Lists.vue";
import Blocks from "@/components/Blocks.vue";
export default {
  name: "App",
  data() {
    return {
      dataLists: [
        {
          id: 0,
          name: "List 1",
          checked: false,
          random: true,
          items: [
            {
              name: "item 1",
              count: 10,
              color: "#974e4e",
              checked: false,
            },
            {
              name: "item 2",
              count: 5,
              color: "#2234b9",
              checked: false,
            },
            {
              name: "item 3",
              count: 8,
              color: "#221100",
              checked: false,
            },
            {
              name: "item 4",
              count: 7,
              color: "#45ffaa",
              checked: false,
            },
            {
              name: "item 5",
              count: 10,
              color: "#1144aa",
              checked: false,
            },
          ],
        },
        {
          id: 1,
          name: "List 2",
          checked: true,
          random: true,
          items: [
            {
              name: "item 1",
              count: 10,
              color: "#974e4e",
              checked: false,
            },
            {
              name: "item 2",
              count: 5,
              color: "#2234b9",
              checked: false,
            },
            {
              name: "item 3",
              count: 6,
              color: "#8811b1",
              checked: true,
            },
            {
              name: "item 4",
              count: 10,
              color: "#224e4e",
              checked: true,
            },
          ],
        },
        {
          id: 2,
          name: "List 3",
          checked: true,
          random: true,
          items: [
            {
              name: "item 1",
              count: 3,
              color: "#F8E6E0",
              checked: true,
            },
            {
              name: "item 2",
              count: 5,
              color: "#B40404",
              checked: true,
            },
            {
              name: "item 3",
              count: 8,
              color: "#01DF01",
              checked: true,
            },
            {
              name: "item 4",
              count: 10,
              color: "#0B0B3B",
              checked: true,
            },
            {
              name: "item 5",
              count: 2,
              color: "#F781F3",
              checked: true,
            },
            {
              name: "item 6",
              count: 1,
              color: "#81BEF7",
              checked: true,
            },
          ],
        },
        {
          id: 3,
          name: "List 4",
          checked: true,
          random: false,
          items: [
            {
              name: "item 1",
              count: 10,
              color: "#2E64FE",
              checked: true,
            },
            {
              name: "item 2",
              count: 5,
              color: "#40FF00",
              checked: true,
            },
            {
              name: "item 3",
              count: 6,
              color: "#3A2F0B",
              checked: true,
            },
            {
              name: "item 4",
              count: 10,
              color: "#DF013A",
              checked: true,
            },
          ],
        },
      ],
    };
  },
  components: {
    Lists,
    Blocks,
  },
  methods: {
    onCountChange(count, id, itemName) {
      this.dataLists[id].items.map((i) => {
        if (i.name == itemName) {
          i.count = count;
        }
        return i;
      });
    },
    onColorChange(color, id, itemName) {
      this.dataLists[id].items.map((i) => {
        if (i.name == itemName) {
          i.color = color;
        }
        return i;
      });
    },
    onListCheck(id, checked) {
      this.dataLists[id].items.forEach((item) => {
        item.checked = checked;
      });
    },
    onItemCheck(id) {
      this.dataLists[id].checked = true;
    },
    randomHandler(random, id) {
      this.dataLists[id].random = random;
    },
    deleteBlock(id, name) {
      this.dataLists[id].items.forEach((item) => {
        if (item.name == name) {
          item.count--;
        }
      });
    },
  },
};
</script>

<style>
.app {
  display: flex;
  justify-content: space-around;
}
.leftpart {
  width: 40%;
  min-height: 90vh;
  border: 1px solid black;
}
.rightpart {
  width: 40%;
  border: 1px solid black;
}
</style>
