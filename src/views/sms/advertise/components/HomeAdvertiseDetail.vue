<template> 
  <el-card class="form-container" shadow="never">
    <el-form :model="homeAdvertise"
             :rules="rules"
             ref="homeAdvertiseFrom"
             label-width="150px"
             size="small">
      <el-form-item label="Name of the advertisement：" prop="name">
        <el-input v-model="homeAdvertise.name" class="input-width"></el-input>
      </el-form-item>
      <el-form-item label="Advertising Position：">
        <el-select v-model="homeAdvertise.type">
          <el-option
            v-for="type in typeOptions"
            :key="type.value"
            :label="type.label"
            :value="type.value">
          </el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="Starting time：" prop="startTime">
        <el-date-picker
          type="datetime"
          placeholder="Select Date"
          v-model="homeAdvertise.startTime"></el-date-picker>
      </el-form-item>
      <el-form-item label="Time due：" prop="endTime">
        <el-date-picker
          type="datetime"
          placeholder="Select Date"
          v-model="homeAdvertise.endTime"></el-date-picker>
      </el-form-item>
      <el-form-item label="On/Offline：">
        <el-radio-group v-model="homeAdvertise.status">
          <el-radio :label="0">Go offline</el-radio>
          <el-radio :label="1">Go online</el-radio>
        </el-radio-group>
      </el-form-item>
      <el-form-item label="Advertisement Pictures：">
        <single-upload v-model="homeAdvertise.pic"></single-upload>
      </el-form-item>
      <el-form-item label="Arrange in order：">
        <el-input v-model="homeAdvertise.sort" class="input-width"></el-input>
      </el-form-item>

      <el-form-item label="Advertising Links：" prop="url">
        <el-input v-model="homeAdvertise.url" class="input-width"></el-input>
      </el-form-item>
      <el-form-item label="Advertising Remarks：">
        <el-input
          class="input-width"
          type="textarea"
          :rows="5"
          placeholder="Please enter content"
          v-model="homeAdvertise.note">
        </el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="onSubmit('homeAdvertiseFrom')">Submit</el-button>
        <el-button v-if="!isEdit" @click="resetForm('homeAdvertiseFrom')">Reset</el-button>
      </el-form-item>
    </el-form>
  </el-card>
</template>
<script>
  import SingleUpload from '@/components/Upload/singleUpload'
  import {createHomeAdvertise, getHomeAdvertise, updateHomeAdvertise} from '@/api/homeAdvertise'
  const defaultTypeOptions = [
    {
      label: 'PC homepage rotation',
      value: 0
    },
    {
      label: 'APP homepage rotation',
      value: 1
    }
  ];
  const defaultHomeAdvertise = {
    name: null,
    type: 1,
    pic: null,
    startTime: null,
    endTime: null,
    status: 0,
    url: null,
    note: null,
    sort: 0
  };
  export default {
    name: 'HomeAdvertiseDetail',
    components:{SingleUpload},
    props: {
      isEdit: {
        type: Boolean,
        default: false
      }
    },
    data() {
      return {
        homeAdvertise: null,
        rules: {
          name: [
            {required: true, message: 'Please enter the name of the advertisement', trigger: 'blur'},
            {min: 2, max: 140, message: 'From 2 to 140 characters in length', trigger: 'blur'}
          ],
          url: [
            {required: true, message: 'Please enter the advertisement link', trigger: 'blur'}
          ],
          startTime: [
            {required: true, message: 'Please select a start time', trigger: 'blur'}
          ],
          endTime: [
            {required: true, message: 'Please select an expiration date', trigger: 'blur'}
          ],
          pic: [
            {required: true, message: 'Please select the advertisement picture', trigger: 'blur'}
          ]
        },
        typeOptions: Object.assign({}, defaultTypeOptions)
      }
    },
    created(){
      if (this.isEdit) {
        getHomeAdvertise(this.$route.query.id).then(response => {
          this.homeAdvertise = response.data;
        });
      }else{
        this.homeAdvertise = Object.assign({},defaultHomeAdvertise);
      }
    },
    methods: {
      onSubmit(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
            this.$confirm('Whether to submit data', 'Tips', {
              confirmButtonText: 'Recognize',
              cancelButtonText: 'Cancel',
              type: 'warning'
            }).then(() => {
              if (this.isEdit) {
                updateHomeAdvertise(this.$route.query.id, this.homeAdvertise).then(response => {
                  this.$refs[formName].resetFields();
                  this.$message({
                    message: 'Modified successfully',
                    type: 'success',
                    duration:1000
                  });
                  this.$router.back();
                });
              } else {
                createHomeAdvertise(this.homeAdvertise).then(response => {
                  this.$refs[formName].resetFields();
                  this.homeAdvertise = Object.assign({},defaultHomeAdvertise);
                  this.$message({
                    message: 'Submitted successfully',
                    type: 'success',
                    duration:1000
                  });
                });
              }
            });

          } else {
            this.$message({
              message: 'Validation failure',
              type: 'error',
              duration:1000
            });
            return false;
          }
        });
      },
      resetForm(formName) {
        this.$refs[formName].resetFields();
        this.homeAdvertise = Object.assign({},defaultHomeAdvertise);
      }
    }
  }
</script>
<style scoped>
  .input-width {
    width: 70%;
  }
</style>


