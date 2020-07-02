<template>
  <select @change="timezonechoose($event)">
    <option
      :value="key"
      v-for="(key,index) in list"
      :key="index"
      
    >{{index}}</option>
    <!-- <option value="8" selected>UTC+8</option>
                    <option value="0">UTC</option>
                    <option value="1">UTC+1</option>
                    <option value="2">UTC+2</option>
                    <option value="3">UTC+3</option>
                    <option value="4">UTC+4</option>
                    <option value="5">UTC+5</option>
                    <option value="6">UTC+6</option>
                    <option value="7">UTC+7</option>
                    <option value="8">UTC+8</option>
                    <option value="9">UTC+9</option>
                    <option value="10">UTC+10</option>
                    <option value="11">UTC+11</option>
                    <option value="12">UTC+12</option>
                    <option value="-11">UTC-11</option>
                    <option value="-10">UTC-10</option>
                    <option value="-9">UTC-9</option>
                    <option value="-8">UTC-8</option>
                    <option value="-7">UTC-7</option>
                    <option value="-6">UTC-6</option>
                    <option value="-5">UTC-5</option>
                    <option value="-4">UTC-4</option>
                    <option value="-3">UTC-3</option>
                    <option value="-2">UTC-2</option>
    <option value="-1">UTC-1</option>-->
  </select>
</template>

<script>
export default {
  name: "selectBox",
  data: function() {
    return {
      val: 8
    };
  },
  props: {
    list: {}
  },
  methods: {
    timezonechoose(event) {
      this.val = event.target.value;
    //   console.log(event.target.value);
      this.$emit("timezone1", event.target.value);
    }
  }
};
</script>

<style scoped>
select {
  width: 112px;
  height: 32px;
  background-color: #e3e7ee;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  font-size: 14px;
  padding-left: 10px;
  margin-top: 14px;
  margin-left: 14px;
  margin-bottom: 14px;
  font-family: PingFang SC, Verdana, Helvetica Neue, Microsoft Yahei,
    Hiragino Sans GB, Microsoft Sans Serif, WenQuanYi Micro Hei, sans-serif;
}
</style>