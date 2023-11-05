<template>
  <div class="app-container">
<!--    <div class="address-layout">-->
<!--      <el-row :gutter="20">-->
<!--        <el-col :span="6">-->
<!--          <div class="out-border">-->
<!--            <div class="layout-title">&lt;!&ndash; 学习教程 &ndash;&gt;Study Tutorials</div>-->
<!--            <div class="color-main address-content">-->
<!--              <a href="https://www.macrozheng.com" target="_blank">&lt;!&ndash; mall学习教程 &ndash;&gt;Mall Study Tutorials</a>-->
<!--            </div>-->
<!--          </div>-->
<!--        </el-col>-->
<!--        <el-col :span="6">-->
<!--          <div class="out-border">-->
<!--            <div class="layout-title">&lt;!&ndash;视频教程&ndash;&gt;Video Tutorials</div>-->
<!--            <div class="color-main address-content">-->
<!--              <a href="https://www.macrozheng.com/mall/catalog/mall_video.html" target="_blank">Video Tutorials</a>-->
<!--            </div>-->
<!--          </div>-->
<!--        </el-col>-->
<!--        <el-col :span="6">-->
<!--          <div class="out-border">-->
<!--            &lt;!&ndash;            <div class="layout-title">点Star支持项目</div>&ndash;&gt;-->
<!--            <div class="color-main address-content">-->
<!--              <a href="https://github.com/macrozheng/mall" target="_blank">&lt;!&ndash;mall项目&ndash;&gt;Project for Group VI-->
<!--              </a>-->
<!--            </div>-->
<!--          </div>-->
<!--        </el-col>-->
<!--      </el-row>-->
<!--    </div>-->
    <div class="total-layout">
      <el-row :gutter="20">
        <el-col :span="6">
          <div class="total-frame">
            <img :src="img_home_order" class="total-icon">
            <div class="total-title"><!--今日订单总数-->Today's order total</div>
            <div class="total-value">200</div>
          </div>
        </el-col>
        <el-col :span="6">
          <div class="total-frame">
            <img :src="img_home_today_amount" class="total-icon">
            <div class="total-title"><!--今日销售总额-->Today's Total Sales</div>
            <div class="total-value">SG5000.00</div>
          </div>
        </el-col>
        <el-col :span="6">
          <div class="total-frame">
            <img :src="img_home_yesterday_amount" class="total-icon">
            <div class="total-title"><!--昨日销售总额-->Yesterday's sales total</div>
            <div class="total-value">SG5000.00</div>
          </div>
        </el-col>
        <!--<el-col :span="6">-->
        <!--<div class="total-frame">-->
        <!--<svg-icon icon-class="total-week" class="total-icon">-->
        <!--</svg-icon>-->
        <!--<div class="total-title">近7天销售总额</div>-->
        <!--<div class="total-value">￥50000.00</div>-->
        <!--</div>-->
        <!--</el-col>-->
      </el-row>
    </div>
