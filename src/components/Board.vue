<template>
  <div>
    <Squares
      v-for="square in squares"
      :key="square"
      :btnValues="square"
      :step="Number(numberInput)"
      :onClickBtn="onClickBtn"
      :arrPlay="arrPlay"
      :win="win"
    ></Squares>
  </div>
</template>

<script>
import Squares from "@/components/Squares";
const genArr = number => {
  var arr = [];
  for (let x = 1; x <= number; x++) {
    arr.push(x * number);
  }
  console.log(arr);
  return arr;
};

export default {
  name: "Board",
  props: {
    numberInput: Number,
    step: Number,
    onClickBtn: Function,
    arrPlay: Array,
    win: Object
  },
  data() {
    console.log("bbbb");
    return {
      squares: []
    };
  },
  watch: {
    numberInput: function(newVal, oldVal) {
      this.squares = genArr(newVal);
    }
  },
  components: {
    Squares
  }
};
</script>
