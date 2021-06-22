<template>
  <div class="webpage__form-component">
    <h1 class="mt-8">Fill out the details for this Purchase Order</h1>
    <el-form class="webpage__form">
      <div class="webpage__form-block">
        <el-form-item label="Delivery date" :required="true">
          <el-date-picker v-model="form.date" type="date" placeholder="dd.mm.yyyy"></el-date-picker>
        </el-form-item>
        <el-form-item label="Location" :required="true">
          <el-select v-model="form.location" placeholder="---------" :required="true">
            <el-option label="Florida" value="1"></el-option>
            <el-option label="New York" value="2"></el-option>
            <el-option label="California" value="3"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="Legal entity" :required="true">
          <el-select v-model="form.entity" placeholder="select Location first">
            <el-option label="Sole proprietorship" value="1"></el-option>
            <el-option label="Partnership" value="2"></el-option>
            <el-option label="C corporation" value="3"></el-option>
            <el-option label="Limited liability company (LLC)" value="4"></el-option>
            <template #prefix>
              <i class="el-icon-warning"></i>
            </template>
          </el-select>
        </el-form-item>
        <el-form-item label="Taxes">
          <el-select v-model="form.taxes" multiple placeholder="select Taxes">
            <el-option
              v-for="item in 10"
              :key="item" 
              :label="`Vat ${item}0%`"
              :value="item">
            </el-option>
          </el-select>
        </el-form-item>
      </div>
      <div class="webpage__form-block webpage__form-block--column">
        <el-form-item label="Supplier" :required="true">
          <el-dropdown v-model="form.supplier">
            <span class="el-dropdown-link">Amazon</span>
            <el-dropdown-menu slot="dropdown">
              <el-dropdown-item
                v-for="item in form.supplier"
                :key="item"
                :value="item">
                <span v-text="item"></span> 
              </el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
        </el-form-item>
        <el-form-item label="Currency" :required="true">
          <el-dropdown v-model="form.currency">
            <span class="el-dropdown-link">USD</span>
            <el-dropdown-menu slot="dropdown">
              <el-dropdown-item v-for="item in form.currency"
                :key="item"
                :value="item">
                <span v-text="item"></span>
              </el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
        </el-form-item>
        <el-form-item label="Terms of Payment">
          <el-dropdown v-model="form.terms">
            <span class="el-dropdown-link">Prepayment</span>
            <el-dropdown-menu slot="dropdown">
              <el-dropdown-item v-for="item in form.terms"
                :key="item"
                :value="item">
                <span v-text="item"></span>
              </el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
        </el-form-item>
        <el-form-item label="Contract">
          <el-dropdown v-model="form.contract">
            <span class="el-dropdown-link"># 20304 - Precodo Inc.</span>
            <el-dropdown-menu slot="dropdown">
              <el-dropdown-item v-for="item in form.contract"
                :key="item"
                :value="item">
                <span v-text="item"></span> 
              </el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
        </el-form-item>
      </div>
      <div class="webpage__form-block">
        <el-form-item label="Department" :required="true">
          <el-select v-model="form.department" placeholder="Select department" :required="true">
            <el-option label="CSM" value="1"></el-option>
            <el-option label="ESM" value="2"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="Payment method" :required="true">
          <el-select v-model="form.payment" placeholder="Select payment method" :required="true">
            <el-option label="Bank Transfer" value="1"></el-option>
            <el-option label="Credit card" value="2"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="Cost center" :required="true">
          <el-select v-model="form.costCenter" placeholder="Select cost center" :required="true">
            <el-option label="Posters" value="1"></el-option>
            <el-option label="Staff" value="2"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="Project" :required="true">
          <el-select v-model="form.project" placeholder="Select project" :required="true">
            <el-option label="Website" value="1"></el-option>
            <el-option label="Application" value="2"></el-option>
          </el-select>
        </el-form-item>
      </div>
      <div class="webpage__form-block--input">
        <el-form-item label="Budgets">
          <el-input class="webpage__budgets-wrapper"
            v-model="form.budget" readonly>
            <template #prefix>
              <div>
                <i class="el-icon-warning"></i>
              </div>
              <div>
                <pre class="ul-budget-warning" v-html="budgetWarning" />
              </div>
            </template>
          </el-input>
        </el-form-item>
        <el-form-item label="Note">
          <el-input class="webpage__note-wrapper"
            placeholder="write your note..." 
            v-model="form.note">
          </el-input>
        </el-form-item>
      </div>
      <div class="webpage__form-submit">
        <el-button type="primary">Create</el-button>
        <h2>Total: 2,100.00 UAH</h2>
      </div>
    </el-form>
  </div>
