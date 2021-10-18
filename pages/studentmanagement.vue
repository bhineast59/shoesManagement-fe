<template>
  <div class="container">
    <div class="search">
      <h1 style="text-align: left; font-size: 20px; font-weight: bold">
        QUẢN LÝ HỌC VIÊN
      </h1>
      <div style="display: flex; justify-content: flex-end">
        <a-form :form="formSearchName" @submit="handleSubmitSearchName">
          <a-form-item>
            <a-input-search
              placeholder="Tìm kiếm học viên"
              style="width: 200px; text-align: left"
              v-decorator="[
                'name',
                {
                  rules: [{ required: true, message: 'Vui lòng nhập tên!' }],
                },
              ]"
            />
          </a-form-item>
        </a-form>
        <a class="btn-add" href="#"
          ><a-icon
            class="icoin-add"
            type="plus-square"
            style="font-size: 30px; margin-left: 8px"
        /></a>
      </div>
    </div>
    <div>
      <a-tabs default-active-key="1" @change="callback">
        <a-tab-pane key="1" tab="Tất cả">
          <a-table
            :columns="columns"
            :data-source="dataAll"
            :rowKey="(data) => data.studentId"
            bordered
          >
            <div
              slot="paidtuition"
              slot-scope="text"
              style="
                justify-content: center;
                display: flex;
                flex-wrap: wrap;
                align-items: center;
              "
            >
              <span>
                {{ text }}
              </span>
              <a-divider type="vertical" />
              <a href=""><a-icon type="eye" style="font-size: 20px" /></a>
            </div>
            <span slot="profile">
              <div style="text-align: center">
                <a href=""><a-icon type="eye" style="font-size: 20px" /></a>
              </div>
            </span>
            <span slot="action" slot-scope="text, record">
              <div
                style="
                  justify-content: center;
                  display: flex;
                  flex-wrap: wrap;
                  align-items: center;
                "
              >
                <a href=""><a-icon type="eye" style="font-size: 20px" /></a>
                <a-divider type="vertical" />
                <a-popconfirm
                  v-if="dataAll.length"
                  title="Bạn có chắc chắn xoá?"
                  @confirm="() => onDelete(record.studentId)"
                >
                  <a href="javascript"><a-icon type="delete" style="font-size: 20px" />
                  </a>
                </a-popconfirm>
              </div>
            </span>
          </a-table>
        </a-tab-pane>
        <a-tab-pane key="2" tab="Đã đóng">
          <a-table :columns="columns" :data-source="dataDaDong" :rowKey="(data) => data.studentId" bordered>
            <div
              slot="paidtuition"
              slot-scope="text"
              style="
                justify-content: center;
                display: flex;
                flex-wrap: wrap;
                align-items: center;
              "
            >
              <span>
                {{ text }}
              </span>
              <a-divider type="vertical" />
              <a href=""><a-icon type="eye" style="font-size: 20px" /></a>
            </div>        
            <span slot="profile">
              <div style="text-align: center">
                <a href=""><a-icon type="eye" style="font-size: 20px" /></a>
              </div>
            </span>
            <span slot="action" slot-scope="text, record">
              <div
                style="
                  justify-content: center;
                  display: flex;
                  flex-wrap: wrap;
                  align-items: center;
                "
              >
                <a href=""><a-icon type="eye" style="font-size: 20px" /></a>
                <a-divider type="vertical" />
                <a-popconfirm
                  v-if="dataDaDong.length"
                  title="Bạn có chắc chắn xoá?"
                  @confirm="() => onDelete(record.studentId)"
                >
                  <a href="javascript"
                    ><a-icon type="delete" style="font-size: 20px" />
                  </a>
                </a-popconfirm>
              </div>
            </span>
          </a-table>
        </a-tab-pane>

        <a-tab-pane key="3" tab="Nợ phí"> 
          <a-table :columns="columns" :data-source="dataNoPhi" :rowKey="(data) => data.studentId" bordered>
            <div
              slot="paidtuition"
              slot-scope="text"
              style="
                justify-content: center;
                display: flex;
                flex-wrap: wrap;
                align-items: center;
              "
            >
              <span>
                {{ text }}
              </span>
              <a-divider type="vertical" />
              <a href=""><a-icon type="eye" style="font-size: 20px" /></a>
            </div>
            <span slot="profile">
              <div style="text-align: center">
                <a href=""><a-icon type="eye" style="font-size: 20px" /></a>
              </div>
            </span>
            <span slot="action" slot-scope="text, record">
              <div
                style="
                  justify-content: center;
                  display: flex;
                  flex-wrap: wrap;
                  align-items: center;
                "
              >
                <a href=""><a-icon type="eye" style="font-size: 20px" /></a>
                <a-divider type="vertical" />
                <a-popconfirm
                  v-if="dataNoPhi.length"
                  title="Bạn có chắc chắn xoá?"
                  @confirm="() => onDelete(record.studentId)"
                >
                  <a href="javascript"
                    ><a-icon type="delete" style="font-size: 20px" />
                  </a>
                </a-popconfirm>
              </div>
            </span>
          </a-table>
        </a-tab-pane>
   
        </a-tabs>
    </div>
  </div>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";
