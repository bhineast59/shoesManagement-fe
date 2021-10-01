<template>
  <div>
    <a-table :columns="columns" :data-source="data">
      <span slot="action">
        <div>
          <a-icon type="form" @click="showModal" />
          <a-modal v-model="myModel.visible" title="Basic Modal" @ok="handleOk">
            <p>Some contents...</p>
            <p>Some contents...</p>
            <p>Some contents...</p>
          </a-modal>
        </div>
      </span>
    </a-table>
  </div>
</template>

<script lang="ts">
const columns = [
  {
    dataIndex: "name",
    key: "name",
    title: "Name",
  },
  {
    title: "Age",
    dataIndex: "age",
    key: "age",
  },
  {
    title: "Address",
    dataIndex: "address",
    key: "address",
  },
  {
    title: "Action",
    key: "action",
    scopedSlots: { customRender: "action" },
  },
];

const data = [
  {
  }
];
import { Vue, Component } from "vue-property-decorator";
// import MenuItem from 'ant-design-vue/types/menu/menu-item'
@Component({
  layout: "menu",
  name: "index",
})
export default class IndexPage extends Vue {
  public myModel = {
    visible: false,
  };
  async created() {
    const a = await this.$axios.$get("/Users");
    console.log(a);
  }
  data() {
    return {
      data,
      columns,
      visible: false,
    };
  }
  showModal(): void {
    this.myModel.visible = true;
  }
  handleOk(): void {
    this.myModel.visible = false;
  }
}
</script>

<style scoped>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>


