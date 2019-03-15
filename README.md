## 作者想说
感谢各位小伙伴的不断建议，inputs组件的进步都是因为你们哦~！

如果该组件有什么问题还请大家说出来哦，还有如果有什么建议的话也可以提下呐 ~
如果觉得好用，可以回来给个五星好评么~~(❁´◡`❁)\*✲ﾟ\*  蟹蟹~拜托啦~

## 组件简介
本组件目前支持 input、radio、checkbox、上传图片、日期选择、城市选择等类型的快速开发，自动判断、自动取值，只要你填写好每项的类型数据，就可以很方便的开发啦！甚至，表单的类型、布局、取值可以由后端接口动态决定！有需要的小伙伴快点下载吧

---
### 警告
picker-date类型在较为复杂的页面，“日”一列的picker-view-column可能会有例如从3月31日切换为2月时的28日跳到27日的bug，并且滑动至28时，值不会变成28而是27，只能点击选择28才能变更，这是在我自己的项目中发现的问题，是嵌套在官方组件segmented-control的tab切换显示或隐藏环境中出现此bug， 还请大家注意测试, 目前不知道原因，有知道的小伙伴麻烦和我说下

# 更新说明

| 序号 | 更新说明 |
|---|------|
| 2.8 | 紧急修复开发者工具更新后出现从后台进入前台input视图为空bug（数据还在）,例如选择图片后返回时input视图为空 |
| 2.7 | 修复picker初始值显示，并增加该属性，详见picker类型 |
| 2.6 | 修复h5报错问题，修改picker类型选择方式为弹出,并增加picker按钮名属性 |
| 2.5 | 1、引入官方picker-city城市选择(稍做修改)<br>2、更改日期控件的默认值defaultDate属性为defaultValue<br>3、修复未判断picker-city的bug|
| 2.4 | 新增changeReSet属性|
| 2.3 | 1、新增defaultValue属性，支持input、radio、checkbox、pics的初始化默认值设置,详见一、input、二、pics、三、radio、四、checkbox， <br>2、新增选中的图片可大图预览|
| 2.2 | 新增时分秒选择与日期融合，详见 五、日期控件|
| 2.1 | 修复pics类型问题，与cssMode为scrollX时样式问题，修复H5 picker-date类型，defaultDate报错问题，修复H5|
| 2.0 | 1、修复input软键盘弹出式样式改变问题（统一单位使用px，数值使用windowHieght计算）<br>2、radio、checkbox、pics等类型统一指定项内数组名为itemArray<br>3、inputs属性改为inputsArray，便于区分<br>4、修复一些bug|
| 1.9 | 新增variableName属性，可自定义该项的变量名, 修复pickers组件的样式问题 |
| 1.8 | 新增日期选择控件 —— picker-date |
| 1.7 | 新增cssMode属性，可控制非input、picker-date类型的项内布局方式,可在父组件传入，也可在项内属性中传入,默认为wrap |
| 1.6 | ruleName属性修改为ruleArray, 可以支持一个以上的规则或协议 |
| 1.5 | 新增radio(单选)类型，checkbox（多选）类型 |
|  | 为提升用户体验，在循环项数较多的情况下，防止超屏，新增overflow_x为scroll(x轴滚动) |
|  | 判断类型使用type判断 |
|  | 完善213-226行的判断写法不正确问题 |
### 新增的changeReSet属性说明(有重置需求的可使用)
在父级传入的inputsArray改变时，可以选择重置数据，但是视图的重置需要先inputsArray=[ ]后setTimeout 300或者多少后重新赋值，过程中可以设置主按钮文字为‘加载中’等，可增强用户体验
### 新增的defaultValue属性说明
支持input、radio、checkbox、pics的初始化默认值设置， radio仅能设置一个defaultValue为true，若有多个则取最先选中的值

---
# 下次更新方向
picker自定义。敬请期待

---

# inputs组件使用说明
注：有引入官方的uni-Icon组件（删除图片的叉叉），可自行修改

## html中使用

```html
<template>
  <view>
	<inputs :inputsArray="inputsArray" activeName="申请入驻" :ifCode="true" 
			:ifRule="true" :ruleArray="ruleArray" 
			v-on:chaildOpenEvent="openWin" 
			v-on:activeFc="activeFc"  :onLoadData="onLoadData" 
			cssMode="wrap"/>
  </view>
</template>
```
## JS中引入、注册并使用组件
```javascript
<script>
  import inputs from /*inputs组件文件路径；*/
  export default {
    data() {
      return {
	    title: 'Hello',
		inputsArray: [{
			type: 'picker-date',
			title: '日期',
			mode: 'picker-dateTime',
			variableName: 'date'
		}, {
			type: 'pics',
			title: '图片',
			itemArray: [{
				title: '测试',
				ignore: true，
				defaultValue: '' // 本地图片路径
			}],
			variableName: 'pic'
		}, {
			title: 'radio',
			type: 'radio',
			itemArray: [{
				name: 'aa',
				value: 'aa',
				defaultValue: true
			}, {
				name: 'bb',
				value: 'bb'
			}]
		}, {
			title: 'checkbox',
			type: 'checkbox',
			itemArray: [{
				name: 'aa',
				value: 'aa',
				defaultValue: true
			}, {
				name: 'bb',
				value: 'bb',
				defaultValue: true
			}]
		}, {
			title: '测试',
			ignore: true
		}, {
			title: '手机号',
			defaultValue: '13856954623',
			phone: true
		}],
		ruleArray: [{
			name: '某规则',
			value: 'aa'
		}],
		onLoadData： 'data_'	//获取数据时默认变量名前缀
      };
    },
    methods: {
      openWin(value) {
        //打开规则或协议页
		//若有一个以上的rule，则根据value打开规则页面
		console.log(value);
      },
      activeFc(res) {	// 最终取值
        //主方法，携带用户输入的数据对象
        let _this = this;
        console.log(JSON.stringify(res));
        // 如果项内定义了variableName属性，则取值为定义的variableName，否则取值为 this.onloadData + index, onloadData默认值为'data_'
        // 需要把数据传至服务器时也可以把整个对象传过去，由后端直接处理数据，这样可以实现整体的表单类型、布局、取值都由后端决定
        submitFc(res[_this.onLoadData + '0'], res[_this.onLoadData + '1'], ……, function(result) {
          console.log(JSON.stringify(result))
          if(result.data && result.data == 'success')
            _app.showToast('申请发送成功');
          else
            _app.showToast('出了些问题:' + JSON.stringify(result));
          }, function(err) {
            _app.showToast('申请发送失败:' + JSON.stringify(err));
          });
        }
      },
    components: {inputs}
  }
</script>
```

---

## 传给inputs组件的属性
| 属性名| 是否必填| 值类型| 默认值| 说明|
|------|---|----|---|-------|
| inputsArray| 是| Array\<Object\>| []| 需循环的inputs数组（可从后端接口获取）|
| activeName| 是| String| '发送'| 主功能按钮的文字说明|
| ifCode| 否| Boolean| false| 是否启用验证码功能, 若启用则需完善381-386行的发送验证码方法|
| ifRule| 否| Boolean| false| 是否需要用户同意某规则或协议|
| ruleArray| ifRule为true时是| Array\<Object\>| []| 需要用户同意某规则或协议的数组|
| v-on:chaildOpenEvent| ifRule为true时是| Function| | 打开某规则或协议的方法|
| v-on:activeFc| 是| Function| | 主功能方法，携带一个用户所输入的数据对象|
| onLoadData| 否| String| 'data_'| activeFc返回的对象中的数据变量名前缀，后面跟index，看下方说明|
| titleFontSize| 否| Number| 屏幕高度*.021 px | title(左边)的文字大小|
| titleFontColor| 否| String| '#666666'| title(左边)的文字颜色|
| contentFontSize| 否| Number| 屏幕高度*.018 px| 内容(右边)的文字大小|
| cssMode| 否| String| 'wrap'| 非input、picker-date类型的项内布局方式|
| changeReSet| 否| Boolean| false| 在inputsArray改变时可重置所有数据为空，但不重置视图，若需重置视图看下方说明|
### changeReSet属性说明(有重置需求的可使用)
在父级传入的inputsArray改变时，可以选择重置数据，但是视图的重置需要先inputsArray=[ ]后setTimeout 300或者多少后重新赋值，过程中可以设置主按钮文字为‘加载中’等，可增强用户体验
### ruleArray属性说明
| 属性 | 说明|
|---|---|
| name| 需要用户同意某规则或协议的名字 |
| value| 需要用户同意某规则或协议的标识(父级方法判断用) |

### cssMode属性说明
| 值| 说明|
|---|---|
| wrap| 布局方式: 全显+换行  |
| scrollX| 布局方式: 非全显+滑动 |
注：cssMode属性可在父级中传入， 默认为wrap，也可在项内属性中传入,优先级: 项内属性>父级属性.


## inputsArray属性说明

### 一、input
| 属性名| 是否必填| 值类型| 默认值| 说明|
|------|---|----|---|-------|
| type| 否| String| ''| 不传该值(因默认为input)|
| title| 是| String| ''| 该项input的标题|
| placeholder| 否| String| '请输入' + this.title| input的placeholder文字|
| ignore| 否| Boolean| false| 是否可忽略该项（判断时可以为空）|
| nullErr| 否| String| this.title + '不能为空'| 为空时提示|
| inputType| 否| String| 'text'| 该项input的类型|
| phone| 否| Boolean| false| 是否设此项为手机号input(判断时，判断此属性)|
| variableName| 否| String| this.onloadData\|\|'data_' + index| 自定义变量名,取值时用|
| defaultValue| 否| String| ''| 该项input的初始化默认值|
### 二、上传图片
| 属性名| 是否必填| 值类型| 默认值| 说明|
|------|---|----|---|-------|
| type| 是| String| ''| 传固定值 type: 'pics'|
| itemArray| 是| Array\<Object\>| []| 循环的图片数组，下方说明|
| title| 否| String| ''| 该项图片的标题|
| ignore| 否| Boolean| false| 是否可忽略该项（判断时可以为空）|
| cssMode| 否| String| 'wrap'| 非input、picker-date类型的项内布局方式|
| variableName| 否| String| this.onloadData\|\|'data_' + index| 自定义变量名,取值时用|
#### pics的itemArray属性说明
| 属性名| 是否必填| 值类型| 默认值| 说明|
|------|---|----|---|-------|
| title| 否| String| ''| 该项图片的标题|
| nullErr| 否| String| this.title + '不能为空'| 为空时提示|
| ignore| 否| Boolean| false| 可以为空， 不判断是否为空,默认为必填，必填则在title前面有 * 标识|
| defaultValue| 否| String| ''| 该项pics的初始化默认图片路径(本地图片路径)|
注：若启用此项，则需完善463-470行的上传图片至服务器方法
### 三、radio(单选)
| 属性名| 是否必填| 值类型| 默认值| 说明|
|------|---|----|---|-------|
| type| 是| String| ''| 传固定值 type: 'radio'|
| title| 否| String| ''| 该项radio的标题|
| itemArray| 是| Array\<Object\>| []| 需循环的radio数组|
| ignore| 否| Boolean| false| 是否可忽略该项（判断时可以为空）|
| nullErr| 否| String| this.title + '不能为空'| 为空时提示|
| cssMode| 否| String| 'wrap'| 非input、picker-date类型的项内布局方式|
| variableName| 否| String| this.onloadData\|\|'data_' + index| 自定义变量名,取值时用|
#### radio的itemArray属性说明
| 属性名| 是否必填| 值类型| 默认值| 说明|
|------|---|----|---|-------|
| name| 是| String| ''| 该radio的标题|
| value| 是| | | 该项radio的值|
| defaultValue| 否| Boolean| false| 该项radio的初始化默认值,(只能设置一个true，若设置多个为true，则取最先为true的值)|
### 四、checkbox(多选)
| 属性名| 是否必填| 值类型| 默认值| 说明|
|------|---|----|---|-------|
| type| 是| String| ''| 传固定值 type: 'checkbox'|
| title| 否| String| ''| 该项checkbox的标题|
| itemArray| 是| Array\<Object\>| []| 需循环的checkbox数组|
| ignore| 否| Boolean| false| 是否可忽略该项（判断时可以为空）|
| nullErr| 否| String| this.title + '不能为空'| 为空时提示|
| cssMode| 否| String| 'wrap'| 非input、picker-date类型的项内布局方式|
| variableName| 否| String| this.onloadData\|\|'data_' + index| 自定义变量名,取值时用|
#### checkbox的itemArray属性说明
| 属性名| 是否必填| 值类型| 默认值| 说明|
|------|---|----|---|-------|
| name| 是| String| ''| 该checkbox的标题|
| value| 是| | | 该项checkbox的值|
| defaultValue| 否| Boolean| false| 该项checkbox的初始化默认值|

注： checkbox类型与radio类型差不多，只是取值时checkbox为数组，根据需求使用

### 五、日期控件
| 属性名| 是否必填| 值类型| 默认值| 说明|
|------|---|----|---|-------|
| type| 是| String| ''| 传固定值 type: 'picker-date'|
| title| 否| String| ''| 该项picker的标题|
| indicatorStyle| 否| String| 'height: '+ 屏幕高度*.05 +'px;'| picker的行内样式|
| height| 否| String| 屏幕高度*.2 px| picker的高度|
| mode| 否| String| 'picker-date'| picker-date的类型|
| startYear| 否| Number| new Date().getFullYear() - 5（前五年）| 开始年份, 可直接输入四位数字|
| endYear| 否| Number| new Date().getFullYear() + 5 (后五年)|  结束年份, 可直接输入四位数字|
| defaultValue|否|Date日期对象| new Date()|默认日期, 可传new Date(年,月,日,时,分,秒),为空则默认为现在，注意:所传月份需-1|
| variableName| 否| String| this.onloadData\|\|'data_' + index| 自定义变量名,取值时用|
| chooseName| 否| String| 选择日期| 选择日期按钮命名|
| editorName| 否| String| 更改| 更改日期按钮命名|
| confirmName| 否| String| 确定| 弹出时,确定选择日期按钮命名|
| onceShowDefaultValue| 否| Boolean| false| 在设置defaultValue时，初始化时是否显示初始值|
#### mode属性说明
| 值|  值类型|说明|
|------|---|----|---|-------|
| picker-dateTime| String| 日期加时间|
| picker-date| String| 日期|
| picker-time| String| 时间|

注：所传的defaultDate若不在范围中，则将显示范围内的最后一年最后一月最后一日, defaultValue中所传的月份需-1;
### 六、城市选择
| 属性名| 是否必填| 值类型| 默认值| 说明|
|------|---|----|---|-------|
| type| 是| String| ''| 传固定值 type: 'picker-city'|
| title| 否| String| ''| 该项picker的标题|
| indicatorStyle| 否| String| 'height: '+ 屏幕高度*.05 +'px;'| picker的行内样式|
| height| 否| String| 屏幕高度*.2 px| picker的高度|
| defaultValue|否|Array| [0, 0, 0]|默认城市(需注意对应的项是否存在)|
| variableName| 否| String| this.onloadData\|\|'data_' + index| 自定义变量名,取值时用|
| chooseName| 否| String| 选择城市| 选择城市按钮命名|
| editorName| 否| String| 更改| 更改城市按钮命名|
| confirmName| 否| String| 确定| 弹出时,确定选择城市按钮命名|
| onceShowDefaultValue| 否| Boolean| false| 在设置defaultValue时，初始化时是否显示初始值|

注：picker-city取值时返回对象，可根据需求修改
