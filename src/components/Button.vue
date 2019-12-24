<template>
  <button
    class="aaa"
    :class="{
      bbb: win.arrWin.filter(x => x.key == value).length > 0 ? true : false
    }"
    :value="value"
    @click="e => execute(e)"
    :disabled="arrPlay[value - 1].value || win.status ? true : false"
  >
    {{ arrPlay[value - 1].value }}
  </button>
</template>

<script>
export default {
  name: "Button",
  data() {
    return {
      people: ""
    };
  },
  props: {
    value: Number,
    clickBtn: {
      type: Function
    },
    arrPlay: Array,
    win: Object
  },
  methods: {
    execute(e) {
      this.clickBtn(e);
    }
  }
};
</script>
<style scoped>
.aaa {
  background: rgb(37, 34, 34);
  width: 30px;
  max-width: 30px;
  height: 30px;
  max-height: 30px;
}
.bbb {
  background: red;
}
</style>
