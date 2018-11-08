<template>
  <div>
    <div class="navbar navbar-fixed-top" style="width:100%;background-color: #001a3d; text-align:center">
      <h1 class="navbar-brand navbar-brand-name" id="show" style="color: white">一分钟看懂你的好友的关系图</h1>
    </div>
    <div id="myChart" :style="{width: '1000px', height: '900px',margin:'0px auto'}"></div>
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
        mychart:"",
        nodes:[],
        collectNodesName:{},
        links:[],
        updateFlag:1
      }
    },
    watch:{
      updateFlag:function (newVal, oldVal) {
        this.setoption();
      }
    },
    mounted(){
      this.connetWebSocket();
      this.draw();
      // setInterval(this.inputMessage,1000);
    },
    methods: {
      draw(){
        this.mychart = this.$echarts.init(document.getElementById('myChart'));
        this.setoption();
      },
      setoption(){
        var webkitDep = {
          "type": "force",
          "categories": [//关系网类别，可以写多组
            {
              "name": "好友关系",//关系网名称
              "keyword": {},
              "base": "好友关系"
            }
          ],
          "nodes": this.nodes,
          //   [//展示的节点
          //   {
          //     "name": "刘烨",//节点名称
          //     "value": 1,
          //     "category": 0//与关系网类别索引对应，此处只有一个关系网所以这里写0
          //   },
          //   {
          //     "name": "霓娜",
          //     "value": 50,
          //     "category": 0
          //   },
          //   {
          //     "name": "诺一",
          //     "value": 30,
          //     "category": 0
          //   }
          // ],
          "links": this.links
          //   [//节点之间连接
          //   {
          //     "source": 0,//起始节点，0表示第一个节点
          //     "target": 1 //目标节点，1表示与索引为1的节点进行连接
          //   },
          //   {
          //     "source": 1,
          //     "target": 2
          //   },
          //   {
          //     "source": 1,
          //     "target": 2
          //   }
          //
          // ]
        };
        var option = {
          title: {
            text: '好友关系图',
            subtext: '好友的生命图',
            top: 'top',
            left: 'center',
            textStyle:{
              color: '#F1F1F3'
            }
          },
          color:"#07b5f1",
          legend: {
            data: ['好友关系'],//此处的数据必须和关系网类别中name相对应
            top:50,
            textStyle:{
              color: '#F1F1F3'
            }
          },
          series: [{
            type: 'graph',
            layout: 'force',
            color:"#07b5f1",
            animation: false,
            label: {
              normal: {
                show:true,
                position: 'right',
                color: '#07b5f1'
              }
            },
            draggable: true,
            data: webkitDep.nodes.map(function (node, idx) {
              node.id = idx;
              return node;
            }),
            categories: webkitDep.categories,
            force: {
              edgeLength: 105,//连线的长度
              repulsion: 100  //子节点之间的间距
            },
            edges: webkitDep.links
          }]
        };
        this.mychart.setOption(option);
      },
      setNods(node_name){
        var node = {
          "name": node_name,//节点名称
          "value": 1,
          "category": 0,//与关系网类别索引对应，此处只有一个关系网所以这里写0
          "symbol": 'image://https://gss0.bdstatic.com/-4o3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike150%2C5%2C5%2C150%2C50/sign=6b03dae80746f21fdd395601974d0005/cb8065380cd791232b140067a0345982b2b78029.jpg',
          "symbolSize":50
          // "symbol": 'image://../images/me.png  src/assets/a.jpg'
        };
        this.nodes.push(node);
      },
      setLinks(source_name,target_name){
        var link = {
          "source": this.collectNodesName[source_name],
          "target": this.collectNodesName[target_name]
        };
        this.links.push(link)
      },
      judgeTargetNode(obj){
        //这部分是links需要连接的那个node
        if (!!this.collectNodesName[this.translation(obj.target_name)]){//已经存在这个需要连接的node
          this.setLinks(this.translation(obj.source_name),this.translation(obj.target_name))
        } else {//不存在这个需要连接的node
          this.collectNodesName[this.translation(obj.target_name)] = this.nodes.length;//记录这个node的名称与 在nodes中的位置
          this.setNods(this.translation(obj.target_name));
          this.setLinks(this.translation(obj.source_name),this.translation(obj.target_name))

        }
      },
      translation(data){//转中文
        var str = data.replace(/(\\u)(\w{1,4})/gi,function($0){
          return (String.fromCharCode(parseInt((escape($0).replace(/(%5Cu)(\w{1,4})/g,"$2")),16)));
        });
        return str;
      },
      onopen(){
        console.log('WebSocket open');//成功连接上Websocket
        // setTimeout(this.sendMessage(),3000);
        sleep(8000);
        this.sendMessage()
      },
      onmessage(e){

        var list = e.data;
        for (var i = 0 ; i < list.length ; i++){
          if (!!this.collectNodesName[this.translation(list[i].source_name)]){//已经存在这个原始node
            //这部分是links需要连接的那个node
              this.judgeTargetNode(list[i])
          }else {//不存在这个原始node
              this.collectNodesName[this.translation(list[i].source_name)] = this.nodes.length;//记录这个node的名称与位置
              this.setNods(this.translation(list[i].source_name));
              //这部分是links需要连接的那个node
              this.judgeTargetNode(list[i])
          }
        }
        this.updateFlag++;
        // console.log(e.data);
        // var obj = eval('(' + e.data + ')');
        // if (!!this.collectNodesName[this.translation(obj.source_name)]){//已经存在这个原始node
        //   //这部分是links需要连接的那个node
        //     this.judgeTargetNode(obj)
        // }else {//不存在这个原始node
        //     this.collectNodesName[this.translation(obj.source_name)] = this.nodes.length;//记录这个node的名称与位置
        //     this.setNods(this.translation(obj.source_name));
        //     //这部分是links需要连接的那个node
        //     this.judgeTargetNode(obj)
        // }
        // console.log(this.nodes)
      },
      connetWebSocket(){
        /*创建socket连接*/
        let msg = '';
        if (window.s) {
          window.s.close()
        }
        this.webSocket = new WebSocket("ws://127.0.0.1:8000/echo_relationship");
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
    }
  }
</script>

<style scoped>

</style>
