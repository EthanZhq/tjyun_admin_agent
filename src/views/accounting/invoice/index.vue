<template>
  <div>
    <div style="padding:0 30px">
      <div>
        <div style="margin-top: 15px;display:flex;">
          <el-input
            v-model="input"
            style="width:215px;marging-right:20px;"
            placeholder="请输入项目名称"
            clearable
          />
          <div style="margin-left: 20px;">
            <el-select
              v-model="value"
              clearable
              placeholder="请选择回款状态"
            >
              <el-option
                v-for="item in options"
                :key="item.value"
                :label="item.label"
                :value="item.value"
              />
            </el-select>
          </div>
          <div style="margin-left: 20px;">
            <el-select
              v-model="value"
              clearable
              placeholder="请选择开票状态"
            >
              <el-option
                v-for="item in options"
                :key="item.value"
                :label="item.label"
                :value="item.value"
              />
            </el-select>
          </div>
          <div style="margin-left: 300px;">
            <el-button type="primary">搜索</el-button>
          </div>

        </div>
      </div>

      <div class="head">
        <el-button
          type="primary"
          plain
          @click="open(0)"
        >开 票</el-button>
        <el-button
          type="primary"
          plain
          @click="open(1)"
        >确认回款</el-button>
        <el-button
          plain
          style="background:#F3F3F3;color:#1c1c1c;"
          @click="open(2)"
        >开票历史</el-button>
        <el-button
          plain
          style="background:#F3F3F3;color:#1c1c1c;"
          @click="open(3)"
        >回款历史</el-button>
        <el-button
          plain
          style="background:#F3F3F3;color:#1c1c1c;"
          @click="open(4)"
        >查 看</el-button>
        <el-button
          plain
          style="background:#F3F3F3;color:#1c1c1c;"
          @click="open(5)"
        >导 出</el-button>
        <el-button
          plain
          style="background:#F3F3F3;color:#1c1c1c;"
          @click="open(6)"
        >操作记录</el-button>
      </div>
      <!-- 表格 -->
      <div>
        <el-table
          ref="multipleTable"
          :data="tableData"
          border
          tooltip-effect="dark"
          style="width:95%"
          height="450"
          @selection-change="handleSelectionChange"
        >
          <el-table-column
            type="selection"
            width="55"
          />
          <el-table-column
            prop="id"
            label="编号"
            width="180"
          >U2019100001</el-table-column>
          <el-table-column
            prop="name"
            label="项目名称"
            width="150"
          >万科新都荟
          </el-table-column>
          <el-table-column
            prop="address"
            label="套数"
            width="150"
          >1</el-table-column>
          <el-table-column
            prop="commissioned"
            label="应结佣金"
            width="120"
          >50000</el-table-column>

          <el-table-column
            prop="commission"
            sortable
            label="实结佣金"
            width="120"
          >30000</el-table-column>
          <el-table-column
            prop="lossCommission"
            label="损失佣金"
            width="120"
          >20000</el-table-column>
          <el-table-column
            prop="organization"
            label="累积开票金额"
            width="120"
          > <span style="color:#108EE9">未结算</span> </el-table-column>
          <el-table-column
            prop="whether"
            label="开票状态"
            width="120"
          >未开票</el-table-column>

          <el-table-column
            prop="date"
            label="累积回款金额"
            width="120"
          ><span style="color:#108EE9">10000</span></el-table-column>
          <el-table-column
            prop="state"
            label="回款状态"
            width="120"
          >分批回</el-table-column>
          <el-table-column
            prop="state"
            label="最近开票日期"
            width="160"
          >2019-11-15 08:00:00</el-table-column>

          <el-table-column
            prop="state"
            label="生成日期"
            width="160"
          >2019-11-15 08:00:00
          </el-table-column>
        </el-table>
      </div>
      <div class="paging">
        <div class="paging-right">
          <el-pagination
            :current-page="currentPage4"
            :page-size="100"
            :total="400"
            :pager-count="5"
            :page-sizes="[5,100, 200, 300, 400]"
            layout="total, sizes, prev, pager, next, jumper"
            @size-change="handleSizeChange"
            @current-change="handleCurrentChange"
          />
        </div>
      </div>
    </div>

    <makeOut
      :make-out="makeOut"
      @cancel="cancels(0)"
    />
    <requireP
      :require-p="requireP"
      @cancel="cancels(1)"
    />
  </div>
</template>

<script>
import MakeOut from './makeOut'
import RequireP from './requireP'
export default {
  components: {
    MakeOut, RequireP
  },
  data() {
    return {
      makeOut: false,
      requireP: false,
      follow: false,
      returnCommission: false,
      options: [{
        value: '选项1',
        label: '黄金糕'
      },
      {
        value: '选项2',
        label: '双皮奶'
      },
      {
        value: '选项3',
        label: '蚵仔煎'
      },
      {
        value: '选项4',
        label: '龙须面'
      },
      {
        value: '选项5',
        label: '北京烤鸭'
      }
      ],
      value: '',
      input: '',
      // input1: '',
      // input2: '',
      // input3: '',
      // select: '',
      value1: true,
      currentPage4: 10,
      tableData: [{}, {}, {}, {}, {}, {}, {}, {}, {}],
      requireTable: [{}, {}, {}, {}, {}, {}, {}, {}, {}]
    }
  },
  created() {
    // this.theme = this.list[0]
  },
  methods: {
    // 打开生成页面
    open(state) {
      if (state === 0) {
        console.log(this.makeOut)
        this.makeOut = true
        console.log(this.makeOut)
      }
      if (state === 1) {
        console.log(this.requireP)
        this.requireP = true
        console.log(this.requireP)
      }
      if (state === 2) {
        console.log(this.follow)
        this.follow = true
        console.log(this.follow)
      }
      if (state === 3) {
        console.log(this.returnCommission)
        this.returnCommission = true
        console.log(this.returnCommission)
      }
    },
    cancels(state) {
      if (state === 0) {
        this.makeOut = false
        console.log(this.makeOut)
      }
      if (state === 1) {
        this.requireP = false
        console.log(this.requireP)
      }
      if (state === 2) {
        this.follow = false
        console.log(this.follow)
      }
      if (state === 3) {
        this.returnCommission = false
        console.log(this.returnCommission)
      }
    },
    // 关闭弹框
    toggleSelection(rows) {
      if (rows) {
        rows.forEach(row => {
          this.$refs.multipleTable.toggleRowSelection(row)
        })
      } else {
        this.$refs.multipleTable.clearSelection()
      }
    },
    handleSelectionChange(val) {
      this.multipleSelection = val
    },
    handleSizeChange(val) {
      console.log(`每页 ${val} 条`)
    },
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`)
    }
  }
}
</script>
<style
  scoped
  lang="scss"
    >
.el-select .el-input {
  width: 130px;
}
.input-with-select .el-input-group__prepend {
  background-color: #fff;
}
.head {
  margin-right: 30px;
  height: 100px;
  align-items: center;
  display: flex;
  font-display: row;
  button {
    background: #4171f9;
    color: #ffffff;
  }
}
.paging {
  height: 100px;
  display: flex;
  margin-right: 120px;
  justify-content: flex-end;
  align-items: center;
  .paging-right {
    display: flex;
    justify-content: center;
    align-items: center;
  }
}
.container {
  position: relative;
  display: flex;
  padding: 15px 30px;
  color: #333;
  font-size: 15px;
}
</style>
