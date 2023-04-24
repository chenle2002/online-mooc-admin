<template>
  <el-dialog
    :title="!dataForm.id ? '新增' : '修改'"
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
      <el-form-item label="课程名称" prop="name">
        <el-input v-model="dataForm.name" placeholder=""></el-input>
      </el-form-item>
      <el-form-item label="课程描述" prop="description">
        <el-input v-model="dataForm.description" placeholder=""></el-input>
      </el-form-item>
      <el-form-item label="课程分类" prop="sortId">
        <el-input v-model="dataForm.sortId" placeholder=""></el-input>
      </el-form-item>
      <el-form-item label="教师Id" prop="teacherId">
        <el-input v-model="dataForm.teacherId" placeholder=""></el-input>
      </el-form-item>
      <el-form-item label="封面" prop="image">
        <div class="selectfile">选择image文件</div>
        <single-upload v-model="dataForm.image"></single-upload>
      </el-form-item>

      <el-form-item label="pdf" prop="pdf">
        <div class="selectfile">选择pdf文件</div>
        <UploadPdf v-model="dataForm.pdf"></UploadPdf>
      </el-form-item>
    </el-form>
    <span slot="footer" class="dialog-footer">
      <el-button @click="visible = false">取消</el-button>
      <el-button type="primary" @click="dataFormSubmit()">确定</el-button>
    </span>
  </el-dialog>
</template>

<script>
import SingleUpload from "@/components/upload/singleUpload";
import UploadPdf from "@/components/upload/uploadPdf";
export default {
  components: { SingleUpload, UploadPdf },
  data() {
    return {
      path: "",
      // 下载的文件名
      fileName: "",
      // 目录树
      filenames: [],
      // 显示位置
      location: "/",
      dialogVisibleDelete: false,

      visible: false,
      dataForm: {
        id: 0,
        description: "",
        sortId: "",
        teacherId: "",
        name: "",
        image: "",
        pdf: ""
      },
      filename: "",
      selectFileobj: null,
      dataRule: {
        description: [{ required: true, message: "不能为空", trigger: "blur" }],
        sortId: [{ required: true, message: "不能为空", trigger: "blur" }],
        teacherId: [{ required: true, message: "不能为空", trigger: "blur" }],
        name: [{ required: true, message: "不能为空", trigger: "blur" }]
      }
    };
  },
  methods: {
    init(id) {
      this.dataForm.id = id || 0;
      this.visible = true;
      this.$nextTick(() => {
        this.$refs["dataForm"].resetFields();
        if (this.dataForm.id) {
          this.$http({
            url: this.$http.adornUrl(
              `/course/courserdes/info/${this.dataForm.id}`
            ),
            method: "get",
            params: this.$http.adornParams()
          }).then(({ data }) => {
            if (data && data.code === 0) {
              this.dataForm.description = data.courserDes.description;
              this.dataForm.sortId = data.courserDes.sortId;
              this.dataForm.teacherId = data.courserDes.teacherId;
              this.dataForm.name = data.courserDes.name;
              this.dataForm.image = data.courserDes.image;
              this.dataForm.pdf = data.courserDes.pdf;
            }
          });
        }
      });
    },
    // 表单提交
    dataFormSubmit() {
      // 上传按钮

      this.$refs["dataForm"].validate(valid => {
        if (valid) {
          this.$http({
            url: this.$http.adornUrl(
              `/course/courserdes/${!this.dataForm.id ? "save" : "update"}`
            ),
            method: "post",
            data: this.$http.adornData({
              id: this.dataForm.id || undefined,
              description: this.dataForm.description,
              sortId: this.dataForm.sortId,
              teacherId: this.dataForm.teacherId,
              name: this.dataForm.name,
              image: this.dataForm.image,
              pdf: this.dataForm.pdf
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
