<template>
  <v-card>
    <v-flex xs12 sm10>
      <v-tree url="/item/category/list"
              :isEdit="isEdit"
              @handleAdd="handleAdd"
              @handleEdit="handleEdit"
              @handleDelete="handleDelete"
              @handleClick="handleClick"
      />
    </v-flex>
  </v-card>
</template>

<script>
  export default {
    name: "category",
    data() {
      return {
        isEdit: true
      }
    },
    methods: {
      handleAdd(node) {
        console.log("add .... ");
        console.log(node);
        this.$http.get("/item/category/add", {
          params: {
            id: node.id,
            name: node.name,
            parentId: node.parentId,
            isParent: node.isParent,
            sort: node.sort
          }
        }).then(resp => { // 这里使用箭头函数
          if (resp.status === 200) {
            this.$message.success("新增节点成功！")
          } else {
            this.$message.success("新增节点失败！")

          }
        })
      },
      handleEdit(id, name) {
        console.log("edit... id: " + id + ", name: " + name)
        this.$http.get("/item/category/edit", {
          params: {
            id: id,
            name: name
          }
        }).then(resp => {
          if (resp.status === 200) {
            this.$message.success("修改成功！")
          } else {
            this.$message.success("修改失败！")
          }
        });


      },
      handleDelete(id) {
        console.log("delete node ... " + id)

        this.$http.get("/item/category/delete", {
          params: {
            id: id,
          }
        }).then(resp => { // 这里使用箭头函数
          if (resp.status === 200) {
            this.$message.success("删除节点成功！")
          } else {
            this.$message.success("删除节点失败！")
          }
        })
      },
      handleClick(node) {
        console.log(node)
      }
    }
  };
</script>

<style scoped>

</style>
