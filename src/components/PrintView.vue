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
  //   watch: {
  //     html(val) {
  //       if (val) {
  //         this.setBodyHtml(val);
  //       }
  //     }
  //   },
  methods: {
    print() {
        // window.print();
      console.log(window.document);
      
      if (this.html) {
        this.setBodyHtml();
      }
    },
    setBodyHtml() {
      console.log(0);

      const document = window.document;
      const iframe = window.frames[0];
      iframe.document.head.innerHTML = document.head.innerHTML; // 获取当前文档的头部给iframe
      iframe.document.body.innerHTML = this.html; // 把传过来的html给iframe头部
      console.log(iframe.document.head);
      console.log(iframe.document.body);
      // 图片和样式加载完成
      // eslint-disable-next-line no-unused-vars
      //   Promise.all([this.loadStyle(), this.loadImage()]).then(res => {
      //     //   打印
      //     console.log(4);
      //     iframe.window.print();
      //     console.log(5);
      //   });
      // eslint-disable-next-line no-unused-vars
    //   console.log(iframe.document.body.innerHTML);  
    //   iframe.window.print();
      
      // eslint-disable-next-line no-unused-vars
        Promise.all([this.loadStyle()]).then(res => {
          //   打印
          console.log(4);
          iframe.window.print();
          console.log(5);
        });
    },
    loadStyle() {
      const iframe = window.frames[0];
      const styles = iframe.document.head.getElementsByTagName("style"); // <style>
      const links = iframe.document.head.getElementsByTagName("link"); // <link>
      let arrs = [];
      arrs = arrs.concat(...styles, ...links);
      console.log(arrs);
      // eslint-disable-next-line no-unused-vars
      return new Promise((resolve, reject) => {
        for (let i = 0; i < arrs.length; i++) {
          arrs[i].onload = function() {
            if (i === arrs.length - 1) {
              console.log("style 样式加载完成");
              resolve("style 样式加载完成");
            }
          };
        }
      });
    },
    loadImage() {
      const iframe = window.frames[0];
      const imgs = iframe.document.body.getElementsByTagName("img"); // <img>

      // eslint-disable-next-line no-unused-vars
      return new Promise((resolve, reject) => {
        for (let i = 0; i < imgs.length; i++) {
          imgs[i].onload = function() {
            if (i === imgs.length - 1) {
              console.log("img 加载完成");
              resolve("img 加载完成");
            }
          };
        }
      });
    }
  }
};
</script>

<style scoped>
</style>
