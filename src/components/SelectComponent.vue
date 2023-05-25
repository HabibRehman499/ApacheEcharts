<template>
  <div>
    <el-select
      v-model="value"
      placeholder="Select"
      multiple
      collapse-tags
      clearable
      @change="changeHandler"
      @remove-tag="removetag"
    >
      <el-option label="All" value="-1" @click.native="selectAll"></el-option>
      <el-option
        v-for="item in options"
        :key="item.id"
        :label="item.label"
        :value="item.value"
      >
      </el-option>
    </el-select>
    <div id="lineChart" style="width: 100%; height: 300px"></div>
    <!-- <el-button @click="renderLineChart" >Get Line Chart</el-button> -->
  </div>
</template>

<script>
export default {
  name: "SelectComponent",

  data() {
    return {
      getLineChart: null,
      options: [
        {
          value: [150, 230, 224, 218, 135, 147, 260],
          label: "Option1",
          id: "1",
        },
        {
          value: [160, 240, 234, 258, 145, 147, 270],
          label: "Option2",
          id: "2",
        },
        {
          value: [170, 250, 244, 248, 155, 157, 250],
          label: "Option3",
          id: "3",
        },
        {
          value: [180, 260, 254, 238, 165, 167, 280],
          label: "Option4",
          id: "4",
        },
        {
          value: [190, 270, 264, 228, 175, 177, 290],
          label: "Option5",
          id: "5",
        },
      ],
      value: [],
    };
  },
  mounted() {
    this.getLineChart = this.$echarts.init(
      document.getElementById("lineChart")
    );
    this.selectAll();
  },
  methods: {
    renderLineChart(val) {
      if (this.getLineChart) {
        this.getLineChart.clear();
        const seriesList = [];
        this.value.forEach((item)=>{
          if(item != '-1'){
            
            seriesList.push({
            type: "line",
            data: item,
          });
          }
        });
        
        // console.log("Val",val);

        const option = {
          xAxis: {
            type: "category",
            data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
          },
          yAxis: {
            type: "value",
          },
          series: seriesList,
        };

        this.getLineChart.setOption(option);
      }
    },
    // Here options is dropdown Value and value is v model
    changeHandler(val) {
      // Logic for All
      if (val.includes("-1")) {
        if (val.length - 1 === this.options.length) {
          this.value = ["-1"];
        } else {
          this.value = val.filter((item) => item !== "-1");
        }

      } 
      // Logic for individually selecting All
      else {
        if (val.length === this.options.length) {
          this.value = ["-1", ...val];
        } else {
          this.value = val;
          
        }
      }
      // console.log('Change',this.value);
      this.renderLineChart(this.value);
    },
    // Here options is dropdown Value and value is v model
    selectAll() {
      if (this.value.includes("-1")) {
        this.value = [];
        // this.renderLineChart(this.value);
      } else {
        this.value = ["-1", ...this.options.map((item) => item.value)];
      }
      // console.log('All',this.value);
      this.renderLineChart(this.value);

    },
    removetag(val) {
      val === "-1" ? (this.value = []) : "";
    },
  },
};
</script>

<style>
el-select {
  width: 500px;
}
</style>
