<template>
  <div class="printer-component">
    <div class="printer-content">
      <b>深圳问止中医投资发展有限公司问止中医诊所</b>
      <hr />
      <div class="printer-block">
        <Printer-cell prefix="姓名" content="贺荣"></Printer-cell>
        <Printer-cell prefix="性别" content="男"></Printer-cell>
        <Printer-cell prefix="年龄" content="19"></Printer-cell>
        <Printer-cell prefix="电话" content="****8846"></Printer-cell>
      </div>
      <hr />
      <div class="printer-block">
        <Printer-cell :type="1" prefix="日期" content="2020/5/21"></Printer-cell>
        <Printer-cell prefix="剂数：" content="5剂"></Printer-cell>
        <Printer-cell prefix="用量：" content="200ml"></Printer-cell>
        <Printer-cell prefix="频率：" content="每日2次"></Printer-cell>
      </div>
      <hr />
      <div class="printer-block">
        <Printer-cell
          :type="1"
          :width="300"
          :prefixWidth="80"
          prefix="服药时间："
          content="每日2次，早晚饭后一小时温服"
        ></Printer-cell>
      </div>
    </div>

    <PrintView :html="printHtml"></PrintView>
  </div>
</template>

<script>
import PrintView from "./PrintView.vue";
import PrinterCell from "./PrinterCell.vue";
export default {
  components: {
    PrintView,
    PrinterCell
  },
  name: "PrintTest",
  data() {
    return {
      printHtml: ""
    };
  },
  methods: {},
  mounted() {
    this.printHtml = this.$el.getElementsByClassName(
      "printer-content"
    )[0].innerHTML;
  }
};
</script>

<style scoped>
.printer-component {
  margin-bottom: 100px;
  font-size: 5px;
}
.printer-block {
  display: flex;
  flex-flow: row wrap;
  width: 300px;
}
</style>
