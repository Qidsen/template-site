<template>
  <div class="webpage__filter-component">
    <h1>Select items to add to the Purchase Order</h1>
    <div class="d-flex webpage__select-items">
      <div class="d-flex flex-column webpage__filter-wrapper">
        <el-button @click="showFilters" :class="{'webpage__filter--open':isFiltersShow}" class="webpage__filter" type="primary" plain>
          <FilterSvg /> {{ isFiltersShow ? "Hide filters" : "Show filters" }}
        </el-button>
      </div>
      <div class="d-flex webpage__checkbox-wrapper">
        <div class="d-flex webpage__categories">
          <label class="webpage__checkbox-group-label">Categories</label>
          <el-checkbox-group v-model="checkbox.categories">
            <el-checkbox label="All"></el-checkbox>
            <el-checkbox label="Products"></el-checkbox>
            <el-checkbox label="New Product"></el-checkbox>
          </el-checkbox-group>
        </div>
        <div class="d-flex webpage__items">
          <label class="webpage__checkbox-group-label">Items</label>
          <el-checkbox-group v-model="checkbox.items">
            <el-checkbox label="All"></el-checkbox>
          </el-checkbox-group>
        </div>
      </div>
    </div>
    <transition name="fade">
      <div v-if="isFiltersShow">
        <el-form class="d-flex webpage__filter-show">
          <div class="webpage__filter-items">
            <div class="webpage__filter-input">
              <div class="webpage__filter-block">
                <el-form-item label="Request for proposals">
                  <el-input v-model="filter.request"></el-input>
                </el-form-item>
                <el-form-item label="Purchase requsition number">
                  <el-input v-model="filter.purchase"></el-input>
                </el-form-item>
              </div>
              <div class="webpage__filter-block">
                <el-form-item label="Creation date">
                  <el-date-picker v-model="filter.creation" type="date" placeholder="All dates"></el-date-picker>
                </el-form-item>
                <el-form-item label="Delivery date">
                  <el-date-picker 
                    class="webpage__filter-date--range"
                    v-model="filter.delivery"
                    type="daterange"
                    range-separator="-"
                    start-placeholder="Start date"
                    end-placeholder="End date"
                    format="MMMM d">
                  </el-date-picker>
                </el-form-item>
              </div>
            </div>
            <hr>
            <div class="webpage__filter-select">
              <div class="webpage__filter-block">
                <el-form-item label="Location">
                  <el-select v-model="filter.location" placeholder="all">
                    <el-option label="Florida" value="1"></el-option>
                    <el-option label="New York" value="2"></el-option>
                    <el-option label="California" value="3"></el-option>
                  </el-select>
                </el-form-item>
                <el-form-item label="Requester">
                  <el-select v-model="filter.requester" placeholder="all">
                    <el-option label="Amazon" value="1"></el-option>
                    <el-option label="eBay" value="2"></el-option>
                    <el-option label="AliExpress" value="3"></el-option>
                  </el-select>
                </el-form-item>
              </div>
              <div class="webpage__filter-block">
                <el-form-item label="Department">
                  <el-select v-model="filter.department" placeholder="all">
                    <el-option label="CSM" value="1"></el-option>
                    <el-option label="ESM" value="2"></el-option>
                  </el-select>
                </el-form-item>
                <el-form-item label="Cost center">
                  <el-select v-model="filter.costCenter" placeholder="all">
                    <el-option label="Posters" value="1"></el-option>
                    <el-option label="Staff" value="2"></el-option> 
                  </el-select>
                </el-form-item>
              </div>
            </div>
            <div class="webpage__filter-total">
              <div class="webpage__filter-block">
                <el-form-item label="Total">
                  <el-dropdown class="webpage__filter-dropdown" v-model="filter.rate">
                    <span class="el-dropdown-link">
                      UAH<i class="el-icon-arrow-down el-icon--right"></i>
                    </span>
                    <el-dropdown-menu slot="dropdown">  
                      <el-dropdown-item v-for="item in filter.rate"
                        :key="item"
                        :value="item">
                        <span v-text="item"></span>
                      </el-dropdown-item>
                    </el-dropdown-menu>   
                  </el-dropdown>
                </el-form-item>
                <el-form-item>
                  <div class="webpage__filter-total--inputs">
                    <el-input type="number" min="0" placeholder="from" v-model="filter.totalFrom"></el-input>
                    <el-input type="number" min="0" placeholder="to" v-model="filter.totalTo"></el-input>
                  </div>
                </el-form-item>
              </div>
            </div>
          </div>
          <div class="webpage__filter-buttons">
            <div class="webpage__filter-buttons-left">
              <el-button class="webpage__filter-button--reset" type="primary" plain>
                Reset filters
              </el-button>
            </div>
            <div class="webpage__filter-buttons-right">
              <el-button class="webpage__filter-button--save" type="text">Save filter</el-button>
              <el-button class="webpage__filter-button--filter" type="primary">Filter</el-button> 
            </div>
          </div>
        </el-form>
      </div>
    </transition>
  </div>
