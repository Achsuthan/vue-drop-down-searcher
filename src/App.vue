<template>
  <div class="container">
    <br />
    <div class="row">
      <div class="col-12">
        <span>Single Select :</span>
        <VueDropDown
          class="col-12"
          :list="list"
          :isSingle="true"
          :selectedList="singleSelectedList"
          @inputChange="inputChangeFn"
          @selectedValues="val => selectedValeChangedFn(val,true)"
        />
        <span>Selected Values :</span>
        <br />
        <span>{{singleSelectedList.length > 0 ? '1 : ' : ''}}  {{singleSelectedList.length > 0 ? singleSelectedList[0].name : ''}}</span>
        <br />
        <br />
        <br />

        <span>Multi Select :</span>
        <VueDropDown
          class="col-12"
          :list="list"
          :isSingle="false"
          :selectedList="multiSelectedList"
          @inputChange="inputChangeFn"
          @selectedValues="val=> selectedValeChangedFn(val, false)"
        />
        <span>Selected Values :</span>
        <template v-for="(val, index) in multiSelectedList">
          <div :key="index">
            <span>{{index + 1}} : {{val.name}}</span>
            <br />
          </div>
        </template>
      </div>
    </div>
  </div>
</template>

<script>
import VueDropDown from "./components/VueDropDown";

export default {
  name: "App",
  components: {
    VueDropDown
  },
  data() {
    return {
      singleSelectedList: [],
      multiSelectedList: [],
      list: [
        {
          name: "End Game",
          value: "End Game1"
        },
        {
          name: "The Lion King",
          value: "The Lion King"
        },
        {
          name: "Spider-Man: Far From Home",
          value: "Spider-Man: Far From Home"
        },
        {
          name: "Captain Marvel",
          value: "Captain Marvel"
        },
        {
          name: "Jorker",
          value: "Jorker"
        }
      ]
    };
  },
  methods: {
    inputChangeFn(val) {
      console.log("value chaned ", val);
    },
    selectedValeChangedFn(values, isSingle) {
      isSingle
        ? (this.singleSelectedList = values)
        : (this.multiSelectedList = values);
    }
  }
};
</script>

