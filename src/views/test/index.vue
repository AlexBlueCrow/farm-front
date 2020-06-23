<template>
  <div>
    
    <el-date-picker
      v-model="value"
      type="daterange"
      :picker-options="pickerOptions"
      range-separator="至"
      start-placeholder="开始日期"
      end-placeholder="结束日期"
      align="right">
    </el-date-picker>
    <el-button-group>
      <el-button v-on:click='setdate("day")'>最近一天</el-button>
      <el-button v-on:click='setdate("week")'>最近一周</el-button>
    </el-button-group>
    <el-input v-model='farmname' placeholder="农场名称" clearable></el-input>
    <el-button v-on:click='inquire' >查询</el-button>
    
    
    <div v-if="show" >
        <el-table 
          :data="orders" 
          style="width: 100%"
          height="500"
          border='true' stripe=true>
            <el-table-column prop="effect_time" label="日期" >
            </el-table-column>
            <el-table-column prop="name_rec" label="收件姓名">
            </el-table-column>
            <el-table-column prop="deliver_address" label="收货地址">
            </el-table-column>
            <el-table-column prop="phone_num" label="手机号码">
            </el-table-column>
            <el-table-column prop="price_paid" label="支付金额">
            </el-table-column>
            <el-table-column prop="item" label="商品名称">
            </el-table-column>
            <el-table-column prop="price_paid" label="支付金额">
            </el-table-column>
            <el-table-column prop="deliver_time" label="配送时间">
            </el-table-column>
            <el-table-column prop="farm_name" label="所属农场">
            </el-table-column>
        </el-table>
    </div>
  </div>

  
</template>

<script>

import axios from "axios";

var aData = new Date();
export default {
  
  data(){
    return {
      date1:aData,
      date2:aData,
      farmname:'',
      show:false,
      orders:[],
      value:''
    }
  },
  methods:{
    
    inquire:function(){
        
        axios.get('http://localhost:8000/api/test/',{
            params:{
            date1:this.date1,
            date2:this.date2,
            }
        }).then((response) => { 
          this.orders = response.data
          this.show=true
        })
      },
    setdate:function(key){
      switch(key){
        case 'day':
          
          break
        case 'week':
          alert('week')
          break
      }
    }
  }
}
</script>