<!--    <el-card class="mine-layout">-->
<!--      <div style="text-align: center">-->
<!--        <img width="150px" height="150px" src="http://macro-oss.oss-cn-shenzhen.aliyuncs.com/mall/banner/qrcode_for_macrozheng_258.jpg">-->
<!--      </div>-->
<!--            <div style="text-align: center">mall全套学习教程连载中！</div>-->
<!--            <div style="text-align: center;margin-top: 5px"><span class="color-main">关注公号</span>，第一时间获取。</div>-->
<!--    </el-card>-->
    <div class="un-handle-layout">
      <div class="layout-title"><!--待处理事务-->Pending matters</div>
      <div class="un-handle-content">
        <el-row :gutter="20">
          <el-col :span="8">
            <div class="un-handle-item">
              <span class="font-medium"><!--待付款订单-->Pending orders</span>
              <span style="float: right" class="color-danger">(10)</span>
            </div>
          </el-col>
          <el-col :span="8">
            <div class="un-handle-item">
              <span class="font-medium"><!--已完成订单-->Completed Orders</span>
              <span style="float: right" class="color-danger">(10)</span>
            </div>
          </el-col>
          <el-col :span="8">
            <div class="un-handle-item">
              <span class="font-medium"><!--待确认收货订单-->Pending Receipt Confirmation Orders</span>
              <span style="float: right" class="color-danger">(10)</span>
            </div>
          </el-col>
        </el-row>
        <el-row :gutter="20">
          <el-col :span="8">
            <div class="un-handle-item">
              <span class="font-medium"><!--待发货订单-->Orders to be shipped</span>
              <span style="float: right" class="color-danger">(10)</span>
            </div>
          </el-col>
          <el-col :span="8">
            <div class="un-handle-item">
              <span class="font-medium"><!--新缺货登记-->Registration of new stock-outs</span>
              <span style="float: right" class="color-danger">(10)</span>
            </div>
          </el-col>
          <el-col :span="8">
            <div class="un-handle-item">
              <span class="font-medium"><!--待处理退款申请-->Pending Refund Requests</span>
              <span style="float: right" class="color-danger">(10)</span>
            </div>
          </el-col>
        </el-row>
        <el-row :gutter="20">
          <el-col :span="8">
            <div class="un-handle-item">
              <span class="font-medium"><!--已发货订单-->Shipped Orders</span>
              <span style="float: right" class="color-danger">(10)</span>
            </div>
          </el-col>
          <el-col :span="8">
            <div class="un-handle-item">
              <span class="font-medium"><!--待处理退货订单-->Pending Return Orders</span>
              <span style="float: right" class="color-danger">(10)</span>
            </div>
          </el-col>
