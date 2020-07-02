<template>
  <button @click="$emit('switch1')">
    <slot></slot>
  </button>
</template>
<script>
export default {
  name: "switchButton"
};
</script>
<style scoped>
button {
  border: 0;
  outline: none;
  float: right;
  width: 124px;
  height: 32px;
  box-shadow: 0 2px 4px rgba(160, 127, 127, 0.1);
  border-radius: 5px;
  font-size: 14px;
  background-color: #f7a735;
  color: #fff;
  margin-right: 14px;
  margin-top: 14px;
  margin-bottom: 14px;
  font-family: PingFang SC, Verdana, Helvetica Neue, Microsoft Yahei,
    Hiragino Sans GB, Microsoft Sans Serif, WenQuanYi Micro Hei, sans-serif;
}
</style>