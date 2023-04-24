<template>
  <div class="pdf">
    <pdf
      ref="pdf"
      :src="pdfUrl"
      :page="pageNum"
      :rotate="pageRotate"
      @password="password"
      @progress="loadedRatio = $event"
      @page-loaded="pageLoaded($event)"
      @num-pages="pageTotalNum = $event"
      @error="pdfError($event)"
      @link-clicked="page = $event"
    >
    </pdf>
    <div class="pdf-tab">
      <el-button
        type="text"
        class="btn-def btn-pre"
        @click.stop="firstPage"
        :disabled="pageNum === 1"
        >首页</el-button
      >
      <el-button
        type="text"
        class="btn-def btn-pre"
        @click.stop="prePage"
        :disabled="pageNum === 1"
        >上一页</el-button
      >
      <el-button
        type="text"
        class="btn-def btn-next"
        @click.stop="nextPage"
        :disabled="pageNum === pageTotalNum"
        >下一页</el-button
      >

      >
    </div>
    <div class="pdf-page">{{ pageNum }}/{{ pageTotalNum }}</div>
  </div>
</template>
<script>
import pdf from "vue-pdf";
export default {
  name: "Pdf",
  components: {
    pdf
  },
  props: {
    pdfUrl: {
      type: String
    }
  },
  data() {
    return {
      pageNum: 1,
      pageTotalNum: 1,
      pageRotate: 0,
      // 加载进度
      loadedRatio: 0,
      curPageNum: 0
    };
  },
  mounted: function() {},
  methods: {
    firstPage() {
      this.pageNum = 1;
    },
    prePage() {
      var p = this.pageNum;
      p = p > 1 ? p - 1 : this.pageTotalNum;
      this.pageNum = p;
    },
    nextPage() {
      var p = this.pageNum;
      p = p < this.pageTotalNum ? p + 1 : 1;
      this.pageNum = p;
    },
    lastPage() {
      this.pageNum = this.pageTotalNum;
    },
    clock() {
      this.pageRotate += 90;
    },
    counterClock() {
      this.pageRotate -= 90;
    },
    password(updatePassword, reason) {
      updatePassword(prompt('password is "123456"'));
    },
    pageLoaded(e) {
      this.curPageNum = e;
    },
    pdfError(error) {
      console.error(error);
    },
    pdfPrintAll() {
      this.$refs.pdf.print();
    },
    pdfPrint() {
      this.$refs.pdf.print(100, [1, 2]);
    }
  }
};
</script>

<style lang="scss" scoped>
.pdf-tab {
  display: flex;
}
.pdf-page {
  text-align: right;
}
</style>
