<template>
  <a-cascader
    :options="options"
    :load-data="loadData"
    placeholder="Please select"
    change-on-select
    @change="onChange"
  />
</template>
<script>
import { Cascader } from 'ant-design-vue';
import Vue from 'vue';
Vue.use(Cascader);
export default {
  data() {
    return {
      options: [
        {
          value: 'zhejiang',
          label: 'Zhejiang',
          isLeaf: false,
        },
        {
          value: 'jiangsu',
          label: 'Jiangsu',
          isLeaf: false,
        },
      ],
    };
  },
  methods: {
    onChange(value) {
      console.log(value);
    },
    loadData(selectedOptions) {
      const targetOption = selectedOptions[selectedOptions.length - 1];
      targetOption.loading = true;

      // load options lazily
      setTimeout(() => {
        targetOption.loading = false;
        targetOption.children = [
          {
            label: `${targetOption.label} Dynamic 1`,
            value: 'dynamic1',
          },
          {
            label: `${targetOption.label} Dynamic 2`,
            value: 'dynamic2',
          },
        ];
        this.options = [...this.options];
      }, 1000);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
