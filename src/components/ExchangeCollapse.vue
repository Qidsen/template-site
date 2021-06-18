<template>
  <div class="webpage__exchange">
    <el-collapse v-model="info.activeNames">
      <el-collapse-item title="Exchange rate" name="1">
        <el-form class="webpage__exchange-form">
          <template v-for="(item, index) in info.rates">
            <el-form-item
              :key="index"
              :label="`${item.name}`">
                <el-input class="webpage__rate-wrapper"
                v-model="item.rate" readonly>
              </el-input>
            </el-form-item>
          </template>
        </el-form>
      </el-collapse-item>
    </el-collapse>
  </div>
</template>

<script>
export default {
  data: () => ({
    info: {
      activeNames: ['1'],
      rates: [
        {
          name: "USD:UAH",
          rate: 26.543545,
        },
        {
          name: "USD:EUR",
          rate: 26.543545,
        },
        {
          name: "USD:VND",
          rate: 24234.500000,
        }
      ],
    },
  }),
}
</script>

<style lang="scss">
  .webpage__exchange {
    padding-top: 50px;
    .el-collapse {
      border: none;
    }
    .el-collapse-item {
      margin-bottom: -1px;
      background-color: #CDDAEA;
      border-radius: 10px;
      overflow: hidden;
      padding: 24px;
      width: 50%;
      .el-collapse-item__header {
        background: transparent;
        border: none;
        margin: 0;
        color: #7C869C;
          font-family: Roboto;
          font-size: 20px;
          font-weight: 700;
          line-height: 24px;
        }
        .el-collapse-item__wrap {
        background: transparent;
      }
    }
    .webpage__exchange-form {
      display: flex;
      justify-content: space-between; 
      label {
        color: #7C869C;
        font-family: Roboto;
        font-size: 15px;
        font-weight: 700;
        line-height: 18px;
      }
      input {
        color: #7C869C;
        font-family: Roboto;
        font-size: 15px;
        font-weight: 400;
        line-height: 18px;
      }
    }
    .el-collapse-item__wrap {
      border: none;
    }
  }
</style>