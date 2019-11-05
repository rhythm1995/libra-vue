<template>
  <div>
    <el-row>
      <el-col>
        <el-row
          :gutter="20"
          class="mgb20"
        >
          <el-col :span="8">
            <el-card
              shadow="hover"
              :body-style="{padding: '0px'}"
            >
              <div class="grid-content grid-con-1">
                <i class="el-icon-lx-people grid-con-icon"></i>
                <div class="grid-cont-right">
                  <div class="grid-num">1234</div>
                  <div>用户访问量</div>
                </div>
              </div>
            </el-card>
          </el-col>
          <el-col :span="8">
            <el-card
              shadow="hover"
              :body-style="{padding: '0px'}"
            >
              <div class="grid-content grid-con-2">
                <i class="el-icon-lx-notice grid-con-icon"></i>
                <div class="grid-cont-right">
                  <div class="grid-num">321</div>
                  <div>系统消息</div>
                </div>
              </div>
            </el-card>
          </el-col>
          <el-col :span="8">
            <el-card
              shadow="hover"
              :body-style="{padding: '0px'}"
            >
              <div class="grid-content grid-con-3">
                <i class="el-icon-lx-goods grid-con-icon"></i>
                <div class="grid-cont-right">
                  <div class="grid-num">5000</div>
                  <div>数量</div>
                </div>
              </div>
            </el-card>
          </el-col>
        </el-row>
        <el-card shadow="hover">
          <div
            slot="header"
            class="clearfix"
          >
            <span>待办事项</span>
            <el-button
              style="float: right; padding: 3px 0"
              type="text"
            >添加</el-button>
          </div>
          <template>
            <el-table
              :data="tableData"
              style="width: 100%"
            >
              <el-table-column
                prop="id"
                label="ID"
              >
              </el-table-column>
              <el-table-column
                prop="name"
                label="姓名"
              >
              </el-table-column>
              <el-table-column
                prop="age"
                label="年龄"
              >
              </el-table-column>
              <el-table-column
                prop="createdAt"
                label="创建日期"
              >
              </el-table-column>
              <el-table-column
                prop="updatedAt"
                label="更新日期"
              >
              </el-table-column>
            </el-table>
          </template>
        </el-card>
      </el-col>
    </el-row>s
  </div>
</template>

<script>
import bus from '../common/bus';
export default {
  name: 'dashboard',
  data() {
    return {
      name: localStorage.getItem('ms_username'),
      tableData: []
    }
  },
  computed: {
    role() {
      return this.name === 'admin' ? '超级管理员' : '普通用户';
    }
  },
  methods: {
    async getUserList() {
      const data = await this.$api.user.find();
      return data;
    }
  },
  async created() {
    const data = await this.getUserList();
    this.$nextTick(() => {
      this.tableData = data.rows.map((item) => {
        return {
          id: String(item.id),
          name: item.name,
          age: String(item.age),
          createdAt: item.updatedAt,
          updatedAt: item.updatedAt
        }
      });
    });
  },
}

</script>

<style lang="less" scoped>
.el-row {
  margin-bottom: 20px;
}

.grid-content {
  display: flex;
  align-items: center;
  height: 100px;
}

.grid-cont-right {
  flex: 1;
  text-align: center;
  font-size: 14px;
  color: #999;
}

.grid-num {
  font-size: 30px;
  font-weight: bold;
}

.grid-con-icon {
  font-size: 50px;
  width: 100px;
  height: 100px;
  text-align: center;
  line-height: 100px;
  color: #fff;
}

.grid-con-1 .grid-con-icon {
  background: rgb(45, 140, 240);
}

.grid-con-1 .grid-num {
  color: rgb(45, 140, 240);
}

.grid-con-2 .grid-con-icon {
  background: rgb(100, 213, 114);
}

.grid-con-2 .grid-num {
  color: rgb(45, 140, 240);
}

.grid-con-3 .grid-con-icon {
  background: rgb(242, 94, 67);
}

.grid-con-3 .grid-num {
  color: rgb(242, 94, 67);
}

.user-info {
  display: flex;
  align-items: center;
  padding-bottom: 20px;
  border-bottom: 2px solid #ccc;
  margin-bottom: 20px;
}

.user-avator {
  width: 120px;
  height: 120px;
  border-radius: 50%;
}

.user-info-cont {
  padding-left: 50px;
  flex: 1;
  font-size: 14px;
  color: #999;
}

.user-info-cont div:first-child {
  font-size: 30px;
  color: #222;
}

.user-info-list {
  font-size: 14px;
  color: #999;
  line-height: 25px;
}

.user-info-list span {
  margin-left: 70px;
}

.mgb20 {
  margin-bottom: 20px;
}

.todo-item {
  font-size: 14px;
}

.todo-item-del {
  text-decoration: line-through;
  color: #999;
}

.schart {
  width: 100%;
  height: 300px;
}
</style>
