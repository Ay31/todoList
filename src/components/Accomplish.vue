<template>
  <div class="section">
    <h2>Accomplish</h2>
    <table class="pre">
      <tbody>
        <tr>
          <th>todo</th>
          <th>Message</th>
          <th>Leval</th>
          <th>Handle</th>
        </tr>
        <tr v-for="(item,index) of note" :key="index" v-show="item.isShow">
          <td>{{item.todo}}</td>
          <td>{{item.mes}}</td>
          <td>{{item.sta}}</td>
          <td>
            <button @click="toDelete(index)">delete</button>
            <button @click="goBack(index)">back</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
import Bus from "@/bus";
export default {
  name: "Accomplish",
  data() {
    return {
      note: []
    };
  },
  methods: {
    toDelete(index) {
      this.note[index].isShow = !this.note[index].isShow;
    },
    goBack(index) {
      var vm = this;
      this.note[index].isShow = !this.note[index].isShow;
      Bus.$emit("back", vm.note[index].id);
    }
  },
  created() {
    var vm = this;
    Bus.$on("finsh", function(val) {
      vm.note.push(val);
    });
  }
};
</script>