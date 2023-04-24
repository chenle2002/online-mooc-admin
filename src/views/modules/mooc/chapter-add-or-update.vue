<template>
  <el-dialog
    :title="!dataForm.courseId ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible"
  >
    <el-form
      :model="dataForm"
      :rules="dataRule"
      ref="dataForm"
      @keyup.enter.native="dataFormSubmit()"
      label-width="80px"
    >
      <el-form-item label="章节名称" prop="name">
        <el-input v-model="dataForm.name" placeholder=""></el-input>
      </el-form-item>
      <el-form-item label="视频" prop="video">
        <UploadVideo v-model="dataForm.video"></UploadVideo>
      </el-form-item>
    </el-form>
    <span slot="footer" class="dialog-footer">
      <el-button @click="visible = false">取消</el-button>
      <el-button type="primary" @click="dataFormSubmit()">确定</el-button>
    </span>
  </el-dialog>
</template>

<script>
import UploadVideo from "@/components/upload/uploadVideo";
export default {
  components: { UploadVideo },
  data() {
    return {
      visible: false,
      dataForm: {
        courseId: 0,
        name: "",
        parentCid: "",
        catLevel: "",
        showStatus: "",
        icon: "",
        sort: "",
        video: ""
      },
      dataRule: {
        name: [{ required: true, message: "不能为空", trigger: "blur" }]
      }
    };
  },
  methods: {
    init(id) {
      this.dataForm.courseId = id || 0;
      this.visible = true;
      this.$nextTick(() => {
        this.$refs["dataForm"].resetFields();
        if (this.dataForm.courseId) {
          this.$http({
            url: this.$http.adornUrl(
              `/course/coursetree/info/${this.dataForm.courseId}`
            ),
            method: "get",
            params: this.$http.adornParams()
          }).then(({ data }) => {
            if (data && data.code === 0) {
              this.dataForm.name = data.courseTree.name;
              this.dataForm.parentCid = data.courseTree.parentCid;
              this.dataForm.catLevel = data.courseTree.catLevel;
              this.dataForm.showStatus = data.courseTree.showStatus;
              this.dataForm.icon = data.courseTree.icon;
              this.dataForm.video = data.courseTree.video;
            }
          });
        }
      });
    },
    // 表单提交
    dataFormSubmit() {
      this.$refs["dataForm"].validate(valid => {
        if (valid) {
          this.$http({
            url: this.$http.adornUrl(
              `/course/coursetree/${
                !this.dataForm.courseId ? "save" : "update"
              }`
            ),
            method: "post",
            data: this.$http.adornData({
              courseId: this.dataForm.courseId || undefined,
              name: this.dataForm.name,
              parentCid: this.dataForm.parentCid,
              catLevel: this.dataForm.catLevel,
              showStatus: this.dataForm.showStatus,
              icon: this.dataForm.icon,
              sort: this.dataForm.sort,
              video: this.dataForm.video
            })
          }).then(({ data }) => {
            if (data && data.code === 0) {
              this.$message({
                message: "操作成功",
                type: "success",
                duration: 1500,
                onClose: () => {
                  this.visible = false;
                  this.$emit("refreshDataList");
                }
              });
            } else {
              this.$message.error(data.msg);
            }
          });
        }
      });
    }
  }
};
</script>
