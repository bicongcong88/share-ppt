
title: code-standard
url: http://git.iciba.com:8181/edu-fe/share-ppts
transition: zoomin
files:
theme: moon
highlightStyle: monokai_sublime
headFiles:
usemathjax: no
date: 2018年11月1日


<!-- #0 -->
[slide]

# 前端代码规范

--------------------------------------------------------------------------------


- 越规范, 越效率

- 多提意见, 多补充, 每个人都会提高

- 大家相互监督, 共同进步


<div style="float:right;margin-top:250px">
2018年11月01日 <br><br>
分享人：毕小葱
</div>



<!-- #1 -->
[slide]

# 目录

--------------------------------------------------------------------------------

- [通用规范](#2)
- [HTML 规范](#4)
- [CSS 规范](#6)
- [VUE 规范](#10)
- [JS 规范](#14)

<!-- #2 -->
[slide]

# 通用规范 (一)

--------------------------------------------------------------------------------

- 缩进

  - > 推荐: 4个空格（大家协商的结果）

  - > 但是, 不能出现1个空格或3个空格或奇数个空格的缩进

  - > 根据上下文对齐, 不要多缩进, 也不要少缩进

- 分号

  - > 推荐不带分号(不强烈, 完全根据个人习惯)

  - > **css 或 less 必须带分号**

- 引号

  - > 推荐单引号(不强烈, 完全根据个人习惯)

  - > **HTML 属性值必须是双引号**

<!-- #3 -->
[slide]

# 通用规范 (二)

--------------------------------------------------------------------------------

- 空行

  - > 不推荐两行以上的空行间隔

  - > 有关联的, 一行相隔

  - > 无关联的, 两行相隔

- 注释

  - > 工具类或方法, 必须带注释

  - > 关键参数或属性, 必须带注释

  - > 关键方法, 必须带注释

  - > 业务节点, 必须带注释

  - > 推荐 **多写注释**, 造福他人, 造福自己

<!-- #4 -->
[slide]

# HTML 规范

--------------------------------------------------------------------------------

- 有头有尾, 标签闭合
- 换行(尤其注意,不推荐多标签嵌套在一行)
- class 在前, 尽量不使用id
- 样式处理在 css 中完成，不要在html里写样式不允许 style="XXX"
- 尽量不要在html里做复杂的逻辑判断
- 带上必要注释

<!-- #5 -->
[slide]
# 优化代码Demo

- 源代码
```
<div class="title">
    <div v-if="type=='loan' || type=='setbank' || type === 'bInstal'">
        <img @click="hideSelectList" src="XXXX">
        <h2>{{type=='setbank'? '设置自动扣款卡': '收款银行卡'}}</h2>
        <h3 v-if="type=='setbank'">选定或添加银行卡即同意该卡为默认代扣卡</h3>
    </div>
    <div v-else>
        <span class="left-arrow" @click="hideSelectList"></span>
        <h2>选择银行卡</h2>
    </div>
</div>
```

<!-- #6 -->
[slide]

- 修改后的代码
```
<div class="title">
    <img v-if="ifShowClose" @click="hideSelectList" src="XXXX">
    <span v-else class="left-arrow" @click="hideSelectList"></span>
    <h2>{{title}}</h2>
    <h3 v-if="type=='setbank'">选定或添加银行卡即同意该卡为默认代扣卡</h3>
</div>
```
```
ifShowClose() {
    const showList = ['loan', 'setbank', 'bInstal']
    return showList.includes(this.type)
},
title() {
    switch (this.type) {
        case 'loan':
        case 'bInstal':
            return '收款银行卡'
        case 'setbank':
            return '设置自动扣款卡'
        default:
            return '选择银行卡'
    }
}
```





<!-- #7 -->
[slide]

# CSS 规范

--------------------------------------------------------------------------------

- 一般写法
- 命名空间
- 属性顺序

<!-- #8 -->
[slide]

# CSS 规范(-)

--------------------------------------------------------------------------------

- `key: value` 写法, `:` 后面有一个空格
- 不允许所有的样式写在一行
- 不推荐直接为标签写样式，容易全局污染，并且不易后人维护

<!-- #9-->
[slide]
# CSS 规范(二)
- `&` 配合 `命名空间` 写法, 注意全局污染

```
<div class="mine">
    <div v-for="(item, index) in courseList" :key="index" class="mine-item">
        <p class="mine-item-title">{{item.title}}</p>
        <div class="mine-item-teacher">
            <img class="mine-item-teacher-img" :src="item.teacherImage"/>
            <span class="mine-item-teacher-name">{{item.teacherName}}</span>
            <span class="mine-item-teacher-desc">{{item.teacherTitle}}</span>
        </div>
    </div>
</div>
```
```
.mine {
    min-height: 100%;
    background-color: $g-bgc;
    &-item {
        float: left;
        box-sizing: border-box;
        background-color: #fff;
        &-teacher {
            height: 250px;
            padding: 20px 20px 29px;
            &-img {
               margin-bottom: 14px;
               margin-left: 30px;
            }
        }
    }
}
```



<!-- #10 -->
[slide]
# CSS 规范(三)
- 属性顺序

```css

    .class {
        /* 第一顺序, 定义盒类型 */
        display: flex;
        float: left;
        box-sizing: border-box;
        flex-direction: column;
        overflow: hidden;
        /* 第二顺序, 定位 */
        position: absolute;
        top: 0;
        left: 0;
        z-index: 999;
        /* 第三顺序, 盒模型 */
        width: 100px;
        height: auto;
        margin: 30px;
        padding: 30px;
        border: 1px solid #ccc;
        /* 第四顺序, 盒子装饰 */
        background-image: url('a.png');
        background-size: cover;
        outline: 1px solid #bbb;
        box-shadow: 1px 0 5px #000;
        border-radius: 50%;
        /* 第五顺序, 文本修饰 */
        font-size: 24px;
        line-height: 2;
        color: inherit;
        text-align: center;
        white-space: nowrap;
        /* 第六顺序, 其他 */
		CSS3
    }
```


<!-- #11 -->
[slide]

# VUE 规范

--------------------------------------------------------------------------------

- 一般写法
- 折行
- 顺序


<!-- #12 -->
[slide]

# VUE 规范（规范一）

--------------------------------------------------------------------------------

- 组件名: 小写 `<vue-bar-holder>` 而不是 `<vueBarHolder>`
- 属性名: 小写 `:video-cover` 而不是 `:videoCover`
- 属性值: 大写 `:video-cover="videoCover"`




<!-- #13 -->
[slide]
```html

<!-- 属性换行 -->
<video-m3u8
    ref="video"
    :cover="false"
    :src="videoSrc"
></video-m3u8>

<!-- json换行 -->
<div
	class="detail-index-item"
	v-for="(item, index) in main.lessons"
	:key="index"
	:class="{
		lock: item.isPreSale,
		done: isPreSale,
		try: !hasBuy,
		on: index,
		live: item.isLive,
	}"
	:data-cnzz="pageName + ',' + title + ',' + item.title + ',课程详情'"
	@click="lessonClick(item)"
>
```
<!-- #14 -->
[slide]

## VUE 属性顺序
- 第一序列: 原生属性
- 第二序列: `v-xxx` 命令
- 第三序列: `:xxx` 属性绑定
- 第四序列: `@xxx` 事件绑定


<!-- #15 -->
[slide]

# JS 规范

--------------------------------------------------------------------------------

- 遵照ESlint
- 多用ES6写法（变量声明const和let、模板字符串、箭头函数、展开运算符、数组的方法）
- 注意变量名和方法名的定义
- 推荐 === 严格等于
- 每当拷贝代码的时候自省（能否抽离）


<!-- #16 -->
[slide]
# 优化代码demo

- 源代码
```
getRepayType:function(v){
    if(v=='1'){
        return '每月等额'
    }else if(v=='2'){
        return '等额本金'
    }else if(v=='3'){
        return '先息后本'
    }else if(v=='7'){
        return '按月等额本息'
    }
},
```
- 修改代码格式
```
getRepayType: function(v) {
    if (v === '1') {
        return '每月等额'
    } else if (v === '2') {
        return '等额本金'
    } else if (v === '3') {
        return '先息后本'
    } else if (v === '7') {
        return '按月等额本息'
    }
},
```

<!-- #17 -->
[slide]
- 优化后代码（一）
```
getRepayType: function(v) {
    switch (v) {
        case '1':
            return '每月等额'
        case '2':
            return '等额本金'
        case '3':
            return '先息后本'
        case '7':
            return '按月等额本息'
    }
},
```

- 优化后的代码(二)
```
getRepayType(type) {
    const repayTips = {
        1: '每月等额',
        2: '等额本金',
        3: '先息后本',
        7: '按月等额本息'
    }
    return repayTips[type]
},
```


<!-- #18 -->
[slide]

# 总结
- 目前我们项目中代码不规范的现象还很普遍
- 希望这次分享能给大家带来收获
- 大家共同监督，共同进步




--------------------------------------------------------------------------------