import { IStudentList } from "src/enums/models/response/studentList";
import { IFindStudent } from "src/enums/models/request/findstudent";
import { WrappedFormUtils } from "ant-design-vue/types/form/form";
import { IDeleteStudent } from "src/enums/models/request/deletestudent";
// import MenuItem from 'ant-design-vue/types/menu/menu-item'

@Component({
  layout: "menu",
  name: "studentmanagement",
  async fetch() {
    this.dataAll = await this.$axios.$get("/Student/get-all-student");
    this.dataDaDong = await this.$axios.$get("/Student/get-tuition");
    this.dataNoPhi = await this.$axios.$get("/Student/get-tuition2");
  },
})
export default class StudentManagement extends Vue {
  private formSearchName!: WrappedFormUtils;
  studentList!: IStudentList;
  private dataAll: Array<IStudentList> = [];
  private dataDaDong: Array<IStudentList> = [];
  private dataNoPhi: Array<IStudentList> = [];
  private deletestudent!: IDeleteStudent;
  private tabchange: any = 1;
  private columns: Array<any> = [
    {
      title: "Mã sinh viên",
      dataIndex: "studentId",
      key: "studentId",
    },
    {
      title: "Họ và tên",
      dataIndex: "name",
      key: "name",
    },
    {
      title: "Số điện thoại",
      dataIndex: "phoneNumber",
      key: "phone",
    },
    {
      title: "Facebook",
      dataIndex: "facebookUrl",
      key: "facebook",
    },
    {
      title: "Địa chỉ hiện tại",
      dataIndex: "currentAddress",
      key: "address",
    },
    {
      title: "Đã đóng",
      dataIndex: "piece",
      slots: { title: "title" },
      scopedSlots: { customRender: "paidtuition" },
      key: "paidtuition",
    },
    {
      title: "Tổng phí",
      dataIndex: "totalPrice",
      key: "totaltuition",
    },
    {
      title: "Hồ sơ",
      scopedSlots: { customRender: "profile" },
      key: "profile",
    },
    {
      title: "Hành động",
      scopedSlots: { customRender: "action" },
      key: "action",
    },
  ];
  onDelete(key: number) {
    this.deletestudent = {
      id: key,
    };
    this.$axios
      .$post("/Student/remove-student", this.deletestudent)
      .then((response) => {
        response = true;
        this.dataAll = this.dataAll.filter((item) => item.studentId !== key);
        this.dataDaDong = this.dataDaDong.filter(
          (item) => item.studentId !== key
        );
        this.$message.success("Xoá thành công");
      })
      .catch((error) => {
        this.$message.error("Xoá thất bại");
      });
  }

  handleSubmitSearchName(e: any) {
    e.preventDefault()
    this.formSearchName.validateFields((err: any, values: IFindStudent) => {
      if (!err) {
        if(this.tabchange == 1){
        this.$axios
          .$post("/Student/find-student", values)
          .then((response) => {
              this.dataAll =response
            }).catch((error) => {})
        }
      if(this.tabchange == 2){
        this.$axios
          .$post("/Student/find-student-1", values)
          .then((response) => {
              this.dataDaDong =response
            }).catch((error) => {})
      }    
      if(this.tabchange == 3){
        this.$axios
          .$post("/Student/find-student-2", values)
          .then((response) => {
              this.dataNoPhi =response
            }).catch((error) => {})
          
      }
    }
  })
  }

  callback(key:any) {
      this.tabchange = key;
    }

  async created() {
    this.formSearchName = this.$form.createForm(this)
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
