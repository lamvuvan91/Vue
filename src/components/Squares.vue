<template>
  <div class="board">
    <Button
      v-for="bt in arrvalue"
      :key="bt"
      :value="bt"
      :clickBtn="onClickBtn"
      :arrPlay="arrPlay"
      :win="win"
    ></Button>
  </div>
</template>

<script>
const genArr = (number, step) => {
  var arr = [];
  for (let x = number - step; x < number; x++) {
    arr.push(x + 1);
  }
  return arr;
};
import Button from "@/components/Button";
export default {
  name: "Squares",
  props: {
    btnValues: Number,
    step: Number,
    onClickBtn: Function,
    arrPlay: Array,
    win: Object
  },
  data() {
    return {
      arrvalue: genArr(this.btnValues, this.step)
    };
  },
  components: {
    Button
  }
};
</script>
<style scoped>
.board {
  display: flex;
  justify-content: center;
}
</style>
