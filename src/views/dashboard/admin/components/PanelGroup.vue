<template>
  <el-row :gutter="40" class="panel-group">
    <el-col :xs="12" :sm="12" :lg="6" class="card-panel-col">
      <div class="card-panel" @click="handleSetLineChartData('newVisitis')">
        <div class="card-panel-icon-wrapper icon-people">
          <svg-icon icon-class="peoples" class-name="card-panel-icon" />
        </div>
        <div class="card-panel-description">
          <div class="card-panel-text">
            {{ $t('dashboard.productCount') }}
          </div>
          <count-to :start-val="0" :end-val="counts.productCount" :duration="2600" class="card-panel-num" />
        </div>
      </div>
    </el-col>
    <el-col :xs="12" :sm="12" :lg="6" class="card-panel-col">
      <div class="card-panel" @click="handleSetLineChartData('messages')">
        <div class="card-panel-icon-wrapper icon-money">
          <svg-icon icon-class="command" class-name="card-panel-icon" />
        </div>
        <div class="card-panel-description">
          <div class="card-panel-text">
            {{ $t('dashboard.formulaCount') }}
          </div>
          <count-to :start-val="0" :end-val="counts.formulaCount" :duration="3000" class="card-panel-num" />
        </div>
      </div>
    </el-col>
    <el-col :xs="12" :sm="12" :lg="6" class="card-panel-col">
      <div class="card-panel" @click="handleSetLineChartData('messages')">
        <div class="card-panel-icon-wrapper icon-message">
          <i style="font-size: 48px" class="el-icon-notebook-2" />
        </div>
        <div class="card-panel-description">
          <div class="card-panel-text">
            {{ $t('dashboard.masterCount') }}
          </div>
          <count-to :start-val="0" :end-val="counts.masterCount" :duration="3000" class="card-panel-num" />
        </div>
      </div>
    </el-col>
    <!--    <el-col :xs="12" :sm="12" :lg="5" class="card-panel-col">-->
    <!--      <div class="card-panel" @click="handleSetLineChartData('purchases')">-->
    <!--        <div class="card-panel-icon-wrapper icon-money">-->
    <!--          <i style="font-size: 48px" class="el-icon-s-opportunity" />-->
    <!--        </div>-->
    <!--        <div class="card-panel-description">-->
    <!--          <div class="card-panel-text">-->
    <!--            {{ $t('dashboard.instanceCount') }}-->
    <!--          </div>-->
    <!--          <count-to :start-val="0" :end-val="counts.instanceCount" :duration="3200" class="card-panel-num" />-->
    <!--        </div>-->
    <!--      </div>-->
    <!--    </el-col>-->
    <el-col :xs="12" :sm="12" :lg="6" class="card-panel-col">
      <div class="card-panel" @click="handleSetLineChartData('shoppings')">
        <div class="card-panel-icon-wrapper icon-shopping">
          <i style="font-size: 48px" class="el-icon-edit-outline" />
        </div>
        <div class="card-panel-description">
          <div class="card-panel-text">
            {{ $t('dashboard.formulaGroupCount') }}
          </div>
          <count-to :start-val="0" :end-val="counts.groupCount" :duration="3600" class="card-panel-num" />
        </div>
      </div>
    </el-col>
  </el-row>
</template>

<script>
import CountTo from 'vue-count-to'
import DashboardApi from '@/api/DashboardApi'

export default {
  components: {
    CountTo
  },
  data() {
    return {
      counts: {
        productCount: 0,
        masterCount: 0,
        formulaCount: 0,
        groupCount: 0
      }
    }
  },
  created() {
    this.getCounts()
  },
  methods: {
    async getCounts() {
      const { data } = await DashboardApi.getCounts()
      this.counts = data
    },
    handleSetLineChartData(type) {
      this.$emit('handleSetLineChartData', type)
    }
  }
}
</script>

<style lang="scss" scoped>
.panel-group {
  margin-top: 18px;

  .card-panel-col {
    margin-bottom: 32px;
  }

  .card-panel {
    height: 108px;
    cursor: pointer;
    font-size: 12px;
    position: relative;
    overflow: hidden;
    color: #666;
    background: #fff;
    box-shadow: 4px 4px 40px rgba(0, 0, 0, .05);
    border-color: rgba(0, 0, 0, .05);

    &:hover {
      .card-panel-icon-wrapper {
        color: #fff;
      }

      .icon-people {
        background: #40c9c6;
      }

      .icon-message {
        background: #36a3f7;
      }

      .icon-money {
        background: #f4516c;
      }

      .icon-shopping {
        background: #67C23A
      }
    }

    .icon-people {
      color: #E6A23C;
    }

    .icon-message {
      color: #36a3f7;
    }

    .icon-money {
      color: #f4516c;
    }

    .icon-shopping {
      color: #34bfa3
    }

    .card-panel-icon-wrapper {
      float: left;
      margin: 14px 0 0 14px;
      padding: 16px;
      transition: all 0.38s ease-out;
      border-radius: 6px;
    }

    .card-panel-icon {
      float: left;
      font-size: 48px;
    }

    .card-panel-description {
      float: right;
      font-weight: bold;
      margin: 26px;
      margin-left: 0px;

      .card-panel-text {
        line-height: 18px;
        color: rgba(0, 0, 0, 0.45);
        font-size: 16px;
        margin-bottom: 12px;
      }

      .card-panel-num {
        font-size: 20px;
      }
    }
  }
}

@media (max-width: 550px) {
  .card-panel-description {
    display: none;
  }

  .card-panel-icon-wrapper {
    float: none !important;
    width: 100%;
    height: 100%;
    margin: 0 !important;

    .svg-icon {
      display: block;
      margin: 14px auto !important;
      float: none !important;
    }
  }
}
</style>
