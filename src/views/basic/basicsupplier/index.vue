<template>
  <div class="basicSupplier">
    <h3>供应商</h3>
    <div class="basicVendor">
      <div class="Vendor-Class" v-show="isShow">
        <h4 class="supplier-title">供应商分类</h4>
        <div class="VendorClass">
          <Tree :data="data5" :render="renderContent"></Tree>
        </div>
        <div class="tree-button">
          <el-button size="mini">修改</el-button>
          <el-button size="mini">删除</el-button>
          <el-button size="mini">增加同级</el-button>
          <el-button size="mini">增加下级</el-button>
        </div>
      </div>
      <div class="Telescopic" @click="toggle">
        <img :src="imgUrl">
      </div>
      <div class="Vendor-table">
        <el-input placeholder="请输入内容" v-model="input5" class="input-with-select">
          <el-select v-model="select" slot="prepend" placeholder="请选择">
            <el-option label="餐厅名" value="1"></el-option>
            <el-option label="订单号" value="2"></el-option>
            <el-option label="用户电话" value="3"></el-option>
          </el-select>
          <el-button slot="append" icon="el-icon-search"></el-button>
        </el-input>
        <div class="Supplier-table">
          <el-table
            :data="tableData"
            border
            style="width: 100%"
            height="458">
            <el-table-column
              fixed
              prop="row"
              label="行号"
              width="50">
            </el-table-column>
            <el-table-column
              fixed
              type="selection"
              width="55">
            </el-table-column>
            <el-table-column
              prop="date"
              label="日期"
              width="150">
            </el-table-column>
            <el-table-column
              prop="name"
              label="姓名"
              width="120">
            </el-table-column>
            <el-table-column
              prop="province"
              label="省份"
              width="120">
            </el-table-column>
            <el-table-column
              prop="city"
              label="市区"
              width="120">
            </el-table-column>
            <el-table-column
              prop="address"
              label="地址"
              width="300">
            </el-table-column>
            <el-table-column
              prop="zip"
              label="邮编"
              width="120">
            </el-table-column>
            <el-table-column
              prop="position"
              label="职位"
              width="120">
            </el-table-column>
            <el-table-column
              prop="time"
              label="时间"
              width="120">
            </el-table-column>
            <el-table-column
              prop="school"
              label="毕业学校"
              width="120">
            </el-table-column>
            <el-table-column
              fixed="right"
              label="操作"
              width="100">
              <template slot-scope="scope">
                <el-button @click="handleClick(scope.row)" type="text" size="small">查看</el-button>
                <el-button type="text" size="small">编辑</el-button>
              </template>
            </el-table-column>
          </el-table>
          <el-pagination
            @size-change="handleSizeChange"
            @current-change="handleCurrentChange"
            :current-page="currentPage4"
            :page-sizes="[100, 200, 300, 400]"
            :page-size="100"
            layout="total, sizes, prev, pager, next, jumper"
            :total="400">
          </el-pagination>
          <div class="left-button">
            <el-button size="mini">期初导入</el-button>
            <el-button size="mini">空白新增</el-button>
            <el-button size="mini">复制新增</el-button>
            <el-button size="mini">修改</el-button>
            <el-button size="mini">删除</el-button>
          </div>
          <div class="right-button">
            <el-button size="mini">打印</el-button>
            <el-button size="mini">退出</el-button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import left_arrow from '@/assets/index_images/left_arrow.png'
