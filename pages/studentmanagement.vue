<template>  
  <div class="container">
      <div class = "search">
        <a-input-search placeholder="Search student" style="width: 200px; text-align: left"   />     
        <button class="btn"> <a-icon class="icoin-add" type="plus-square" /></button> 
      </div>
      <div>
        <a-tabs default-active-key="1">
            <a-tab-pane key="1" tab="Tuition Debt">
                
            </a-tab-pane>
            <a-tab-pane key="2" tab="Paid Tuition">
            </a-tab-pane>  
            <a-tab-pane key="3" tab="Tab 3" disabled>
                Tab 3
            </a-tab-pane>        
        </a-tabs>
      </div>
      <div>
          <a-table :columns="columns" :data-source="data" :row-key='data => data.id'>  
        <span slot="action" slot-scope="text, record">
            <a>Profile - {{ record.name }}</a>
            <a-divider type="vertical" />
            <button type="primary"> <a-icon type="delete" /></button> 
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
  async fetch(){
      this.data = await this.$axios.$get('/list-all-student')
  }, 
})
export default class StudentManagement extends Vue {
    private columns: Array<any> = [
    {
        title: 'Student ID',
        dataIndex: 'id',
        key: 'id',
    },
    {
        title: 'Full name',
        dataIndex: 'name',
        key: 'name',   
    },
    {
        title: 'Phone Number',
        dataIndex: 'phone',
        key: 'phone',   
    },
    {
        title: 'Facebook',
        dataIndex: 'facebook',
        key: 'facebook',   
    },
    {
        title: 'Address',
        dataIndex: 'address',
        key: 'address',   
    },
    {
        title: 'Paid Tuition',
        dataIndex: 'paidtuition',
        key: 'paidtuition',   
    },
    {
        title: 'Total Tuition',
        dataIndex: 'totaltuition',
        key: 'totaltuition',   
    },
    {
        title: 'Profile',
        dataIndex: 'profile',
        key: 'profile',   
    },
    {
        title: 'Action',
        scopedSlots: { customRender: 'action' },
        key: 'action',   
    }
    ];
    private data: Array<any> = [
    ];
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
    font-size: 20px;
}
.btn :hover {
    background-color: rgb(223, 207, 207);
}
</style>