</template>

<script>
import FilterSvg from '@/assets/img/svg/filter.svg'

export default {
  components: {
    FilterSvg
  },
  data: () => ({
    isFiltersShow: false,
    checkbox: {
      categories: [], 
      items: "",
    },
    filter: {
      request: "",
      purchase: "",
      creation: "",
      delivery: "",
      location: "",
      department: "",
      requester: "",
      cost: "",
      totalFrom: "",
      totalTo: "",
      rate: ["UAH", "USD", "EUR", "VND"],
    },
  }),
  methods: {
    showFilters() {
      this.isFiltersShow = !this.isFiltersShow
    }
  }
}
</script>

<style lang="scss">
  .webpage__filter-component {
    .webpage__filter {
      font-family: Roboto;
      font-size: 18px;
      font-weight: 700;
      line-height: 18px;
      border: 2px solid #B4CCE6;
      border-radius: 10px;
      svg {
        fill: #5093E1;
      }
      span {
        width: 132px;
        display: flex;
        align-items: center;
        justify-content: space-between;
      }
      &:hover, &:focus {
        svg {
          fill: white;
        }
      }
    }
    .webpage__filter-wrapper button {
      width: 172px;
    }
    .webpage__filter--open {
      height: 85px;
      background-color: #CDDAEA;
      border: none;
      border-radius: 10px 10px 0 0;
      position: relative;
      svg {
        transform: rotate(180deg);
      }
      &:hover, &:focus, &:active {
        background-color: #CDDAEA;
        color: black;
        svg {
          fill: black;
        }
      }
      &:before {
        content: '';
        display: block;
        height: 32px;
        width: 32px;
        background-color: #CDDAEA;
        position: absolute;
        left: 100%;
        top: 53px;
      }
      &:after {
        content: '';
        display: block;
        height: 32px;
        width: 32px;
        position: absolute;
        background-color: #e2e7ed;
        left: calc(100% + 1px);
        top: 53px;
        border-bottom-left-radius: 50%;
      }
    }
    .webpage__select-items {
      justify-content: space-between;
      width: 90%;
    }
    .webpage__checkbox-wrapper {
      width: 50%;
      height: 5%;
      flex-wrap: wrap;
      padding: 16px 110px 16px 24px;
      justify-content: space-between;
      background-color: #CDDAEA;
      box-shadow: 0px 2px 8px rgba(0, 0, 1, 0.15);
      border-radius: 10px;
    }
    .webpage__checkbox-group-label {
      margin-right: 16px;
      font-family: Roboto;
      font-size: 18px;
      font-weight: 700;
      line-height: 18px;
      letter-spacing: 0px;
      text-align: left;
      color: #4E5361;
    }
    .el-checkbox__label {
      font-family: Roboto;
      font-size: 15px;
      font-weight: 400;
      line-height: 18px;
      letter-spacing: 0px;
      text-align: left;
      color: #7C869C;
    }
    .webpage__filters-wrapper {
      width: 1308px;
      height: 322px;
      background: #CDDAEA;
      box-shadow: 0px 2px 8px rgba(0, 0, 1, 0.15);
      border-radius: 10px;
      transform: matrix(-1, 0, 0, 1, 0, 0);
    }
  }
  .webpage__filter-show {
    background-color: #CDDAEA;
    padding: 20px 20px;
    width: 80%;
    border-radius: 0px 10px 10px 10px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;

    .webpage__filter-items {
      display: flex;
      justify-content: space-between;
      flex-wrap: wrap;
    
      .webpage__filter-input, .webpage__filter-select {
        display: flex;
        flex-direction: column;
        justify-content: space-between;

        .webpage__filter-block {
          display: flex;
          justify-content: space-between;
          flex-wrap: wrap;

          .el-form-item {
            font-family: Roboto;
            font-size: 15px;
            font-weight: 700;
            line-height: 18px;
            color:#7C869C;
            margin: 5px 10px 0px 10px;

            .el-input input, .webpage__filter-date--range {
              width: 230px;
            }
          }
        }
      }
      hr {
        width: 2px;
        height: 115px;
        background-color: #E2E7ED;
        border: none;
        margin: 50px 0 auto 0;
      }
      .webpage__filter-select {
        input {
          font-family: Roboto;
          font-size: 15px;
          font-style: normal;
          font-weight: 400;
          line-height: 18px;  
          background-color: transparent;
          border: 2px solid #E2E7ED;

          &::placeholder {
            color: #7C869C;
          }
        } 
      }
      .webpage__filter-total {
        .webpage__filter-block {
          display: flex;
          flex-direction: column;
             
          .webpage__filter-total--inputs {
            display: flex;
            justify-content: space-between;

            input {
              margin: 0 10px 10px 0;
              width: 109px;
              border-radius: 5px;
            }
          }
        }
        .el-form-item {
          display: flex;
          justify-content: space-between;
          font-family: Roboto;
          font-size: 15px;
          font-style: normal;
          font-weight: 700;
          line-height: 18px;
          margin: 0;

          &::before, &::after {
            content: none;
          }

          .webpage__filter-dropdown {
            margin-right: 10px;
            font-family: Roboto;
            font-size: 15px;
            font-style: normal;
            font-weight: 400;
            line-height: 18px;
            letter-spacing: 0px;
            text-align: left;
          }
        }
      }
    }
    .webpage__filter-buttons {
      display: flex;
      justify-content: space-between;
      flex-wrap: wrap;
      
      margin: 0px 10px 0px 10px;
      padding-top: 30px;

      .webpage__filter-buttons-left {
        .webpage__filter-button--reset {
          width: 172px;
          height: 50px;
          font-family: Roboto;
          font-size: 18px;
          font-weight: 700;
          line-height: 18px;
          border: 3px solid #B4CCE6;
          border-radius: 10px;

          .span {
            width: 132px;
            display: flex;
            justify-content: center;
          }
        }
      }
      .webpage__filter-buttons-right {
        .webpage__filter-button--save {
          font-family: Roboto;
          font-size: 18px;
          font-style: normal;
          font-weight: 700;
          line-height: 18px;
          color: #5093E1;
          margin-right: 20px;
        }
        .webpage__filter-button--filter {
          width: 231px;
          height: 50px;
          border-radius: 10px;
          font-family: Roboto;
          font-size: 18px;
          font-weight: 700;
        }
      }
    }
  }
  .fade-enter-active, .fade-leave-active {
    transition: opacity .5s;
  }
  .fade-enter, .fade-leave-to /* .fade-leave-active до версии 2.1.8 */ {
    opacity: 0;
  }

  @media all and (max-width: 1830px) {
    .webpage__filter-total {
      padding: 10px 10px;
    }
  }

  @media all and (max-width: 1551px) {
    .webpage__filter-show {
      width: 100%;
      
      .webpage__filter-items {
        display: flex;
        flex-direction: row;

        .webpage__filter-block {
          display: flex;
          flex-direction: column;
        }
      }
      hr {
        display: none;
      }
    }
  }

  @media all and (max-width: 1200px) {
    .webpage__select-items {
      flex-direction: column-reverse;
    }
    .webpage__filter-wrapper {
      padding-top: 24px;
    }
    .webpage__categories, .webpage__items {
      flex-direction: column;
      
      .el-checkbox-group {
        display: flex;
        flex-direction: column;
        padding-top: 12px;
      }
    }
    .webpage__filter-show .webpage__filter-buttons {
      display: block;
      
      .webpage__filter-buttons-right {
        display: flex;
        flex-direction: column;
        align-items: flex-start;

        .el-button {
          margin-left: 0;
        }
      }
    }
  }
</style>