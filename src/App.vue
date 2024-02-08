<template>
  <div id="app">
    <h2>ConversationWrapper + MsgItem 的例子:</h2>
    <div class="c1">
      <ConversationWrapper>
        <MsgItem
          v-for="(item, index) in list1"
          :key="index"
          :msg="item.msg"
          :index="index"
          :contentType="item.contentType"
          :showFeedback="item.showFeedback"
          :feedbackList="item.feedbackList"
          :feedbackHandler="item.feedbackHandler"
          :likeType="item.likeType">
        </MsgItem>
        <MsgItem
          :slots="['content', 'feedback']"
          :contentType="0"
          :showFeedback="true">
          <span slot="content">这是slot="content"里的内容</span>
          <span slot="feedback" class="feedback-slot">
            <i class="iconfont icon-jita icon-slot"></i>
            <i class="iconfont icon-beisi icon-slot"></i>
            <i class="iconfont icon-jiazigu icon-slot"></i>
            <i class="iconfont icon-qin icon-slot"></i>
          </span>
        </MsgItem>
      </ConversationWrapper>
    </div>
    <h2><br />ConversationBlock 的例子:</h2>
    <div class="c1">
      <ConversationBlock
        :list="list2"
        :height="300"
        :userOptions="userOptions"
        :answerOptions="answerOptions" />
    </div>

    <input type="text" v-model="inputText" @keydown.enter="handleAdd" />
    <button @click="handleAdd" style="margin-left: 10px">添加</button>
  </div>
</template>

<script>
  import ConversationBlock from './components/conversationBlock.vue'
  import ConversationWrapper from './components/conversationWrapper.vue'
  import MsgItem from './components/msgItem.vue'
  export default {
    name: 'App',
    components: {
      ConversationWrapper,
      ConversationBlock,
      MsgItem,
    },
    data() {
      return {
        list1: [
          { msg: 'hello', contentType: 1 },
          { msg: '你好', contentType: 0 },
          { msg: '介绍一下北京', contentType: 1 },
          {
            msg: '北京位于北纬39度56分、东经116度20分，地处华北大平原的北部，东面与天津市毗连，其余均与河北省相邻。地势西北高、东南低，西部、北部和东北部三面环山，东南部为平原地区。北京的气候属于暖温带半湿润半干旱季风气候。',
            contentType: 0,
            type: 1,
            showFeedback: true,
            feedbackHandler: this.feedbackHandler,
            likeType: 0,
          },
          { msg: '简单介绍一下紫禁城', contentType: 1 },
          {
            msg: '紫禁城，位于中国北京的中心，旧称“紫禁城”，现为“故宫”，是明清两代的皇家宫殿。它始建于明成祖永乐四年（1406年），以南京故宫为蓝本进行建设，历时14年，于永乐十八年（1420年）建成。这座宫殿占地约72万平方米，有大小宫殿七十多座，房屋九千余间，是世界上现存规模最大、保存最为完整的木质结构古建筑群之一。',
            contentType: 0,
            type: 1,
            showFeedback: true,
            feedbackList: ['like', 'diss'],
            feedbackHandler: this.feedbackHandler,
            likeType: 0,
          },
        ],
        list2: [
          { msg: 'hello', contentType: 1 },
          { msg: '你好', contentType: 0 },
        ],
        userOptions: {
          position: 'right',
        },
        answerOptions: {},
        inputText: '',
      }
    },
    methods: {
      feedbackHandler(e) {
        console.log('feedback :>> ', e)
        if (e.type == 'like' || e.type == 'diss') {
          this.list1[e.index].likeType = e.value
        }
      },
      handleAdd() {
        this.list2.push({
          msg: this.inputText,
          contentType: 1,
        })
        this.inputText = ''
      },
    },
  }
</script>

<style>
  @import url('https://at.alicdn.com/t/c/font_4434434_2bpgagal1bj.css');
  * {
    box-sizing: border-box;
  }
  #app {
    padding: 20px;
    width: 1000px;
    margin: auto;
  }
  .c1 {
    width: 100%;
    background: #eee;
    margin-bottom: 10px;
  }
  .feedback-slot {
    font-size: 20px;
  }
  .icon-slot {
    margin-right: 8px;
  }
</style>
