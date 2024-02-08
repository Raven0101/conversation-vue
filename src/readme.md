# 组件 ConversationBlock

开箱即用的极简对话区域组件，只需传入对话列表即可

```
import ConversationBlock from 'conversationBlock.vue'
```

## Props

**1. list**

- **类型**：Array
- **描述**：消息列表，用于存储和展示消息数据。

**2. height**

- **类型**：String, Number
- **描述**：高度属性，可以接收字符串或数字类型的数据，用于设置区域的高度。（注意只有设置高度才能实现 list 增加消息自动滑动到最下方）

**3. userOptions**

- **类型**：Object
- **描述**：用户自定义配置对象.

**4. answerOptions**

- **类型**：Object
- **描述**：回答者自定义配置对象。

**5. showFeedback**

- **类型**：Boolean
- **描述**：是否显示反馈的开关，当值为`true`时，将显示反馈功能；当值为`false`时，将隐藏反馈功能。

**6. feedbackList**

- **类型**：Array
- **描述**：反馈可操作内容的列表，用于存储和展示用户可进行的反馈操作。

**7. feedbackHandler**

- **类型**：Function
- **描述**：反馈处理函数，当用户进行反馈操作时，将调用此函数来处理用户的反馈。

# 组件 ConversationWrapper

包裹一个对话区域

```
import ConversationWrapper from 'ConversationWrapper.vue'
```

## Props

**1. height**

- **类型**：String, Number
- **描述**：高度属性，可以接收字符串或数字类型的数据，用于设置区域高度。

# 组件 MgsItem

单个对话气泡组件

```
import MsgPop from 'msgItem.vue'
```

## Prosp

**1. msg**

- **类型**：`undefined`
- **描述**：消息内容，支持 HTML

**2. contentType**

- **类型**：`[String, Number]`
- **描述**：消息类型。0 代表回答者，1 代表提问者。
- **默认值**：`1`

**2. index**

- **类型**：`[String, Number]`
- **描述**：唯一识别本消息的 index

**2. options**

- **类型**：`Object`
- **描述**：可配置项，包括头像、对齐位置、自定义类名。
- **默认值**：`{avatar: undefined, position: 'left'，customClass:undefined}`

**2. showFeedback**

- **类型**：`Boolean`
- **描述**：是否显示反馈
- **默认值**：`false`

**2. feedbackList**

- **类型**：`Array`
- **描述**：反馈可操作内容列表，包括'like'、'diss'、'reAnswer'和'feedback'。
- **默认值**：`['like', 'diss', 'reAnswer', 'feedback']`

**2. likeType**

- **类型**：`[String, Number]`
- **描述**：点赞状态。1 代表点赞，0 代表无状态，-1 代表点踩。
- **默认值**：`0`

**2. feedbackHandler**

- **类型**：`Function`
- **描述**：处理反馈的回调函数
- **默认值**：空函数 `() => {}`

**2. slots**

- **类型**：`Array`
- **描述**：应用的 slot，包括'content'和'feedback'。
- **默认值**：空数组 `[]`

## 一些公共属性说明

**1. options (userOptions、answerOptions 同)**
可配置项：`头像'avatar'、对齐位置'position'、自定义类名'customClass'`

**1. feedbackList**

可选值：`'like'点赞, 'diss'点踩, 'reAnswer'重新回答, 'feedback'反馈问题`

**2. likeType**

返回值：`1 代表点赞，0 代表无状态，-1 代表点踩`

**3. feedbackHandler**

处理反馈的回调函数，传参包含 index、type 和 value 的对象。type 与 feedbackList 里一致，当 type='like'或 type='diss'时，value 为当前 likeType，其他情况 value=undefined

## 示例

运行 npm run serve 查看示例
