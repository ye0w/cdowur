<template>
  <div class="box">
    <e-chart ref="myChart" id="myChart" />
  </div>
</template>
  
  <script>
import * as echarts from "echarts";
export default {
  mounted() {
    let myChart = echarts.init(this.$refs.myChart);

    let option = {
      // dataset: {
      //   source: [
      //     ["type", "rider1","rider2","rider3","rider4","rider5"],
      //     ["rider1", 99,92],
      //     ["rider2", 98,78],
      //     ["rider3",0,0,],
      //     ["rider4",98,84],
      //     ["rider5",102,79]
      //   ]
      // },
      color: ["#32f1dd", "#fa5435"],
      title: {
        text: "Rider energy level report \n Total and over-CP\n Percentage of defined maximum",
        left: "center",
        //top: "top",
        padding: [-1.5,0,0,0],

        textStyle: {
          fontSize: 15,
          fontWeight: "bolder",
          FontFamily: "Arial",
          color: "#F2EB3E",
        },
      },

      //悬浮提示窗
      tooltip: {
        trigger: "axis",
        backgroundColor: "rgba(50,50,50,0.7)",
        borderColor: "#ffffff",
        formatter: function (params) {
          var relVal = params[0].name;
          for (var i = 0; i < params.length; i++) {
            relVal +=
              "<br/>" +
              params[i].marker +
              params[i].seriesName +
              " : " +
              params[i].value +
              "%";
          }
          return relVal;
        },
        axisPointer: {
          type: "shadow",
          label: {
            show: true,
          },
        },
        textStyle: {
          fontSize: 10,
          lineHeight: 5,
          FontFamily: "Arial",
          color: "#ffffff",
        },
      },

      //图例
      legend: {
        show: true,
        icon: "circle",
        right: 50,
        top: 5,
        bottom: 0,
        orient: "vertical",
        itemWidth: 8,
        itemHeight: 8,
        textStyle: {
          color: "white",
          fontWeight: "lighter",
        },
      },

      xAxis: [
        {
          type: "category",
          scale: true,
          splitNumber: 15,
          nameLocation: "middle",
          axisLabel: {
            color: "#d5cece",
          },
          axisLine: {
            lineStyle: {
              color: "#d5cece",
            },
          },
          data: ["Rider 1", "Rider 2", "Rider 3", "Rider 4", "Rider 5"],
        },
      ],

      yAxis: {
        type: "value",
        name: "Ride energy, % Max",
        min: 0,
        max: 120,
        nameLocation: "middle",
        nameTextStyle: {
          verticalAlign: "top",
          lineHeight: -80,
          color: "#F2EB3E",
          fontWeight: "lighter",
          //padding:[3,4],
        },
        axisLabel: {
          formatter: "{value} %",
          color: "#d5cece",
        },
      },

      series: [
        {
          name: "Energy total, KJ",
          type: "bar",
          barWidth: "15%",
          label: {
            normal: {
              show: true,
              position: "top",
              formatter: "{c}%",
              textStyle: {
                color: "#d5cece",
                fontWeight: "normal",
                fontSize: "12",
              },
            },
          },
          data: [99, 98, "-", 98, 102],
        },
        {
          name: "Over CP enery, KJ",
          type: "bar",
          barWidth: "15%",
          label: {
            normal: {
              show: true,
              position: "top",
              formatter: "{c}%",
              textStyle: {
                color: "#d5cece",
                fontWeight: "normal",
                fontSize: "12",
              },
            },
          },
          //柱状图渐变色
          // itemStyle:{
          //   normal:{
          //     color: new echarts.graphic.LinearGradient(0, 1, 0, 0, [{
          // 		offset: 0,
          // 		color: "#fa5435" // 0%
          // 	}, {
          // 		offset: 0.6,
          // 		color: "#f3836f" // 60%
          // 	}, {
          // 		offset: 1,
          // 		color: "#f8b9ad" // 100%
          // 	}], false)
          //   },
          // },
          data: [92, 78, "-", 84, 79],
        },
      ],
    };
    myChart.setOption(option);
  },
};
</script>
  
<style scoped>
#myChart {
  padding-top: 4vh;
  padding-bottom: 4vh;
  margin: 0 auto;
  display: flex;
  justify-content: center;
  height: 40vh;
  width: 70vw;
  background-color: rgba(0, 0, 0, 0.3);
  border-radius: 8px;
}

.box {
  height: 48vh;
  width: 70vw;
  /* border-style: solid;
      border-width: 1px;
      border-color: #F2EB3E; */
  border-radius: 8px;
}
</style>
  