<template>
  <div>
    <div class="navbar navbar-fixed-top" style="width:100%;background-color: #001a3d; text-align:center">
      <h1 class="navbar-brand navbar-brand-name" id="show" style="color: white">一分钟看懂校园招聘企业与高校的关系</h1>
      <!--<i class="fa fa-square-o"></i><font color="#fff">-->
      <!--<button type="button" id="send_message" @click="sendMessage">发送 message</button>-->
      <!--<button type="button" id="close_websocket" @click = closeConnect>关闭 websocket</button>-->
    </div>
    <div id="total_dom" :style="{width: '1300px', height: '300px',margin:'20px auto'}">
    </div>
    <div id="myChart" :style="{width: '1300px', height: '500px',margin:'0px auto'}"></div>
    <div style="margin-left:1100px;margin-top:-420px;color: white;z-index: 1;position:absolute;font-size: 35px">{{ dataTime }}</div>
  </div>

</template>

<script>

  function sleep(n) {
    var start = new Date().getTime();
    //  console.log('休眠前：' + start);
    while (true) {
      if (new Date().getTime() - start > n) {
        break;
      }
    }
    // console.log('休眠后：' + new Date().getTime());
  }
  export default {
    name: 'hello',
    data () {
      return {
        msg: 'Welcome to Your Vue.js App',
        dataTime:'2017-01-01',
        dataC9: [],
        totalC9: 0,
        total985: 0,
        total211: 0,
        totalBasic: 0,
        totalTop: 0,
        data211: [],
        data985: [],
        dataNomal: [],
        dataLowNomal: [],
        xdata: ['2017-01-01', '2017-01-03', '2017-01-04', '2017-01-05', '2017-01-06', '2017-01-07', '2017-01-09', '2017-01-10', '2017-01-11', '2017-01-12', '2017-01-13', '2017-01-14', '2017-01-16', '2017-01-17', '2017-01-18', '2017-01-19', '2017-01-20', '2017-01-23', '2017-02-03', '2017-02-04', '2017-02-05', '2017-02-06', '2017-02-07', '2017-02-08', '2017-02-09', '2017-02-10', '2017-02-13', '2017-02-14', '2017-02-15', '2017-02-16', '2017-02-17', '2017-02-18', '2017-02-19', '2017-02-20', '2017-02-21', '2017-02-22', '2017-02-23', '2017-02-24', '2017-02-25', '2017-02-26', '2017-02-27', '2017-02-28', '2017-03-01', '2017-03-02', '2017-03-03', '2017-03-04', '2017-03-05', '2017-03-06', '2017-03-07', '2017-03-08', '2017-03-09', '2017-03-10', '2017-03-11', '2017-03-12', '2017-03-13', '2017-03-14', '2017-03-15', '2017-03-16', '2017-03-17', '2017-03-18', '2017-03-19', '2017-03-20', '2017-03-21', '2017-03-22', '2017-03-23', '2017-03-24', '2017-03-25', '2017-03-26', '2017-03-27', '2017-03-28', '2017-03-29', '2017-03-30', '2017-03-31', '2017-04-01', '2017-04-02', '2017-04-03', '2017-04-05', '2017-04-06', '2017-04-07', '2017-04-08', '2017-04-09', '2017-04-10', '2017-04-11', '2017-04-12', '2017-04-13', '2017-04-14', '2017-04-15', '2017-04-16', '2017-04-17', '2017-04-18', '2017-04-19', '2017-04-20', '2017-04-21', '2017-04-22', '2017-04-23', '2017-04-24', '2017-04-25', '2017-04-26', '2017-04-27', '2017-04-28', '2017-04-29', '2017-05-01', '2017-05-02', '2017-05-03', '2017-05-04', '2017-05-05', '2017-05-06', '2017-05-07', '2017-05-08', '2017-05-09', '2017-05-10', '2017-05-11', '2017-05-12', '2017-05-13', '2017-05-14', '2017-05-15', '2017-05-16', '2017-05-17', '2017-05-18', '2017-05-19', '2017-05-20', '2017-05-21', '2017-05-22', '2017-05-23', '2017-05-24', '2017-05-25', '2017-05-26', '2017-05-27', '2017-05-28', '2017-05-30', '2017-05-31', '2017-06-01', '2017-06-02', '2017-06-03', '2017-06-04', '2017-06-05', '2017-06-06', '2017-06-07', '2017-06-08', '2017-06-09', '2017-06-10', '2017-06-11', '2017-06-12', '2017-06-13', '2017-06-14', '2017-06-15', '2017-06-16', '2017-06-17', '2017-06-18', '2017-06-19', '2017-06-20', '2017-06-21', '2017-06-22', '2017-06-23', '2017-06-24', '2017-06-25', '2017-06-26', '2017-06-27', '2017-06-28', '2017-06-29', '2017-06-30', '2017-07-01', '2017-07-03', '2017-07-04', '2017-07-05', '2017-07-06', '2017-07-07', '2017-07-10', '2017-07-12', '2017-07-13', '2017-07-14', '2017-07-17', '2017-07-18', '2017-07-19', '2017-07-21', '2017-07-26', '2017-07-27', '2017-07-29', '2017-08-01', '2017-08-03', '2017-08-04', '2017-08-06', '2017-08-07', '2017-08-08', '2017-08-11', '2017-08-15', '2017-08-17', '2017-08-18', '2017-08-20', '2017-08-21', '2017-08-22', '2017-08-23', '2017-08-24', '2017-08-25', '2017-08-26', '2017-08-27', '2017-08-28', '2017-08-29', '2017-08-30', '2017-08-31', '2017-09-01', '2017-09-02', '2017-09-03', '2017-09-04', '2017-09-05', '2017-09-06', '2017-09-07', '2017-09-08', '2017-09-09', '2017-09-10', '2017-09-11', '2017-09-12', '2017-09-13', '2017-09-14', '2017-09-15', '2017-09-16', '2017-09-17', '2017-09-18', '2017-09-19', '2017-09-20', '2017-09-21', '2017-09-22', '2017-09-23', '2017-09-24', '2017-09-25', '2017-09-26', '2017-09-27', '2017-09-28', '2017-09-29', '2017-09-30', '2017-10-01', '2017-10-02', '2017-10-06', '2017-10-07', '2017-10-08', '2017-10-09', '2017-10-10', '2017-10-11', '2017-10-12', '2017-10-13', '2017-10-14', '2017-10-15', '2017-10-16', '2017-10-17', '2017-10-18', '2017-10-19', '2017-10-20', '2017-10-21', '2017-10-22', '2017-10-23', '2017-10-24', '2017-10-25', '2017-10-26', '2017-10-27', '2017-10-28', '2017-10-29', '2017-10-30', '2017-10-31', '2017-11-01', '2017-11-02', '2017-11-03', '2017-11-04', '2017-11-05', '2017-11-06', '2017-11-07', '2017-11-08', '2017-11-09', '2017-11-10', '2017-11-11', '2017-11-12', '2017-11-13', '2017-11-14', '2017-11-15', '2017-11-16', '2017-11-17', '2017-11-18', '2017-11-19', '2017-11-20', '2017-11-21', '2017-11-22', '2017-11-23', '2017-11-24', '2017-11-25', '2017-11-26', '2017-11-27', '2017-11-28', '2017-11-29', '2017-11-30', '2017-12-01', '2017-12-02', '2017-12-03', '2017-12-04', '2017-12-05', '2017-12-06', '2017-12-07', '2017-12-08', '2017-12-09', '2017-12-10', '2017-12-11', '2017-12-12', '2017-12-13', '2017-12-14', '2017-12-15', '2017-12-16', '2017-12-17', '2017-12-18', '2017-12-19', '2017-12-20', '2017-12-21', '2017-12-22', '2017-12-23', '2017-12-24', '2017-12-25', '2017-12-26', '2017-12-27', '2017-12-28', '2017-12-29', '2017-12-30', '2017-12-31'],
        mychart: "",
        timerClock: 1000,
        webSocket: '',
        color_dict: {
            "985高校":"#eb870d",
            "211高校":"#5bbd2c",
            "C9高校":"#de0029",
            "普通一本高校":"#f9f500",
            "普通二本高校":"#00a6ae"
        },
        sortedTotalData: [{
          name: 'C9高校',
          value: this.totalC9,
          color: new this.$echarts.graphic.LinearGradient(0, 0, 0, 1, [{
            offset: 0,
            color: 'rgba(222, 0, 41, 0.3)'
          }, {
            offset: 0.8,
            color: 'rgba(222, 0, 41, 0)'
          }], false)
        }, {
          name: '985高校',
          value: this.total985,
          color: new this.$echarts.graphic.LinearGradient(0, 0, 0, 1, [{
            offset: 0,
            color: 'rgba(235, 135, 13, 0.3)'
          }, {
            offset: 0.8,
            color: 'rgba(235, 135, 13, 0)'
          }], false)
        }, {
          name: '211高校',
          value: this.total211,
          color: new this.$echarts.graphic.LinearGradient(0, 0, 0, 1, [{
            offset: 0,
            color: 'rgba(91,189,44, 0.3)'
          }, {
            offset: 0.8,
            color: 'rgba(91,189,44, 0)'
          }], false),
        }, {
          name: '普通一本高校',
          value: this.totalTop,
          color: new this.$echarts.graphic.LinearGradient(0, 0, 0, 1, [{
            offset: 0,
            color: 'rgba(249, 245, 0, 0.3)'
          }, {
            offset: 0.8,
            color: 'rgba(249, 245, 0, 0)'
          }], false)
        }, {
          name: '普通二本高校',
          value: this.totalBasic,
          color: new this.$echarts.graphic.LinearGradient(0, 0, 0, 1, [{
            offset: 0,
            color: 'rgba(0,166, 174, 0.3)'
          }, {
            offset: 0.8,
            color: 'rgba(0,166, 174, 0)'
          }], false)
        }]
      }
    },
    mounted(){
      // this.connetWebSocket();
      // this.setnumber();
      this.drawLine();
      // this.inputNumber();
      // setInterval(this.inputNumber,100);
      // setTimeout(this.sendMessage(),2000);
      // setTimeout(this.closeConnect(),5000)
    },
    watch: {
      //观察option的变化
      dataLowNomal: function (newVal, oldVal) {
        this.setoptinManyLin();
        this.sortedTotalData.sort(function (a, b) {
          return a.value - b.value;
        });
        console.log(this.sortedTotalData);
        this.drawBar();
        // console.log("调用了")
      },
    },

    methods: {
      setnumber(){
        for (let i = 1; i < 1001; i++) {
          this.xdata.push(i)
        }
      },
      inputNumber() {

        // while (1) {
        let num1 = Math.floor(Math.random() * (5 - 5000) + 5000);
        let num2 = Math.floor(Math.random() * (5 - 5000) + 5000);
        let num3 = Math.floor(Math.random() * (5 - 5000) + 5000);
        let num4 = Math.floor(Math.random() * (5 - 5000) + 5000);
        let num5 = Math.floor(Math.random() * (5 - 5000) + 5000);
        this.dataC9.push(num1);
        this.data211.push(num2);
        this.data985.push(num3);
        this.dataNomal.push(num4);
        this.dataLowNomal.push(num5);
        if (this.data.length >= 1001) {
          this.data.splice(0, 1);
          this.xdata.splice(0, 1);
          this.timerClock += 1;
          this.xdata.push(this.timerClock);
        }
      },

      drawLine() {
        // 基于准备好的dom，初始化echarts实例
        this.mychart = this.$echarts.init(document.getElementById('myChart'));
        this.bar_dom = this.$echarts.init(document.getElementById('total_dom'));
        console.log(this.sortedTotalData);
        this.setoptinManyLin();
        this.drawBar();
      },
      get_Rank_Data(raw_data) {
        let rank_data = [];

        // chrome在这里的排序有问题，详情参考这篇博客:
        // console.log("https://www.cnblogs.com/yzeng/p/3949182.html?utm_source=tuicool&utm_medium=referral");
        for (var i = 0; i < rank_data.length; i++) {
          rank_data.oldIndex = i;
        }
        return rank_data.sort(function (a, b) {
          return a.value - b.value || a.oldIndex - b.oldIndex;
        });
      },

      drawBar() {
        var bar_option = {
          color: ['#3398DB'],
          title: {
            text: '2017年各类别高校平均校园招聘企业总数排名',
            textStyle: {
              color: '#fff',
              fontSize: 24,
            }
          },
          tooltip: {
            trigger: 'axis',
            axisPointer: {
              type: 'shadow'
            },
            formatter: "{b} <br> 来校企业总数: {c}"
          },
          /*legend: {
           data: [date]
           },*/
          grid: {
            left: '4%',
            right: '4%',
            bottom: '2%',
            containLabel: true
          },
          xAxis: {
            type: 'value',
            boundaryGap: [0, 10],
            min: 0,
            max: 1000,
            interval: 200,
            axisLabel: {
              formatter: '{value}',
              textStyle: {
                color: '#fff',
                fontWeight: '80'
              }
            },
            axisLine: {
              lineStyle: {
                color: '#F1F1F3' //坐标轴线线的颜色。
              }
            },
          },
          yAxis: {
            type: 'category',
            data: this.sortedTotalData.map(function (item) {
              return item.name;
            }),
            axisLabel: {
              show: true,
              interval: 0,
              rotate: 0,
              margin: 10,
              inside: false,
              textStyle: {
                //color: '#fff',
                fontWeight: '50'
              }
            },
            axisLine: {
              lineStyle: {
                color: '#F1F1F3' //坐标轴线线的颜色
              }
            },
          },
          series: [{
            type: 'bar',
            itemStyle: {
              normal: {
                color: function (params) {
                  var color_dict =  {
                    "985高校":"#eb870d",
                      "211高校":"#5bbd2c",
                      "C9高校":"#de0029",
                      "普通一本高校":"#f9f500",
                      "普通二本高校":"#00a6ae"
                  };
                  var colorList = [
                    '#C1232B','#B5C334','#FCCE10','#E87C25','#27727B',
                    '#FE8463'
                  ];
                  console.log(params);
                  return color_dict[params.name];
//                  return params.color;
                },
              }
            },
            label: {
              normal: {
                show: true,
                // formatter: '{c}',
                formatter: function (v) {
                  var val = v.data;
                  if (val == 0) {
                    return '';
                  }
                  return val;
                },
                color: '#fff',
                position: 'right'
              }
            },
            data: this.sortedTotalData.map(function (item) {
              return item.value.toFixed(2);
            })
          }]
        };
        this.bar_dom.setOption(bar_option);
      },

      setoptinManyLin(){
        this.mychart.setOption({
          backgroundColor: '#394056',
          title: {
            text: '2017年全国各类别高校校园招聘日均企业数量走势图',
            textStyle: {
              fontWeight: 'normal',
              fontSize: 24,
              color: '#F1F1F3'
            },
            left: '0%'
          },
          tooltip: {
            trigger: 'axis',
            axisPointer: {
              lineStyle: {
                color: '#57617B'
              }
            }
          },
          // dataZoom: {
          //     show: true,
          //     realtime: true,
          //     start: 20,
          //     end: 80,
          //     xAxisIndex: [0, 1]
          //   },
          legend: {
            icon: 'rect',
            itemWidth: 14,
            itemHeight: 5,
            itemGap: 13,
            data: ['C9', '211', '985', '一本', '二本'],
            right: '4%',
            textStyle: {
              fontSize: 12,
              color: '#F1F1F3'
            }
          },
          grid: {
            left: '3%',
            right: '4%',
            bottom: '3%',
            containLabel: true
          },
          xAxis: [{
            type: 'category',
            boundaryGap: false,
            axisLine: {
              lineStyle: {
                color: '#F1F1F3' //坐标轴线线的颜色。
              }
            },
            data: this.xdata
          }, {
            axisPointer: {
              show: false
            },
            axisLine: {
              lineStyle: {
                color: '#57617B'
              }
            },
            axisTick: {
              show: false
            },

            position: 'bottom',
            offset: 20,
            // data: ['', '', '', '', '', '', '', '', '', '', {
            //   value: '周六',
            //   textStyle: {
            //     align: 'left'
            //   }
            // }, '周日']
          }],
          yAxis: [{
            type: 'value',
            name: '单位（个）',
            max: 26,
            min: 0,
            axisTick: {
              show: false
            },
            axisLine: {
              lineStyle: {
                color: '#F1F1F3'
              }
            },
            axisLabel: {
              margin: 10,
              textStyle: {
                fontSize: 14
              }
            },
            splitLine: {
              lineStyle: {
                color: '#57617B'
              }
            }
          }],
          series: [{
            name: 'C9',
            type: 'line',
            smooth: true,
            symbol: 'circle',
            symbolSize: 5,
            showSymbol: false,
            lineStyle: {
              color: '#F1F1F3',
              normal: {
                width: 1
              }
            },
            areaStyle: {
              normal: {
                color: new this.$echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                  offset: 0,
                  color: 'rgba(222, 0, 41, 0.3)'
                }, {
                  offset: 0.8,
                  color: 'rgba(222, 0, 41, 0)'
                }], false),
                shadowColor: 'rgba(0, 0, 0, 0.1)',
                shadowBlur: 10
              }
            },
            itemStyle: {
              normal: {
                color: 'rgb(222, 0, 41)',
                borderColor: 'rgba(222, 0, 41,0.27)',
                borderWidth: 12

              }
            },
            data: this.dataC9
          }, {
            name: '985',
            type: 'line',
            smooth: true,
            symbol: 'circle',
            symbolSize: 5,
            showSymbol: false,
            lineStyle: {
              color: '#F1F1F3',
              normal: {
                width: 1
              }
            },
            areaStyle: {
              normal: {
                color: new this.$echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                  offset: 0,
                  color: 'rgba(235, 135, 13, 0.3)'
                }, {
                  offset: 0.8,
                  color: 'rgba(235, 135, 13, 0)'
                }], false),
                shadowColor: 'rgba(0, 0, 0, 0.1)',
                shadowBlur: 10
              }
            },
            itemStyle: {
              normal: {
                color: 'rgb(235, 135, 13)',
                borderColor: 'rgba(235, 135, 13,0.2)',
                borderWidth: 12

              }
            },
            data: this.data985
          }, {
            name: '211',
            type: 'line',
            smooth: true,
            symbol: 'circle',
            symbolSize: 5,
            showSymbol: false,
            lineStyle: {
              color: '#F1F1F3',
              normal: {
                width: 1
              }
            },
            areaStyle: {
              normal: {
                color: new this.$echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                  offset: 0,
                  color: 'rgba(91,189,44, 0.3)'
                }, {
                  offset: 0.8,
                  color: 'rgba(91,189,44, 0)'
                }], false),
                shadowColor: 'rgba(0, 0, 0, 0.1)',
                shadowBlur: 10
              }
            },
            itemStyle: {
              normal: {

                color: 'rgb(91,189,44)',
                borderColor: 'rgba(91,189,44,0.2)',
                borderWidth: 12
              }
            },
            data: this.data211
          },
            {
              name: '一本',
              type: 'line',
              smooth: true,
              symbol: 'circle',
              symbolSize: 5,
              showSymbol: false,
              lineStyle: {
                normal: {
                  width: 1
                }
              },
              areaStyle: {
                normal: {
                  color: new this.$echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                    offset: 0,
                    color: 'rgba(249, 245, 0, 0.3)'
                  }, {
                    offset: 0.8,
                    color: 'rgba(249, 245, 0, 0)'
                  }], false),
                  shadowColor: 'rgba(0, 0, 0, 0.1)',
                  shadowBlur: 10
                }
              },
              itemStyle: {
                normal: {
                  color: 'rgb(249, 245, 0)',
                  borderColor: 'rgba(249, 245, 0,0.27)',
                  borderWidth: 12

                }
              },
              data: this.dataNomal
            },
            {
              name: '二本',
              type: 'line',
              smooth: true,
              symbol: 'circle',
              symbolSize: 5,
              showSymbol: false,
              lineStyle: {
                normal: {
                  width: 1
                }
              },
              areaStyle: {
                normal: {
                  color: new this.$echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                    offset: 0,
                    color: 'rgba(0,166, 174, 0.3)'
                  }, {
                    offset: 0.8,
                    color: 'rgba(0,166, 174, 0)'
                  }], false),
                  shadowColor: 'rgba(0, 0, 0, 0.1)',
                  shadowBlur: 10
                }
              },
              itemStyle: {
                normal: {
                  color: 'rgb(0,166, 174)',
                  borderColor: 'rgba(0,166, 174,0.27)',
                  borderWidth: 12

                }
              },
              data: this.dataLowNomal
            }]
        });

      },
      setoptin1setoptin1() {
        // 绘制图表
        this.mychart.setOption({
          color: ['#07b5f1', '#008bf3'],
          title: {
            text: 'QQ Show',
            subtext: '',
            x: 'center',
            textStyle: {
              color: '#fff'
            }
          },
          tooltip: {
            trigger: 'axis',
            axisPointer: {
              animation: false
            }
          },
          legend: {
            data: ['点赞数', '评论数'],
            x: 'left',
            textStyle: {
              color: '#fff'
            }
          },
          toolbox: {
            feature: {
              dataZoom: {
                yAxisIndex: 'none'
              },
              restore: {},
              saveAsImage: {}
            }
          },
          axisPointer: {
            link: {xAxisIndex: 'all'}
          },

          grid: [{
            left: 50,
            right: 50,
            height: '35%'
          }, {
            left: 50,
            right: 50,
            top: '55.5%',
            height: '35%'
          }],
          xAxis: [
            {
              type: 'category',
              boundaryGap: false,
              data: this.xdata,
              axisLine: {
                // onZero: true,
                lineStyle: {
                  color: '#fff'
                }
              }
            },
            {
              gridIndex: 1,
              type: 'category',
              boundaryGap: false,

              data: this.xdata,
              position: 'top',
              axisLine: {
                // onZero: true,
                lineStyle: {
                  color: '#fff'
                }
              }
            }
          ],
          yAxis: [
            {
              name: '点赞数',
              type: 'value',
              // max: 500,
              axisLine: {
                lineStyle: {
                  color: '#fff'
                }
              }
            },
            {
              gridIndex: 1,
              name: '评论数',
              type: 'value',
              inverse: true,
              axisLine: {
                lineStyle: {
                  color: '#fff'
                }
              }
            }
          ],
          series: [
            {
              name: '点赞数',
              type: 'line',
              symbolSize: 8,
              hoverAnimation: false,
              data: this.data
            },
            {
              name: '评论数',
              type: 'line',
              xAxisIndex: 1,
              yAxisIndex: 1,
              symbolSize: 8,
              hoverAnimation: false,
              data: this.data
            }
          ]
        })
      },
      setoptin() {
        // 绘制图表
        this.mychart.setOption({
          title: {
            text: 'QQ Show',
            x: 'center',
            textStyle: { //设置主标题风格
              color: '#fff',//设置主标题字体颜色
            }
          },

          color: '#07b5f1',
          xAxis: {
            type: 'category',
            data: this.xdata,
            axisLine: {
              lineStyle: {
                color: '#fff'
              }
            }

          },
          yAxis: {
            type: 'value',
            axisLine: {
              lineStyle: {
                color: '#fff'
              }
            }

          },
          series: [{
            data: this.data,
            type: 'line'
          }]
        });
      },
      onopen(){
        console.log('WebSocket open');//成功连接上Websocket
        // setTimeout(this.sendMessage(),3000);
        sleep(6000)
        this.sendMessage()
      },
      onmessage(e){
        // console.log('message: ' + e.data);//打印出服务端返回过来的数据
        // console.log(JSON.parse(e.data).count)
        var obj = eval('(' + e.data + ')');
        // console.log(obj.count)
        // this.xdata.push( obj.name);
        this.dataTime = obj.date;
        this.total985 += obj['985'];
        this.total211 += obj['211'];
        this.totalC9 += obj['c9'];
        this.totalTop += obj['top'];
        this.totalBasic += obj['basic'];

        this.data985.push(Math.ceil(obj['985']));
        this.data211.push(Math.ceil(obj['211']));
        this.dataC9.push(Math.ceil(obj['c9']));
        this.dataNomal.push(Math.ceil(obj['top']));
        this.dataLowNomal.push(Math.ceil(obj['basic']));
        for (var i = 0; i < 5; i++) {
          if (this.sortedTotalData[i].name === 'C9高校') {
            this.sortedTotalData[i].value = this.totalC9;
          } else if (this.sortedTotalData[i].name === '985高校') {
            this.sortedTotalData[i].value = this.total985;
          } else if (this.sortedTotalData[i].name === '211高校') {
            this.sortedTotalData[i].value = this.total211;
          } else if (this.sortedTotalData[i].name === '普通一本高校') {
            this.sortedTotalData[i].value = this.totalTop;
          } else if (this.sortedTotalData[i].name === '普通二本高校') {
            this.sortedTotalData[i].value = this.totalBasic;
          }
        }
      },
      connetWebSocket(){
        /*创建socket连接*/
        let msg = '';
        if (window.s) {
          window.s.close()
        }
        this.webSocket = new WebSocket("ws://127.0.0.1:8000/echo");
        this.webSocket.onopen = this.onopen;
        this.webSocket.onmessage = this.onmessage;
        // Call onopen directly if socket is already open
        if (this.webSocket.readyState == WebSocket.OPEN) this.webSocket.onopen();
        window.s = this.webSocket;
        // setTimeout(this.sendMessage(),4000)
      },
      sendMessage(){
        // console.log(this.webSocket.readyState);
        if (this.webSocket.readyState == 1) {
          if (!window.s) {
            alert("websocket未连接.");
          } else {
            window.s.send("websocket");//通过websocket发送数据
          }
        } else {
          console.log("websocket正在连接");
        }

      },
      closeConnect(){
        window.s.send("1");
        if (window.s) {
          window.s.close();//关闭websocket
          console.log('websocket已关闭');
        }
      }
    },
    created(){

    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .test {

  }

  .total_dom {
    width: 80%;
    display: block;
    margin: 40px auto;
    border: solid 2px #cfd1d1;
    border-radius: 5px;
    height: 50px;
    font-size: 20px;
    color: white;
  }
</style>
