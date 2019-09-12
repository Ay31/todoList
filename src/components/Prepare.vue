<template>
  <div class="section">
    <h2>Prepare</h2>
    <table class="pre">
      <tbody>
        <tr>
          <th>todo</th>
          <th>Message</th>
          <th>Leval</th>
          <th>Handle</th>
        </tr>
        <tr v-for="(item,index) of note" :key="item.id" v-show="item.isShow">
          <td>{{item.todo}}</td>
          <td>{{item.mes}}</td>
          <td>{{item.sta}}</td>
          <td>
            <button @click="toDelete(index)">delete</button>
            <button @click="toFinsh(index)">finish</button>
          </td>
        </tr>
      </tbody>
    </table>
    <hr />
  </div>
</template>

<script>
import Bus from "@/bus";

export default {
  name: "Prepare",
  data() {
    return {
      note: []
    };
  },
  methods: {
    toDelete(index) {
      this.note[index].isShow = !this.note[index].isShow;
    },
    toFinsh(index) {
      var vm = this;
      var obj = JSON.parse(JSON.stringify(this.note[index]));
      Bus.$emit("finsh", obj);
      this.note[index].isShow = !this.note[index].isShow;
    }
  },
  created() {
    var vm = this;
    Bus.$on("send", function(val) {
      vm.note.push(val);
    });
    Bus.$on("back", function(key) {
      vm.note[key - 1].isShow = !vm.note[key - 1].isShow;
    });
  }
};
</script>

<style>
hr {
  margin-top: 30px;
}

h2 {
  margin-top: 10px;
}

table {
  margin: 0 auto;
  text-align: center;
}

th {
  padding: 10px;
  padding-top: 0;
}

tr > th:nth-of-type(2) {
  width: 300px;
}

tr > th:nth-of-type(4) {
  width: 300px;
}

td {
  padding: 13px 0;
}

td > button {
  margin: 5px;
}
</style>