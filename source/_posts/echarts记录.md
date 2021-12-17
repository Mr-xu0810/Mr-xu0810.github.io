---
title: echarts记录
date: 2021-12-15 20:04:50
author: Mr-xu
img: /images/2.jpg
top: false
cover: false
summary: 记录一下echarts部分配置
tags:
  - echarts
  - js
---

# echarts 记录

## echarts饼图设定每个扇形的颜色

##### data数据中加入itemStyle

exp: option配置

```json
 [{ name: '测试', value: 1212, itemStyle: { color: '#ff0000' } }]
```

##### 不在data中加入( series里加入itemStyle )：

exp: option配置

```javascript
[{ name: 'task', type: 'pie'，radius: '50%', itemStyle: {
normal: {
	color: function(params) {
		var colorList = [ '#66FF99', '#FF9966', '#FF0033' ]  
		return colorList[params.dataIndex]
	}
}
} }]
```

## 动态数据
> echarts动态数据处理时，只需要将数据处理成option对应的数据格式后，在调用setOption(options)
> echarts 会根据数据进行相应的动画来实现图表的数据动态化


## echart自适应

```javascript
myLogLine.setOption(option);
window.addEventListener("resize", () => { myLogLine.resize();});
```

