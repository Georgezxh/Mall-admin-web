<template> 
  <div class="app-container">
    <div class="table-layout">
      <el-row>
        <el-col :span="4" class="table-cell-title">Name</el-col>
        <el-col :span="4" class="table-cell-title">Coupon Type</el-col>
        <el-col :span="4" class="table-cell-title">Available commodities</el-col>
        <el-col :span="4" class="table-cell-title">Utilization threshold</el-col>
        <el-col :span="4" class="table-cell-title">Nominal value</el-col>
        <el-col :span="4" class="table-cell-title">Statuses</el-col>
      </el-row>
      <el-row>
        <el-col :span="4" class="table-cell">{{coupon.name}}</el-col>
        <el-col :span="4" class="table-cell">{{coupon.type | formatType}}</el-col>
        <el-col :span="4" class="table-cell">{{coupon.useType | formatUseType}}</el-col>
        <el-col :span="4" class="table-cell">Available for ${{coupon.minPoint}}</el-col>
        <el-col :span="4" class="table-cell">${{coupon.amount}}</el-col>
        <el-col :span="4" class="table-cell">{{coupon.endTime | formatStatus}}</el-col>
      </el-row>
      <el-row>
        <el-col :span="4" class="table-cell-title">Validity period</el-col>
        <el-col :span="4" class="table-cell-title">Total circulation</el-col>
        <el-col :span="4" class="table-cell-title">Already collected</el-col>
        <el-col :span="4" class="table-cell-title">Awaiting collection</el-col>
        <el-col :span="4" class="table-cell-title">Utilized</el-col>
        <el-col :span="4" class="table-cell-title">Unutilized</el-col>
      </el-row>
      <el-row>
        <el-col :span="4" class="table-cell" style="font-size: 13px">
          {{coupon.startTime|formatDate}}至{{coupon.endTime|formatDate}}
        </el-col>
        <el-col :span="4" class="table-cell">{{coupon.publishCount}}</el-col>
        <el-col :span="4" class="table-cell">{{coupon.receiveCount}}</el-col>
        <el-col :span="4" class="table-cell">{{coupon.publishCount-coupon.receiveCount}}</el-col>
        <el-col :span="4" class="table-cell">{{coupon.useCount}}</el-col>
        <el-col :span="4" class="table-cell">{{coupon.publishCount-coupon.useCount}}</el-col>
      </el-row>
    </div>
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
          <el-form-item label="Usage state：">
            <el-select v-model="listQuery.useStatus" placeholder="All" clearable class="input-width">
              <el-option v-for="item in useTypeOptions"
                         :key="item.value"
                         :label="item.label"
                         :value="item.value">
              </el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="Order Number：">
            <el-input v-model="listQuery.orderSn" class="input-width" placeholder="Order Number"></el-input>
          </el-form-item>
        </el-form>
      </div>
    </el-card>
    <div class="table-container">
      <el-table ref="couponHistoryTable"
                :data="list"
                style="width: 100%;"
                v-loading="listLoading" border>
        <el-table-column label="Coupon code" width="160" align="center">
          <template slot-scope="scope">{{scope.row.couponCode}}</template>
        </el-table-column>
        <el-table-column label="Get your membership" width="140" align="center">
          <template slot-scope="scope">{{scope.row.memberNickname}}</template>
        </el-table-column>
        <el-table-column label="Collection Methods" width="100" align="center">
          <template slot-scope="scope">{{scope.row.getType | formatGetType}}</template>
        </el-table-column>
        <el-table-column label="Collection time" width="160" align="center">
          <template slot-scope="scope">{{scope.row.createTime | formatTime}}</template>
        </el-table-column>
        <el-table-column label="Current state" width="140" align="center">
          <template slot-scope="scope">{{scope.row.useStatus | formatCouponHistoryUseType}}</template>
        </el-table-column>
        <el-table-column label="Usage time" width="160" align="center">
          <template slot-scope="scope">{{scope.row.useTime | formatTime}}</template>
        </el-table-column>
        <el-table-column label="Order Number" align="center">
          <template slot-scope="scope">{{scope.row.orderSn===null?'N/A':scope.row.orderSn}}</template>
        </el-table-column>
      </el-table>
    </div>
    <div class="pagination-container">
      <el-pagination
        background
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        layout="total, sizes,prev, pager, next,jumper"
        :current-page.sync="listQuery.pageNum"
        :page-size="listQuery.pageSize"
        :page-sizes="[5,10,15]"
        :total="total">
      </el-pagination>
    </div>
  </div>
