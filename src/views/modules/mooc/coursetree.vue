<!--  -->
<template>
  <div>
    <el-switch
      v-model="draggable"
      active-text="开启拖拽"
      inactive-text="关闭拖拽"
    >
    </el-switch>
    <el-button v-if="draggable" @click="batchsave()"
      >批量保存拖拽结果
    </el-button>
    <el-button type="danger" @click="batchDelete">批量删除</el-button>
    <el-tree
      :data="data"
      :props="defaultProps"
      @node-click="handleNodeClick"
      :expand-on-click-node="false"
      show-checkbox
      node-key="courseId"
      :default-expanded-keys="expendKey"
      :draggable="draggable"
      :allow-drop="allowDrop"
      @node-drop="handleDrop"
      ref="menuTree"
    >
      <span class="custom-tree-node" slot-scope="{ node, data }">
        <span>{{ node.label }}</span>
        <span>
          <el-button
            v-if="node.level <= 2"
            type="text"
            size="mini"
            @click="() => append(data)"
          >
            Append
          </el-button>
          <el-button type="text" size="mini" @click="edit(data)">
            Edit
          </el-button>
          <el-button
            v-if="node.childNodes == 0"
            type="text"
            size="mini"
            @click="() => remove(node, data)"
          >
            Delete
          </el-button>
        </span>
      </span>
    </el-tree>
    <el-dialog
      :title="title"
      :visible.sync="dialogVisible"
      width="30%"
      :close-on-click-modal="false"
    >
      <el-form :model="course">
        <el-form-item label="课程名称">
          <el-input v-model="course.name" autocomplete="off"></el-input>
        </el-form-item>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button @click="dialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="submitData">确 定</el-button>
      </span>
    </el-dialog>

  </div>
</template>

<script>
//这里可以导入其他文件（比如：组件，工具js，第三方插件js，json文件，图片文件等等）
//例如：import 《组件名称》 from '《组件路径》';

