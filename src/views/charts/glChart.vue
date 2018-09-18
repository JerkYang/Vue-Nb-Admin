<template>
  <div class='chart-container'>
    <el-row :gutter="20" style="margin-top:50px;">
      <el-col :span="7">
        <el-card class="box-card">
          <div slot="header" class="clearfix">
            <div>
              <span><font style="color: #ffffff" size="6px">锅炉报警</font></span>
            </div>
          </div>
          <div class="component-item" style="height:420px">
            <chart height='100%' width='100%' class="charts"></chart>
          </div>
        </el-card>
      </el-col>
      <el-col :span="10">
        <el-card class="box-card">
          <div slot="header" class="clearfix">
            <span><font style="color: #ffffff" size="6px">锅炉能源使用</font></span>
          </div>
          <el-row>
            <!--第一列-->
            <el-col :span="12">
              <!--第一行-->
              <el-row>
                <div class="component-item" style="height:210px">
                  <gl-ydl height='100%' width='100%' class="charts" id="glydl"></gl-ydl>
                </div>
              </el-row>
              <!-- 第二行-->
              <el-row>
                <div class="component-item" style="height:210px">
                  <gl-ysl height='100%' width='100%' class="charts" id="glysl"></gl-ysl>
                </div>
              </el-row>
            </el-col>
            <!--第二列-->
            <el-col :span="12">
              <!--第一行-->
              <el-row>
                <div class="component-item" style="height:210px">
                  <gl-ytrq height='100%' width='100%' class="charts" id="glytrq"></gl-ytrq>
                </div>
              </el-row>
              <!--第二行-->
              <el-row>
                <div class="component-item" style="height:210px">
                  <gl-yzq height='100%' width='100%' class="charts" id="glyzq"></gl-yzq>
                </div>
              </el-row>
            </el-col>
          </el-row>
        </el-card>
      </el-col>
      <el-col :span="7">
        <el-card class="box-card">
          <div slot="header" class="clearfix">
            <span><font style="color: #ffffff" size="6px">锅炉体检</font></span>
          </div>
          <div class="component-item" style="height:420px">
            <div>
              <div class="table" id="table1">
              <span>
                <font style="color: #00f2fc" size="6px">锅炉运行总时长
                  <span style="margin-left: 100px;">{{date|formatDate}}</span>
                </font>
              </span>
              </div>
              <div class="table" id="table2">
              <span><font style="color: #00fd7f" size="6px">正常运行总时长
              <span style="margin-left: 100px;">{{date.getTime()-6 * 60 * 60 * 1000|formatDate}}</span>
              </font></span>
              </div>
              <div class="table" id="table3">
              <span><font style="color: #fd4501" size="6px">异常运行总时长
              <span style="margin-left: 100px;">{{date.getTime()-10 * 60 * 60 * 1000|formatDate}}</span>
              </font></span>
              </div>
            </div>
            <div>
              <div class="table">
              <span>
                <font style="color: #00f2fc" size="6px">锅炉运行总时长
                  <span style="margin-left: 100px;">
                    <el-input size="small" v-model="input" placeholder="请输入内容"><el-button type="primary"
                                                                                          icon="el-icon-search">搜索</el-button></el-input>
                  </span>
                </font>
              </span>
              </div>
              <div class="table">
              <span><font style="color: #00fd7f" size="6px">正常运行总时长
              <span style="margin-left: 100px;">{{date.getTime()-6 * 60 * 60 * 1000|formatDate}}</span>
              </font></span>
              </div>
              <div class="table">
              <span><font style="color: #fd4501" size="6px">异常运行总时长
              <span style="margin-left: 100px;">{{date.getTime()-10 * 60 * 60 * 1000|formatDate}}</span>
              </font></span>
              </div>
            </div>
            <!--<el-table :data="tableData" style="width: 100%">
              <el-table-column prop="totaltime" label="锅炉运行总时长" >
                <el-table-column prop="normal" label="正常运行时长" width="180"></el-table-column>
                <el-table-column prop="abnormal" label="异常运行时长" width="180"></el-table-column>
              </el-table-column>
            </el-table>-->
          </div>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
  import Chart from '@/components/Charts/glChart'
  import glYdl from '@/components/Charts/glYdl'
  import glYsl from '@/components/Charts/glYsl'
  import glYtrq from '@/components/Charts/glYtrq'
  import glYzq from '@/components/Charts/glYzq'
  import { formatDate } from '@/utils/date.js'

  export default {
    name: 'glChart',
    components: { Chart, glYdl, glYsl, glYtrq, glYzq },
    data() {
      return {
        date: new Date()
      }
    },
    filters: {
      formatDate(time) {
        var date = new Date(time)
        return formatDate(date, 'hh:mm:ss')
      }
    },
    mounted() {
      var _this = this // 声明一个变量指向vue实例this,保证作用域一致
      this.timer = setInterval(function() {
        _this.date = new Date()// 修改数据date
      }, 1000)
    },
    beforeDestroy() {
      if (this.timer) {
        clearInterval(this.timer)// 在vue实例销毁钱，清除我们的定时器
      }
    }
  }
</script>

<style scoped>
  .chart-container {
    position: relative;
    padding: 20px;
    width: 100%;
    height: 85vh;
    background: #222834;
  }

  .component-item {
    min-height: 100px;
    background: #2d363f;
  }

  .box-card {
    background: #2d363f;
    border: none
  }

  .charts el-card__body {
    padding: 0px;
  }

  #glydl, #glysl {
    left: -20px;
  }

  #table2, #table3 {
    border-top: 0px;
  }

  .table {
    height: 15%;
    line-height: 63px;
    text-align: center;
    border: 2px solid #ffffff
  }
</style>

