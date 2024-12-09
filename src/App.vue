<template>
  <div class="main">
    <el-button type="primary" @click="console.log(allTds)">
      打印数据
    </el-button>
    <ul class="one">
      <li class="shear" @click="shear" title="剪切"><i class="icon iconfont icon-msnui-cut-file"></i></li>
      <li class="copy" @click="copy" title="复制"><i class="icon iconfont icon-fuzhi_fuzhi"></i></li>
      <li class="paste" @click="paste" title="粘贴"><i class="icon iconfont icon-niantie"></i></li>
      <li class="bor" style="width: 1px">|</li>
      <li class="" @click="addFun" title="计算公式"><i class="icon iconfont icon-kmd"></i></li>
      <li class="readOnly" @click="readOnly" title="固定表格项"><i class="icon iconfont icon-suozi"></i></li>
      <li class="containLi" @click.stop="containLi('small_ul_one')" title="增删行列" style="width: 50px">
        <span><i class="icon iconfont icon-shanchulie"></i></span>
        <span>
          <i style="font-size:16px " class="icon iconfont icon-xiajiantou"></i>
        </span>
        <ul v-show="small_ul_one">
          <li @click.stop="addRow" class="addRow"><i class="icon iconfont icon-charuxing"></i>插入行</li>
          <li @click.stop="addCol" class="addCol"><i class="icon iconfont icon-charulie"></i>插入列</li>
          <li @click.stop="deleteRow" class="deleteRow"><i class="icon iconfont icon-shanchuxing"></i>删除行</li>
          <li @click.stop="deleteCol" class="deleteCol"><i class="icon iconfont icon-shanchulie"></i>删除列</li>
        </ul>
      </li>
      <li @click="merge" class="merge" title="合并/拆分单元格"><i class="icon iconfont icon-hebingdanyuange"></i></li>
      <!-- <li class="split" title="拆分单元格"><i class="icon iconfont icon-quxiaohebingdanyuange"></i></li> -->
      <li class="containLi" title="隐藏单元格" style="width: 90px;display: none">
        <i class="icon iconfont "></i>
        <span>隐藏内容</span>
        <span>
          <i style="font-size:16px " class="icon iconfont icon-xiajiantou"></i>
        </span>
        <ul style="text-align: center;" v-show="small_ul_two">
          <li>tab栏可见</li>
          <li>列表头可见</li>
          <li>行表头可见</li>
          <li>新建表页可见</li>
        </ul>
      </li>
      <li class="bor" style="width: 1px">|</li>
      <li class="containLi" @click.stop="containLi('small_ul_three')" title="控件类型" style="width: 50px">
        <span><i class="icon iconfont icon-kongjian"></i></span>
        <span>
          <i style="font-size:16px " class="icon iconfont icon-xiajiantou"></i>
        </span>
        <ul v-show="small_ul_three">
          <li @click.stop="isData" class="isData"><i class="icon iconfont icon-riqi"></i>日期控件</li>
          <li @click.stop="isSelect" class="isSelect"><i class="icon iconfont icon-duoxuanxialakuang"></i>下拉控件</li>
          <li @click.stop="isOne" class="isOne"><i class="icon iconfont icon-danxuananniu"></i>单选控件</li>
          <li @click.stop="isMore" class="isMore"><i class="icon iconfont icon-fuxuan"></i>复选控件</li>
        </ul>
      </li>
    </ul>
    <ul class="two">
      <li style="width: 100px">
        <i class="icon iconfont"></i>
        <select class="typeFont" @change="typeFont" name="" id="">
          <option value="SimSun">宋体</option>
          <option value="SimHei">黑体</option>
          <option value="Microsoft YaHei">微软雅黑</option>
          <option value="Microsoft JhengHei">微软正黑体</option>
          <option value="NSimSun">新宋体</option>
          <option value="PMingLiU">新细明体</option>
          <option value="DFKai-SB">标楷体</option>
          <option value="FangSong">仿宋</option>
          <option value="KaiTi">楷体</option>
          <option value="Times New Roman">新罗马字体</option>
        </select>
      </li>
      <li style="width: 60px">
        <i class="icon iconfont"></i>
        <select @change="typeFontSize" name="" id="" class="typeFontSize">
          <option value="10px">11</option>
          <option value="12px">12</option>
          <option value="14px">13</option>
          <option value="16px">14</option>
          <option value="18px">15</option>
          <option value="20px">16</option>
          <option value="22px">17</option>
        </select>
      </li>
      <li class="addFont" @click="addFont" title="字号加"><i class="icon iconfont icon-boshiweb_jiazihao"></i></li>
      <li class="reduceFont" @click="reduceFont" title="字号减"><i class="icon iconfont icon-boshiweb_jianzihao"></i></li>
      <li class="blod" @click="blod" title="加粗"><i class="icon iconfont icon-jiacu"></i></li>
      <li class="italic" @click="italic" title="斜体"><i class="icon iconfont icon-xieti"></i></li>
      <li class="underline" @click="underline" title="下划线"><i class="icon iconfont icon-icxiahuaxian24px"></i></li>
      <li title="对齐方式" @click.stop="containLi('small_ul_four')" class="containLi" style="width: 50px">
        <span><i class="icon iconfont icon-zuoduiqi"></i></span>
        <span>
          <i style="font-size:16px " class="icon iconfont icon-xiajiantou"></i>
        </span>
        <ul v-show="small_ul_four">
          <li @click.stop="align" _name="textAlign" value="left"><i class="icon iconfont icon-zuoduiqi"></i>左对齐</li>
          <li @click.stop="align" _name="textAlign" value="center"><i class="icon iconfont icon-alignmiddle"></i>居中对齐</li>
          <li @click.stop="align" _name="textAlign" value="right"><i class="icon iconfont icon-youduiqi"></i>右对齐</li>
          <li @click.stop="align" _name="verticalAlign" value="top"><i class="icon iconfont icon-jushang"></i>垂直居上</li>
          <li @click.stop="align" _name="verticalAlign" value="middle"><i class="icon iconfont icon-juzhong"></i>垂直居中</li>
          <li @click.stop="align" _name="verticalAlign" value="bottom"><i class="icon iconfont icon-juxia"></i>垂直居下</li>
        </ul>
      </li>
      <li title="边框" @click.stop="containLi('small_ul_five')" class="containLi" style="width: 50px">
        <span><i class="icon iconfont icon-suoyoubiankuang"></i></span>
        <span>
          <i style="font-size:16px " class="icon iconfont icon-xiajiantou"></i>
        </span>
        <ul v-show="small_ul_five">
          <li @click.stop="allBorder" class="allBorder"><i class="icon iconfont icon-suoyoubiankuang"></i>全部边框</li>
          <!-- <li @click.stop="allBorder" class="allBorder" ><i class="icon iconfont icon-waibiankuang"></i>外边框</li> -->
          <li @click.stop="leftBorder" class="leftBorder"><i class="icon iconfont icon-zuobiankuang"></i>左边框</li>
          <li @click.stop="topBorder" class="topBorder"><i class="icon iconfont icon-shangbiankuang"></i>上边框</li>
          <li @click.stop="rightBorder" class="rightBorder"><i class="icon iconfont icon-youbiankuang"></i>右边框</li>
          <li @click.stop="bottomBorder" class="bottomBorder"><i class="icon iconfont icon-xiabiankuang"></i>底部边框</li>
          <li @click.stop="noneBorder" class="noneBorder"><i class="icon iconfont icon-wubiankuang"></i>无边框</li>
        </ul>
      </li>
      <!-- <li title="文字方向"><i class="icon iconfont icon-wenzifangxiang"></i></li> -->
      <li style="margin-top:0px;" class="choiceColor" title="单元格背景色">
        <!-- <i class="icon iconfont icon-beijingse cp1"></i> -->
        <el-color-picker @change="changeBackgroundColor" size="small" v-model="backgroundColor" recommend />
      </li>
      <li style="margin-top:0px;margin-left:20px;" class="choiceColor isFont" title="字体颜色">
        <!-- <i class="icon iconfont icon-wenzibeijingse cp2"></i> -->
        <el-color-picker @change="changeColor" size="small" v-model="Color" recommend />
      </li>
    </ul>
    <!-- 公式 -->
    <div class="div" v-show="inputDiv" style="textAlign:left">
      <el-input class="addFunInput" v-model="ruleMsg" placeholder="请输入合法公式" style="width: 300px"></el-input>
      <el-button size="small" @click="sureAddFun" type="info">确认</el-button>
      <el-button size="small" @click="noSureAdd" type="warning">取消</el-button>
      <el-button size="small" type="danger" @click="delFun">删除</el-button>
    </div>
    <!-- 表格 -->
    <div class="hello">
      <div v-show='activeDiv' :style=leftStyle style="width:0;" class="leftDiv all"></div>
      <div v-show='activeDiv' :style=rightStyle style="width:0;" class="rightdiv all"></div>
      <div v-show='activeDiv' :style=topStyle style="height:0;" class="topDiv all"></div>
      <div v-show='activeDiv' :style=bottomStyle style="height:0;" class="bottomDiv all"></div>
      <div class="columnResizer" @mousedown="columnResizerDown" @mouseup="columnResizerUp"></div>
      <div class="columnResizerLong" v-show="isColumnResizerLong" @mouseup="columnResizerUp"></div>
      <div class="rowResizer" @mousedown="rowResizerDown" @mouseup="columnResizerUp"></div>
      <div class="rowResizerLong" v-show="isRowResizerLong" @mouseup="columnResizerUp"></div>
      <table @mousemove="tableMove" @mouseup="columnResizerUp" :style="tableStyle" class="myTable">
        <thead>
          <tr>
            <td v-for="(td,tdIndex) in headTd" :key="tdIndex" @mouseover="headOver" :fromTd="tdIndex" :class="td.class" :style="td.ownStyle">
              {{td.value}}
            </td>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item,index) in allTds" :key="index">
            <td @click.stop="dj" @dblclick="sj" v-for="(tds,tdIndex) in item" :key="tdIndex" @blur="noEditor" @mousedown="mdown" @mouseover="mover" @mouseout="mout" @mouseup="mup" v-show="tds.ownMerge.isShow" :fromTr="index" :fromTd="tdIndex" :class="tds.class" :style="tds.ownStyle" :id="tds.newId" :rowspan="tds.ownMerge.rowspan" :colspan="tds.ownMerge.colspan">
              {{tds.value}}
              <el-date-picker v-model="tds.ownType.dataModel" v-if="tds.ownType.isData" type="date" value="yyyy-MM-dd" format="yyyy年MM月dd日" placeholder="Select date" style="width:100%" size="small"></el-date-picker>
              <el-select size="small" v-if="tds.ownType.isSelect" v-model="tds.ownType.selectModel" style="width:100%">
                <el-option v-for="item in tds.ownType.selectData" :value="item" :key="item">{{ item }}</el-option>
              </el-select>
              <el-radio-group size="small" v-if="tds.ownType.isOne" v-model="tds.ownType.oneModel">
                <el-radio v-for="(item,index) in tds.ownType.oneData" :label="item" :key="index"></el-radio>
              </el-radio-group>
              <el-radio-group size="small" v-if="tds.ownType.isMore" v-model="tds.ownType.moreModel">
                <el-radio v-for="(item,index) in tds.ownType.moreData" :label="item" :key="index"></el-radio>
              </el-radio-group>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import math from 'mathjs';
