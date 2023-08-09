<template>
  <!-- 全景看板 -->
  <div
    ref="home"
    class="home"
    id="homeVisible"
  >
    <div
      v-if="!isFullScreen"
      class="fullscreen-area"
    >
      <a-icon
        class="fullscreen-icon"
        @click="enterfullscreen"
        type="fullscreen"
      />
      <!-- <a-icon
        class="fullscreen-icon"
       
        @click="exitfullscreen"
        type="fullscreen-exit"
      /> -->
    </div>
    <div
      v-if="isFullScreen"
      class="fullscreen-area2"
    >
      <!-- <a-icon
        class="fullscreen-icon"
        
        @click="enterfullscreen"
        type="fullscreen"
      /> -->
      <a-icon
        class="fullscreen-icon"
        @click="exitfullscreen"
        type="fullscreen-exit"
      />
    </div>
    <div class="home-header">
      <div style="position: absolute;left: -34px;margin-top: 10px;">
        <a-select
          style="width:8vw;border:1px solid #00fffc;"
          @change="gdsListselect"
          v-model="orgNo"
          class="filter-value"
          placeholder="请选择地区"
        >
          <a-select-option
            v-for="(item,index) in gdsList"
            :value="item.value"
            :key="index"
          >{{ item.title }}</a-select-option> </a-select>
        <a-select
          v-model="suoNo"
          @change="suoListselect"
          style="width:8vw;border:1px solid #00fffc"
          class="filter-value"
          placeholder="请选择供电所"
          allowClear
        >
          <a-select-option
            v-for="(item,index) in suoList"
            :value="item.value"
            :key="index"
          >{{ item.title }}</a-select-option> </a-select>
        <a-select
          @change="zhengListselect"
          v-model="zhengNo"
          style="width:8vw;border:1px solid #00fffc"
          class="filter-value"
          placeholder="请选择镇"
          allowClear
        >
          <a-select-option
            v-for="(item,index) in zhengList"
            :value="item.value"
            :key="index"
          >{{ item.title }}</a-select-option> </a-select>
        <a-select
          v-model="cunNo"
          @change="cunselect"
          style="width:8vw;border:1px solid #00fffc"
          class="filter-value"
          placeholder="请选择村"
          allowClear
        >
          <a-select-option
            v-for="(item,index) in cunList"
            :value="item.value"
            :key="index"
          >{{ item.title }}</a-select-option> </a-select>
      </div>
      <div style="position: absolute;right: 0;color:#fff">{{jp_date+jp_week}}</div>
      <img
        style="margin-top: 10px;"
        src="@/assets/images/newvisi/titlepng.png"
      >
      <!-- <span class="sblue">"村网共建"全景视图</span> -->
      <span></span>
    </div>
    <div class="home-main">
      <div class="home-main-top">
        <div
          class="border-radius"
          style="width:24.5%"
        >
          <div
            class=""
            style="margin-left:20px;height:10%"
          >
            <div style="padding:10px;display: flex;align-items: center;">
              <img
                src="@/assets/images/newvisi/u157.svg"
                alt=""
              >
              <img
                src="@/assets/images/newvisi/u157.svg"
                alt=""
              >
              <img
                src="@/assets/images/newvisi/u157.svg"
                alt=""
              >
              <span style="color:#00FCFC;font-size:18px;margin-left:20px">{{cunName}}电力便民服务点</span>
            </div>
          </div>
          <!-- <div class="discenter">
              <el-image
                        v-for="(item, index) in bm.baseInfoContentFileList"
                          :key="index"
                          style="width: 25vh; height: 15vh"
                          :src="`${imgViewHost}${item.fileNo}`"
                          :preview-src-list="[`${imgViewHost}${item.fileNo}`]"
                        >
                        </el-image>
            </div> -->
          <div
            class="discenter"
            style="height:40%"
          >
            <!-- :autoplaySpeed="500" -->
            <a-carousel
              autoplay
              style="width: 25vh; height: 15vh"
              arrows
            >
              <template #prevArrow>
                <a-icon
                  type="left"
                  class="bluesel"
                  style="left: -40px;font-size:25px;z-index: 1;"
                />
              </template>
              <template #nextArrow>
                <a-icon
                  type="right"
                  class="bluesel"
                  style="right: -40px;font-size:25px;z-index: 1;"
                />
              </template>
              <el-image
                v-for="(item, index) in bm.baseInfoContentFileList"
                :key="index"
                style="width: 25vh; height: 15vh"
                :src="`${imgViewHost}${item.fileNo}`"
                :preview-src-list="[`${imgViewHost}${item.fileNo}`]"
              >
              </el-image>
            </a-carousel>
          </div>
          <div
            class="visicontent contenttext"
            style="height:40%"
          >
            <div
              class="contebox"
              style="width:100%;height:100%;overflow: auto;"
            >{{ bm.contentData }}</div>
          </div>
        </div>
        <div
          class="border-radius"
          style="width:49%;height:100%"
        >
          <div
            class=""
            style="margin-left:20px;height:10%"
          >
            <div style="padding:10px;display: flex;align-items: center;">
              <img
                src="@/assets/images/newvisi/u157.svg"
                alt=""
              >
              <img
                src="@/assets/images/newvisi/u157.svg"
                alt=""
              >
              <img
                src="@/assets/images/newvisi/u157.svg"
                alt=""
              >
              <span style="color:#00FCFC;font-size:18px;margin-left:20px">办电便民</span>
            </div>
          </div>
          <div style="display:flex;justify-content: space-around;height:90%">
            <div
              class="visicontenttop"
              style="height:90%"
            >
              <div style="display:flex;color:#fff;font-size:16px;justify-content: center;position: relative;padding:10px;height: 15%;">
                <div
                  class="svgimg1"
                  style="margin-right:10px"
                >
                  <img
                    src="@/assets/images/newvisi/u109.png"
                    alt=""
                  >
                </div>用户用电统计
                <a-month-picker
                  @change="maxTimeChange"
                  size="small"
                  class="monthclass1"
                  v-model="maxTime"
                  :allowClear="false"
                />
              </div>
              <div
                class="yd"
                style="height:30%"
              >
                <div class="yd-item">
                  <div class="yd-span">
                    <div style="font-size:16px;margin-top: 2px;">用户量</div>
                    <div>环比</div>
                  </div>
                  <div class="yd-span">
                    <div style="font-size:18px;color:#FBA067;">{{RESIDENT_USER}}<span style="color:#00FCFC;font-size:12px">户</span></div>
                    <div style="color:#D9001B">{{RESIDENT_USER_CHAIN_BASE}}</div>
                  </div>
                </div>
                <div class="yd-item">
                  <div class="yd-span">
                    <div style="font-size:16px">用电量</div>
                    <div>环比</div>
                  </div>
                  <div class="yd-span">
                    <div style="font-size:18px;color:#FBA067;">{{CONSUMER_ELECTRIC}}<span style="color:#00FCFC;font-size:12px">万千瓦时</span></div>
                    <div style="color:#D9001B">{{CONSUMER_ELECTRIC_CHAIN_BASE}}</div>
                  </div>

                </div>
              </div>
              <div style="display:flex;color:#fff;font-size:16px;justify-content: center;position: relative;padding:20px;height: 20%;">
                <div
                  class="svgimg1"
                  style="background:#99B616;margin-right:10px"
                >
                  <img
                    src="@/assets/images/newvisi/u170.svg"
                    alt=""
                  >
                </div>线上业务统计
                <a-month-picker
                  size="small"
                  @change="lastTimeChange"
                  class="monthclass2"
                  v-model="lastTime"
                  :allowClear="false"
                />
              </div>
              <div
                class="yd"
                style="height: 40%;"
              >
                <div class="yd-item">
                  <div class="yd-span">
                    <div style="font-size:16px">线上办电率</div>
                    <div>环比</div>
                  </div>
                  <div class="yd-span">
                    <div style="font-size:18px;color:#FBA067;">{{LINE_PAYFEE_RATE}}<span style="color:#00FCFC;font-size:12px">%</span></div>
                    <div style="color:#D9001B">{{LINE_HANDLE_CHAIN_BASE}}</div>
                  </div>
                </div>
                <div class="yd-item">
                  <div class="yd-span">
                    <div style="font-size:16px">线上缴费率</div>
                    <div>环比</div>
                  </div>
                  <div class="yd-span">
                    <div style="font-size:20px;color:#FBA067;">{{LINE_HANDLE_RATE}}<span style="color:#00FCFC;font-size:12px">%</span></div>
                    <div style="color:#D9001B">{{LINE_PAYFEE_CHAIN_BASE}}</div>
                  </div>

                </div>
              </div>
            </div>
            <div
              class="visicontenttop"
              style="height:90%;display: flex;flex-direction: column;justify-content: space-around;"
            >
              <div style="display:flex;justify-content: space-around;margin-bottom:10px 0;padding:20px;">
                <div style="display:flex;color:#fff;flex-direction: column;justify-content: center;align-items: center;flex:1">
                  <div
                    class="svgimg1"
                    style="background:#00A6A6"
                  >
                    <img
                      src="@/assets/images/newvisi/u174.png"
                      alt=""
                    >
                  </div>
                  <div style="font-size:16px;margin-top: 4px;">客户诉求管理</div>
                </div>
                <div class="columncenter">
                  <div style="font-size:14px;color:#00fffc">客户意见登记</div>
                  <div style="font-size:20px;color:#FBA067;">{{customRegistNum}}<span style="color:#00FCFC;font-size:12px">项</span></div>
                </div>
                <div class="columncenter">
                  <div style="font-size:14px;color:#00fffc">客户意见反馈</div>
                  <div style="font-size:20px;color:#FBA067;">{{customFeedbackNum}}<span style="color:#00FCFC;font-size:12px">项</span></div>
                </div>
              </div>
              <div class="dashline"></div>
              <div style="display:flex;justify-content: space-around;margin-bottom:10px 0;padding:20px;">
                <div style="display:flex;color:#fff;flex-direction: column;justify-content: center;align-items: center;flex:1">
                  <div
                    class="svgimg1"
                    style="background:#F9BD6D"
                  >
                    <img
                      src="@/assets/images/newvisi/u411.png"
                      alt=""
                    >
                  </div>
                  <div style="font-size:16px;margin-top: 4px;">特殊群体服务</div>
                </div>
                <div class="columncenter">
                  <div style="font-size:14px;color:#00fffc">特殊群体人员</div>
                  <div style="font-size:20px;color:#FBA067;">{{specialPeopleNum}}<span style="color:#00FCFC;font-size:12px">人</span></div>
                </div>
                <div class="columncenter">
                  <div style="font-size:14px;color:#00fffc">特殊群体服务</div>
                  <div style="font-size:20px;color:#FBA067;">{{specialServiceNum}}<span style="color:#00FCFC;font-size:12px">次</span></div>
                </div>
              </div>
              <div class="dashline"></div>
              <div style="display:flex;justify-content: space-around;margin-bottom:10px 0;padding:20px;">
                <div style="display:flex;color:#fff;flex-direction: column;justify-content: center;align-items: center;flex:1">
                  <div
                    class="svgimg1"
                    style="background:#00B3CC"
                  >
                    <img
                      src="@/assets/images/newvisi/u378.svg"
                      alt=""
                    >
                  </div>
                  <div style="font-size:16px;margin-top: 4px;">网格云电话</div>
                </div>
                <div class="columncenter">
                  <div style="font-size:14px;color:#00fffc">知晓率</div>
                  <div style="font-size:20px;color:#FBA067;">{{knowRate}}</div>
                </div>
                <div class="columncenter">
                  <div style="font-size:14px;color:#00fffc">活跃率</div>
                  <div style="font-size:20px;color:#FBA067;">{{activityRate}}</div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div
          class="border-radius"
          style="width:24.5%;height: 100%;"
        >
          <div
            class=""
            style="margin-left:20px;height:10%;"
          >
            <div style="padding:10px;display: flex;align-items: center;">
              <img
                src="@/assets/images/newvisi/u157.svg"
                alt=""
              >
              <img
                src="@/assets/images/newvisi/u157.svg"
                alt=""
              >
              <img
                src="@/assets/images/newvisi/u157.svg"
                alt=""
              >
              <span style="color:#00FCFC;font-size:18px;margin-left:20px">"二十节气"工作计划</span>
            </div>
          </div>
          <div style="width:100%;height: 45%;">
            <div
              class="sblue"
              style="margin-left:20px;padding:0px 0"
            >本月</div>
            <div
              class="sblue"
              style="width:90%;margin:0 auto;line-height: 23px;"
            >
              <div class="disflex">
                <div
                  class="sbluebor"
                  style="width:35%"
                >节气</div>
                <div
                  class="sbluebor"
                  style="width:65%"
                >工作重点</div>
              </div>
              <div
                v-for="(item,index) in benmon"
                class="disflex"
              >
                <div
                  style="width:35%;text-align: center;display: flex;"
                  class="sred sbluebor"
                >{{item.solarTermsName+'('+item.solarTermsDate+')'}}</div>
                <div
                  class="sbluebor"
                  style="width:65%"
                >{{item.workContent}}</div>
              </div>
              <!-- <div class="disflex">
                <div style="width:35%" class="sred sbluebor">夏至（6月21日）</div>
                <div  class="sbluebor" style="width:65%">制定防汛预案，完善防汛人员，做好防汛工作</div>
              </div> -->
            </div>
          </div>
          <div style="width:100%;height: 45%;">
            <div
              class="sblue"
              style="margin-left:20px;padding:0px 0"
            >下月</div>
            <div
              class="sblue"
              style="width:90%;margin:0 auto;line-height: 23px;"
            >
              <div class="disflex">
                <div
                  class="sbluebor"
                  style="width:35%"
                >节气</div>
                <div
                  class="sbluebor"
                  style="width:65%"
                >工作重点</div>
              </div>
              <div
                v-for="(item,index) in xiamon"
                class="disflex"
              >
                <div
                  style="width:35%;text-align: center;display: flex;"
                  class="sred sbluebor"
                >{{item.solarTermsName+'('+item.solarTermsDate+')'}}</div>
                <div
                  class="sbluebor"
                  style="width:65%"
                >{{item.workContent}}</div>
              </div>
              <!-- <div class="disflex">
                <div style="width:35%" class="sred sbluebor">夏至（6月21日）</div>
                <div  class="sbluebor" style="width:65%">制定防汛预案，完善防汛人员，做好防汛工作</div>
              </div> -->
            </div>
          </div>
          <div>
            <div></div>
            <div></div>
          </div>
        </div>
      </div>
      <div class="home-main-bottom">
        <div class="hmb-area">
          <div
            class="border-radius"
            style="width:49%;height: 100%;"
          >
            <div
              class=""
              style="margin-left:20px;height: 10%;"
            >
              <div style="padding:10px;display: flex;align-items: center;">
                <img
                  src="@/assets/images/newvisi/u157.svg"
                  alt=""
                >
                <img
                  src="@/assets/images/newvisi/u157.svg"
                  alt=""
                >
                <img
                  src="@/assets/images/newvisi/u157.svg"
                  alt=""
                >
                <span style="color:#00FCFC;font-size:18px;margin-left:20px">安全用电</span>
              </div>
            </div>
            <div style="width:100%;display: flex;height: 90%;">
              <div style="width:50%;">
                <div style="display: flex;justify-content: space-around;height: 30%;">
                  <div style="text-align: center;">
                    <div style="color:#fff;padding:5px;font-size:16px">电力隐患排查</div>
                    <div style="display:flex">
                      <!-- <div v-show="DANGER_TROUBLE_NUM.length<5" class="numback">0</div> -->
                      <div
                        v-show="DANGER_TROUBLE_NUM.length<3"
                        class="numback"
                      >0</div>
                      <div
                        v-show="DANGER_TROUBLE_NUM.length<2"
                        class="numback"
                      >0</div>
                      <div
                        v-show="DANGER_TROUBLE_NUM.length<1"
                        class="numback"
                      >0</div>
                      <div class="numback">{{ DANGER_TROUBLE_NUM.substr(0,1) }}</div>
                      <div
                        v-show="DANGER_TROUBLE_NUM.length>=2"
                        class="numback"
                      >{{ DANGER_TROUBLE_NUM.substr(1,1) }}</div>
                      <div
                        v-show="DANGER_TROUBLE_NUM.length>=3"
                        class="numback"
                      >{{ DANGER_TROUBLE_NUM.substr(2,1) }}</div>
                      <div
                        v-show="DANGER_TROUBLE_NUM.length>=4"
                        class="numback"
                      >{{ DANGER_TROUBLE_NUM.substr(3,1) }}</div>
                      <div
                        v-show="DANGER_TROUBLE_NUM.length>=5"
                        class="numback"
                      >{{ DANGER_TROUBLE_NUM.substr(4,1) }}</div>
                      <span style="color:#fff;padding-top:30px">项</span>
                    </div>
                  </div>
                  <div style="text-align: center;">
                    <div style="color:#fff;padding:5px;font-size:16px">电力隐患治理</div>
                    <div style="display:flex">
                      <div
                        v-show="DANGER_TREAT_NUM.length<3"
                        class="numback"
                      >0</div>
                      <div
                        v-show="DANGER_TREAT_NUM.length<2"
                        class="numback"
                      >0</div>
                      <div
                        v-show="DANGER_TREAT_NUM.length<1"
                        class="numback"
                      >0</div>
                      <div class="numback">{{ DANGER_TREAT_NUM.substr(0,1) }}</div>
                      <div
                        v-show="DANGER_TREAT_NUM.length>=2"
                        class="numback"
                      >{{ DANGER_TREAT_NUM.substr(1,1) }}</div>
                      <div
                        v-show="DANGER_TREAT_NUM.length>=3"
                        class="numback"
                      >{{ DANGER_TREAT_NUM.substr(2,1) }}</div>
                      <div
                        v-show="DANGER_TREAT_NUM.length>=4"
                        class="numback"
                      >{{ DANGER_TREAT_NUM.substr(3,1) }}</div>
                      <div
                        v-show="DANGER_TREAT_NUM.length>=5"
                        class="numback"
                      >{{ DANGER_TREAT_NUM.substr(4,1) }}</div>
                      <span style="color:#fff;padding-top:30px">项</span>
                    </div>
                  </div>
                </div>
                <div style="color: #fff;font-size: 16px;text-align: center;padding-right: 60px;">电力隐患排查分布统计</div>
                <div style="height:60%;display: flex;flex-direction: column;justify-content: space-around;">
                  <div
                    v-for="(item,index) in spreadList"
                    style="color:#fff;margin-left:20px;margin-top:5px;display:flex"
                  >
                    <div style="padding:0px 5px 5px 5px;width:80px">{{item.name}}</div>
                    <span
                      style="color:#fff;position:absolute;z-index: 999;"
                      :style="{left:100+(item.percent*1.2)+'px'}"
                    >{{item.num}}</span>
                    <a-progress
                      stroke-color="#FF6633"
                      style="width:60%;"
                      :percent="item.percent"
                    />
                    <span style="color:#0272FC">{{item.percent}}%</span>
                  </div>
                  <!-- <div style="color:#fff;text-align:center;padding:5px;">电力隐患分布统计</div>
          <div  style="color:#fff;margin-left:20px;margin-top:5px;display:flex">
            <div style="padding:0px 5px 5px 5px;width:80px">超高树竹</div>
            <span style="color:#fff;position:absolute;z-index: 999;" :style="{left:100+(tallNumPrecent*1.5)+'px'}">{{tallNum}}</span>
            <a-progress  stroke-color="#FF6633" style="width:60%;" :percent="tallNumPrecent"/>
            <span style="color:#0272FC">{{tallNumPrecent}}%</span>
          </div>
          <div  style="color:#fff;margin-left:20px;margin-top:5px;display:flex">
            <div style="padding:0px 5px 5px 5px;width:80px">线下鱼塘</div>
            <span style="color:#fff;position:absolute;z-index: 999;" :style="{left:100+(fishNumPrecent*1.5)+'px'}">{{fishNum}}</span>
            <a-progress  stroke-color="#FF6633" style="width:60%" :percent="fishNumPrecent"/>
            <span style="color:#0272FC">{{fishNumPrecent}}%</span>
          </div>
          <div  style="color:#fff;margin-left:20px;margin-top:5px;display:flex">
            <div style="padding:0px 5px 5px 5px;width:80px">外力破坏</div>
            <span style="color:#fff;position:absolute;z-index: 999;" :style="{left:100+(breakNumPrecent*1.5)+'px'}">{{breakNum}}</span>
            <a-progress  stroke-color="#FF6633" style="width:60%" :percent="breakNumPrecent"/>
            <span style="color:#0272FC">{{breakNumPrecent}}%</span>
          </div>
          <div  style="color:#fff;margin-left:20px;margin-top:5px;display:flex">
            <div style="padding:0px 5px 5px 5px;width:80px">森草火情</div>
            <span style="color:#fff;position:absolute;z-index: 999;" :style="{left:100+(fireNumPrecent*1.5)+'px'}">{{fireNum}}</span>
            <a-progress  stroke-color="#FF6633" style="width:60%" :percent="fireNumPrecent"/>
            <span style="color:#0272FC">{{fireNumPrecent}}%</span>
          </div>
          <div  style="color:#fff;margin-left:20px;margin-top:5px;display:flex">
            <div style="padding:0px 5px 5px 5px;width:80px">窃电</div>
            <span style="color:#fff;position:absolute;z-index: 999;" :style="{left:100+(stealNumPrecent*1.5)+'px'}">{{stealNum}}</span>
            <a-progress  stroke-color="#FF6633" style="width:60%" :percent="stealNumPrecent"/>
            <span style="color:#0272FC">{{stealNumPrecent}}%</span>
          </div>
          <div  style="color:#fff;margin-left:20px;margin-top:5px;display:flex">
            <div style="padding:0px 5px 5px 5px;width:80px">其他</div>
            <span style="color:#fff;position:absolute;z-index: 999;" :style="{left:100+(hiddenOtherNumPrecent*1.5)+'px'}">{{hiddenOtherNum}}</span>
            <a-progress  stroke-color="#FF6633" style="width:60%" :percent="hiddenOtherNumPrecent"/>
            <span style="color:#0272FC">{{hiddenOtherNumPrecent}}%</span>
          </div> -->
                </div>
              </div>
              <div class="dashlineheight"></div>
              <div style="width:50%">
                <div style="color:#fff;padding:5px;font-size:16px;text-align:center">联动协调事项</div>
                <pepEcharts
                  :key="echartkey"
                  style="height:70%"
                  ref="pepEcharts"
                  chartId="pepEcharts"
                ></pepEcharts>
                <div style="color:#ccc;padding:5px;font-size:14px">注：联动协调事项指乡镇村级组织协助电网企业开展重难点问题协调工作</div>
              </div>
            </div>
          </div>
          <div
            class="border-radius"
            style="width:24.5%;height: 100%;"
          >
            <div
              class=""
              style="margin-left:20px;height: 10%;"
            >
              <div style="padding:10px;display: flex;align-items: center;">
                <img
                  src="@/assets/images/newvisi/u157.svg"
                  alt=""
                >
                <img
                  src="@/assets/images/newvisi/u157.svg"
                  alt=""
                >
                <img
                  src="@/assets/images/newvisi/u157.svg"
                  alt=""
                >
                <span style="color:#00FCFC;font-size:18px;margin-left:20px">节能低碳
                </span>
              </div>
            </div>
            <div style="color:#fff;height:40%">
              <div style="margin-left:20px;font-size: 16px;text-align:center;margin-bottom: 5px;">错避峰用电引导</div>
              <div class="visicontentflex">
                <div
                  class="flexcenter"
                  style="text-align: center;width:50%"
                >
                  <div class="titfc">迎峰度夏</div>
                  <div>
                    <span class="numfc">{{ yfdx }}</span>
                    <span class="zwfc">次</span>
                  </div>
                </div>
                <div
                  class="flexcenter"
                  style="text-align: center;width:50%"
                >
                  <div class="titfc">迎峰度冬</div>
                  <div>
                    <span class="numfc">{{ yfdd }}</span>
                    <span class="zwfc">次</span>
                  </div>
                </div>
                <div
                  class="flexcenter"
                  style="text-align: center;width:50%"
                >
                  <div class="titfc">春节用电</div>
                  <div>
                    <span class="numfc">{{ cjyd }}</span>
                    <span class="zwfc">次</span>
                  </div>
                </div>
                <div
                  class="flexcenter"
                  style="text-align: center;width:50%"
                >
                  <div class="titfc">春耕春灌</div>
                  <div>
                    <span class="numfc">{{ cgcg }}</span>
                    <span class="zwfc">次</span>
                  </div>
                </div>
              </div>
            </div>
            <div style="color:#fff;height:40%;margin-top:20px">
              <div style="margin-left:20px;font-size: 16px;text-align:center;margin-bottom: 5px;">农业生产供电保障</div>
              <div class="visicontentflex">
                <div
                  class="flexcenter"
                  style="text-align: center;width:50%"
                >
                  <div class="titfc">机井灌溉</div>
                  <div>
                    <span class="numfc">{{ jjgg }}</span>
                    <span class="zwfc">次</span>
                  </div>
                </div>
                <div
                  class="flexcenter"
                  style="text-align: center;width:50%"
                >
                  <div class="titfc">机电灌溉</div>
                  <div>
                    <span class="numfc">{{ jdgg }}</span>
                    <span class="zwfc">次</span>
                  </div>
                </div>
                <div
                  class="flexcenter"
                  style="text-align: center;width:50%"
                >
                  <div class="titfc">防汛排涝</div>
                  <div>
                    <span class="numfc">{{ fxpl }}</span>
                    <span class="zwfc">次</span>
                  </div>
                </div>
                <div
                  class="flexcenter"
                  style="text-align: center;width:50%"
                >
                  <div class="titfc">其他</div>
                  <div>
                    <span class="numfc">{{ qt }}</span>
                    <span class="zwfc">次</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div
            class="border-radius"
            style="width:24.5%"
          >
            <div
              class=""
              style="margin-left:20px;height:10%"
            >
              <div style="padding:10px;display: flex;align-items: center;">
                <img
                  src="@/assets/images/newvisi/u157.svg"
                  alt=""
                >
                <img
                  src="@/assets/images/newvisi/u157.svg"
                  alt=""
                >
                <img
                  src="@/assets/images/newvisi/u157.svg"
                  alt=""
                >
                <span style="color:#00FCFC;font-size:18px;margin-left:20px;margin-top:3px">成果展示</span>
              </div>
            </div>
            <div
              class="discenter"
              style="height:40%"
            >
              <!-- :autoplaySpeed="500" -->
              <a-carousel
                autoplay
                style="width: 25vh; height: 15vh"
                arrows
              >
                <template #prevArrow>
                  <a-icon
                    type="left"
                    class="bluesel"
                    style="left: -40px;font-size:25px;z-index: 1;"
                  />
                </template>
                <template #nextArrow>
                  <a-icon
                    type="right"
                    class="bluesel"
                    style="right: -40px;font-size:25px;z-index: 1;"
                  />
                </template>
                <el-image
                  v-for="(item, index) in cg.baseInfoContentFileList"
                  :key="index"
                  style="width: 25vh; height: 15vh"
                  :src="`${imgViewHost}${item.fileNo}`"
                  :preview-src-list="[`${imgViewHost}${item.fileNo}`]"
                >
                </el-image>
              </a-carousel>
            </div>
            <div
              class="visicontent contenttext"
              style="height:40%"
            >
              <div
                class="contebox"
                style="width:100%;height:100%;overflow: auto;"
              >{{ cg.contentData }}</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { homecityrankingApi, queryDetailApi, pageInfoApi, playVideoApi } from '@/api/home/home.js'
