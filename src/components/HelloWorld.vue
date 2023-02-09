<template>
  <div class="hello">
    <div>表单1</div>
    <formTemp ref="formData1" :fromData="formData1" ruleForm:='ruleForm1'></formTemp>
    <div>表单2</div>
    <formTemp ref="formData2" :fromData="formData2" ruleForm:='ruleForm2'></formTemp>
    <div>表单3</div>
    <formTemp ref="formData3" :fromData="formData3" ruleForm:='ruleForm3'></formTemp>
    <el-button type="primary" @click="submitFrom()">提交按钮</el-button>
  </div>
</template>

<script>
import formTemp from "./form.vue";
export default {
  name: "HelloWorld",
  components: {
    formTemp: formTemp,
  },
  data() {
    return {
      ruleForm1:{
        name1:'',
        resource:'',
        desc:''
      },
      ruleForm2:{
        name:'',
        resource:''
      },
      ruleForm3:{
        name:''
      },
      formData1: [
        {
          name: "name",
          type: "text",
          label: "活动名称1",
          value: "",
        },

        {
          name: "resource",
          type: "text",
          label: "活动性质1",
          value: "",
        },
        {
          name: "desc",
          type: "text",
          label: "特殊资源1",
          value: "",
        },
      ],
      formData2: [
        {
          name: "name",
          type: "text",
          label: "活动名称2",
          value: "",
        },

        {
          name: "resource",
          type: "text",
          label: "活动性质2",
          value: "",
        },
      ],
      formData3: [
        {
          name: "name",
          type: "text",
          label: "活动名称3",
          value: "",
        },
      ],
    };
  },
  methods: {
    submitFrom() {
      console.log(this);
      let that = this;
      that.$refs["formData1"].$emit("submitForm");
      console.log(that.$refs.formData1.isRule);
      if (!that.$refs.formData1.isRule) {
        return alert("表单1未通过验证");
      }
      that.$refs["formData2"].$emit("submitForm");
      console.log(that.$refs.formData1.isRule);
      if (!that.$refs.formData2.isRule) {
        return alert("表单2未通过验证");
      }
      that.$refs["formData3"].$emit("submitForm");
      console.log(that.$refs.formData1.isRule);
      if (!that.$refs.formData3.isRule) {
        return alert("表单3未通过验证");
      }
      console.log("可以提交");
    },
  },
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
