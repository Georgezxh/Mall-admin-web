<template> 
  <div class="app-container">
    <el-card class="filter-container" shadow="never">
      <div>
        <i class="el-icon-search"></i>
        <span>Filter Search</span>
        <el-button
          style="float:right"
          type="primary"
          @click="handleSearchList()"
          size="small">
          Inquiry Search
        </el-button>
        <el-button
          style="float:right;margin-right: 15px"
          @click="handleResetSearch()"
          size="small">
          Reset
        </el-button>
      </div>
      <div style="margin-top: 15px">
        <el-form :inline="true" :model="listQuery" size="small" label-width="140px">
          <el-form-item label="Product Name：">
            <el-input v-model="listQuery.productName" class="input-width" placeholder="Product Name"></el-input>
          </el-form-item>
          <el-form-item label=" Recommended Status：">
            <el-select v-model="listQuery.recommendStatus" placeholder="All" clearable class="input-width">
              <el-option v-for="item in recommendOptions"
                         :key="item.value"
                         :label="item.label"
                         :value="item.value">
              </el-option>
            </el-select>
          </el-form-item>
        </el-form>
      </div>
    </el-card>
    <el-card class="operate-container" shadow="never">
      <i class="el-icon-tickets"></i>
      <span>Data sheet</span>
      <el-button size="mini" class="btn-add" @click="handleSelectProduct()">Select product</el-button>
    </el-card>
    <div class="table-container">
      <el-table ref="newProductTable"
                :data="list"
                style="width: 100%;"
                @selection-change="handleSelectionChange"
                v-loading="listLoading" border>
        <el-table-column type="selection" width="60" align="center"></el-table-column>
        <el-table-column label="Serial number" width="120" align="center">
          <template slot-scope="scope">{{scope.row.id}}</template>
        </el-table-column>
        <el-table-column label="Product Name" align="center">
          <template slot-scope="scope">{{scope.row.productName}}</template>
        </el-table-column>
        <el-table-column label="Recommended or not" width="200" align="center">
          <template slot-scope="scope">
            <el-switch
              @change="handleRecommendStatusStatusChange(scope.$index, scope.row)"
              :active-value="1"
              :inactive-value="0"
              v-model="scope.row.recommendStatus">
            </el-switch>
          </template>
        </el-table-column>
        <el-table-column label="Arrange in order" width="160" align="center">
          <template slot-scope="scope">{{scope.row.sort}}</template>
        </el-table-column>
        <el-table-column label="Statuses" width="160" align="center">
          <template slot-scope="scope">{{scope.row.recommendStatus | formatRecommendStatus}}</template>
        </el-table-column>
        <el-table-column label="Operational" width="180" align="center">
          <template slot-scope="scope">
            <el-button size="mini"
                       type="text"
                       @click="handleEditSort(scope.$index, scope.row)">Setting Sorting
            </el-button>
            <el-button size="mini"
                       type="text"
                       @click="handleDelete(scope.$index, scope.row)">Delete
            </el-button>
          </template>
        </el-table-column>
      </el-table>
    </div>
    <div class="batch-operate-container">
      <el-select
        size="small"
        v-model="operateType" placeholder="Batch operation">
        <el-option
          v-for="item in operates"
          :key="item.value"
          :label="item.label"
          :value="item.value">
        </el-option>
      </el-select>
      <el-button
        style="margin-left: 20px"
        class="search-button"
        @click="handleBatchOperate()"
        type="primary"
        size="small">
        Recognize
      </el-button>
    </div>
    <div class="pagination-container">
      <el-pagination
        background
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        layout="total, sizes,prev, pager, next,jumper"
        :page-size="listQuery.pageSize"
        :page-sizes="[5,10,15]"
        :current-page.sync="listQuery.pageNum"
        :total="total">
      </el-pagination>
    </div>
    <el-dialog title="Select product" :visible.sync="selectDialogVisible" width="50%">
      <el-input v-model="dialogData.listQuery.keyword"
                style="width: 250px;margin-bottom: 20px"
                size="small"
                placeholder="Product Name Search">
        <el-button slot="append" icon="el-icon-search" @click="handleSelectSearch()"></el-button>
      </el-input>
      <el-table :data="dialogData.list"
                @selection-change="handleDialogSelectionChange" border>
        <el-table-column type="selection" width="60" align="center"></el-table-column>
        <el-table-column label="Product Name" align="center">
          <template slot-scope="scope">{{scope.row.name}}</template>
        </el-table-column>
        <el-table-column label="Product number" width="160" align="center">
          <template slot-scope="scope">NO.{{scope.row.productSn}}</template>
        </el-table-column>
        <el-table-column label="Price" width="120" align="center">
          <template slot-scope="scope">￥{{scope.row.price}}</template>
        </el-table-column>
      </el-table>
      <div class="pagination-container">
        <el-pagination
          background
          @size-change="handleDialogSizeChange"
          @current-change="handleDialogCurrentChange"
          layout="prev, pager, next"
          :current-page.sync="dialogData.listQuery.pageNum"
          :page-size="dialogData.listQuery.pageSize"
          :page-sizes="[5,10,15]"
          :total="dialogData.total">
        </el-pagination>
      </div>
      <div style="clear: both;"></div>
      <div slot="footer">
        <el-button  size="small" @click="selectDialogVisible = false">Cancel</el-button>
        <el-button  size="small" type="primary" @click="handleSelectDialogConfirm()">Recognize</el-button>
      </div>
    </el-dialog>
    <el-dialog title="Setting Sorting"
               :visible.sync="sortDialogVisible"
               width="40%">
      <el-form :model="sortDialogData"
               label-width="150px">
        <el-form-item label="Arrange in order：">
          <el-input v-model="sortDialogData.sort" style="width: 200px"></el-input>
        </el-form-item>
      </el-form>
      <span slot="footer">
        <el-button @click="sortDialogVisible = false" size="small">Cancel</el-button>
        <el-button type="primary" @click="handleUpdateSort" size="small">Recognize</el-button>
      </span>
    </el-dialog>
  </div>