<!--          <el-col :span="8">-->
<!--            <div class="un-handle-item">-->
<!--              <span class="font-medium">&lt;!&ndash;广告位即将到期&ndash;&gt;Ad space will expire soon</span>-->
<!--              <span style="float: right" class="color-danger">(10)</span>-->
<!--            </div>-->
<!--          </el-col>-->
        </el-row>
      </div>
    </div>
    <div class="overview-layout">
      <el-row :gutter="20">
        <el-col :span="12">
          <div class="out-border">
            <div class="layout-title"><!--商品总览-->Product Overview</div>
            <div style="padding: 40px">
              <el-row>
                <el-col :span="6" class="color-danger overview-item-value">100</el-col>
                <el-col :span="6" class="color-danger overview-item-value">400</el-col>
                <el-col :span="6" class="color-danger overview-item-value">50</el-col>
                <el-col :span="6" class="color-danger overview-item-value">500</el-col>
              </el-row>
              <el-row class="font-medium">
                <el-col :span="6" class="overview-item-title"><!--已下架-->Off the Shelves</el-col>
                <el-col :span="6" class="overview-item-title"><!--已上架-->Already on the Shelves</el-col>
                <el-col :span="6" class="overview-item-title"><!--库存紧张-->Stocks are tight.</el-col>
                <el-col :span="6" class="overview-item-title"><!--全部商品-->All Products</el-col>
              </el-row>
            </div>
          </div>
        </el-col>
        <el-col :span="12">
          <div class="out-border">
            <div class="layout-title"><!--用户总览-->User Overview</div>
            <div style="padding: 40px">
              <el-row>
                <el-col :span="6" class="color-danger overview-item-value">100</el-col>
                <el-col :span="6" class="color-danger overview-item-value">200</el-col>
                <el-col :span="6" class="color-danger overview-item-value">1000</el-col>
                <el-col :span="6" class="color-danger overview-item-value">5000</el-col>
              </el-row>
              <el-row class="font-medium">
                <el-col :span="6" class="overview-item-title"><!--今日新增-->Today's additions</el-col>
                <el-col :span="6" class="overview-item-title"><!--昨日新增-->Yesterday's additions</el-col>
                <el-col :span="6" class="overview-item-title"><!--本月新增-->New this month</el-col>
                <el-col :span="6" class="overview-item-title"><!--会员总数-->Total members</el-col>
              </el-row>
            </div>
          </div>
        </el-col>
      </el-row>
    </div>
    <div class="statistics-layout">
      <div class="layout-title"><!--订单统计-->Order Statistics</div>
      <el-row>
        <el-col :span="4">
          <div style="padding: 20px">
            <div>
              <div style="color: #909399;font-size: 14px"><!--本月订单总数-->Total orders for the month</div>
              <div style="color: #606266;font-size: 24px;padding: 10px 0">10000</div>
              <div>
                <span class="color-success" style="font-size: 14px">+10%</span>
                <span style="color: #C0C4CC;font-size: 14px"><!--同比上月-->Compared with Previous Month</span>
              </div>
            </div>
            <div style="margin-top: 20px;">
              <div style="color: #909399;font-size: 14px"><!--本周订单总数-->Total orders for the week</div>
              <div style="color: #606266;font-size: 24px;padding: 10px 0">1000</div>
              <div>
                <span class="color-danger" style="font-size: 14px">-10%</span>
                <span style="color: #C0C4CC;font-size: 14px"><!--同比上周-->Compared to Last Week</span>
              </div>
            </div>
            <div style="margin-top: 20px;">
              <div style="color: #909399;font-size: 14px"><!--本月销售总额-->Total sales for the month</div>
              <div style="color: #606266;font-size: 24px;padding: 10px 0">100000</div>
              <div>
                <span class="color-success" style="font-size: 14px">+10%</span>
                <span style="color: #C0C4CC;font-size: 14px"><!--同比上月-->Compared with Previous Mont</span>
              </div>
            </div>
            <div style="margin-top: 20px;">
              <div style="color: #909399;font-size: 14px"><!--本周销售总额-->Total sales for the week</div>
              <div style="color: #606266;font-size: 24px;padding: 10px 0">50000</div>
              <div>
                <span class="color-danger" style="font-size: 14px">-10%</span>
                <span style="color: #C0C4CC;font-size: 14px"><!--同比上周-->Compared to Last Week</span>
              </div>
            </div>
          </div>
        </el-col>
        <el-col :span="20">
          <div style="padding: 10px;border-left:1px solid #DCDFE6">
            <el-date-picker
              style="float: right;z-index: 1"
              size="small"
              v-model="orderCountDate"
              type="daterange"
              align="right"
              unlink-panels
              range-separator="until"
              start-placeholder="Start date"
              end-placeholder="End date"
              @change="handleDateChange"
              :picker-options="pickerOptions">
            </el-date-picker>
            <div>
              <ve-line
                :data="chartData"
                :legend-visible="false"
                :loading="loading"
                :data-empty="dataEmpty"
                :settings="chartSettings"></ve-line>
            </div>
          </div>
        </el-col>
      </el-row>
    </div>
  </div>
</template>

