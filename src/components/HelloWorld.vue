<template>
  <div>
    <div class="navbar navbar-fixed-top" style="width:100%;background-color: #001a3d; text-align:center" >
      <h1 class="navbar-brand navbar-brand-name" id="show" style="color: white">QQ Show </h1>
      <!--<i class="fa fa-square-o"></i><font color="#fff">-->
      <!--<button type="button" id="send_message" @click="sendMessage">发送 message</button>-->
      <!--<button type="button" id="close_websocket" @click = closeConnect>关闭 websocket</button>-->
    </div>
    <div id="myChart" :style="{width: '1300px', height: '430px',margin:'0 auto'}"></div>
  </div>

</template>

<script>

  export default {
    name: 'hello',
    data () {
      return {
        msg: 'Welcome to Your Vue.js App',
        dataC9:[5000],
        data211:[5000],
        data985:[5000],
        dataNomal:[5000],
        dataLowNomal:[5000],
        xdata:[],
        mychart: "",
        timerClock:1000,
        webSocket:''
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
      data:function (newVal, oldVal) {
          this.setoptin1setoptin1();
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
        this.dataC9.push(num1);this.data211.push(num2);
        this.data985.push(num3);this.dataNomal.push(num4);this.dataLowNomal.push(num5);
        if (this.data.length >= 1001) {
          this.data.splice(0, 1);
          this.xdata.splice(0, 1);
          this.timerClock += 1;
          this.xdata.push(this.timerClock);
        }
      },
      drawLine() {
        // 基于准备好的dom，初始化echarts实例
        this.mychart = this.$echarts.init(document.getElementById('myChart'))
        this.setoptinManyLin()
      },
      setoptinManyLin(){
        this.mychart.setOption({
          backgroundColor: '#394056',
          title: {
            text: '请求数',
            textStyle: {
              fontWeight: 'normal',
              fontSize: 16,
              color: '#F1F1F3'
            },
            left: '6%'
          },
          tooltip: {
            trigger: 'axis',
            axisPointer: {
              lineStyle: {
                color: '#57617B'
              }
            }
          },
          legend: {
            icon: 'rect',
            itemWidth: 14,
            itemHeight: 5,
            itemGap: 13,
            data: ['C9', '211', '985','一本','二本'],
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
                color: '#57617B'
              }
            },
            data: ['13:00', '13:05', '13:10', '13:15', '13:20', '13:25', '13:30', '13:35', '13:40', '13:45', '13:50', '13:55']
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
            data: ['', '', '', '', '', '', '', '', '', '', {
              value: '周六',
              textStyle: {
                align: 'left'
              }
            }, '周日']
          }],
          yAxis: [{
            type: 'value',
            name: '单位（%）',
            axisTick: {
              show: false
            },
            axisLine: {
              lineStyle: {
                color: '#57617B'
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
            data: [220, 182, 191, 134, 150, 120, 110, 125, 145, 122, 165, 122]
          }, {
            name: '985',
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
            data: [120, 110, 125, 145, 122, 165, 122, 220, 182, 191, 134, 150]
          }, {
            name: '211',
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
            data: [220, 182, 125, 145, 122, 191, 134, 150, 120, 110, 165, 122]
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
              data: [182, 134, 191, 145, 110, 120, 145, 122, 145, 122, 145, 122]
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
              data: [213, 134, 191, 234, 110, 111, 145, 24, 145, 122, 145, 122]
            }]
        });

      },
      setoptin1setoptin1() {
        // 绘制图表
        this.mychart.setOption({
          color: ['#07b5f1','#008bf3'],
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
        this.sendMessage()
      },
      onmessage(e){
        // console.log('message: ' + e.data);//打印出服务端返回过来的数据
        // console.log(this)
        this.data.push(e.data);
        if (this.data.length >= 1001) {
          this.data.splice(0, 1);
          this.xdata.splice(0, 1);
          this.timerClock += 1;
          this.xdata.push(this.timerClock);
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
        }else {
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
</style>
