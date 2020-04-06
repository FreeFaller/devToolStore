
<template>
    <div>
        <!--Breadcrumb start-->
        <Breadcrumb>
            <BreadcrumbItem to="">Home</BreadcrumbItem>
            <BreadcrumbItem>about</BreadcrumbItem>
        </Breadcrumb>
        <!--searchBar start-->
        <SearchBar 
            :searchElems="searchElems" 
            :serachValue="serachValue"
            @search="search"
            @reset="reset"
        />
        <!--table start-->
        <Table :columns="columns1" :data="tableData"></Table>
        <Page 
            v-if="pageTotal"
            show-sizer 
            show-total
            :total="pageTotal" 
            :current="pageData.pageNo" 
            :pageSize="pageData.pageSize" 
            @on-change="pageChange" 
            @on-page-size-change="pageSizeChange"  
        />

        <!--form start-->
        <Modal
            v-model="FEHPVBmodal"
            title="表单提交"
            footer-hide
        >
            <div>
                <Form ref="form1" :model="formData" :rules="ruleValidate" :label-width="80">
                  <FormItem label="Name" prop="name">
                      <Input v-model="formData.name" placeholder="name"></Input>
                  </FormItem>
                  <FormItem>
                    <Button type="primary" @click="handleSubmit">提交</Button>
                    <Button @click="modalCancel" style="margin-left: 8px">取消</Button>
                  </FormItem>
              </Form>
            </div>
        </Modal>

    </div>
</template>
<script>
import SearchBar from '@feHelper/searchBar1-base/index.vue'
export default { 
    components:{
        SearchBar
    },
    data(){
        return{
            
            //翻页数据
            pageData:{
                pageNo: 1,
                pageSize: 20
            },
            //总条数
            pageTotal: 100,
            //搜索元素数据
            searchElems: [
                {
                    title: '区域',
                    key: 'cityId',
                    type: 'select',
                    placeholder: '搜索',
                    items: [
                        {label: '区域1', value: 1},
                    ]
                }
            ],
            //搜索值数据
            serachValue:{
                cityId: 2,
            },
            //表格列数据
            columns1: [
                {
                    title: 'Name',
                    key: 'name'
                },
                {
                    title: '操作',
                    render: (h, params) => {
                      return <div><a href="javascript:;" onClick={this.formEdit.bind(null, params)}>编辑</a></div>;
                    }
                }
            ],
            //表格数据
            tableData: [
                {
                    name: 'John',
                }
            ],
            //modal
            FEHPVBmodal: false,

            //表单数据
            formData: {},
            //表单验证规则
            ruleValidate: {
                name: [
                    { required: true, message: 'error', trigger: 'blur' }
                ]
            }
        }
    },
    methods:{
        //获取表格数据
        getTableData(){
            let sendData = {
                ...this.pageData,
                ...this.serachValue
            }
            ajax.post('api', sendData).then((res) => {
                this.pageTotal = pageTotal
                this.tableData = []
            })
        },
        //页码更换
        pageChange(v){
            this.pageData.pageNo = v
            this.getTableData()
        },
        //页面显示条数更换
        pageSizeChange(v){
            this.pageData.pageSize = v
            this.pageData.pageNo = 1
            this.getTableData()
        },
        //搜索栏搜索事件
        search(v){
            this.serachValue = v
            this.pageData.pageNo = 1
            this.getTableData()
        },
        //搜索栏重置事件
        reset(v){
            this.serachValue = v
            this.pageData.pageNo = 1
            this.getTableData()
        },

        //表单编辑
        formEdit(params) {
          this.formData = Object.assign({}, params.row)
          this.$refs['form1'].resetFields()
          this.FEHPVBmodal = true;
        },

        //取消
        modalCancel(){
            this.FEHPVBmodal = false;
        },

        //表单提交
        handleSubmit () {
          this.$refs['form1'].validate((valid) => {
              if (valid) {
                  this.$Message.success('Success!');
                  let sendData = {...this.formData}
                  ajax.post('api', sendData).then((res) => {
                    //提交成功处理
                  })
              } else {
                  //验证失败处理
                  this.$Message.error('Fail!');
              }
          })
      }
    },
}
</script>