import moment from 'moment'
import {
  queryList,
  findTreeTown,
  convenFindMaxTime,
  convenCloud,
  convenList,
  carbonList,
  carbonProducer,
  convenSpecial,
  convenConsumerElec,
  convenOnlineMap,
  electricSpread,
  electricList,
  electricJoint,
  solarTerms,
  queryDetail,
} from '@/api/home/visi.js'
import { mapActions, mapGetters } from 'vuex'
import { TreeSelect } from 'ant-design-vue'
import pepEcharts from './eacharts/pepEcharts.vue'
import { baseInfoApi } from '@/api/gridmanager/manager.js'
const SHOW_PARENT = TreeSelect.SHOW_PARENT
export default {
  components: {
    pepEcharts,
  },
  data() {
    return {
      spreadList: [],
      echartkey: 0,
      cunName: '',
      jp_week: '',
      jp_date: '',
      benmon: [],
      xiamon: [],
      bm: {
        townFileList: [],
      },
      cg: {
        townFileList: [],
      },
      eachartData: [],
      knowRate: '',
      activityRate: '',
      customFeedbackNum: '',
      customRegistNum: '',
      specialPeopleNum: '',
      specialServiceNum: '',
      RESIDENT_USER: '',
      CONSUMER_ELECTRIC: '',
      RESIDENT_USER_CHAIN_BASE: '',
      CONSUMER_ELECTRIC_CHAIN_BASE: '',
      LINE_PAYFEE_RATE: '',
      LINE_HANDLE_RATE: '',
      LINE_HANDLE_CHAIN_BASE: '',
      LINE_PAYFEE_CHAIN_BASE: '',
      yfdx: '',
      yfdd: '',
      cjyd: '',
      cgcg: '',
      jjgg: '',
      jdgg: '',
      fxpl: '',
      qt: '',
      DANGER_TREAT_NUM: '',
      DANGER_TROUBLE_NUM: '',
      tallNumPrecent: 0,
      fishNumPrecent: 0,
      breakNumPrecent: 0,
      fireNumPrecent: 0,
      stealNumPrecent: 0,
      hiddenOtherNumPrecent: 0,
      tallNum: '',
      fishNum: '',
      breakNum: '',
      fireNum: '',
      stealNum: '',
      hiddenOtherNum: '',
      maxTime: '',
      lastTime: '',
      suoNo: '',
      zhengNo: '',
      cunNo: '',
      gdsList: [],
      suoList: [],
      zhengList: [],
      cunList: [],
      monthTime: '',
      SHOW_PARENT,
      ORG_NO: null,
      treeData: [],
      featureImgViewList: [],
      imgViewHost: '/uds-file/down-file/',
      baseInfo: {},
      isFullScreen: false,
      rankingArr: [], // 排名列表
      nowMonthRanking: {
        monthChain: 0,
        monthMark: ['0', '0', '0', '.', '0', '0'],
        countryChain: 0,
        countryRank: ['0', '0', '0'],
        cityChain: 0,
        cityRank: ['0', '0', '0'],
      },
      videoUrl: '',
      ScrollTimer: null,
      featureTagData: [], // 供电所特色顶部标签页
      featureAllData: [], // 供电所特色全量数据
      featureColumnData: [], // 供电所特色标签页选中时对应的数据列表
      featureIndex: '', // 当前选中的标签页
      featurePage: 0, // 当前选中的页码
      orgNo: '',
      villageNo: '',
    }
  },
  created() {
    this.getfindTreeTown()
    // this.getMaxTime()
    // this.getmonthTime()
  },
  mounted() {
    if (location.origin.indexOf('localhost') !== -1) {
      this.imgViewHost = 'http://192.168.66.20:18080/uds-file/down-file/'
    }
    var weekarr = new Array('日', '一', '二', '三', '四', '五', '六')
    var myDate = new Date()
    var year = myDate.getFullYear()
    var month = myDate.getMonth() + 1
    var date = myDate.getDate()
    var hours = myDate.getHours()
    this.jp_week = '星期' + weekarr[new Date().getDay()]
    this.jp_date = year + '-' + month + '-' + date
    // this.getTreeSelectData()
  },
  watch: {
    ORG_NO() {
      this.getOrgTitle()
      this.getRanking()
      this.getcolData()
    },
    lastTime() {
      //线上业务统计
      convenOnlineMap({ villageNo: this.cunNo, orgNo: this.suoNo, townNo: this.zhengNo, ym: this.lastTime }).then(
        (res) => {
          if (!res.data) return
          this.LINE_PAYFEE_RATE = Number(res.data.LINE_PAYFEE_RATE).toFixed(2)
          this.LINE_HANDLE_CHAIN_BASE = res.data.LINE_HANDLE_CHAIN_BASE
          this.LINE_HANDLE_RATE = Number(res.data.LINE_HANDLE_RATE).toFixed(2)
          this.LINE_PAYFEE_CHAIN_BASE = res.data.LINE_PAYFEE_CHAIN_BASE
        }
      )
    },
    maxTime() {
      //用户用电
      convenConsumerElec({ villageNo: this.cunNo, orgNo: this.suoNo, townNo: this.zhengNo, ym: this.maxTime }).then(
        (res) => {
          this.RESIDENT_USER = res.data.RESIDENT_USER
          this.CONSUMER_ELECTRIC = res.data.CONSUMER_ELECTRIC
          this.RESIDENT_USER_CHAIN_BASE = res.data.RESIDENT_USER_CHAIN_BASE
          this.CONSUMER_ELECTRIC_CHAIN_BASE = res.data.CONSUMER_ELECTRIC_CHAIN_BASE
        }
      )
    },
    cunNo() {
      this.getconven()
      this.getlist()
      this.cunName = this.cunList.find((e) => e.value == this.cunNo).title
    },
  },
  beforeDestroy() {
    clearInterval(this.ScrollTimer)
  },
  methods: {
    ...mapGetters(['userInfo']),
    lastTimeChange(date, dateString) {
      this.lastTime = dateString
    },
    maxTimeChange(date, dateString) {
      this.maxTime = dateString
    },
    getconven() {
      const newyear = new Date().getFullYear()
      //二十四节气
      solarTerms({ villageNo: this.cunNo }).then((res) => {
        if (res.data.length == 0) {
          this.benmon = []
          this.xiamon = []
          return
        }
        this.benmon = []
        this.xiamon = []

        if (res.data.length > 0) this.benmon.push(res.data[0])
        if (res.data.length > 1) this.benmon.push(res.data[1])
        if (res.data.length > 2) this.xiamon.push(res.data[2])
        if (res.data.length > 3) this.xiamon.push(res.data[3])
      })
      //网格云电话
      convenCloud({ villageNo: this.cunNo, orgNo: this.suoNo, townNo: this.zhengNo, ym: this.lastTime }).then((res) => {
        if (!res.data) return
        this.knowRate = res.data.knowRate
        this.activityRate = res.data.activityRate
      })
      //客户诉求管理
      convenList({ villageNo: this.cunNo, orgNo: this.suoNo, townNo: this.zhengNo, ym: newyear }).then((res) => {
        if (!res.data) return
        this.customFeedbackNum = res.data.customFeedbackNum
        this.customRegistNum = res.data.customRegistNum
      })
      //节能低碳
      carbonList({ villageNo: this.cunNo, orgNo: this.suoNo, townNo: this.zhengNo, ym: newyear }).then((res) => {
        if (!res.data) return
        this.yfdx = res.data.find((e) => e.elecGuideType == '01').elecNum
        this.yfdd = res.data.find((e) => e.elecGuideType == '02').elecNum
        this.cjyd = res.data.find((e) => e.elecGuideType == '03').elecNum
        this.cgcg = res.data.find((e) => e.elecGuideType == '04').elecNum
      })
      //农业生产供电保障
      carbonProducer({ villageNo: this.cunNo, orgNo: this.suoNo, townNo: this.zhengNo, ym: newyear }).then((res) => {
        if (!res.data) return
        this.jjgg = res.data.find((e) => e.elecSupplyType == '06').supplyNum
        this.jdgg = res.data.find((e) => e.elecSupplyType == '07').supplyNum
        this.fxpl = res.data.find((e) => e.elecSupplyType == '08').supplyNum
        this.qt = res.data.find((e) => e.elecSupplyType == '09').supplyNum
      })
      //特殊群体服务
      convenSpecial({ villageNo: this.cunNo, orgNo: this.suoNo, townNo: this.zhengNo, ym: newyear }).then((res) => {
        if (!res.data) return
        this.specialPeopleNum = res.data.specialPeopleNum
        this.specialServiceNum = res.data.specialServiceNum
      })
      //用户用电
      convenConsumerElec({ villageNo: this.cunNo, orgNo: this.suoNo, townNo: this.zhengNo, ym: this.maxTime }).then(
        (res) => {
          if (!res.data) return
          this.RESIDENT_USER = res.data.RESIDENT_USER
          this.CONSUMER_ELECTRIC = res.data.CONSUMER_ELECTRIC
          this.RESIDENT_USER_CHAIN_BASE = res.data.RESIDENT_USER_CHAIN_BASE
          this.CONSUMER_ELECTRIC_CHAIN_BASE = res.data.CONSUMER_ELECTRIC_CHAIN_BASE
        }
      )
      //线上业务统计
      convenOnlineMap({ villageNo: this.cunNo, orgNo: this.suoNo, townNo: this.zhengNo, ym: this.lastTime }).then(
        (res) => {
          if (!res.data) return
          this.LINE_PAYFEE_RATE = Number(res.data.LINE_PAYFEE_RATE).toFixed(2)
          this.LINE_HANDLE_CHAIN_BASE = res.data.LINE_HANDLE_CHAIN_BASE
          this.LINE_HANDLE_RATE = Number(res.data.LINE_HANDLE_RATE).toFixed(2)
          this.LINE_PAYFEE_CHAIN_BASE = res.data.LINE_PAYFEE_CHAIN_BASE
        }
      )
      //电力隐患分布统计
      electricSpread({ villageNo: this.cunNo, orgNo: this.suoNo, townNo: this.zhengNo, ym: newyear })
        .then((res) => {
          if (!res.data)
            return (this.spreadList = [
              {
                num: 0,
                percent: 0,
                name: '超高树竹',
              },
              {
                num: 0,
                percent: 0,
                name: '线下鱼塘',
              },
              {
                num: 0,
                percent: 0,
                name: '外力破坏',
              },
              {
                num: 0,
                percent: 0,
                name: '森草火情',
              },
              {
                num: 0,
                percent: 0,
                name: '窃电',
              },
              {
                num: 0,
                percent: 0,
                name: '其他',
              },
            ])
          this.tallNumPrecent = res.data.tallNumPrecent
          this.tallNum = res.data.tallNum
          this.fishNumPrecent = res.data.fishNumPrecent
          this.fishNum = res.data.fishNum
          this.breakNumPrecent = res.data.breakNumPrecent
          this.breakNum = res.data.breakNum
          this.fireNumPrecent = res.data.fireNumPrecent
          this.fireNum = res.data.fireNum
          this.stealNumPrecent = res.data.stealNumPrecent
          this.stealNum = res.data.stealNum
          this.hiddenOtherNumPrecent = res.data.hiddenOtherNumPrecent
          this.hiddenOtherNum = res.data.hiddenOtherNum
          this.spreadList = []
          this.spreadList.push({
            num: res.data.tallNum,
            percent: +res.data.tallNumPrecent,
            name: '超高树竹',
          })
          this.spreadList.push({
            num: res.data.fishNum,
            percent: +res.data.fishNumPrecent,
            name: '线下鱼塘',
          })
          this.spreadList.push({
            num: res.data.breakNum,
            percent: +res.data.breakNumPrecent,
            name: '外力破坏',
          })
          this.spreadList.push({
            num: res.data.fireNum,
            percent: +res.data.fireNumPrecent,
            name: '森草火情',
          })
          this.spreadList.push({
            num: res.data.stealNum,
            percent: +res.data.stealNumPrecent,
            name: '窃电',
          })
          this.spreadList.push({
            num: res.data.hiddenOtherNum,
            percent: +res.data.hiddenOtherNumPrecent,
            name: '其他',
          })
          this.spreadList = this.setArray(this.spreadList)

          // this.spreadList=this.spreadList.reverse()
          console.log(this.spreadList, 'spreadList')
        })
        .catch((err) => {
          this.spreadList = [
            {
              num: 0,
              percent: 0,
              name: '超高树竹',
            },
            {
              num: 0,
              percent: 0,
              name: '线下鱼塘',
            },
            {
              num: 0,
              percent: 0,
              name: '外力破坏',
            },
            {
              num: 0,
              percent: 0,
              name: '森草火情',
            },
            {
              num: 0,
              percent: 0,
              name: '窃电',
            },
            {
              num: 0,
              percent: 0,
              name: '其他',
            },
          ]
        })
      //电力隐患排查-隐患治理
      electricList({ villageNo: this.cunNo, orgNo: this.suoNo, townNo: this.zhengNo, ym: newyear }).then((res) => {
        if (!res.data) return
        this.DANGER_TREAT_NUM = res.data.DANGER_TREAT_NUM + ''
        this.DANGER_TROUBLE_NUM = res.data.DANGER_TROUBLE_NUM + ''
        // this.DANGER_TREAT_NUM=1+''
        // this.DANGER_TROUBLE_NUM=1+''
      })
      //玫瑰花
      electricJoint({ villageNo: this.cunNo, orgNo: this.suoNo, townNo: this.zhengNo, ym: newyear })
        .then((res) => {
          if (!res.data) {
            this.eachartData = [
              {
                name: '暂无数据',
                value: 0,
                num: 0,
              },
            ]
            return this.$refs.pepEcharts.myEcharts(this.eachartData)
          }
          this.eachartData = []
          if (+res.data.visionNum) {
            this.eachartData.push({
              name: '线路巡视',
              value: res.data.visionNumPrecent,
              num: res.data.visionNum,
            })
          }
          if (+res.data.shareNum) {
            this.eachartData.push({
              name: '信息共享',
              value: res.data.shareNumPrecent,
              num: res.data.shareNum,
            })
          }
          if (+res.data.unityNum) {
            this.eachartData.push({
              name: '电力施工协调',
              value: res.data.unityNumPrecent,
              num: res.data.unityNum,
            })
          }
          if (+res.data.issueNum) {
            this.eachartData.push({
              name: '用电纠纷化解',
              value: res.data.issueNumPrecent,
              num: res.data.issueNum,
            })
          }
          if (+res.data.otherNum) {
            this.eachartData.push({
              name: '其他',
              value: res.data.otherNumPrecent,
              num: res.data.otherNum,
            })
          }

          // {
          //   name: '电力施工协调',
          //   value: res.data.unityNumPrecent,
          //   num: res.data.unityNum,
          // },
          // {
          //   name: '用电纠纷化解',
          //   value: res.data.issueNumPrecent,
          //   num: res.data.issueNum,
          // },
          // {
          //   name: '其他',
          //   value: res.data.otherNumPrecent,
          //   num: res.data.otherNum,
          // },
          // ]
          console.log(this.eachartData)
          // this.echartkey++
          this.$refs.pepEcharts.myEcharts(this.eachartData)
        })
        .catch((err) => {
          this.eachartData = [
            {
              name: '暂无数据',
              value: 0,
              num: 0,
            },
          ]
          this.$refs.pepEcharts.myEcharts(this.eachartData)
        })
    },
    getMaxTime() {
      convenFindMaxTime({ villageNo: this.cunNo, orgNo: this.suoNo, townNo: this.zhengNo }).then((res) => {
        if (res.data) {
          this.maxTime = res.data.YM
        } else {
          this.maxTime = this.$lastMonth
        }
        this.lastTime = this.$lastMonth
        this.getconven()
      })
    },
    gdsListselect() {
      this.suoList = this.gdsList.find((e) => e.value == this.orgNo).children
    },
    suoListselect(value, option) {
      console.log(value, 'suoListselect')
      // this.zhengNo = undefined
      // this.cunNo = undefined
      // if (value == undefined) {
      //   this.cunList = []
      //   this.zhengList = []
      // } else {
      //   this.isZhen = false
      // }
      this.zhengList = this.suoList.find((e) => e.value == this.suoNo).children
      this.zhengNo = this.suoList.find((e) => e.value == this.suoNo).children[0].value
      this.cunList = this.zhengList.find((e) => e.value == this.zhengNo).children
      this.cunNo = this.suoList.find((e) => e.value == this.suoNo).children[0].children[0].value
      console.log(this.suoList.find((e) => e.value == this.suoNo),'this.suoList.find((e) => e.value == this.suoNo)')
    },
    zhengListselect(value, option) {
      // this.cunNo = undefined
      // if (value == undefined) {
      //   this.cunList = []
      // } else {
        // this.isZhen = false
      // }
      this.cunList = this.zhengList.find((e) => e.value == this.zhengNo).children
      // this.cunNo = this.suoList.find((e) => e.value == this.suoNo).children[0].children[0].value
      this.cunNo = this.cunList[0].value
    },
    cunselect(value, option) {
      // if (value !== undefined) {
      //   this.isCun = false
      // }
    },
    getlist() {
      queryDetail({ orgNo: this.suoNo, topicType: '10' }).then((res) => {
        if (res.data.length == 0) {
          this.bm = []
          return
        }
        this.bm = res.data[0]
      })
      queryDetail({ orgNo: this.suoNo, topicType: '11' }).then((res) => {
        if (res.data.length == 0) {
          this.cg = []
          return
        }
        this.cg = res.data[0]
      })
      // queryDetail({orgNo:this.suoNo,topicType: "11"}).then(res=>{
      //   if(res.data.length==0){
      //     this.bm=[]
      //     this.cg=[]
      //     return}
      //  this.bm=res.data.find(e=>e.contentType=='01')
      //  this.cg=res.data.find(e=>e.contentType=='02')
      // })
    },
    getfindTreeTown() {
      // console.log(this.userInfo(),'this.userInfo()')
      findTreeTown({ orgNo: this.userInfo().orgCode }).then((res) => {
        const data = JSON.parse(res.data)
        console.log(data)
        this.gdsList = data
        console.log(this.userInfo())
        // if(this.userInfo().orgCode.length==9){
        //  let orgNosel= this.userInfo().orgCode.substr(0,7)
        //  console.log(orgNosel)
        //  this.gdsList= [this.gdsList.find(e=>e.value==orgNosel)]
        //  console.log(this.gdsList)
        // }
        this.orgNo = this.gdsList[0].value
        this.suoList = this.gdsList.find((e) => e.value == this.orgNo).children
        this.suoNo = this.suoList[0].value
        this.zhengList = this.suoList.find((e) => e.value == this.suoNo).children
        this.zhengNo = this.zhengList[0].value
        this.cunList = this.zhengList.find((e) => e.value == this.zhengNo).children
        this.cunNo = this.cunList[0].value
        console.log(JSON.parse(res.data))
        this.getMaxTime()
        this.getlist()
      })
    },
    gohome() {
      this.$router.push({ name: 'viewhome' })
    },
    getmonthTime() {
      this.monthTime = this.$lastMonth
      // let Date1 = new Date().getDate()
      // if (Date1 <= 5) {
      //   this.monthTime = this.$lastMonth3
      // }else{
      //   this.monthTime = this.$lastMonth
      // }
    },
    monthTimePickers(date, dateString) {
      this.monthTime = dateString
    },
    getTreeSelectData() {
      getTreeDataApi({ ORG_NO: this.userInfo().orgCode }).then((res) => {
        this.treeData = this.renderTreeNodes(JSON.parse(res.data))
        console.log(this.treeData, 'treeData')
      })
    },
    renderTreeNodes(data) {
      const setData = data.map((item) => {
        // if (item.children && item.children.length) {
        //   item.disabled = true
        //   this.renderTreeNodes(item.children)
        // }
        // if((!this.ORG_NO) && (!item.children || item.children.length == 0)) {
        //   this.ORG_NO = item.key
        // }
        if (item.children && item.children.length) {
          item.disabled = true
          this.renderTreeNodes(item.children)
        } else if (item.level <= 3) {
          item.disabled = true
        }
        if (!this.ORG_NO && !(item.children && item.children.length) && item.level >= 4) {
          this.ORG_NO = item.key
        }
        return item
      })
      return setData
    },
    // 特色轮播查看大图
    getFeatureImgView() {
      this.featureImgViewList = []
      if (
        this.featureColumnData.length > 0 &&
        this.featureColumnData[this.featurePage].baseInfoContentFileList &&
        this.featureColumnData[this.featurePage].baseInfoContentFileList.length > 0
      ) {
        this.featureColumnData[this.featurePage].baseInfoContentFileList.forEach((item) => {
          this.featureImgViewList.push(this.imgViewHost + item.fileNo)
        })
      }
    },
    getVideo() {
      if (this.featureColumnData.length > 0 && this.featureColumnData[this.featurePage].supportMode == '02') {
        const fileNo = this.featureColumnData[this.featurePage].baseInfoContentFileList[0].fileNo
        playVideoApi({ fileNo }).then((res) => {
          this.videoUrl = res.data
        })
      }
    },
    // 顶部tab切换
    changeTab(id) {
      this.featureIndex = id
      this.featurePage = 0
      this.filterColumnData(this.featureIndex)
      // this.getFeatureImgView()
      // this.getVideo()
    },
    // 顶部栏目列表
    getcolData() {
      const params = {
        ORG_NO: this.ORG_NO,
        TOPIC_TYPE: '04',
        TOPIC_STATUS: '01',
      }
      pageInfoApi(params).then((res) => {
        this.featureTagData = res.data.records
        this.featureIndex = this.featureTagData[0].ID
        this.getFeatureData()
      })
    },
    // 获取供电所特色全量数据（分页需要前端自己处理）
    getFeatureData() {
      const params = {
        orgNo: this.ORG_NO,
        topicType: '04',
      }
      queryDetailApi(params).then((res) => {
        this.featureAllData = res.data
        this.filterColumnData(this.featureIndex)
        this.getVideo()
      })
    },
    // 筛选要展示的栏目
    filterShowData(index) {
      this.featurePage = index
      this.getFeatureImgView()
      this.getVideo()
    },
    // 整合每个栏目类型的条数
    filterColumnData(id) {
      this.featureColumnData = this.featureAllData.filter((item) => {
        if (id == item.topicId) {
          return true
        }
        return false
      })
    },
    // 供电所基本信息，主要是名称名称
    getOrgTitle() {
      baseInfoApi({ ORG_NO: this.ORG_NO }).then((res) => {
        this.baseInfo = res.data[0]
      })
    },
    // 获取每月排名
    getRanking() {
      const Date1 = new Date().getDate()
      let yM1 = ''
      if (Date1 <= 5) {
        yM1 = this.$lastMonth3
      } else {
        yM1 = this.$lastMonth
      }

      const params = {
        ORG_NO: this.ORG_NO,
        // yM: this.$configDay('2', 1, 'yyyy-MM'),
        yM: yM1,
      }
      homecityrankingApi(params).then((res) => {
        console.log(res, 'quans')
        this.rankingArr = res.data.ranking
        // 本月排名相关数据处理
        this.nowMonthRanking.monthChain = Number(this.rankingArr[0].ratioTotalMark).toFixed(0)
        this.nowMonthRanking.countryChain = Number(this.rankingArr[0].ratioContyRanking)
        this.nowMonthRanking.cityChain = Number(this.rankingArr[0].ratioCityRanking)
        let countryList = []
        let cityList = []
        let totalScoreList = []
        countryList = this.rankingArr[0].contyRanking.split('')
        cityList = this.rankingArr[0].cityRanking.split('')
        totalScoreList = Number(this.rankingArr[0].totalMark).toFixed(2).split('')
        this.nowMonthRanking.countryRank.splice(3 - countryList.length, countryList.length, ...countryList)
        this.nowMonthRanking.cityRank.splice(3 - cityList.length, cityList.length, ...cityList)
        this.nowMonthRanking.monthMark.splice(6 - totalScoreList.length, totalScoreList.length, ...totalScoreList)
      })
    },
    compare(property) {
      return function (a, b) {
        return b[property] - a[property]
      }
    },
    setArray(arr) {
      arr.sort(this.compare('num'))
      console.log(arr)
      return arr
    },
    getPopupContainer() {
      return this.$refs.home
    },
    enterfullscreen() {
      //进入全屏
      this.isFullScreen = true
      const docElm = this.$refs.home // 指定容器id
      //W3C
      if (docElm.requestFullscreen) {
        docElm.requestFullscreen()
      }
      //FireFox
      else if (docElm.mozRequestFullScreen) {
        docElm.mozRequestFullScreen()
      }
      //Chrome等
      else if (docElm.webkitRequestFullScreen) {
        docElm.webkitRequestFullScreen()
      }
      //IE11
      else if (docElm.msRequestFullscreen) {
        docElm.msRequestFullscreen()
      }
      this.getconven()
      this.getlist()
      // this.$refs.portrait.cleartime()
      // this.$refs.portrait.getPortraitData()
      console.log(docElm.style)
    },
    showImageView() {
      setTimeout(() => {
        const docElm = this.$refs.home
        if (document.getElementsByClassName('el-image-viewer__wrapper').length > 0) {
          docElm.appendChild(document.getElementsByClassName('el-image-viewer__wrapper')[0])
        }
      }, 10)
    },
    //退出全屏
    exitfullscreen() {
      this.isFullScreen = false
      if (document.exitFullscreen) {
        document.exitFullscreen()
      } else if (document.mozCancelFullScreen) {
        document.mozCancelFullScreen()
      } else if (document.webkitCancelFullScreen) {
        document.webkitCancelFullScreen()
      } else if (document.msExitFullscreen) {
        document.msExitFullscreen()
      }
      // this.$refs.portrait.cleartime()
      // this.$refs.portrait.getPortraitData()
      this.getconven()
      this.getlist()
    },
  },
}
</script>

