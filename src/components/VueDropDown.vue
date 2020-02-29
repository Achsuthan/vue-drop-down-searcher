<template >
  <div v-click-outside="closeEvent">
    <div
      class="dd-header"
      @click="toggleListFn()"
    >
      <label class="col-12">
        <ul style="display: inline">
          <template v-for="(item, index) in internalSelectedList">
            <li :key="index" @click="reveItemFn(index)" style="display: inline">
              <div
                style="display: inline-block; padding: 2px; border: 1px solid #0074D9; background-color: #0074D9; border-radius : 5px; margin: 5px;cursor: pointer; color: white"
              >
                {{item[selectedlabelName]}}
                <span style="paddingLeft: '5px', color: 'white'">X</span>
              </div>
            </li>
          </template>

          <input
            class="form-control"
            style="outline: none; border: none; font-size: 14px;"
            :placeholder="placeholder"
            v-model="value"
          />
        </ul>
      </label>
    </div>
    <template v-if="listOpen">
      <div>
        <ul @mouseenter="mouseEnterEventFn()" @mouseleave="mouseLeaveEventFn()" class="dd-list">
          <template v-for="(item, index) in internalList">
            <li
              :class="selectedClassnameFn(item) ? 'dd-list-item selected' : 'dd-list-item' "
              :key="index"
              @click="dropDownSelectedItemFn(item);"
            >{{item[labelName]}}</li>
          </template>
        </ul>
      </div>
    </template>
  </div>
</template>

<script>
import Vue from 'vue'
export default {
  name: "VueDropDown",
  props: {
    placeholder: {
      default: "Search...",
      type: String
    },
    labelName: {
      default: "name",
      type: String
    },
    selectedlabelName: {
      default: "name",
      type: String
    },
    isSingle: {
      default: true,
      type: Boolean
    },
    list: {
      default: function() {
        return [];
      },
      type: Array
    },
    selectedList: {
      default: function() {
        return [];
      },
      type: Array
    },
    searchKey: {
      default: "",
      type: String
    }
  },
  data() {
    return {
      value: "",
      listOpen: false,
      internalSelectedList: [],
      internalList: []
    };
  },
  created() {
    this.internalSelectedList = this.selectedList;
    this.value = this.searchKey;
    this.internalList = this.list;
  },
  watch: {
    selectedList(val) {
      this.internalSelectedList = val;
    },
    searchKey(val) {
      this.val = val;
      if (val) {
        this.filterList(val);
      }
    },
    value(val) {
      if (val) {
        this.filterList(val);
      } else {
        this.internalList = this.list;
      }
      this.$emit("inputChanged", val);
    }
  },
  methods: {
    nameOfCustomEventToCall(){
      console.log("hello")
    },
    filterList(value) {
      this.internalList = [];
      this.internalList = [
        ...this.list.filter(val => {
          if (val.name.toUpperCase().includes(value.toUpperCase())) {
            return val;
          }
        })
      ];
    },
    toggleListFn() {
      this.listOpen = !this.listOpen;
    },
    mouseEnterEventFn() {
      window.removeEventListener("mousedown", close);
    },
    mouseLeaveEventFn() {
      window.addEventListener("mousedown", close);
    },
    reveItemFn(index) {
      let tmpArray = this.internalSelectedList.filter((item, i) => i !== index);
      this.internalSelectedList = tmpArray;
      this.$emit("toggleItem", tmpArray);
    },
    dropDownSelectedItemFn(item) {
      // console.log("dropDownSelectedItemFn called", item);
      let totalSelectedItem = [...this.internalSelectedList];
      if (this.isSingle) {
        totalSelectedItem = [item];
        this.internalSelectedList = totalSelectedItem;
      } else if (!this.selectedClassnameFn(item)) {
        totalSelectedItem.push(item);
        this.internalSelectedList = totalSelectedItem;
      } else {
        totalSelectedItem.splice(totalSelectedItem.indexOf(item), 1);
        this.internalSelectedList = totalSelectedItem;
      }
      this.value = "";
      this.$emit("toggleItem", totalSelectedItem);
    },
    selectedClassnameFn(item) {
      let found = false;
      this.internalSelectedList.filter(val => {
        val[this.labelName].toUpperCase() === item[this.labelName].toUpperCase()
          ? (found = true)
          : null;
      });
      return found;
    },
    closeEvent: function () {
      this.listOpen = false
    }
  },
};

Vue.directive('click-outside', {
  bind: function (el, binding, vnode) {
    el.clickOutsideEvent = function (event) {
      // here I check that click was outside the el and his childrens
      if (!(el == event.target || el.contains(event.target))) {
        // and if it did, call method provided in attribute value
        vnode.context[binding.expression](event);
      }
    };
    document.body.addEventListener('click', el.clickOutsideEvent)
  },
  unbind: function (el) {
    document.body.removeEventListener('click', el.clickOutsideEvent)
  },
});
</script>

<style scoped>
@import "./styles/global.css";
.container {
  padding: "2px";
  margin: "5px";
}

.item {
  color: "white";
  display: "inline-block";
  padding: "2px";
  border: "1px solid #0074D9";
  background-color: "#0074D9";
  border-radius: "5px";
  margin: "5px";
  cursor: "pointer";
}

.inputField {
  outline: "none";
  border: "none";
  font-size: "12px";
}
</style>