</template>

<script>
export default {
  data: () => ({
    form: {
      date: "",
      location: "",
      entity: "",
      taxes: [],
      supplier: ["Amazon", "eBay", "AliExpress"],
      currency: ["USD", "EUR", "BTC"],
      department: "1",
      payment: "1",
      terms: ["Prepayment", "Nonpayment"],
      contract: ["# 20304 - Precodo Inc.", "# 20305 - Precodo Inc."],
      costCenter: "1",
      project: "1",
      note: "",
      budget: "",
    },
  }),
  computed: {
    budgetWarning() {
      return `<b>to view Budgets select:</b>\n- Delivery date, Location\n- Department, Cost center, Project`;
    },
  },
}
</script>

<style lang="scss">
  .webpage__form-component {
    .webpage__form {
      padding: 20px 20px;
      display: flex;
      justify-content: space-between;
      flex-direction: column;
      width: 90%;
      background-color: white;
      box-shadow: 0px 2px 8px rgba(0, 0, 1, 0.15);
      border-radius: 10px;
    }
    .webpage__form-block, .webpage__form-block--input {
      width: 80%;
      display: flex;
      justify-content: space-between;
      flex-wrap: wrap;
    }
    .webpage__form-block .el-form-item__content, .webpage__form-block input {
      width: 230px;
    }
    .webpage__form-block--column .el-form-item{
      display: flex;
      flex-direction: column;
    }
    .el-form-item__label {
      padding: 10px 0px;
      font-family: Roboto;
      font-size: 15px;
      font-weight: 700;
      line-height: 18px;
      text-align: left;
      color: #7C869C;
    }
    .el-dropdown-link, .el-select input {
      font-family: Roboto;
      color: #5093E1;
      font-weight: 500;
      font-size: 15px;
    }
    .el-input__prefix {
      text-align: left;
      display: flex;
      justify-content: space-between;
      margin: 0;
      padding: 0;
    }
    .ul-budget-warning {
      margin: 0;
      padding: 5px 5px;
      list-style: none;
      font-family: Roboto;
      font-size: 15px;
      line-height: 18px;
      color: #7C869C;
    }
    .ul-budget-warning li:before {
      content: "-";
      position: relative;
      left: -5px;
    }
    .el-icon-warning {
      margin: 10px 5px;
      color: #7C869C;
    }
    .webpage__form button {
      width: 231px;
      height: 50px;
      border-radius: 10px;
      font-family: Roboto;
      font-size: 18px;
      font-weight: 700;
    }
    .webpage__form-submit {
      display: flex;
    }
    .webpage__form-submit h2 {
      padding-left: 21px; 
      color: #7C869C;
      font-family: Roboto;
      font-size: 18px;
      font-weight: 700;
      line-height: 18px;
    }
    .el-select .el-tag {
      background-color: #5093E1;
      color: white;
      font-family: Roboto;
      font-size: 15px;
      font-weight: 400;
    }
  }
  .webpage__form-component {
      .webpage__form-block--input {
        width: 80%;

        .el-form-item {
          width: 46%;
        }

        input {
          height: 68px;
        }
      }
    }

  @media all and (max-width: 768px) {
    .webpage__form-component {
      width: calc(100% - 40px);
      .webpage__form-block--input {
        width: 100%;

        .el-form-item {
          width: 100%;
        }
      }
    }
  }
</style>