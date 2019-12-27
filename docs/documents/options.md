### 最简配置
```javascript
export const crudOptions = {
  columns: [ //字段配置
    {
      title: '地区',  
      key: 'province', 
      type: 'select',
      dict: {url:'/dict/getProvinceList'}
    }
  ]
}
```
### 最全配置
```javascript
export const crudOptions = {
  columns: [ //字段配置
    {
      title: '地区',  
      key: 'province', 
      // -----下方的配置都是可选的------
      type: 'select', //字段类型，根据类型可生成该字段的默认配置，下方那么多配置基本可以不用写
      sortable: true, //是否支持排序
      search: {
        disabled: false, //是否禁用该字段的查询，默认false
        component:{}, //查询框组件配置，默认根据form配置生成 
        slot:false //是否启用搜索框的slot插槽,需要d2-crud-x才支持，示例 http://qiniu.veryreader.com/D2CrudPlusExample/#/form/slot
      },
      form: {
        rules: [ // 表单校验规则
          { required: true, message: '请选择地区' }
        ],
        disabled:false, //是否禁用该字段的添加与修改
        addDisabled: false, //是否在添加时禁用该字段
        editDisabled: false, //是否在修改时禁用该字段
        component: { //添加和修改时form表单的组件
          name: 'dict-select', //组件名称
          props: { //组件的参数
            // d2-crud中默认组件的参数需要配置在component下，而自定义组件又要写在props下，经常会搞混
            // d2-crud-plus会将props复制一份到component下，所以参数全部配置在props下即可
            filterable: true, //可过滤选择项[不同组件参数不同]
            multiple: true, //支持多选[不同组件参数不同]
            clearable: true //可清除[不同组件参数不同]
          }
        },
        valueChange(key ,value ,form){
            //form表单数据change事件，表单某项有改动将触发此事件
        },
        slot:false //是否启用form编辑框的slot插槽,需要d2-crud-x才支持，示例 http://qiniu.veryreader.com/D2CrudPlusExample/#/form/slot
      },
      valueBuilder (row,key) {
        // 某些组件传入的value值可能是一个复杂对象，而row中的单个属性的值不合适传入
        // 则需要在打开编辑对话框前将row里面多个字段组合成组件需要的value对象
        // 例如：国际手机号(mobileValue为此column的key) 示例 http://qiniu.veryreader.com/D2CrudPlusExample/#/form/phone
        // row.mobileValue = { phoneNumber: row.phone, callingCode: row.code, countryCode: row.country }
      },
      valueResolve (row,key) { 
        // 组件中传回的值也需要分解成row中多个字段的值，用于提交给后台。
        // if (row.mobileValue != null) {
        //  row.phone = row.mobileValue.phoneNumber
        //  row.code = row.mobileValue.callingCode
        //  row.country = row.mobileValue.countryCode
        // } 
      },
      dict: { // 数据字典配置， 供select等组件通过value匹配label
        data: [ // 本地数据字典
          { value: 'sz', label: '深圳' },
           { value: 'gz', label: '广州' }, 
           { value: 'wh', label: '武汉' }, 
           { value: 'sh', label: '上海' }
        ],
        url:'/dict/get', // 若data为空，则通过http请求获取远程数据字典
        // value:'value', value的属性名
        // label:'label', label的属性名
        // children:'children', children的属性名
        // isTree: false //是否是树形结构
      },
      rowSlot: false, // 是否启用该cell的slot插槽,需要d2-crud-x才支持，见 http://qiniu.veryreader.com/D2CrudPlusExample/#/form/slot
      formatter (row, column, value, index) {
        // cell 格式化，与d2-crud一致
      }
    }
  ],
  // 下方的配置都是可选的
  formOptions: { // 与d2-crud一致
    labelWidth: '100px',
    labelPosition: 'left',
    saveLoading: false,
    gutter: 20
  },
  searchOptions: {
    disabled: false //是否禁用搜索工具条
  },
  options: { // 与官d2-crud一致
    stripe: true,
    border: true,
    highlightCurrentRow: false
  },
  addTemplate: {}, //根据form配置自动生成
  editTemplate: {}, //根据form配置自动生成
  addRules: {}, //根据form配置自动生成
  editRules: {},//根据form配置自动生成
  list: [], //数据列表
  loading: false, //当前是否loading
  page: {
    current: 1,
    size: 20,
    total: 1
  },
  rowHandle: { 
    //行操作栏，与d2-crud一致，默认配置有修改与删除
  }
}

```