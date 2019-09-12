<template>
  <div class="section">
    <h1 class="title">
      <button @click="toPre">ToDo</button>List
    </h1>
    <div class="main">
      <div class="inputArea">
        <label>todo:</label>
        <input type="text" v-model="todo" value="点击标题'ToDo'提交" />
      </div>
      <div class="inputArea">
        <label class="lMes">Message:</label>
        <textarea v-model="mes"></textarea>
      </div>
      <div class="inputArea">
        <label>Leval:</label>
        <label for>normal</label>
        <input type="radio" name="status" value="normal" v-model="sta" />
        <label for>urgent</label>
        <input type="radio" name="status" value="urgent" v-model="sta" />
      </div>
    </div>
    <hr />
  </div>
</template>

<script>
import Bus from "@/bus";

export default {
  name: "InputArea",
  data() {
    return {
      todo: "点击标题'ToDo'提交",
      mes: "每个人都有做的好事和想做好的事。",
      sta: "normal",
      id: 0
    };
  },
  methods: {
    toPre() {
      if (this.todo && this.mes && this.sta) {
        this.id++;
        var obj = {
          todo: this.todo,
          mes: this.mes,
          sta: this.sta,
          isShow: true,
          id: this.id
        };
        Bus.$emit("send", obj);
        this.todo = "";
        this.mes = "";
        this.sta = "normal";
      } else {
        alert("请输入完整信息。");
      }
    }
  }
};
</script>

<style>

.title {
  padding: 10px;
  text-align: center;
  background: #474747;
  font-weight: 700;
  color: #fff;
}

h1 > button {
  font-size: 32px;
  background: #474747;
  color: #fff;
  margin-right: 5px;
  outline-color: 0;
}

.section {
  margin: 20px;
}

.inputArea {
  margin: 20px 0;
}

.inputArea > label:nth-of-type(1) {
  display: inline-block;
  width: 80px;
}

.inputArea > input {
  border: 1px solid #000;
}

.lMes {
  position: relative;
  top: 50%;
  transform: translateY(-50%);
}


input[type="radio"] {
  margin-right: 20px;
}

input[type="text"] {
  text-indent: 7px;
  width: 91%;
  border-color: rgb(169, 169, 169);
}

textarea {
  text-indent: 7px;
  width: 91%;
}
</style>