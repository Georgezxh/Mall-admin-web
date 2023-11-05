<template>
  <el-card class="form-container" shadow="never">
    <el-form :model="menu"
             :rules="rules"
             ref="menuFrom"
             label-width="150px">
      <el-form-item label="Menu Name：" prop="title">
        <el-input v-model="menu.title"></el-input>
      </el-form-item>
      <el-form-item label="Parent menu：">
        <el-select v-model="menu.parentId"
                   placeholder="Please select menu">
          <el-option
            v-for="item in selectMenuList"
            :key="item.id"
            :label="item.title"
            :value="item.id">
          </el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="Front-end name：" prop="name">
        <el-input v-model="menu.name"></el-input>
      </el-form-item>
      <el-form-item label="Front-end Icons：" prop="icon">
        <el-input v-model="menu.icon" style="width: 80%"></el-input>
        <svg-icon style="margin-left: 8px" :icon-class="menu.icon"></svg-icon>
      </el-form-item>
      <el-form-item label="Whether to show：">
        <el-radio-group v-model="menu.hidden">
          <el-radio :label="0">Yes</el-radio>
          <el-radio :label="1">No</el-radio>
        </el-radio-group>
      </el-form-item>
      <el-form-item label="Arrange in order：">
        <el-input v-model="menu.sort"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="onSubmit('menuFrom')">Submit</el-button>
        <el-button v-if="!isEdit" @click="resetForm('menuFrom')">Reset</el-button>
      </el-form-item>
    </el-form>
  </el-card>
</template>

<script>
  import {fetchList, createMenu, updateMenu, getMenu} from '@/api/menu';

  const defaultMenu = {
    title: '',
    parentId: 0,
    name: '',
    icon: '',
    hidden: 0,
    sort: 0
  };
  export default {
    name: "MenuDetail",
    props: {
      isEdit: {
        type: Boolean,
        default: false
      }
    },
    data() {
      return {
        menu: Object.assign({}, defaultMenu),
        selectMenuList: [],
        rules: {
          title: [
            {required: true, message: 'Please enter a menu name', trigger: 'blur'},
            {min: 2, max: 140, message: 'From 2 to 140 characters in length', trigger: 'blur'}
          ],
          name: [
            {required: true, message: 'Please enter a front-end name', trigger: 'blur'},
            {min: 2, max: 140, message: 'From 2 to 140 characters in length', trigger: 'blur'}
          ],
          icon: [
            {required: true, message: 'Please enter the front-end icon', trigger: 'blur'},
            {min: 2, max: 140, message: 'From 2 to 140 characters in length', trigger: 'blur'}
          ]
        }
      }
    },
    created() {
      if (this.isEdit) {
        getMenu(this.$route.query.id).then(response => {
          this.menu = response.data;
        });
      } else {
        this.menu = Object.assign({}, defaultMenu);
      }
      this.getSelectMenuList();
    },
    methods: {
      getSelectMenuList() {
        fetchList(0, {pageSize: 100, pageNum: 1}).then(response => {
          this.selectMenuList = response.data.list;
          this.selectMenuList.unshift({id: 0, title: 'No parent menu'});
        });
      },
      onSubmit(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
            this.$confirm('Whether to submit data', 'Tips', {
              confirmButtonText: 'Recognize',
              cancelButtonText: 'Cancel',
              type: 'warning'
            }).then(() => {
              if (this.isEdit) {
                updateMenu(this.$route.query.id, this.menu).then(response => {
                  this.$message({
                    message: 'Modified successfully',
                    type: 'success',
                    duration: 1000
                  });
                  this.$router.back();
                });
              } else {
                createMenu(this.menu).then(response => {
                  this.$refs[formName].resetFields();
                  this.resetForm(formName);
                  this.$message({
                    message: 'Submitted successfully',
                    type: 'success',
                    duration: 1000
                  });
                  this.$router.back();
                });
              }
            });

          } else {
            this.$message({
              message: 'Validation failure',
              type: 'error',
              duration: 1000
            });
            return false;
          }
        });
      },
      resetForm(formName) {
        this.$refs[formName].resetFields();
        this.menu = Object.assign({}, defaultMenu);
        this.getSelectMenuList();
      },
    }
  }
</script>

<style scoped>

</style>