export default {
  data() {
    return {
      title: "",
      draggable: false,
      maxLevel: 0,
      pCid: [],
      dislogType: "",
      updateNode: [],
      course: {
        name: "",
        parentCid: 0,
        catLevel: 0,
        showStatus: 1,
        sort: 0,
        courseId: null,
        icon: "",
        productUnit: null
      },
      data: [],
      expendKey: [],
      defaultProps: {
        children: "children",
        label: "name"
      },
      dialogVisible: false
    };
  },
  methods: {
    append(data) {
      //点击添加的方法，初始化数据并显示对话框
      // console.log("append", data);
      this.title = "添加分类";
      this.dialogType = "append";
      this.dialogVisible = true;
      this.course.parentCid = data.courseId;
      this.course.name = "";
      this.course.catLevel = data.catLevel * 1 + 1;
      this.course.courseId = null;
      this.course.icon = "";
      this.course.productUnit = "";
      this.course.sort = 0;
      this.course.showStatus = 1;
    },
    batchDelete() {
      let courseIds = [];
      let checkedNodes = this.$refs.menuTree.getCheckedNodes();
      console.log("被选中的元素", checkedNodes);
      for (let i = 0; i < checkedNodes.length; i++) {
        courseIds.push(checkedNodes[i].courseId);
      }
      this.$confirm(`是否批量删除【${courseIds}】菜单?`, "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning"
      })
        .then(() => {
          this.$http({
            url: this.$http.adornUrl("/course/coursetree/delete"),
            method: "post",
            data: this.$http.adornData(courseIds, false)
          }).then(({ data }) => {
            this.$message({
              message: "菜单批量删除成功",
              type: "success"
            });
            this.getDataMenu();
          });
        })
        .catch(() => {});
    },
    edit(data) {
      //修改数据的方法，axios动态获取状态
      console.log(data, 111);
      if(data.catLevel==1){
        this.$message({
          message: "您不能在此处修改课程信息！",
          type: "warning"
      })}else{
        this.title = "修改分类";
        this.dialogType = "edit";
        this.dialogVisible = true;
        this.$http({
          url: this.$http.adornUrl(`/course/coursetree/info/${data.courseId}`),
          method: "get"
        }).then(({ data }) => {
          this.course.name = data.courseTree.name;
          this.course.courseId = data.courseTree.courseId;
          this.course.icon = data.courseTree.icon;
          this.course.productUnit = data.courseTree.productUnit;
          this.course.parentCid = data.courseTree.parentCid;
          // console.log(data, 1111);
        });
        }
    },
    submitData() {
      //提交对话框，并根据对话框类型选择不同的更新/添加方法
      if (this.dialogType == "append") {
        this.addcourse();
      }
      if (this.dialogType == "edit") {
        this.editcourse();
      }
    },

    addcourse() {
      //提交添加的方法
      // console.log("提交的三级菜单内容", this.course);
      this.$http({
        url: this.$http.adornUrl("/course/coursetree/save"),
        method: "post",
        data: this.$http.adornData(this.course, false)
      }).then(({ data }) => {
        this.$message({
          message: "课程添加成功",
          type: "success"
        });
        this.dialogVisible = false;
        this.getDataMenu();
        this.expendKey = [this.course.parentCid];
      });
    },
    editcourse() {
      //提交后修改的方法
      var { courseId, name, icon, productUnit } = this.course;
      this.$http({
        url: this.$http.adornUrl("/course/coursetree/update"),
        method: "post",
        data: this.$http.adornData({ courseId, name, icon, productUnit }, false)
      }).then(({ data }) => {
        this.$message({
          message: "菜单修改成功",
          type: "success"
        });
        this.dialogVisible = false;
        this.getDataMenu();
        this.expendKey = [this.course.parentCid];
        // console.log([this.course.parentCid]);
      });
    },

    handleDrop(draggingNode, dropNode, dropType, ev) {
      //将受的需要传给数据库的更新数据保存为数组
      // console.log("handleDrop: ", draggingNode, dropNode);

      let pCid = 0; //当前节点最新父节点的id
      let siblings = null;
      if (dropType == "before" || dropType == "after") {
        pCid =
          dropNode.parent.data.courseId == undefined
            ? 0
            : dropNode.parent.data.courseId;
        siblings = dropNode.parent.childNodes;
      } else {
        pCid = dropNode.data.courseId;
        siblings = dropNode.childNodes;
      }

      this.pCid.push(pCid);
      //当前拖拽节点的最新顺序
      for (let i = 0; i < siblings.length; i++) {
        //便利节点为被拖过去的节点
        if (siblings[i].data.courseId == draggingNode.data.courseId) {
          let catLevel = draggingNode.level;
          //如果受的层级发生变化
          if (siblings[i].level != draggingNode.level) {
            catLevel = siblings[i].level;
            this.updatechildlevel(siblings[i]);
          }
          this.updateNode.push({
            courseId: siblings[i].data.courseId,
            sort: i,
            parentCid: pCid,
            catLevel: catLevel
          });
        } else {
          this.updateNode.push({
            courseId: siblings[i].data.courseId,
            sort: i
          });
        }
      }

      // console.log("update:", this.updateNode);
    },
    updatechildlevel(node) {
      //便利 受节点 的所有孩子，将他们需要传给数据库的更新数据保存为数组
      if (node.childNodes.length > 0) {
        for (let i = 0; i < node.childNodes.length; i++) {
          this.updateNode.push({
            courseId: node.childNodes[i].data.courseId,
            catLevel: node.childNodes[i].level
          });
          this.updatechildlevel(node.childNodes[i]);
        }
      }
    },
    batchsave() {
      //保存拖拽结果，http
      this.$http({
        url: this.$http.adornUrl("/course/coursetree/update/sort"),
        method: "post",
        data: this.$http.adornData(this.updateNode, false)
      }).then(({ data }) => {
        this.$message({
          message: "菜单顺序修改成功",
          type: "success"
        });
        //刷新菜单
        this.getDataMenu();
        this.expendKey = this.pCid;
        this.updateNode = [];
        this.maxLevel = 0;
      });
    },
    allowDrop(draggingNode, dropNode, type) {
      //判断能否拖拽
      //1、被拖动的当前节点以及所在的父节点总层数不能大于3

      //1）、被拖动的当前节点总层数
      // console.log("allowDrop:", draggingNode, dropNode, type);
      //
      this.countNodeLevel(draggingNode);
      //当前正在拖动的节点+父节点所在的深度不大于3即可
      let deep = Math.abs(this.maxLevel - draggingNode.level) + 1;
      // console.log("深度：", deep);

      //   this.maxLevel
      if (type == "inner") {
        // console.log(
        //   `this.maxLevel：${this.maxLevel}；draggingNode.data.catLevel：${draggingNode.data.catLevel}；dropNode.level：${dropNode.level}`
        // );
        return deep + dropNode.level <= 3;
      } else {
        return deep + dropNode.parent.level <= 3;
      }
    },
    countNodeLevel(node) {
      //找到所有子节点，求出最大深度
      if (node.childNodes != null && node.childNodes.length > 0) {
        for (let i = 0; i < node.childNodes.length; i++) {
          if (node.childNodes[i].level > this.maxLevel) {
            this.maxLevel = node.childNodes[i].level;
          }
          this.countNodeLevel(node.childNodes[i]);
        }
      }
    },
    getDataMenu() {
      this.dataListLoading = true;
      this.$http({
        url: this.$http.adornUrl("/course/coursetree/list/tree"),
        method: "get"
      }).then(({ data }) => {
        this.data = data.page;
      });
    },
    remove(node, data) {
      if(data.catLevel==1){
        this.$message({
          message: "您不能在此处删除课程信息！",
          type: "warning"
        })}else {
        var ids = [data.courseId];
        this.$confirm(`是否删除【${data.name}】菜单?`, "提示", {
          confirmButtonText: "确定",
          cancelButtonText: "取消",
          type: "warning"
        })
          .then(() => {
            this.$http({
              url: this.$http.adornUrl("/course/coursetree/delete"),
              method: "post",
              data: this.$http.adornData(ids, false)
            }).then(({ data }) => {
              this.$message({
                message: "菜单删除成功",
                type: "success"
              });
              this.getDataMenu();
              // console.log(node);
              // console.log(node.parent.data.courseId);
              this.expendKey = [node.parent.data.courseId];
            });
          }).catch(() => {});
      }

    },
    handleNodeClick(data) {
      // console.log(data);
    }
  },
  created() {
    this.getDataMenu();
  }
};
</script>
<style scoped></style>
