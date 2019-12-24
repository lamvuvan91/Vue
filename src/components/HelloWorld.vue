<template>
  <div class="hello">
    <p>Người thăng là {{ win.peoPlayWin }}</p>
    <input v-model="numberInput" type="number" v-on:click="addsquares" />
    <Board
      :numberInput="Number(numberInput1)"
      :step="Number(numberInput1)"
      :onClickBtn="onClickBtn"
      :arrPlay="arrPlay"
      :win="win"
    ></Board>
  </div>
</template>

<script>
import Board from "@/components/Board";
const genArrResul = number => {
  var arr = [];
  for (let x = 1; x <= number * number; x++) {
    arr.push({ key: x, value: "" });
  }
  console.log(arr);
  return arr;
};

const sortArr = arr => {
  return arr.sort((a, b) => a.key - b.key);
};

const checkWin = (result, that) => {
  var arrX = result.filter(x => x.value === "X");
  var arrY = result.filter(x => x.value === "Y");
  var resultX = rule(sortArr(arrX), that.numberInput1);
  var resultY = rule(sortArr(arrY));
  console.log("test", that);
  if (resultX.status) {
    that.win.arrWin = resultX.arr;
    that.win.peoPlayWin = "X";
    that.win.status = true;
    return;
  }
  if (resultY.status) {
    that.win.arrWin = resultY.arr;
    that.win.peoPlayWin = "Y";
    that.win.status = true;
    return;
  }
};

const rule = (arr, number) => {
  for (let x = 0; x <= arr.length - 5; x++) {
    //check 5 ngang
    if (
      arr[x].key === arr[x + 1].key - 1 &&
      arr[x].key === arr[x + 2].key - 2 &&
      arr[x].key === arr[x + 3].key - 3 &&
      arr[x].key === arr[x + 4].key - 4
    ) {
      return {
        status: true,
        arr: [arr[x], arr[x + 1], arr[x + 2], arr[x + 3], arr[x + 4]]
      };
    }
    //check 5 doc
    if (
      arr[x].key === arr[x + 1].key - number &&
      arr[x + 1].key === arr[x + 2].key - number &&
      arr[x + 2].key === arr[x + 3].key - number &&
      arr[x + 3].key === arr[x + 4].key - number
    ) {
      return {
        status: true,
        arr: [arr[x], arr[x + 1], arr[x + 2], arr[x + 3], arr[x + 4]]
      };
    }
    //check cheo trai
    if (
      arr[x].key === arr[x + 1].key - number - 1 &&
      arr[x + 1].key === arr[x + 2].key - number - 1 &&
      arr[x + 2].key === arr[x + 3].key - number - 1 &&
      arr[x + 3].key === arr[x + 4].key - number - 1
    ) {
      return {
        status: true,
        arr: [arr[x], arr[x + 1], arr[x + 2], arr[x + 3], arr[x + 4]]
      };
    }
    //check cheo phai
    if (
      arr[x].key === arr[x + 1].key - number + 1 &&
      arr[x + 1].key === arr[x + 2].key - number + 1 &&
      arr[x + 2].key === arr[x + 3].key - number + 1 &&
      arr[x + 3].key === arr[x + 4].key - number + 1
    ) {
      return {
        status: true,
        arr: [arr[x], arr[x + 1], arr[x + 2], arr[x + 3], arr[x + 4]]
      };
    }
  }
  return { status: false, arr: [] };
};
export default {
  name: "HelloWorld",
  components: {
    Board
  },
  data() {
    return {
      numberInput: 0,
      numberInput1: 0,
      peoPlay: "X",
      arrPlay: [],
      win: {
        arrWin: [],
        peoPlayWin: "",
        status: false
      }
    };
  },
  methods: {
    addsquares(e) {
      this.numberInput1 = e.target.value;
      this.arrPlay = genArrResul(e.target.value);
    },
    onClickBtn(e) {
      console.log("fun", e.target.value);
      this.arrPlay[e.target.value - 1].value = this.peoPlay;
      this.peoPlay = this.peoPlay === "X" ? "Y" : "X";
      console.log(this.arrPlay);
      checkWin(this.arrPlay, this);
      console.log("win", this.win);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