<script>
import {str2Date} from '@/utils/date';
import img_home_order from '@/assets/images/home_order.png';
import img_home_today_amount from '@/assets/images/home_today_amount.png';
import img_home_yesterday_amount from '@/assets/images/home_yesterday_amount.png';
const DATA_FROM_BACKEND = {
  columns: ['date', 'orderCount','orderAmount'],
  rows: [
    {date: '2023-10-01', orderCount: 10, orderAmount: 1093},
    {date: '2023-10-02', orderCount: 20, orderAmount: 2230},
    {date: '2023-10-03', orderCount: 33, orderAmount: 3623},
    {date: '2023-10-04', orderCount: 50, orderAmount: 6423},
    {date: '2023-10-05', orderCount: 80, orderAmount: 8492},
    {date: '2023-10-06', orderCount: 60, orderAmount: 6293},
    {date: '2023-10-07', orderCount: 20, orderAmount: 2293},
    {date: '2023-10-08', orderCount: 60, orderAmount: 6293},
    {date: '2023-10-09', orderCount: 50, orderAmount: 5293},
    {date: '2023-10-10', orderCount: 30, orderAmount: 3293},
    {date: '2023-10-11', orderCount: 20, orderAmount: 2293},
    {date: '2023-10-12', orderCount: 80, orderAmount: 8293},
    {date: '2023-10-13', orderCount: 100, orderAmount: 10293},
    {date: '2023-10-14', orderCount: 10, orderAmount: 1293},
    {date: '2023-10-15', orderCount: 40, orderAmount: 4293}
  ]
};
export default {
  name: 'home',
  data() {
    return {
      pickerOptions: {
        shortcuts: [{
          //text: '最近一周',
          text: 'Last week',
          onClick(picker) {
            const end = new Date();
            let start = new Date();
            start.setFullYear(2018);
            start.setMonth(10);
            start.setDate(1);
            end.setTime(start.getTime() + 3600 * 1000 * 24 * 7);
            picker.$emit('pick', [start, end]);
          }
        }, {
          //text: '最近一月',
          text: 'Last month',
          onClick(picker) {
            const end = new Date();
            let start = new Date();
            start.setFullYear(2018);
            start.setMonth(10);
            start.setDate(1);
            end.setTime(start.getTime() + 3600 * 1000 * 24 * 30);
            picker.$emit('pick', [start, end]);
          }
        }]
      },
      orderCountDate: '',
      chartSettings: {
        xAxisType: 'time',
        area:true,
        axisSite: { right: ['orderAmount']},
        labelMap: {'orderCount': 'Number of orders', 'orderAmount': 'Order Amount'}},
      chartData: {
        columns: [],
        rows: []
      },
      loading: false,
      dataEmpty: false,
      img_home_order,
      img_home_today_amount,
      img_home_yesterday_amount
    }
  },
  created(){
    this.initOrderCountDate();
    this.getData();
  },
  methods:{
    handleDateChange(){
      this.getData();
    },
    initOrderCountDate(){
      let start = new Date();
      start.setFullYear(2018);
      start.setMonth(10);
      start.setDate(1);
      const end = new Date();
      end.setTime(start.getTime() + 1000 * 60 * 60 * 24 * 7);
      this.orderCountDate=[start,end];
    },
    getData(){
      setTimeout(() => {
        this.chartData = {
          columns: ['date', 'orderCount','orderAmount'],
          rows: []
        };
        for(let i=0;i<DATA_FROM_BACKEND.rows.length;i++){
          let item=DATA_FROM_BACKEND.rows[i];
          let currDate=str2Date(item.date);
          let start=this.orderCountDate[0];
          let end=this.orderCountDate[1];
          if(currDate.getTime()>=start.getTime()&&currDate.getTime()<=end.getTime()){
            this.chartData.rows.push(item);
          }
        }
        this.dataEmpty = false;
        this.loading = false
      }, 1000)
    }
  }
}
</script>

<style scoped>
.app-container {
  margin-top: 40px;
  margin-left: 120px;
  margin-right: 120px;
}

.address-layout {
}

.total-layout {
  margin-top: 20px;
}

.total-frame {
  border: 1px solid #DCDFE6;
  padding: 20px;
  height: 100px;
}

.total-icon {
  color: #409EFF;
  width: 60px;
  height: 60px;
}

.total-title {
  position: relative;
  font-size: 16px;
  color: #909399;
  left: 70px;
  top: -50px;
}

.total-value {
  position: relative;
  font-size: 18px;
  color: #606266;
  left: 70px;
  top: -40px;
}

.un-handle-layout {
  margin-top: 20px;
  border: 1px solid #DCDFE6;
}

.layout-title {
  color: #606266;
  padding: 15px 20px;
  background: #F2F6FC;
  font-weight: bold;
}

.un-handle-content {
  padding: 20px 40px;
}

.un-handle-item {
  border-bottom: 1px solid #EBEEF5;
  padding: 10px;
}

.overview-layout {
  margin-top: 20px;
}

.overview-item-value {
  font-size: 24px;
  text-align: center;
}

.overview-item-title {
  margin-top: 10px;
  text-align: center;
}

.out-border {
  border: 1px solid #DCDFE6;
}

.statistics-layout {
  margin-top: 20px;
  border: 1px solid #DCDFE6;
}
.mine-layout {
  position: absolute;
  right: 140px;
  top: 107px;
  width: 250px;
  height: 235px;
}
.address-content{
  padding: 20px;
  font-size: 18px
}
</style>