</template>
<script>
  import {formatDate} from '@/utils/date';
  import {getCoupon} from '@/api/coupon';
  import {fetchList as fetchCouponHistoryList} from '@/api/couponHistory';

  const defaultTypeOptions = [
    {
      label: 'Complimentary coupons for the entire site',
      value: 0
    },
    {
      label: 'Membership Coupons',
      value: 1
    },
    {
      label: 'Shopping Coupons',
      value: 2
    },
    {
      label: 'Registration Coupon',
      value: 3
    }
  ];
  const defaultListQuery = {
    pageNum: 1,
    pageSize: 10,
    useStatus: null,
    orderSn: null,
    couponId: null
  };
  const defaultUseTypeOptions= [
    {
      label: "Unused",
      value: 0
    },
    {
      label: "Utilized",
      value: 1
    },
    {
      label: "Expired",
      value: 2
    }
  ];
  export default {
    name: 'couponHistoryList',
    data() {
      return {
        coupon: {},
        listQuery: Object.assign({}, defaultListQuery),
        useTypeOptions:Object.assign({},defaultUseTypeOptions),
        list:null,
        total:null,
        listLoading:false
      }
    },
    created() {
      getCoupon(this.$route.query.id).then(response => {
        this.coupon = response.data;
      });
      this.listQuery.couponId=this.$route.query.id;
      this.getList();
    },
    filters: {
      formatType(type) {
        for (let i = 0; i < defaultTypeOptions.length; i++) {
          if (type === defaultTypeOptions[i].value) {
            return defaultTypeOptions[i].label;
          }
        }
        return '';
      },
      formatUseType(useType) {
        if (useType === 0) {
          return 'Common to all';
        } else if (useType === 1) {
          return 'Assigning classification';
        } else {
          return 'Designated product';
        }
      },
      formatPlatform(platform) {
        if (platform === 1) {
          return 'Mobile platform';
        } else if (platform === 2) {
          return 'PC platform';
        } else {
          return 'Full-platform';
        }
      },
      formatDate(time) {
        if (time == null || time === '') {
          return 'N/A';
        }
        let date = new Date(time);
        return formatDate(date, 'yyyy-MM-dd')
      },
      formatStatus(endTime) {
        let now = new Date().getTime();
        if (endTime > now) {
          return 'Unexpired'
        } else {
          return 'Expired';
        }
      },
      formatGetType(type) {
        if(type===1){
          return 'Proactive acquisition';
        }else{
          return 'Backstage Giveaway';
        }
      },
      formatCouponHistoryUseType(useType) {
        if (useType === 0) {
          return 'Unused';
        } else if (useType === 1) {
          return 'Utilized';
        } else {
          return 'Expired';
        }
      },
      formatTime(time) {
        if (time == null || time === '') {
          return 'N/A';
        }
        let date = new Date(time);
        return formatDate(date, 'yyyy-MM-dd hh:mm:ss')
      },
    },
    methods: {
      getList(){
        this.listLoading=true;
        fetchCouponHistoryList(this.listQuery).then(response=>{
          this.listLoading=false;
          this.list=response.data.list;
          this.total=response.data.total;
        });
      },
      handleResetSearch() {
        this.listQuery = Object.assign({}, defaultListQuery);
        this.listQuery.couponId=this.$route.query.id;
      },
      handleSearchList() {
        this.listQuery.pageNum = 1;
        this.getList();
      },
      handleSizeChange(val) {
        this.listQuery.pageNum = 1;
        this.listQuery.pageSize = val;
        this.getList();
      },
      handleCurrentChange(val) {
        this.listQuery.pageNum = val;
        this.getList();
      }
    }
  }
</script>
<style scoped>
  .app-container {
    width: 80%;
    margin: 20px auto;
  }

  .filter-container {
    margin-top: 20px;
  }

  .table-layout {
    margin-top: 20px;
    border-left: 1px solid #DCDFE6;
    border-top: 1px solid #DCDFE6;
  }

  .table-cell {
    height: 60px;
    line-height: 40px;
    border-right: 1px solid #DCDFE6;
    border-bottom: 1px solid #DCDFE6;
    padding: 10px;
    font-size: 14px;
    color: #606266;
    text-align: center;
    overflow: hidden;
  }

  .table-cell-title {
    border-right: 1px solid #DCDFE6;
    border-bottom: 1px solid #DCDFE6;
    padding: 10px;
    background: #F2F6FC;
    text-align: center;
    font-size: 14px;
    color: #303133;
  }
</style>


