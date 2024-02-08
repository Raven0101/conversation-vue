# 组件 ConversationBlock

开箱即用的极简对话组件

```
import ConversationBlock from 'conversationBlock.vue'
```

## Props

**1. list**

- **类型**：Array
- **描述**：消息列表，用于存储和展示消息数据。

**2. height**

- **类型**：String, Number
- **描述**：高度属性，可以接收字符串或数字类型的数据，用于设置元素的高度。

**3. userOptions**

- **类型**：Object
- **描述**：用户自定义配置对象，用户可以通过此对象设置特定的配置选项。

**4. answerOptions**

- **类型**：Object
- **描述**：回答者自定义配置对象，回答者可以通过此对象设置特定的配置选项。

**5. showFeedback**

- **类型**：Boolean
- **描述**：是否显示反馈的开关，当值为`true`时，将显示反馈功能；当值为`false`时，将隐藏反馈功能。

**6. feedbackList**

- **类型**：Array
- **描述**：反馈可操作内容的列表，用于存储和展示用户可进行的反馈操作。

**7. feedbackHandler**

- **类型**：Function
- **描述**：反馈处理函数，当用户进行反馈操作时，将调用此函数来处理用户的反馈。

**说明**

上述属性描述了一个具有消息列表、高度设置、用户自定义配置、回答者自定义配置、反馈显示开关、反馈可操作内容列表以及反馈处理函数的对象。这个对象可能是一个组件或模块的配置参数，用于实现消息展示、用户反馈等功能。在开发中，根据实际需要，可以对这些属性进行相应的赋值和调用处理。

# 组件 ConversationWrapper

对话区域

```
import ConversationWrapper from 'ConversationWrapper.vue'
```

# 组件 MgsItem

单独对话气泡组件

```
import MsgPop from 'msgItem.vue'
```

## Props 列表

### msg

- **类型**：`undefined`
- **描述**：消息内容，支持 HTML

### contentType

- **类型**：`[String, Number]`
- **描述**：消息类型。0 代表回答者，1 代表提问者。
- **默认值**：`1`

### index

- **类型**：`[String, Number]`
- **描述**：唯一识别本消息的 index

### options

- **类型**：`Object`
- **描述**：可配置项，包括头像、对齐位置。
- **默认值**：`{avatar: undefined, position: 'left'}`

### showFeedback

- **类型**：`Boolean`
- **描述**：是否显示反馈
- **默认值**：`false`

### feedbackList

- **类型**：`Array`
- **描述**：反馈可操作内容列表，包括'like'、'diss'、'reAnswer'和'feedback'。
- **默认值**：`['like', 'diss', 'reAnswer', 'feedback']`

### likeType

- **类型**：`[String, Number]`
- **描述**：点赞状态。1 代表点赞，0 代表无状态，-1 代表点踩。
- **默认值**：`0`

### feedbackHandler

- **类型**：`Function`
- **描述**：处理反馈的回调函数，传参包含 index、type 和 value 的对象。type 与 feedbackList 里一致，当 type='like'或 type='diss'时，value 为当前 likeType，其他情况 value=undefined
- **默认值**：空函数 `() => {}`

### slots

- **类型**：`Array`
- **描述**：应用的 slot，包括'content'和'feedback'。
- **默认值**：空数组 `[]`

## 示例

- 基础用法

```
<template>
    <Conversation class="conversition" id="scroll">
        <MsgPop msg="你好，我是提问者" contentType="1"></MsgPop>
        <MsgPop msg="你好，我是回答者" contentType="0"></MsgPop>
    </Conversation>
</template>
```

![基础用法](image.png)

- 配置头像以及位置

```
<template>
    <Conversation class="conversition" id="scroll">
        <MsgPop
          msg="我在右边"
          contentType="1"
          :options="{ position: 'right' }"
        ></MsgPop>
        <MsgPop
          msg="我在左边"
          contentType="0"
          :options="{ avatar: '/img/编组 6.91f06e99.png', position: 'left' }"
        ></MsgPop>
    </Conversation>
</template>
```

![配置头像以及位置](image-2.png)

- 显示反馈，配置反馈项目，配置反馈处理函数

```
<template>
    <Conversation class="conversition" id="scroll">
        <MsgPop
          msg="默认显示所有反馈项"
          contentType="0"
          :options="options"
          :showFeedback="true"
          :feedbackHandler="feedbackHandler"
          :likeType="likeType"
        ></MsgPop>
        <MsgPop
          msg="可配置反馈项['like', 'diss']"
          contentType="0"
          :options="options"
          :showFeedback="true"
          :feedbackList="['like', 'diss']"
        ></MsgPop>
    </Conversation>
</template>
<script>
    export default {
    data() {
        return {
            likeType:0,
            options:{ avatar: '/img/编组 6.91f06e99.png', position: 'left' }
        }
    },
    methods: {
        handelFeedback(e) {
            console.log('feedback :>> ', e)
            if(e.type=='like'){
                this.likeType=this.likeType==1?0:1
            }else if(e.type=='diss'){
                this.likeType=this.likeType==-1?0:-1
            }else{

            }
        },
    },
    }
</script>
```

![a显示反馈，配置反馈项目，配置反馈处理函数](image-5.png)

- 可用插槽

```
<template>
    <Conversation class="conversition" id="scroll">
        <MsgPop
          msg=""
          contentType="0"
          :showFeedback="true"
          :slots="['content', 'feedback']"
        >
          <template slot="content"
            ><a-button>我是content slot里的按钮</a-button></template
          >
          <template slot="feedback"
            ><a-button>我是feedback slot里的按钮</a-button>
          </template>
        </MsgPop>
    </Conversation>
</template>

```

![可用插槽](image-6.png)
