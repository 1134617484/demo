<template>
  <div>
    <el-form
      :model="ruleForm"
      :rules="rules"
      ref="ruleForm"
      label-width="100px"
      class="demo-ruleForm"
    >
      <el-form-item
        :label="item.label"
        :prop="item.name"
        v-for="(item, index) in fromData"
        :key="index"
        :name="index"
      >
        <el-input v-if="item.type == 'text'" v-model="ruleForm[item.name]"></el-input>

        <el-select
          v-if="item.type == 'region'"
          v-model="item.value"
          :placeholder="item.desc"
        >
          <el-option
            :label="optionItem.label"
            :value="optionItem.value"
            v-for="(optionItem, optionIndex) in item.data"
            :key="optionIndex"
          ></el-option>
        </el-select>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  props: {
    fromData: {
      type: Array,
      required: true,
      default() {
        return [
          {
            name: "name",
            type: "text",
            label: "活动名称",
            value: "",
          },
          {
            name: "region",
            type: "region",
            label: "活动区域",
            value: "",
            desc: "请选择活动区域",
            data: [
              {
                label: "区域一",
                value: "shanghai",
              },
              {
                label: "区域二",
                value: "beijing",
              },
            ],
          },
          {
            name: "type",
            type: "text",
            label: "即时配送",
            value: "",
          },
          {
            name: "resource",
            type: "text",
            label: "活动性质",
            value: "",
          },
          {
            name: "desc",
            type: "text",
            label: "特殊资源",
            value: "",
          },
          {
            name: "delivery",
            type: "text",
            label: "活动形式",
            value: "",
          },
        ];
      },
    },
  },
  data() {
    return {
      ruleForm:{

      },
      rules: {
        name: [
          { required: true, message: "请输入活动名称", trigger: "blur" },
          { min: 3, max: 5, message: "长度在 3 到 5 个字符", trigger: "blur" },
        ],
        region: [
          { required: true, message: "请选择活动区域", trigger: "change" },
        ],
        date1: [
          {
            type: "date",
            required: true,
            message: "请选择日期",
            trigger: "change",
          },
        ],
        date2: [
          {
            type: "date",
            required: true,
            message: "请选择时间",
            trigger: "change",
          },
        ],
        type: [
          {
            type: "array",
            required: true,
            message: "请至少选择一个活动性质",
            trigger: "change",
          },
        ],
        resource: [
          { required: true, message: "请选择活动资源", trigger: "change" },
        ],
        desc: [{ required: true, message: "请填写活动形式", trigger: "blur" }],
      },
      isRule: true,
    };
  },
  mounted() {

    this.$nextTick(function () {
      let that = this;
      this.$on("submitForm", function () {
        console.log("1");
        this.$refs["ruleForm"].validate((valid) => {
          console.log(valid)
          if (valid) {
            that.isRule = true;
          } else {
            console.log("error submit!!");
            that.isRule = false;
            return false;
          }
        });
      });
    });
  },
  methods: {
    resetForm(formName) {
      this.$refs[formName].resetFields();
    },
  },
};
</script>