import right_arrow from '@/assets/index_images/right_arrow.png'
export default {
  data() {
    return {
      imgUrl: left_arrow,
      options: [
        {
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
      input5: '',
      select: '',
      data5: [
        {
          title: '全部服务分类',
          expand: true,
          render: (h, { root, node, data }) => {
            return h(
              'span',
              {
                style: {
                  display: 'inline-block'
                }
              },
              [
                h('span', [
                  h('Icon', {
                    props: {
                      type: 'ios-folder-outline'
                    },
                    style: {
                      marginRight: '8px'
                    }
                  }),
                  h('span', data.title)
                ]),
                h(
                  'span',
                  {
                    style: {
                      display: 'inline-block',
                      marginLeft: '35px',
                      background: 'none'
                    }
                  },
                  [
                    h('Button', {
                      props: Object.assign({}, this.buttonProps, {
                        icon: 'ios-plus-empty',
                        type: 'primary'
                      }),
                      style: {
                        width: '52px'
                      },
                      on: {
                        click: () => {
                          this.append(data)
                        }
                      }
                    })
                  ]
                )
              ]
            )
          },
          children: [
            {
              title: '服务器',
              expand: true,
              children: [
                {
                  title: '服务器1',
                  expand: true
                },
                {
                  title: '服务器2',
                  expand: true
                }
              ]
            },
            {
              title: '网络产品',
              expand: true,
              children: [
                {
                  title: '网络产品1',
                  expand: true
                },
                {
                  title: '网络产品2',
                  expand: true
                }
              ]
            }
          ]
        }
      ],
      tableData: [
        {
          row: '1',
          date: '2016-05-03',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1518 弄',
          zip: 200333,
          position: '销售',
          time: '2017',
          school: '亚历山大大学'
        },
        {
          row: '2',
          date: '2016-05-02',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1518 弄',
          zip: 200333,
          position: '销售',
          time: '2017',
          school: '亚历山大大学'
        },
        {
          row: '3',
          date: '2016-05-04',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1518 弄',
          zip: 200333,
          position: '销售',
          time: '2017',
          school: '亚历山大大学'
        },
        {
          row: '4',
          date: '2016-05-01',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1518 弄',
          zip: 200333,
          position: '销售',
          time: '2017',
          school: '亚历山大大学'
        },
        {
          row: '5',
          date: '2016-05-01',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1518 弄',
          zip: 200333,
          position: '销售',
          time: '2017',
          school: '亚历山大大学'
        },
        {
          row: '6',
          date: '2016-05-01',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1518 弄',
          zip: 200333,
          position: '销售',
          time: '2017',
          school: '亚历山大大学'
        },
        {
          row: '7',
          date: '2016-05-01',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1518 弄',
          zip: 200333,
          position: '销售',
          time: '2017',
          school: '亚历山大大学'
        },
        {
          row: '8',
          date: '2016-05-01',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1518 弄',
          zip: 200333,
          position: '销售',
          time: '2017',
          school: '亚历山大大学'
        }
      ],
      buttonProps: {
        type: 'ghost',
        size: 'small'
      },
      isShow: true
    }
  },
  methods: {
    handleClick(row) {
      console.log(row)
    },
    renderContent(h, { root, node, data }) {
      return h(
        'span',
        {
          style: {
            //            display: 'inline-block'
          }
        },
        [
          h('span', [
            h('Icon', {
              props: {
                type: 'ios-paper-outline'
              },
              style: {
                marginRight: '8px'
              }
            }),
            h('span', data.title)
          ]),
          h(
            'span',
            {
              style: {
                display: 'inline-block',
                float: 'right',
                marginRight: '32px'
              }
            },
            [
              h('Button', {
                props: Object.assign({}, this.buttonProps, {
                  icon: 'ios-plus-empty'
                }),
                style: {
                  marginRight: '8px'
                },
                on: {
                  click: () => {
                    this.append(data)
                  }
                }
              }),
              h('Button', {
                props: Object.assign({}, this.buttonProps, {
                  icon: 'ios-minus-empty'
                }),
                on: {
                  click: () => {
                    this.remove(root, node, data)
                  }
                }
              })
            ]
          )
        ]
      )
    },
    append(data) {
      const children = data.children || []
      children.push({
        title: '服务器',
        expand: true
      })
      this.$set(data, 'children', children)
    },
    remove(root, node, data) {
      const parentKey = root.find(el => el === node).parent
      const parent = root.find(el => el.nodeKey === parentKey).node
      const index = parent.children.indexOf(data)
      parent.children.splice(index, 1)
    },
    toggle: function() {
      this.isShow = !this.isShow
      if (this.imgUrl === left_arrow) {
        this.imgUrl = right_arrow
      } else {
        this.imgUrl = left_arrow
      }
    }
  }
}
</script>

<style lang="scss">
.ivu-icon-ios-folder-outline,
.ivu-icon-ios-paper-outline {
  display: none;
}
.basicSupplier {
  width: 100%;
  justify-content: center;
  padding: 0 10px;
  h3 {
    margin: 25px 0 20px 20px;
  }
  .basicVendor {
    width: 100%;
    display: flex;
    .Vendor-Class {
      width: 250px;
      .supplier-title {
        font-weight: normal;
        font-size: 12px;
        margin: 0 0 15px 0;
      }
      .VendorClass {
        border: 1px solid #cfcfcf;
        height: 492px;
        padding: 10px 10px;
        margin-right: 6px;
      }
    }
    .Vendor-table {
      overflow: hidden;
      width: 100%;
      padding: 0;
      margin-top: -22px;
      .Supplier-table {
        /*height: 492px;*/
      }
      .el-input-group {
        width: 350px;
        float: right;
        margin: 0 0 15px 0;
        .el-input-group__prepend {
          .el-select {
            width: 105px;
          }
        }
      }
      .el-input-group--append > {
        .el-input__inner {
          width: 200px;
        }
      }
      .el-table--border {
        .el-table__header-wrapper {
          height: 30px;
        }
      }
    }
    .Telescopic {
      height: 492px;
      line-height: 492px;
      margin-top: 33px;
      img {
        width: 10px;
        height: 53px;
        display: inline-block;
        vertical-align: middle;
      }
    }
  }
}
.Vendor-table .el-table__body tr,
.Vendor-table .el-table__body .el-table__row {
  height: 30px;
}
.Vendor-table .el-table td,
.el-table th {
  padding: 0;
}
.Vendor-table .el-table {
  font-size: 12px;
}
.Vendor-table .el-table .cell {
  height: 30px;
  line-height: 30px;
}
.Vendor-table .el-pagination {
  border: 1px solid #cfcfcf;
  border-top: none;
}
.Vendor-table .Supplier-table .el-table--border,
.Vendor-table .Supplier-table .el-table--border .el-table--group {
  border: 1px solid #cfcfcf;
  border-bottom: none;
  /*border-right: none;*/
}
.basicVendor .el-button--mini {
  padding: 6px;
}
.basicVendor .el-button + .el-button {
  margin-left: 0;
}
.basicVendor .Supplier-table .left-button {
  float: left;
  margin-top: 10px;
}
.basicVendor .Supplier-table .right-button {
  float: right;
  margin-top: 10px;
}
.tree-button {
  margin-top: 10px;
  float: left;
}
</style>