<style lang="less" scoped>
.hmb-area-3 {
  width: 26%;
  height: 100%;
  border: solid 1px #1e5377;
}
.hmb-area-4 {
  width: 47%;
  height: 100%;
  border: solid 1px #1e5377;
}
.hmb-area-5 {
  width: 26%;
  height: 100%;
  border: solid 1px #1e5377;
  .hmb-right {
    width: 100%;
    height: 85%;
    padding: 0.5vw;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    .hmbr-bottom {
      width: 100%;
      height: 60%;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      .hb-title {
        width: 100%;
        height: 15%;
        display: flex;
        justify-content: center;
        align-items: center;
        border-bottom: solid 1px #81d3f8;
        .title-item {
          width: 25%;
          text-align: center;
          color: #81d3f8;
        }
      }
      .hb-list {
        width: 100%;
        height: 80%;
        overflow-y: scroll;
        // border: solid 1px #1e5377;
        .list-item {
          width: 100%;
          height: 15%;
          display: flex;
          justify-content: center;
          align-items: center;
          // border: solid 1px #1e5377;
          .list-item-col {
            height: 100%;
            width: 25%;
            display: flex;
            justify-content: center;
            .lic-value {
              height: 95%;
              width: 40%;
              display: flex;
              justify-content: center;
              align-items: center;
              color: #fff;
              border-radius: 5px;
              min-height: 12px;
              min-width: 48px;
            }
          }
        }
      }
      .hb-list::-webkit-scrollbar {
        display: none;
      }
    }
  }
}
.header {
  position: relative;
  width: 100%;
  height: 15%;
  background: none !important;
}
.titleclass {
  position: absolute;
  top: 0.3vw;
  left: 0;
  right: 0;
  color: #fff;
  text-align: center;
  font-size: 0.85vw;
  font-weight: 700;
}
.monthclass {
  position: absolute;
  top: 0.3vw;
  width: 5vw;
  z-index: 10;
  right: 3vw;
}
.monthclass2 {
  width: 5vw;
  z-index: 10;
  color: #00fffc;
  border: 1px solid #00fffc;
  margin-left: 50px;
  position: absolute;
  right: 3px;
  top: 18px;
}
/deep/ .ant-select-selection {
  background-color: rgba(26, 39, 64, 0.1) !important;
  border: 1px solid #1a2740;
  color: #00fcfc;
}
.home {
  height: 100%;
  width: 100%;
  background: linear-gradient(rgba(0, 0, 0, 0.35), rgba(0, 0, 0, 0.35)),
    url('~@/assets/images/newvisi/u60.jpg') 0 0 no-repeat;
  background-color: rgba(5, 18, 54, 1);
  background-size: 100% 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  position: relative;
  .home-header {
    position: relative;
    height: 5%;
    width: 95%;
    // background: url('~@/assets/images/newvisi/titleback.png') 0 0 no-repeat;
    background-size: 100% 100%;
    font-size: 2vh;
    color: #fff;
    font-weight: 700;
    display: flex;
    justify-content: center;
    align-items: center;
    img {
      width: 28%;
      height: 130%;
    }
    .home-header-select {
      width: 10vw;
      position: absolute;
      top: 0.1vw;
      left: 4vw;
    }
  }
  .home-main {
    height: 95%;
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    .home-main-top {
      height: 50%;
      width: 100%;
      padding: 0.5vw;
      display: flex;
      justify-content: space-between;
      .hmt-right {
        // flex: 1;
        width: 50%;
        height: 100%;
        padding-left: 1.5vw;
        padding-top: 1.5vw;
        padding-right: 0.5vw;
        display: flex;
        border: 1px solid #1a9cc6;
        flex-direction: column;
        .hmtr-tab {
          height: 12%;
          width: 100%;
          // border: 1px solid #1a9cc6;
          display: flex;
          justify-content: flex-start;
          align-items: center;
          .tab-item {
            width: 16%;
            height: 75%;
            font-size: 16px;
            border: 1px solid #1a9cc6;
            transform: skew(-20deg);
            margin-left: 0.5vw;
            background-color: #59deff;
            display: flex;
            justify-content: center;
            align-items: center;
            color: #333;
            .ti-text {
              transform: skew(20deg);
            }
          }
          .tab-item-select {
            color: #fff;
            font-weight: 700;
            background-color: #02a7f0;
          }
        }
        .hmtr-content {
          margin: 3% 0;
          height: 63%;
          width: 100%;
          display: flex;
          justify-content: space-between;
          .hc-media {
            width: 49%;
            height: 100%;
            .media-img {
              width: 100% !important;
              height: 110% !important;
              background-color: #000;
            }
          }
          .media-carousel {
            width: 100% !important;
            height: 100% !important;
            .media-img-item {
              width: 100%;
              height: 28vh;
            }
          }
          .hc-main {
            width: 49%;
            height: 100%;
            display: flex;
            flex-direction: column;
            .hcm-title {
              width: 100%;
              height: 15%;
              font-size: 15px;
              font-weight: 700;
              color: #81d3f8;
            }
            .hcm-content {
              width: 100%;
              height: 85%;
              font-size: 14px;
              color: #fff;
              overflow-y: scroll;
              white-space: pre-line;
            }
            .hcm-content::-webkit-scrollbar {
              display: none;
            }
          }
        }
        .hmtr-page {
          height: 10%;
          width: 100%;
          display: flex;
          justify-content: flex-end;
          align-items: center;
          .page-item {
            width: 1vw;
            height: 1.5vw;
            margin-right: 0.3vw;
            border: 1px solid #02a7f0;
            display: flex;
            color: #02a7f0;
            font-size: 0.9vw;
            justify-content: center;
            align-items: center;
          }
          .page-item-select {
            background-color: #81d3f8;
            color: #fff;
          }
        }
      }
    }
    .hmb-area {
      height: 100%;
      width: 100%;
      display: flex;
      justify-content: space-between;
    }
    .home-main-bottom {
      height: 50%;
      width: 100%;
      padding: 0.5vw;
      .hmb-area > div > div > img {
        width: 90%;
        display: block;
        margin: 0 auto;
        height: 7.6vh;
      }
    }
  }
}
.border-radius {
  border: solid 1px #1a9cc6;
  background: linear-gradient(to left, #00fcfc, #00fcfc) left top no-repeat,
    linear-gradient(to bottom, #00fcfc, #00fcfc) left top no-repeat,
    linear-gradient(to left, #00fcfc, #00fcfc) right top no-repeat,
    linear-gradient(to bottom, #00fcfc, #00fcfc) right top no-repeat,
    linear-gradient(to left, #00fcfc, #00fcfc) left bottom no-repeat,
    linear-gradient(to bottom, #00fcfc, #00fcfc) left bottom no-repeat,
    linear-gradient(to left, #00fcfc, #00fcfc) right bottom no-repeat,
    linear-gradient(to left, #00fcfc, #00fcfc) right bottom no-repeat;
  background-size: 2px 32px, 32px 2px, 2px 32px, 32px 2px;
}
.cursor {
  cursor: pointer;
}
.month-rate {
  color: #239aff;
}
.month-rate-border {
  border: solid 1px #239aff;
}
.country-rate {
  color: #fed52f;
}
.country-rate-border {
  border: solid 1px #fed52f;
}
.city-rate {
  color: #00fffc;
}
.city-rate-border {
  border: solid 1px #00fffc;
}
.first-list {
  background-color: #f59a23;
}
.fullscreen-area {
  position: absolute;
  z-index: 1;
  top: 0.6vw;
  right: 15px;
  .fullscreen-icon {
    font-size: 18px;
    color: #fff;
  }
}
.fullscreen-area2 {
  position: absolute;
  z-index: 1;
  top: 1vw;
  right: 15px;
  .fullscreen-icon {
    font-size: 18px;
    color: #fff;
  }
}
.discenter {
  display: flex;
  align-items: center;
  justify-content: center;
}
.visicontent {
  border-width: 0px;
  // width: 403px;
  height: 150px;
  // background: inherit;
  background-color: rgba(3, 11, 86, 0.309803921568627);
  box-sizing: border-box;
  border-width: 1px;
  border-style: solid;
  border-color: rgba(2, 10, 140, 1);
  border-radius: 17px;
  // border-bottom-right-radius: 0px;
  -moz-box-shadow: none;
  -webkit-box-shadow: none;
  box-shadow: none;
  overflow: auto;
}
.visicontentflex {
  border-width: 0px;
  width: 90%;
  height: 90%;
  // min-height: 100px;
  background-color: rgba(3, 11, 86, 0.309803921568627);
  box-sizing: border-box;
  border-width: 1px;
  border-style: solid;
  border-color: rgba(2, 10, 140, 1);
  border-radius: 17px;
  // border-bottom-right-radius: 0px;
  -moz-box-shadow: none;
  -webkit-box-shadow: none;
  box-shadow: none;
  display: flex;
  flex-flow: wrap;
  margin: 0 auto;
  // overflow: auto;
}
.visicontenttop {
  border-width: 0px;
  width: 46%;
  height: 100%;
  min-height: 100px;
  background-color: rgba(3, 11, 86, 0.309803921568627);
  box-sizing: border-box;
  border-width: 1px;
  border-style: solid;
  border-color: rgba(2, 10, 140, 1);
  border-radius: 17px;
  -moz-box-shadow: none;
  -webkit-box-shadow: none;
  box-shadow: none;
}
.ant-carousel .slick-prev,
.ant-carousel .slick-prev:hover,
.ant-carousel .slick-prev:focus {
  font-size: inherit;
  left: 10px;
  z-index: 2;
  color: blueviolet;
}

.ant-carousel .slick-next,
.ant-carousel .slick-next:hover,
.ant-carousel .slick-next:focus {
  font-size: inherit;
  right: 10px;
  z-index: 2;
  color: blueviolet;
}
.bluesel {
  color: #888 !important;
}
.sblue {
  color: #00fcfc;
}
.sred {
  color: #fba067;
}
.disflex {
  display: flex;
  width: 100%;
}
.sbluebor {
  border: 1px solid #00fcfc;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 3px;
  word-break: break-all;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2; /* 超出几行省略 */
  overflow: hidden;
}
.numfc {
  text-align: center;
  color: #fba067;
  font-size: 22px;
}
.zwfc {
  text-align: center;
  color: #00fcfc;
  font-size: 12px;
  margin-left: 5px;
}
.titfc {
  // color:#00FCFC;
  text-align: center;
  font-size: 16px;
}
.monthclass1 {
  width: 5vw;
  z-index: 10;
  color: #00fffc;
  border: 1px solid #00fffc;
  margin-left: 50px;
  position: absolute;
  right: 3px;
  top: 8px;
}
.svgimg1 {
  background: #0345dc;
  width: 25px;
  height: 25px;
  border-radius: 100%;
  display: flex;
  align-items: center;
  justify-content: center;

  img {
    width: 18px;
    height: 18px;
  }
}
/deep/.ant-calendar-picker-input.ant-input {
  color: #00fffc;
  background: none;
  border: none;
}
.yd {
  display: flex;
  justify-content: space-around;
  .yd-item {
    position: relative;
    width: 46%;
    height: 88px;
    background-color: rgba(52, 57, 136, 1);
  }
  .yd-span {
    display: flex;
    justify-content: space-around;
    align-items: center;
    color: #00fffc;
    margin-top: 12px;
  }
  .yd-item::after {
    content: '';
    display: block;
    position: absolute;
    top: 0;
    right: 0;
    display: inline-block;
    background: url('../../../assets/images/newvisi/u96.svg');
    background-size: cover;
    width: 10px;
    height: 92px;
  }
  .yd-item::before {
    position: absolute;
    top: 0;
    content: '';
    display: inline-block;
    background: url('../../../assets/images/newvisi/u95.svg');
    background-size: cover;
    width: 10px;
    height: 92px;
  }
}
.columncenter {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  flex: 1;
}
// .dashlineheight{
//   padding-left:5px;
//   background-image:linear-gradient(to right, #fff 5px, transparent 1px);
//   background-size: 20px 30px;
// }
.dashline {
  height: 1px;
  background-image: linear-gradient(to right, #00fffc 0%, #00fffc 50%, transparent 0%);
  background-size: 20px 1px;
  background-repeat: repeat-x;
}
.numback {
  width: 35px;
  height: 50px;
  background: url('../../../assets/images/newvisi/numbackground.png');
  display: flex;
  justify-content: center;
  align-items: center;
  color: #fff;
  font-size: 20px;
  margin-left: 5px;
}
/deep/.ant-select-arrow {
  color: #00fcfc;
}
/deep/.ant-select-selection__clear {
  color: #00fcfc;
}
.contenttext {
  font-size: 16px;
  color: #00fcfc;
  padding: 10px 20px;
  text-align: center;
  margin: 10px;
  .element::-webkit-scrollbar {
    display: none; /* Chrome Safari */
  }
}
.contebox::-webkit-scrollbar {
  display: none;
}
/deep/.ant-progress-bg {
  height: 14px !important;
}
/deep/.ant-progress-text {
  display: none;
}
.flexcenter {
  align-items: center;
  justify-content: center;
  display: flex;
  flex-direction: column;
}

</style>