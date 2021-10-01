<template>  
  <div class="container">    
      <div class = "search">       
        <h1 style="text-align:left;font-size:20px;font-weight:bold">QUẢN LÝ HỌC VIÊN </h1> 
        <div style="display: flex;justify-content: flex-end;">
            <a-input-search placeholder="Tìm kiếm học viên" style="width: 200px; text-align: left"   />     
            <a class="btn-add" href=""><a-icon class="icoin-add" type="plus-square" style="font-size:30px; margin-left: 8px" /></a>
        </div>              
      </div>
      <div>
        <a-tabs default-active-key="1">
            <a-tab-pane key="1" tab="Nợ phí">                
            </a-tab-pane>
            <a-tab-pane key="2" tab="Đóng phí">
            </a-tab-pane>         
        </a-tabs>
      </div>
    <div>
        <a-table :columns="columns" :data-source="data" :row-key='data => data.id' bordered>
            <div slot="paidtuition" slot-scope="text" style="justify-content: center; display: flex; flex-wrap: wrap; align-items: center">
                <span>
                    {{ text }}
                </span>
                <a-divider type="vertical" />             
                <a href=""><a-icon type="eye" style="font-size: 20px" /></a>
            </div>
            <span slot="title">
            </span>
            <span slot="profile">
                <div style="text-align: center">
                    <a href=""><a-icon type="eye" style="font-size: 20px" /></a>
                </div>
            </span>                
            <span slot="action" >
                <div style="justify-content: center; display: flex; flex-wrap: wrap; align-items: center">
                    <a href=""><a-icon type="eye" style="font-size: 20px" /></a>
                    <a-divider type="vertical" />
                    <button type="primary"> <a-icon type="delete" /></button> 
                </div>
            </span>    
        </a-table> 
    </div>
  </div>
</template>
<script lang="ts">
import { Vue, Component } from 'vue-property-decorator'
import { Button } from 'ant-design-vue';
Vue.use(Button);
// import MenuItem from 'ant-design-vue/types/menu/menu-item'
@Component({
  layout: 'menu',
  name: 'studentmanagement',
})
export default class StudentManagement extends Vue {
    private columns: Array<any> = [
    {
        title: 'Mã sinh viên',
        dataIndex: 'id',
        key: 'id',
    },
    {
        title: 'Họ và tên',
        dataIndex: 'name',
        key: 'name',   
    },
    {
        title: 'Số điện thoại',
        dataIndex: 'phone',
        key: 'phone',   
    },
    {
        title: 'Facebook',
        dataIndex: 'facebook',
        key: 'facebook',   
    },
    {
        title: 'Địa chỉ hiện tại',
        dataIndex: 'address',
        key: 'address',   
    },
    {
        title: 'Đã đóng',
        dataIndex: 'price',
        slots: { title: 'title' },
        scopedSlots: { customRender: 'paidtuition' },
        key: 'paidtuition',   
    },
    {
        title: 'Tổng phí',
        dataIndex: 'price',
        key: 'totaltuition',   
    },
    {
        title: 'Hồ sơ',
        scopedSlots: { customRender: 'profile' },
        key: 'profile',   
    },
    {
        title: 'Hành động',
        scopedSlots: { customRender: 'action' },
        key: 'action',   
    }
    ];
    private data: Array<any> = [
    ];
    async created(){
      this.data = await this.$axios.$get('/Student/get-student')    
    } 
}
</script>

<style scoped>
.search {
    text-align: right;
    margin-bottom: 10px;      
}
.btn {
    border: none;
    padding: 5px 5px;
    cursor: pointer;
    width: 30px;
    background-color: white;
}
.icoin-add {
    font-size: 25px;
}
.btn :hover {
    background-color: rgb(223, 207, 207);
}
.btn-add {
    text-decoration: none;
    color: gray;
}
</style>