import jsonData from '@/static/tableData.js'

math.config({
  number: 'BigNumber'
});
export default {
  name: 'hello',
  data () {
    return {
      small_ul_one: false,
      small_ul_two: false,
      small_ul_three: false,
      small_ul_four: false,
      small_ul_five: false,
      backgroundColor: "#fff",
      Color: "#fff",
      headTd: [],
      allTds: [],
      copyArr: [],
      tdSort: "ABCDEFGHIJKLMNOPQRSTUVWXYZ",
      ruleMsg: '',
      inputDiv: false,
      isAddFun: false,
      isFocus: false,
      isCtrl: false,
      addFunPosition: [],
      timer: null,
      isMove: false,
      isColumnResizerLong: false,
      isRowResizerLong: false,
      oldxPosition: 0,
      oldyPosition: 0,
      tdCoordinateX: 0,
      tdCoordinateY: 0,
      activeDiv: false,
      columnResizerMove: true,
      rowResizerMove: true,
      tableColumnIsMove: false,
      tableRowIsMove: false,
      tableStyle: {},
      leftStyle: {
        height: '0px',
        left: 0,
        top: 0
      },
      rightStyle: {
        height: '0px',
        left: 0,
        top: 0
      },
      topStyle: {
        width: '0px',
        left: 0,
        top: 0
      },
      bottomStyle: {
        width: '0px',
        left: 0,
        top: 0
      },
      fontNum: 10,
      color1: '',
      seeDataItemTop: "编辑数据项",
      tabNoActive: false,
      gudingData: [],
      mingxiData: [],
      allGudingId: [],
      allMingxiId: []
    }
  },
  mounted () {
    this.$nextTick(function () {
      this.allTds = jsonData.alltds;
      this.headTd = jsonData.headTd;
      //设置初始table宽度
      var newTableWidth = 0;
      for (var j = 0, length2 = this.headTd.length; j < length2; j++) {
        var oneWidth = parseInt(this.headTd[j].ownStyle.width.substr(0, this.headTd[j].ownStyle.width.length - 2)) + 3;
        newTableWidth = newTableWidth + oneWidth;
      };
      newTableWidth = newTableWidth + 1 + "px";
      this.tableStyle.width = newTableWidth;
      //头部字母和左边排序
      this.allTdSort();
      var _this = this;
      //全局字母按键事件
      document.addEventListener('keyup', function (e) {
        var oEvent = window.event.keyCode;
        // ctrl放开
        if (oEvent == 17) {
          _this.isCtrl = false;
        }
      })
      document.addEventListener("keydown", function (e) {
        var oEvent = window.event;
        if (oEvent.keyCode == 88 && oEvent.ctrlKey) {  //这里只能用alt，shift，ctrl等去组合其他键event.altKey、event.ctrlKey、event.shiftKey 属性 
          //ctrl X 剪切
          _this.shear();
        }
        else if (oEvent.keyCode == 67 && oEvent.ctrlKey) {
          //ctrl C 复制
          _this.copy();
        } else if (oEvent.keyCode == 86 && oEvent.ctrlKey) {
          //ctrl V 粘贴
          _this.paste();
        }
        else if (oEvent.keyCode == 37) {
          //左箭头
          var a = document.querySelector('.isActive');
          if (a) {
            a.previousSibling.click();
          }
        } else if (oEvent.keyCode == 39) {
          //右箭头
          var a = document.querySelector('.isActive');
          if (a) {
            a.nextSibling.click();
          }
        } else if (oEvent.keyCode == 38) {
          //上箭头
          var a = document.querySelector('.isActive');
          if (a) {
            var one = a.getAttribute('fromtr');//获取到td的位置
            var two = a.getAttribute('fromtd');
            document.querySelectorAll('tbody tr')[one - 1].childNodes[two].click();
          }
        } else if (oEvent.keyCode == 40) {
          //下箭头
          var a = document.querySelector('.isActive');
          if (a) {
            var one = a.getAttribute('fromtr');//获取到td的位置
            var two = a.getAttribute('fromtd');
            document.querySelectorAll('tbody tr')[one - 1 + 2].childNodes[two].click();
          }
        } else if (oEvent.keyCode == 13) {
          //回车
          var a = document.querySelector('[isedit="1"]');
          a.setAttribute("contenteditable", "false");
          a.click();
        } else if (oEvent.keyCode == 46) {
          //delete
          var allArea = document.querySelectorAll('.area');
          for (var k = 0, length3 = allArea.length; k < length3; k++) {
            var one = allArea[k].getAttribute('fromtr');
            var two = allArea[k].getAttribute('fromtd');
            _this.allTds[one][two].ownFun = "";
            _this.allTds[one][two].value = "";
            _this.allTds[one][two].class.noDbClick = false;
          };
          var oneArr = document.getElementsByClassName('isActive')[0];
          if (oneArr) {
            var one = oneArr.getAttribute('fromtr');
            var two = oneArr.getAttribute('fromtd');
            _this.allTds[one][two].ownFun = "";
            _this.allTds[one][two].value = "";
            _this.allTds[one][two].class.noDbClick = false;
          };
          //重新计算所有单元格内容
          for (var j = 0, length2 = _this.allTds.length; j < length2; j++) {
            for (var k = 1, length3 = _this.allTds[j].length; k < length3; k++) {
              if (_this.allTds[j][k].ownFun) {
                //获取当前公式
                var msg = _this.allTds[j][k].ownFun.trim().replace(/ /g, "").toLocaleUpperCase();
                //把公式中字母换成数字
                for (var l = 0, length2 = _this.allTds.length; l < length2; l++) {
                  for (var m = 1, length3 = _this.allTds[l].length; m < length3; m++) {
                    msg = msg.replace(_this.allTds[l][m].newId, _this.allTds[l][m].value);
                  }
                };
                try {
                  var newValue = math.eval(msg).toString();
                } catch (error) {
                  _this.$Message.warning('请输入正确公式');
                };
                _this.allTds[j][k].value = newValue;
                var tdEq = _this.allTds[0].length * (j + 1) + k;
                document.getElementsByTagName('td')[tdEq].innerText = newValue;
              }
            }
          };
        } else if (oEvent.keyCode == 17) {
          //按下回车
          _this.isCtrl = true;
        }
        else {
          var a = document.querySelector('.isActive');
          if (a && _this.isAddFun == false) {
            clearTimeout(_this.timer);
            //把选中区域去掉
            var one = a.getAttribute('fromtr');//获取到td的位置
            var two = a.getAttribute('fromtd');
            if (_this.allTds[one][two].class.isClick && _this.allTds[one][two].class.isDbClick) {
              for (var j = 0, length2 = _this.allTds.length; j < length2; j++) {
                for (var k = 0, length3 = _this.allTds[j].length; k < length3; k++) {
                  _this.allTds[j][k].class.area = false;
                  _this.allTds[j][k].class.isActive = false;
                }
              };
              _this.activeDiv = false;
              //更新当前单元格的点击信息，使得单击无效
              a.setAttribute('isEdit', '1');
              var two = a.getAttribute('fromtd');
              a.setAttribute("contenteditable", "true");
              a.focus();
            }
          }
        }
      });
      document.querySelector('body').addEventListener('click', function () {
        _this.small_ul_one = false;
        _this.small_ul_two = false;
        _this.small_ul_three = false;
        _this.small_ul_four = false;
        _this.small_ul_five = false;
      });
    });


    //date时间转换
    // console.log(this.allTds[0])
    // for(var k = 0, length3 = this.allTds.length; k < length3; k++){
    //  for(var j = 0, length2 = this.allTds[k].length; j < length2; j++){
    //    // this.allTds[k][j]
    //    var trueDateModel = this.allTds[k][j].ownType.dataModel;
    //    if (trueDateModel!="") {
    //      console.log(trueDateModel)
    //    trueDateModel = this.formatDate(trueDateModel);
    //    console.log(trueDateModel)
    //    }
    //  }
    // }
  },
  methods: {
    setKey(obj, key, value) {
      obj[key] = value;
    },
    allTdSort (a) {
      //头部td
      for (var j = 1, length2 = this.headTd.length; j < length2; j++) {
        this.headTd[j].value = this.tdSort[j - 1];
      };

      for (var j = 0, length2 = this.allTds.length; j < length2; j++) {
        this.allTds[j][0].value = j + 1;//左边td排序
        //每个单元格赋值id
        for (var k = 1, length3 = this.allTds[j].length; k < length3; k++) {
          var newId = this.tdSort[k - 1] + (j + 1);
          this.allTds[j][k].newId = newId;
        }
      };
    },
    dj (a) {
      //单击事件
      clearTimeout(this.timer);
      this.timer = setTimeout(() => {
        var one = a.srcElement.getAttribute('fromtr');//获取到td的位置
        var two = a.srcElement.getAttribute('fromtd');
        //判断当前单元格能否点击
        if (this.allTds[one][two].class.isClick) {
          //判断如果不是添加公式状态就是单击效果，如果是则添加背景色
          if (!this.isAddFun) {
            //判断是否是ctrl多选
            if (this.isCtrl) {
              this.setKey(this.allTds[one][two].class, 'ctrlActive', true);
              // this.allTds[one][two].class.ctrlActive = true;
            } else {
              //设置选中样式
              this.leftStyle = {
                height: a.target.offsetHeight + 'px',
                left: a.target.offsetLeft - 1 + 'px',
                top: a.target.offsetTop + 'px'
              };
              this.rightStyle = {
                height: a.target.offsetHeight + 'px',
                left: a.target.offsetLeft + a.target.offsetWidth + 'px',
                top: a.target.offsetTop + 'px'
              }
              this.topStyle = {
                width: a.target.offsetWidth + 'px',
                left: a.target.offsetLeft + 'px',
                top: a.target.offsetTop + 'px'
              }
              this.bottomStyle = {
                width: a.target.offsetWidth + 'px',
                left: a.target.offsetLeft + 'px',
                top: a.target.offsetTop + a.target.offsetHeight + 'px'
              }
              if (a.target.getAttribute('isEdit') != 1) {
                this.activeDiv = true;
              }
              //把选中区域去掉
              for (var j = 0, length2 = this.allTds.length; j < length2; j++) {
                for (var k = 0, length3 = this.allTds[j].length; k < length3; k++) {
                  this.allTds[j][k].class.area = false;
                  this.allTds[j][k].class.isActive = false;
                }
              };
              var one = a.srcElement.getAttribute('fromtr');//获取到td的位置
              var two = a.srcElement.getAttribute('fromtd');
              this.allTds[one][two].class.isActive = true;
            }
          } else {
            var one = a.srcElement.getAttribute('fromtr');//获取到td的位置
            var two = a.srcElement.getAttribute('fromtd');
            if (this.addFunPosition[0] != one || this.addFunPosition[1] != two) {
              var thisId = a.srcElement.getAttribute('id');
              this.ruleMsg = this.ruleMsg + thisId;
              document.querySelector('.addFunInput input').focus();
              this.allTds[one][two].class.addFunArea = true;
            }
          }
        }
      }, 200);
    },
    sj (a) {
      //双击事件
      clearTimeout(this.timer);
      //把选中区域去掉
      var one = a.srcElement.getAttribute('fromtr');//获取到td的位置
      var two = a.srcElement.getAttribute('fromtd');
      if (this.allTds[one][two].class.isClick && this.allTds[one][two].class.isDbClick) {
        for (var j = 0, length2 = this.allTds.length; j < length2; j++) {
          for (var k = 0, length3 = this.allTds[j].length; k < length3; k++) {
            this.allTds[j][k].class.area = false;
            this.allTds[j][k].class.isActive = false;
          }
        };
        this.activeDiv = false;
        //更新当前单元格的点击信息，使得单击无效
        a.srcElement.setAttribute('isEdit', '1');
        var two = a.srcElement.getAttribute('fromtd');
        a.srcElement.setAttribute("contenteditable", "true");
        a.srcElement.focus();
        // 获取选定对象
        var selection = getSelection();
        // console.log(selection.getRangeAt(0));
        // 设置最后光标对象
        selection.extend(a.srcElement, "1");
        selection.collapseToEnd();
      }
    },
    noEditor (a) {
      a.target.setAttribute("contenteditable", "false");
      var one = a.srcElement.getAttribute('fromtr');//获取到td的位置
      var two = a.srcElement.getAttribute('fromtd');
      //跟新当前单元格的是否可以单击状态
      a.target.removeAttribute('isEdit');
      this.allTds[one][two].value = a.srcElement.innerText;
      //重新计算所有单元格内容
      for (var j = 0, length2 = this.allTds.length; j < length2; j++) {
        for (var k = 1, length3 = this.allTds[j].length; k < length3; k++) {
          if (this.allTds[j][k].ownFun) {
            //获取当前公式
            var msg = this.allTds[j][k].ownFun.trim().replace(/ /g, "").toLocaleUpperCase();
            //把公式中字母换成数字
            for (var l = 0, length2 = this.allTds.length; l < length2; l++) {
              for (var m = 1, length3 = this.allTds[l].length; m < length3; m++) {
                msg = msg.replace(this.allTds[l][m].newId, this.allTds[l][m].value);
              }
            };
            try {
              var newValue = math.eval(msg).toString();
            } catch (error) {
              this.$Message.warning('请输入正确公式');
            };
            this.allTds[j][k].value = newValue;
            var tdEq = this.allTds[0].length * (j + 1) + k;
            document.getElementsByTagName('td')[tdEq].innerText = newValue;
          }
        }
      };
    },
    mdown (a) {
      //鼠标按下

      this.isMove = true;//可移动
      if (!this.isAddFun) {
        this.activeDiv = false;
      }
      this.oldxPosition = a.x;//更新XY坐标
      this.oldyPosition = a.y;
      var one = a.srcElement.getAttribute('fromtr');//获取到td的位置
      var two = a.srcElement.getAttribute('fromtd');
      this.tdCoordinateX = one;//更新选中区域开头
      this.tdCoordinateY = two;
      for (var j = 0, length2 = this.allTds.length; j < length2; j++) {
        for (var k = 0, length3 = this.allTds[j].length; k < length3; k++) {
          this.allTds[j][k].class.area = false;
          if (!this.isAddFun) {
            this.allTds[j][k].class.isActive = false;
          }
        }
      };
    },
    mover (a) {
      // 鼠标移入
      var _this = this;
      //选中区域部分
      if (this.isMove) {
        var one = a.srcElement.getAttribute('fromtr');//获取到td的位置
        var two = a.srcElement.getAttribute('fromtd');
        for (var k = 0, length3 = _this.allTds.length; k < length3; k++) {
          //设置选中区域样式
          if (_this.tdCoordinateX <= k && k <= one) {
            for (var j = 0, length2 = _this.allTds[k].length; j < length2; j++) {
              if (_this.tdCoordinateY <= j && j <= two) {
                _this.allTds[k][j].class.area = true;
              }
            }
          } else if (one <= k && k <= _this.tdCoordinateX) {
            for (var j = 0, length2 = _this.allTds[k].length; j < length2; j++) {
              if (two <= j && j <= _this.tdCoordinateY) {
                _this.allTds[k][j].class.area = true;
              }
            }
          }
        };
      };
      //左侧调节高度部分
      var newTop = a.srcElement.offsetTop + a.srcElement.offsetHeight - 5;
      if (this.rowResizerMove && a.srcElement.getAttribute('fromtr') && a.srcElement.getAttribute('fromtd') == 0) {
        var two = a.srcElement.getAttribute('fromtr');
        document.getElementsByClassName('rowResizer')[0].setAttribute('clickTd', two);
        document.getElementsByClassName('rowResizer')[0].style.top = newTop + 'px';
        document.getElementsByClassName('rowResizerLong')[0].style.top = newTop + 4 + 'px';
      }
    },
    mout (a) {
      //鼠标移出事件
      var _this = this;
      if (this.isMove) {
        var one = a.srcElement.getAttribute('fromtr');//获取到td的位置
        var two = a.srcElement.getAttribute('fromtd');
        for (var j = 0, length2 = this.allTds.length; j < length2; j++) {
          for (var k = 0, length3 = this.allTds[j].length; k < length3; k++) {
            this.allTds[j][k].class.area = false;
          }
        };
      }
    },
    mup (a) {
      //鼠标松开
      this.isMove = false; //取消可移动
    },
    headOver (a) {
      //头部鼠标进入
      var newLeft = a.srcElement.offsetLeft + a.srcElement.offsetWidth - 5 + 'px';
      if (this.columnResizerMove && a.srcElement.getAttribute('fromtd') != 0) {
        var two = a.srcElement.getAttribute('fromtd');
        document.getElementsByClassName('columnResizer')[0].setAttribute('clickTd', two);
        document.getElementsByClassName('columnResizer')[0].style.left = newLeft;
        document.getElementsByClassName('columnResizerLong')[0].style.left = newLeft;
      }
    },
    tableMove (a) {
      if (this.tableColumnIsMove) {
        this.isColumnResizerLong = true;
        var _columnResizer = document.getElementsByClassName('columnResizer')[0];
        _columnResizer.style.background = '#AAAABB';
        var helloLeft = document.getElementsByClassName('hello')[0].offsetLeft;
        var bodyScrollLeft = document.body.scrollLeft;
        _columnResizer.style.left = a.x - helloLeft + bodyScrollLeft - 5 + 'px';
        document.getElementsByClassName('columnResizerLong')[0].style.left = a.x - helloLeft + bodyScrollLeft - 5 + 'px';
      } else if (this.tableRowIsMove) {
        this.isRowResizerLong = true;
        var _rowResizer = document.getElementsByClassName('rowResizer')[0];
        _rowResizer.style.background = '#AAAABB';
        var helloTop = document.getElementsByClassName('hello')[0].offsetTop;
        var bodyScrollTop = document.documentElement.scrollTop;
        _rowResizer.style.top = a.y - helloTop + bodyScrollTop + 'px';
        document.getElementsByClassName('rowResizerLong')[0].style.top = a.y - helloTop + bodyScrollTop + 'px';
      }
    },
    columnResizerDown (a) {
      //头部宽度调节条按下
      this.columnResizerMove = false;
      this.tableColumnIsMove = true;
      this.activeDiv = false;
    },
    rowResizerDown () {
      //左侧高度调节按下
      this.rowResizerMove = false;
      this.tableRowIsMove = true;
      this.activeDiv = false;
    },
    columnResizerUp (a) {
      //头部宽度调节条放开
      if (this.tableColumnIsMove) {
        this.columnResizerMove = true;
        this.tableColumnIsMove = false;
        this.isColumnResizerLong = false;
        var bodyScrollLeft = document.body.scrollLeft;
        document.getElementsByClassName('columnResizer')[0].style.background = '#eee';
        var tdNum = document.getElementsByClassName('columnResizer')[0].getAttribute('clickTd');
        var helloLeft = document.getElementsByClassName('hello')[0].offsetLeft;
        var tdLeft = document.getElementsByClassName('headTd')[tdNum].offsetLeft;
        var newWidth = a.x - helloLeft - tdLeft + bodyScrollLeft + 'px';
        this.headTd[tdNum].ownStyle.width = newWidth;
        //重置table宽度
        var newTableWidth = 0;
        for (var j = 0, length2 = this.headTd.length; j < length2; j++) {
          var oneWidth = parseInt(this.headTd[j].ownStyle.width.substr(0, this.headTd[j].ownStyle.width.length - 2)) + 3;
          newTableWidth = newTableWidth + oneWidth;
        };
        newTableWidth = newTableWidth + 1 + "px";
        this.tableStyle.width = newTableWidth;
      } else if (this.tableRowIsMove) {
        this.rowResizerMove = true;
        this.tableRowIsMove = false;
        this.isRowResizerLong = false;
        var bodyScrollTop = document.documentElement.scrollTop;
        document.getElementsByClassName('rowResizer')[0].style.background = '#eee';
        var trNum = document.getElementsByClassName('rowResizer')[0].getAttribute('clickTd');
        var helloTop = document.getElementsByClassName('hello')[0].offsetTop;
        var tdTop = document.getElementsByClassName('leftTd')[trNum].offsetTop;
        var newHeight = a.y - helloTop - tdTop + bodyScrollTop + 'px';
        this.allTds[trNum][0].ownStyle.height = newHeight;
      }
    },
    addFun () {
      //获取到被点击到的单元格
      var activeTd = document.getElementsByClassName('isActive')[0];
      if (activeTd) {
        this.isAddFun = true;
        var one = activeTd.getAttribute('fromtr');
        var two = activeTd.getAttribute('fromtd');
        //更新当前需要添加公式的单元格位置
        this.addFunPosition.push(one, two);
        this.inputDiv = true;
        this.ruleMsg = this.allTds[one][two].ownFun;
        document.querySelector('.addFunInput input').focus();
      } else {
        this.$Message.warning('请选择一个单元格');
      }
    },
    sureAddFun () {
      //获取当前公式
      var msg = this.ruleMsg.trim().replace(/ /g, "").toLocaleUpperCase();
      //更新标准公式内容
      this.ruleMsg = msg;
      //把公式中字母换成数字
      for (var j = 0, length2 = this.allTds.length; j < length2; j++) {
        for (var k = 1, length3 = this.allTds[j].length; k < length3; k++) {
          msg = msg.replace(this.allTds[j][k].newId, this.allTds[j][k].value);
        }
      };
      try {
        var newValue = math.eval(msg).toString();
      } catch (error) {
        this.$Message.warning('请输入正确公式');
      };
      var one = this.addFunPosition[0];
      var two = this.addFunPosition[1];
      //获取到计算后的内容
      this.allTds[one][two].value = newValue;
      //把当前公式内容绑定到对应单元格
      this.allTds[one][two].ownFun = this.ruleMsg;
      //把当前单元格变为不可编辑状态
      this.allTds[one][two].class.noDbClick = true;
      //解除添加公式状态
      this.isAddFun = false;
      //让所有添加公式时添加的颜色回到正常
      for (var j = 0, length2 = this.allTds.length; j < length2; j++) {
        for (var k = 1, length3 = this.allTds[j].length; k < length3; k++) {
          this.allTds[j][k].class.addFunArea = false;
        }
      };
      //清空当前正在添加公式的表格的位置信息
      this.addFunPosition = [];
      //去掉公式input
      this.inputDiv = false;
    },
    noSureAdd () {
      this.addFunPosition = [];
      this.ruleMsg = "";
      this.isAddFun = false;
      this.inputDiv = false;
      for (var j = 0, length2 = this.allTds.length; j < length2; j++) {
        for (var k = 0, length3 = this.allTds[j].length; k < length3; k++) {
          this.allTds[j][k].class.addFunArea = false;
        }
      };
    },
    delFun () {
      var actieTd = document.querySelector('.isActive');
      var one = actieTd.getAttribute('fromtr');
      var two = actieTd.getAttribute('fromtd');
      this.allTds[one][two].ownFun = "";
      this.allTds[one][two].class.noDbClick = false;
      document.querySelector('.isActive').classList.remove('noDbClick')
      this.noSureAdd();
    },
    shear () {
      //剪切
      var lastTr = 0;
      this.copyArr = [];
      this.copyArr.push([]);
      var allArea = document.querySelectorAll('.area');
      for (var k = 0, length3 = allArea.length; k < length3; k++) {
        var one = allArea[k].getAttribute('fromtr');
        var two = allArea[k].getAttribute('fromtd');
        var ow = this.allTds[one][two].value;
        this.allTds[one][two].value = "";
        if (k == 0) {
          lastTr = one;
          this.copyArr[0].push(ow);
        } else {
          if (one == lastTr) {
            this.copyArr[this.copyArr.length - 1].push(ow);
          } else {
            this.copyArr.push([]);
            this.copyArr[this.copyArr.length - 1].push(ow);
            lastTr = one;
          }
        }
      };
      var oneArr = document.getElementsByClassName('isActive')[0];
      if (oneArr) {
        this.copyArr = [];
        this.copyArr.push([]);
        var one = oneArr.getAttribute('fromtr');
        var two = oneArr.getAttribute('fromtd');
        var ow = this.allTds[one][two].value;
        this.allTds[one][two].value = "";
        document.querySelector('.isActive').innerHTML = "";
        this.copyArr[0].push(ow);
      }
    },
    containLi (a) {
      this.small_ul_one = false;
      this.small_ul_two = false;
      this.small_ul_three = false;
      this.small_ul_four = false;
      this.small_ul_five = false;
      switch (a) {
        case "small_ul_one":
          this.small_ul_one = true;
          break;
        case "small_ul_two":
          this.small_ul_two = true;
          break;
        case "small_ul_three":
          this.small_ul_three = true;
          break;
        case "small_ul_four":
          this.small_ul_four = true;
          break;
        case "small_ul_five":
          this.small_ul_five = true;
          break;
      }
    },
    paste () {
      //粘贴
      var lastTr = 0;
      var trEq = 0;
      var tdEq = 1;
      var allArea = document.querySelectorAll('.area');
      var copyArrLength = (this.copyArr[0].length) * (this.copyArr.length);
      for (var k = 0, length3 = allArea.length; k < length3; k++) {
        var one = allArea[k].getAttribute('fromtr');
        var two = allArea[k].getAttribute('fromtd');
        if (k == 0) {
          lastTr = one;
          this.allTds[one][two].value = this.copyArr[trEq][k];
        } else {
          if (one == lastTr) {
            if (tdEq < this.copyArr[0].length) {
              this.allTds[one][two].value = this.copyArr[trEq][tdEq];
              tdEq++;
            }
          } else {
            lastTr = one;
            trEq++;
            tdEq = 0;
            this.allTds[one][two].value = this.copyArr[trEq][tdEq];
            tdEq++;
          }
        }
      };
      var oneArr = document.getElementsByClassName('isActive')[0];
      if (oneArr) {
        var one = oneArr.getAttribute('fromtr');
        var two = oneArr.getAttribute('fromtd');
        this.allTds[one][two].value = this.copyArr[0][0];
      }
    },
    copy () {
      //复制
      var lastTr = 0;
      this.copyArr = [];
      this.copyArr.push([]);
      var allArea = document.querySelectorAll('.area');
      for (var k = 0, length3 = allArea.length; k < length3; k++) {
        var one = allArea[k].getAttribute('fromtr');
        var two = allArea[k].getAttribute('fromtd');
        var ow = this.allTds[one][two].value;
        if (k == 0) {
          lastTr = one;
          this.copyArr[0].push(ow);
        } else {
          if (one == lastTr) {
            this.copyArr[this.copyArr.length - 1].push(ow);
          } else {
            this.copyArr.push([]);
            this.copyArr[this.copyArr.length - 1].push(ow);
            lastTr = one;
          }
        }
      };
      var oneArr = document.getElementsByClassName('isActive')[0];
      if (oneArr) {
        this.copyArr = [];
        this.copyArr.push([]);
        var one = oneArr.getAttribute('fromtr');
        var two = oneArr.getAttribute('fromtd');
        var ow = this.allTds[one][two].value;
        this.copyArr[0].push(ow);
      }
    },
    readOnly () {
      var activeTd = document.getElementsByClassName('isActive')[0];
      if (activeTd) {
        var one = activeTd.getAttribute('fromtr');
        var two = activeTd.getAttribute('fromtd');
        this.allTds[one][two].class.isDbClick = false;
        this.allTds[one][two].class.noDbClick = true;
      }
    },
    addRow () {
      //插入行
      this.small_ul_one = false;
      var basickLeftTd = {
        "value": "",
        "class": {
          "area": false,
          "isClick": false,
          "isDbClick": true,
          "isActive": false,
          "leftTd": true
        },
        "ownType": {
          "isData": false,
          "isSelect": false,
          "isOne": false,
          "isMore": false,
          "isImg": false,
          "dataModel": "",
          "selectModel": "",
          "oneModel": "",
          "moreModel": [],
          "imgSrc": "",
          "oneData": [],
          "moreData": [],
          "selectData": []
        },
        "ownMerge": {
          "isShow": true,
          "colspan": "1",
          "rowspan": "1"
        },
        "ownStyle": {}, "ownFun": ""
      };
      var activeTd = document.getElementsByClassName('isActive')[0];
      if (activeTd) {
        var one = activeTd.getAttribute('fromtr');
        var two = activeTd.getAttribute('fromtd');
        this.allTds.splice(one, 0, []);
        for (var k = 0, length3 = this.allTds[0].length; k < length3; k++) {
          if (k == 0) {
            this.allTds[one].push(basickLeftTd);
          } else {
            var basickTd = {
              "value": "",
              "class": {
                "area": false,
                "isClick": true,
                "isDbClick": true,
                "isActive": false
              },
              "ownType": {
                "isData": false,
                "isSelect": false,
                "isOne": false,
                "isMore": false,
                "isImg": false,
                "dataModel": "",
                "selectModel": "",
                "oneModel": "",
                "moreModel": [],
                "imgSrc": "",
                "oneData": [],
                "moreData": [],
                "selectData": []
              },
              "ownMerge": {
                "isShow": true,
                "colspan": "1",
                "rowspan": "1",
                "isOwnData": "123"
              },
              "ownStyle": {}, "ownFun": ""
            };
            this.allTds[one].push(basickTd);
          }
        };
        this.allTdSort();
        this.activeDiv = false;
      }
    },
    addCol () {
      this.small_ul_one = false;
      var activeTd = document.getElementsByClassName('isActive')[0];
      if (activeTd) {
        var one = activeTd.getAttribute('fromtr');
        var two = activeTd.getAttribute('fromtd');
        var headTd = {
          value: '',
          class: {
            area: false,
            headTd: true
          },
          ownStyle: {
            width: "130px"
          }
        };
        this.headTd.splice(two, 0, headTd);
        for (var k = 0, length3 = this.allTds.length; k < length3; k++) {
          var basickTd = {
            "value": "",
            "class": {
              "area": false,
              "isClick": true,
              "isDbClick": true,
              "isActive": false
            },
            "ownType": {
              "isData": false,
              "isSelect": false,
              "isOne": false,
              "isMore": false,
              "isImg": false,
              "dataModel": "",
              "selectModel": "",
              "oneModel": "",
              "moreModel": [],
              "imgSrc": "",
              "oneData": [],
              "moreData": [],
              "selectData": []
            },
            "ownMerge": {
              "isShow": true,
              "colspan": "1",
              "rowspan": "1",
              "isOwnData": "123"
            },
            "ownStyle": {}, "ownFun": ""
          };
          this.allTds[k].splice(two, 0, basickTd)
        }
        this.allTdSort();
        this.activeDiv = false;
      }
    },
    deleteRow () {
      this.small_ul_one = false;
      var activeTd = document.getElementsByClassName('isActive')[0];
      if (activeTd) {
        var one = activeTd.getAttribute('fromtr');
        var two = activeTd.getAttribute('fromtd');
        this.allTds.splice(one, 1);
        this.allTdSort();
        this.activeDiv = false;
      }
    },
    deleteCol () {
      this.small_ul_one = false;
      var activeTd = document.getElementsByClassName('isActive')[0];
      if (activeTd) {
        var one = activeTd.getAttribute('fromtr');
        var two = activeTd.getAttribute('fromtd');
        this.headTd.splice(two, 1);
        for (var k = 0, length3 = this.allTds.length; k < length3; k++) {
          this.allTds[k].splice(two, 1);
        };
        this.allTdSort();
        this.activeDiv = false;
      }
    },
    merge () {
      var allArea = document.querySelectorAll('.area');
      var activeTd = document.querySelector('.isActive');
      if (allArea.length > 0) {
        var tdNum = 1;
        var trNum = 1;
        var oldTr;
        for (var k = 0, length3 = allArea.length; k < length3; k++) {
          var one = allArea[k].getAttribute('fromtr');
          var two = allArea[k].getAttribute('fromtd');
          this.allTds[one][two].ownMerge.isShow = false;
          // this.allTds[one][two].ownStyle.display = "none";
          if (k == 0) {
            oldTr = one;
          } else {
            if (one == oldTr) {
              if (trNum == 1) {
                tdNum++;
              }
            } else {
              oldTr = one;
              trNum++;
            }
          };
        };
        var firstone = allArea[0].getAttribute('fromtr');
        var firsttwo = allArea[0].getAttribute('fromtd');
        this.firstone = firstone;
        this.firsttwo = firsttwo;
        var _this = this;
        this.allTds[firstone][firsttwo].ownMerge.rowspan = trNum;
        this.allTds[firstone][firsttwo].ownMerge.colspan = tdNum;
        // this.allTds[firstone][firsttwo].ownMerge.isShow = true;
        setTimeout(function () {
          _this.allTds[firstone][firsttwo].ownMerge.isShow = true;
        }, 50);
      } else {
        var tdRowspan = parseInt(activeTd.getAttribute("rowspan"));
        var tdColspan = parseInt(activeTd.getAttribute("colspan"));
        var one = parseInt(activeTd.getAttribute("fromtr"));
        var two = parseInt(activeTd.getAttribute("fromtd"));
        if (tdRowspan != 1 || tdColspan != 1) {
          this.allTds[one][two].ownMerge.rowspan = 1;
          this.allTds[one][two].ownMerge.colspan = 1;
          for (var k = 1, length3 = tdColspan; k < length3; k++) {
            var tdNum = two + k;
            this.allTds[one][tdNum].ownMerge.isShow = true;
            for (var j = 1, length3 = tdRowspan; j < length3; j++) {
              var trNum = one + j;
              this.allTds[trNum][two].ownMerge.isShow = true;
              this.allTds[trNum][tdNum].ownMerge.isShow = true;
            }
          };
          this.activeDiv = false;
        }
      }
    },
    typeFont (a) {
      this.changeStyle("fontFamily", a.target.value);
    },
    typeFontSize (a) {
      this.changeStyle("fontSize", a.target.value);
    },
    addFont () {
      if (this.fontNum < 22) {
        this.fontNum = this.fontNum + 2;
        document.querySelector('.typeFontSize').value = this.fontNum + "px";
        this.changeStyle("fontSize", this.fontNum + "px");
      }
    },
    reduceFont () {
      if (this.fontNum > 10) {
        this.fontNum = this.fontNum - 2;
        document.querySelector('.typeFontSize').value = this.fontNum + "px";
        this.changeStyle("fontSize", this.fontNum + "px");
      }
    },
    blod () {
      this.changeStyle('fontWeight', '700');
    },
    italic () {
      this.changeStyle('fontStyle', 'italic');
    },
    underline () {
      this.changeStyle('textDecoration', 'underline');
    },
    align (a) {
      this.small_ul_four = false;
      this.changeStyle(a.target.getAttribute('_name'), a.target.getAttribute('value'));
    },
    choiceColor () {
      document.querySelector('.color div').click();
    },
    allBorder () {
      var actieTd = document.querySelector('.isActive');
      var areaTd = document.querySelectorAll('.area');
      if (actieTd) {
        var one = actieTd.getAttribute('fromtr');
        var two = actieTd.getAttribute('fromtd');
        this.setKey(this.allTds[one][two].ownStyle, 'border', '1px solid black');
        this.setKey(this.allTds[one - 1][two].ownStyle, 'borderBottom', '1px solid black');
        this.setKey(this.allTds[one][two - 1].ownStyle, 'borderRight', '1px solid black');
        actieTd.click();
      } else if (areaTd[0]) {
        for (var k = 0, length3 = areaTd.length; k < length3; k++) {
          var one = areaTd[k].getAttribute('fromtr');
          var two = areaTd[k].getAttribute('fromtd');
          this.setKey(this.allTds[one][two].ownStyle, 'border', '1px solid black');
          this.setKey(this.allTds[one - 1][two].ownStyle, 'borderBottom', '1px solid black');
          this.setKey(this.allTds[one][two - 1].ownStyle, 'borderRight', '1px solid black');
        }
      }
    },
    leftBorder () {
      var actieTd = document.querySelector('.isActive');
      var areaTd = document.querySelectorAll('.area');
      if (actieTd) {
        var one = actieTd.getAttribute('fromtr');
        var two = actieTd.getAttribute('fromtd');
        this.setKey(this.allTds[one][two - 1].ownStyle, 'borderRight', '1px solid black');
        actieTd.click();
      } else if (areaTd[0]) {
        for (var k = 0, length3 = areaTd.length; k < length3; k++) {
          var one = areaTd[k].getAttribute('fromtr');
          var two = areaTd[k].getAttribute('fromtd');
          this.setKey(this.allTds[one][two - 1].ownStyle, 'borderRight', '1px solid black');
        }
      }
    },
    topBorder () {
      var actieTd = document.querySelector('.isActive');
      var areaTd = document.querySelectorAll('.area');
      if (actieTd) {
        var one = actieTd.getAttribute('fromtr');
        var two = actieTd.getAttribute('fromtd');
        this.setKey(this.allTds[one - 1][two].ownStyle, 'borderBottom', '1px solid black');
        actieTd.click();
      } else if (areaTd[0]) {
        for (var k = 0, length3 = areaTd.length; k < length3; k++) {
          var one = areaTd[k].getAttribute('fromtr');
          var two = areaTd[k].getAttribute('fromtd');
          this.setKey(this.allTds[one - 1][two].ownStyle, 'borderBottom', '1px solid black');
        }
      }
    },
    rightBorder () {
      var actieTd = document.querySelector('.isActive');
      var areaTd = document.querySelectorAll('.area');
      if (actieTd) {
        var one = actieTd.getAttribute('fromtr');
        var two = actieTd.getAttribute('fromtd');
        this.setKey(this.allTds[one][two].ownStyle, 'borderRight', '1px solid black');
        actieTd.click();
      } else if (areaTd[0]) {
        for (var k = 0, length3 = areaTd.length; k < length3; k++) {
          var one = areaTd[k].getAttribute('fromtr');
          var two = areaTd[k].getAttribute('fromtd');
          this.setKey(this.allTds[one][two].ownStyle, 'borderRight', '1px solid black');
        }
      }
    },
    bottomBorder () {
      var actieTd = document.querySelector('.isActive');
      var areaTd = document.querySelectorAll('.area');
      if (actieTd) {
        var one = actieTd.getAttribute('fromtr');
        var two = actieTd.getAttribute('fromtd');
        this.setKey(this.allTds[one][two].ownStyle, 'borderBottom', '1px solid black');
        actieTd.click();
      } else if (areaTd[0]) {
        for (var k = 0, length3 = areaTd.length; k < length3; k++) {
          var one = areaTd[k].getAttribute('fromtr');
          var two = areaTd[k].getAttribute('fromtd');
          this.setKey(this.allTds[one][two].ownStyle, 'borderBottom', '1px solid black');
        }
      }
    },
    noneBorder () {
      var actieTd = document.querySelector('.isActive');
      var areaTd = document.querySelectorAll('.area');
      if (actieTd) {
        var one = actieTd.getAttribute('fromtr');
        var two = actieTd.getAttribute('fromtd');
        this.setKey(this.allTds[one][two].ownStyle, 'border', '1px solid #ccc');
        this.setKey(this.allTds[one - 1][two].ownStyle, 'borderBottom', '1px solid #ccc');
        this.setKey(this.allTds[one][two - 1].ownStyle, 'borderRight', '1px solid #ccc');
        actieTd.click();
      } else if (areaTd[0]) {
        for (var k = 0, length3 = areaTd.length; k < length3; k++) {
          var one = areaTd[k].getAttribute('fromtr');
          var two = areaTd[k].getAttribute('fromtd');
          this.setKey(this.allTds[one][two].ownStyle, 'border', '1px solid #ccc');
          this.setKey(this.allTds[one - 1][two].ownStyle, 'borderBottom', '1px solid #ccc');
          this.setKey(this.allTds[one][two - 1].ownStyle, 'borderRight', '1px solid #ccc');
        }
      }
    },
    isData () {
      this.small_ul_three = false;
      this.changeType("isData", true);
    },
    isSelect () {
      this.small_ul_three = false;
      this.changeType("isSelect", true);
    },
    isOne () {
      this.small_ul_three = false;
      this.changeType("isOne", true);
    },
    isMore () {
      this.small_ul_three = false;
      this.changeType("isMore", true);
    },
    isImg () {
      this.small_ul_three = false;
      this.changeType("isImg", true);
    },
    changeBackgroundColor () {
      this.changeStyle('backgroundColor', this.backgroundColor);
    },
    changeColor () {
      this.changeStyle('color', this.Color);
    },
    changeStyle (key, value) {
      var actieTd = document.querySelector('.isActive');
      var areaTd = document.querySelectorAll('.area');
      if (actieTd) {
        var one = actieTd.getAttribute('fromtr');
        var two = actieTd.getAttribute('fromtd');
        this.setKey(this.allTds[one][two].ownStyle, key, value);
        actieTd.click();
      } else if (areaTd[0]) {
        for (var k = 0, length3 = areaTd.length; k < length3; k++) {
          var one = areaTd[k].getAttribute('fromtr');
          var two = areaTd[k].getAttribute('fromtd');
          this.setKey(this.allTds[one][two].ownStyle, key, value);
        }
      }
    },
    changeType (key, value) {
      var actieTd = document.querySelector('.isActive');
      var areaTd = document.querySelectorAll('.area');
      if (actieTd) {
        var one = actieTd.getAttribute('fromtr');
        var two = actieTd.getAttribute('fromtd');
        this.allTds[one][two].value = "";
        this.setKey(this.allTds[one][two].ownType, key, value);
        actieTd.click();
      } else if (areaTd[0]) {
        for (var k = 0, length3 = areaTd.length; k < length3; k++) {
          var one = areaTd[k].getAttribute('fromtr');
          var two = areaTd[k].getAttribute('fromtd');
          this.setKey(this.allTds[one][two].ownType, key, value);
          this.allTds[one][two].value = "";
        }
      }
    },
    formatDate (date) {
      var date = new Date(date);
      var y = date.getFullYear();
      var m = date.getMonth() + 1;
      m = m < 10 ? '0' + m : m;
      var d = date.getDate();
      d = d < 10 ? ('0' + d) : d;
      return y + '-' + m + '-' + d;
    },
    gudingTypeChange (a) {
      if (this.gudingData[a].type == "date") {
        this.gudingData[a].isEdit = true;
      }
    },
    mingxiTypeChange (a) {
      if (this.mingxiData[a].type == "date") {
        this.mingxiData[a].isEdit = true;
      }
    },
  }
}

