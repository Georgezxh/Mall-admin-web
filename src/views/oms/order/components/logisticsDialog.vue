<template> 
  <el-dialog title="Order Tracking"
             :visible.sync="visible"
             :before-close="handleClose"
             width="40%">
    <el-steps direction="vertical"
              :active="6"
              finish-status="success"
              space="50px">
      <el-step  v-for="item in logisticsList"
                :key="item.name"
                :title="item.name"
                :description="item.time"></el-step>
    </el-steps>
  </el-dialog>
</template>
<script>
const defaultLogisticsList=[
  {name: 'Order submitted, awaiting payment',time:'2023-10-28 12:00:00 '},
  {name: 'Order Payment Successful',time:'2023-10-28 12:01:00 '},
  {name: 'Scanning of lower level locations in Beijing',time:'2023-10-28 20:00:00 '},
  {name: 'Unloading and scanning at the distribution center Shenzhen Guangdong',time:'2023-10-29 10:00:00 '},
  {name: 'Issuance scanning at the company in Shenzhen, Guangdong',time:'2023-10-29 18:00:00 '},
  {name: 'Arrive at the destination outlets Singapore companies, express mail will soon be delivered',time:'2023-10-30 11:02:00 '},
  {name: 'Order signed for and looking forward to serving you again!',time:'2023-10-30 17:20:00 '}
];
export default {
  name:'logisticsDialog',
  props: {
    value: Boolean
  },
  computed:{
    visible: {
      get() {
        return this.value;
      },
      set(visible){
        this.value=visible;
      }
    }
  },
  data() {
    return {
      logisticsList:Object.assign({},defaultLogisticsList)
    }
  },
  methods:{
    emitInput(val) {
      this.$emit('input', val)
    },
    handleClose(){
      this.emitInput(false);
    }
  }
}
</script>
<style></style>