</template>
<script>
  import {fetchList,updateRecommendStatus,deleteHotProduct,createHotProduct,updateHotProductSort} from '@/api/hotProduct';
  import {fetchList as fetchProductList} from '@/api/product';

  const defaultListQuery = {
    pageNum: 1,
    pageSize: 5,
    productName: null,
    recommendStatus: null
  };
  const defaultRecommendOptions = [
    {
      label: 'Not recommended',
      value: 0
    },
    {
      label: 'Recommended',
      value: 1
    }
  ];
  export default {
    name: 'hotProductList',
    data() {
      return {
        listQuery: Object.assign({}, defaultListQuery),
        recommendOptions: Object.assign({}, defaultRecommendOptions),
        list: null,
        total: null,
        listLoading: false,
        multipleSelection: [],
        operates: [
          {
            label: "Set as Recommended",
            value: 0
          },
          {
            label: "Cancel referrals",
            value: 1
          },
          {
            label: "Delete",
            value: 2
          }
        ],
        operateType: null,
        selectDialogVisible:false,
        dialogData:{
          list: null,
          total: null,
          multipleSelection:[],
          listQuery:{
            keyword: null,
            pageNum: 1,
            pageSize: 5
          }
        },
        sortDialogVisible:false,
        sortDialogData:{sort:0,id:null}
      }
    },
    created() {
      this.getList();
    },
    filters:{
      formatRecommendStatus(status){
        if(status===1){
          return 'Recommended';
        }else{
          return 'Not recommended';
        }
      }
    },
    methods: {
      handleResetSearch() {
        this.listQuery = Object.assign({}, defaultListQuery);
      },
      handleSearchList() {
        this.listQuery.pageNum = 1;
        this.getList();
      },
      handleSelectionChange(val){
        this.multipleSelection = val;
      },
      handleSizeChange(val) {
        this.listQuery.pageNum = 1;
        this.listQuery.pageSize = val;
        this.getList();
      },
      handleCurrentChange(val) {
        this.listQuery.pageNum = val;
        this.getList();
      },
      handleRecommendStatusStatusChange(index,row){
        this.updateRecommendStatusStatus(row.id,row.recommendStatus);
      },
      handleDelete(index,row){
        this.deleteProduct(row.id);
      },
      handleBatchOperate(){
        if (this.multipleSelection < 1) {
          this.$message({
            message: 'Please select a record',
            type: 'warning',
            duration: 1000
          });
          return;
        }
        let ids = [];
        for (let i = 0; i < this.multipleSelection.length; i++) {
          ids.push(this.multipleSelection[i].id);
        }
        if (this.operateType === 0) {
          //设为推荐
          this.updateRecommendStatusStatus(ids,1);
        } else if (this.operateType === 1) {
          //取消推荐
          this.updateRecommendStatusStatus(ids,0);
        } else if(this.operateType===2){
          //删除
          this.deleteProduct(ids);
        }else {
          this.$message({
            message: 'Please select the type of batch operation',
            type: 'warning',
            duration: 1000
          });
        }
      },
      handleSelectProduct(){
        this.selectDialogVisible=true;
        this.getDialogList();
      },
      handleSelectSearch(){
        this.getDialogList();
      },
      handleDialogSizeChange(val) {
        this.dialogData.listQuery.pageNum = 1;
        this.dialogData.listQuery.pageSize = val;
        this.getDialogList();
      },
      handleDialogCurrentChange(val) {
        this.dialogData.listQuery.pageNum = val;
        this.getDialogList();
      },
      handleDialogSelectionChange(val){
        this.dialogData.multipleSelection = val;
      },
      handleSelectDialogConfirm(){
        if (this.dialogData.multipleSelection < 1) {
          this.$message({
            message: 'Please select a record',
            type: 'warning',
            duration: 1000
          });
          return;
        }
        let selectProducts = [];
        for (let i = 0; i < this.dialogData.multipleSelection.length; i++) {
          selectProducts.push({
            productId:this.dialogData.multipleSelection[i].id,
            productName:this.dialogData.multipleSelection[i].name
          });
        }
        this.$confirm('To add an operation using?', 'Tips', {
          confirmButtonText: 'Recognize',
          cancelButtonText: 'Cancel',
          type: 'warning'
        }).then(() => {
          createHotProduct(selectProducts).then(response=>{
            this.selectDialogVisible=false;
            this.dialogData.multipleSelection=[];
            this.getList();
            this.$message({
              type: 'success',
              message: 'Add successfully!'
            });
          });
        });
      },
      handleEditSort(index,row){
        this.sortDialogVisible=true;
        this.sortDialogData.sort=row.sort;
        this.sortDialogData.id=row.id;
      },
      handleUpdateSort(){
        this.$confirm('Whether to modify the sorting?', 'Tips', {
          confirmButtonText: 'Recognize',
          cancelButtonText: 'Cancel',
          type: 'warning'
        }).then(() => {
          updateHotProductSort(this.sortDialogData).then(response=>{
            this.sortDialogVisible=false;
            this.getList();
            this.$message({
              type: 'success',
              message: 'Deleted successfully!'
            });
          });
        })
      },
      getList() {
        this.listLoading = true;
        fetchList(this.listQuery).then(response => {
          this.listLoading = false;
          this.list = response.data.list;
          this.total = response.data.total;
        })
      },
      updateRecommendStatusStatus(ids,status){
        this.$confirm('Whether to change the recommendation status?', 'Tips', {
          confirmButtonText: 'Recognize',
          cancelButtonText: 'Cancel',
          type: 'warning'
        }).then(() => {
          let params=new URLSearchParams();
          params.append("ids",ids);
          params.append("recommendStatus",status);
          updateRecommendStatus(params).then(response=>{
            this.getList();
            this.$message({
              type: 'success',
              message: 'Modified successfully!'
            });
          });
        }).catch(() => {
          this.$message({
            type: 'success',
            message: 'Cancelled operations!'
          });
          this.getList();
        });
      },
      deleteProduct(ids){
        this.$confirm('Whether to delete the recommendation?', 'Tips', {
          confirmButtonText: 'Recognize',
          cancelButtonText: 'Cancel',
          type: 'warning'
        }).then(() => {
          let params=new URLSearchParams();
          params.append("ids",ids);
          deleteHotProduct(params).then(response=>{
            this.getList();
            this.$message({
              type: 'success',
              message: 'Deleted successfully!'
            });
          });
        })
      },
      getDialogList(){
        fetchProductList(this.dialogData.listQuery).then(response=>{
          this.dialogData.list=response.data.list;
          this.dialogData.total=response.data.total;
        })
      }
    }
  }
</script>
<style></style>