</script>
<style scoped lang="less">
* {
  moz-user-select: -moz-none;
  -moz-user-select: none;
  -o-user-select: none;
  -khtml-user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

table {
  border: 1px solid #ccc;
  border-collapse: collapse;
  position: relative;
  /*width: 698px;*/
  table-layout: fixed;
}
thead {
  background: #eee;
}
thead td {
  height: 20px;
}
tr td:nth-child(1) {
  background: #eee;
  width: 60px;
}
td {
  border: 1px solid #ccc;
  /*width: 400px;*/
  height: 25px;
  table-layout: fixed;
  z-index: 99;
  overflow: hidden;
  /*word-wrap:break-word;*/
}
.area {
  background: #e6efff;
}
.active {
  border: 2px solid #5292f7;
}
.all {
  border: 1px solid #5292f7;
  position: absolute;
  z-index: 100;
}
.hello {
  position: relative;
}
.columnResizer {
  position: absolute;
  cursor: col-resize;
  background: #eee;
  z-index: 100;
  width: 5px;
  height: 19px;
  top: 1px;
  left: 180px;
}
.rowResizer {
  position: absolute;
  cursor: row-resize;
  background: #eee;
  z-index: 100;
  width: 61px;
  height: 5px;
  top: 46px;
  left: 1px;
}
.columnResizer:hover,
.rowResizer:hover {
  background: #aaaabb !important;
}
.columnResizerLong {
  position: absolute;
  height: 100%;
  background: #aaaabb;
  width: 1px;
  left: 100px;
  top: 0;
  z-index: 100;
}
.rowResizerLong {
  position: absolute;
  height: 1px;
  background: #aaaabb;
  width: 100%;
  left: 0px;
  top: 50px;
  z-index: 100;
}
.addFunArea {
  background: #1cf5a5;
}

/*ul开始*/
ul,
li {
  list-style: none;
  margin: 0;
  padding: 0;
}
.left {
  float: left;
}
.right {
  float: right;
}
.one,
.two {
  height: 30px;
  background: #eee;
  line-height: 30px;
  text-align: center;
  margin: 0;
  padding: 0;
}
.two {
  border-top: 1px solid #ccc;
}
.one li:nth-child(5):hover {
}
.one > li,
.two > li {
  float: left;
  width: 30px;
  height: 28px;
  margin-right: 20px;
  display: inline-block;
  text-align: center;
  // border: 1px solid #eee;
}
.one > li:hover,
.two > li:hover {
  // border-top: 1px solid #fff;
  // border-left: 1px solid #fff;
  // border-bottom: 1px solid #251313;
  // border-right: 1px solid #251313;
  cursor: pointer;
  background: #a4cfe8;
}
.two li:nth-child(17):hover,
.two li:nth-child(18):hover {
  background: #eee;
}
.bor:hover {
  // border: 1px solid #eee !important;
  background: #eee !important;
}
.active {
  border-top: 1px solid #fff;
  border-left: 1px solid #fff;
  border-bottom: 1px solid #251313;
  border-right: 1px solid #251313;
}
.containLi {
  position: relative;
  // width: 90px !important;
}
.containLi ul {
  position: absolute;
  // width: 92px;
  text-align: center;
  top: 28px;
  left: -1px;
  background-color: #fff;
  padding: 0;
  font-size: 10px;
  border: 1px solid #ccc;
  border-top: none;
  z-index: 101;
}
.containLi ul li {
  width: 92px;
  text-align: left;
  line-height: 32px;
}
.containLi ul li:hover {
  background: #ccc;
}
.liActive {
  background: #ccc;
}
.containLi ul li i {
  font-size: 16px;
  margin-right: 3px;
  margin-left: 12px;
}
.model {
  width: 100%;
  height: 100%;
  left: 0px;
  top: 0px;
  position: absolute;
  z-index: 997;
  background-color: rgba(0, 0, 0, 0.3);
}
.seeDataItem {
  position: absolute;
  width: 860px;
  height: 600px;
  background-color: #fafafa;
  z-index: 998;
  left: 50%;
  top: 50%;
  margin-top: -300px;
  margin-left: -430px;
}
.seeDataItem .top {
  height: 35px;
  line-height: 35px;
  font-size: 18px;
}
.seeDataItem .con {
  height: 495px;
  margin-top: 30px;
  position: absolute;
  width: 92%;
  margin-left: 4%;
  border: 1px solid #ddd;
}
.alltab {
  position: absolute;
  width: 135px;
  height: 30px;
  line-height: 30px;
  left: -1px;
  top: -30px;
  background: #fafafa;
  border: 1px solid #ddd;
  border-bottom: none;
  cursor: pointer;
}
.tab2 {
  left: 134px;
  border-left: none;
}
.tabnoActive {
  background-color: #fff;
}
.seeDataItem .con .kubiaoName {
  height: 40px;
  line-height: 40px;
  text-align: left;
}
.seeDataItem .con .kubiaoName span {
  margin-left: 30px;
  margin-right: 20px;
  font-weight: 700;
}
.kubiaoHead {
  height: 40px;
  line-height: 40px;
}
.kubiaoHead div {
  text-align: center;
}
.kubiaoCon {
  height: 413px;
  overflow: hidden;
  overflow-y: auto;
  text-align: left;
}
.kubiaoBottom {
  height: 41px;
  line-height: 41px;
  text-align: right;
}
.ctrlActive {
  background-color: #afe0ef;
}
.postil {
  position: relative;
}
.postil::after {
  content: "";
  width: 0;
  height: 0;
  border-top: 10px solid red;
  border-left: 10px solid transparent;
  right: 0;
  top: 0px;
  position: absolute;
}
</style>
