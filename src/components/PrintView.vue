<template>
  <div class="print">
    <button @click="print">打印</button>
    <iframe id="iframe" style="display: none;"></iframe>
  </div>
</template>

<script>
export default {
  name: "PrintView",
  props: {
    html: {
      type: String,
      default: ""
    }
  },
  methods: {
    print() {
      if (this.html) {
        this.setBodyHtml();
      }
    },
    setBodyHtml() {
      const document = window.document;
      const iframe = window.frames[0];
      iframe.document.head.innerHTML = document.head.innerHTML; // 获取当前文档的头部给iframe
      iframe.document.body.innerHTML = this.html; // 把传过来的html给iframe头部
      // 图片和样式加载完成
      // iframe.window.print();
      // eslint-disable-next-line no-unused-vars
      Promise.all([this.loadStyle(), this.loadImage()]).then(res => {
        //   打印
        iframe.window.print();
      });
    },
    loadStyle() {
      const iframe = window.frames[0];
      const styles = iframe.document.head.getElementsByTagName("style"); // <style>
      const links = iframe.document.head.getElementsByTagName("link"); // <link>
      let arrs = [];
      arrs = arrs.concat(...styles, ...links);
      // eslint-disable-next-line no-unused-vars
      return new Promise((resolve, reject) => {
        if (arrs.length) {
          for (let i = 0; i < arrs.length; i++) {
            arrs[i].onload = function() {
              if (i === arrs.length - 1) {
                resolve("style 样式加载完成");
              }
            };
          }
        } else {
          resolve("style 样式加载完成");
        }
      });
    },
    loadImage() {
      const iframe = window.frames[0];
      const imgs = iframe.document.body.getElementsByTagName("img"); // <img>
      // eslint-disable-next-line no-unused-vars
      return new Promise((resolve, reject) => {
        if (imgs.length) {
          for (let i = 0; i < imgs.length; i++) {
            imgs[i].onload = function() {
              if (i === imgs.length - 1) {
                resolve("img 加载完成");
              }
            };
          }
        } else {
          resolve("img 加载完成");
        }
      });
    }
  }
};
</script>

<style scoped>
</style>
