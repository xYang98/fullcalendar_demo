@[TOC](vue-full-calendar版本: "2.7.0")
# 1.效果图

![大概样式](https://img-blog.csdnimg.cn/20200401094148906.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDI1NDI0Mw==,size_16,color_FFFFFF,t_70#pic_center)
![大概样式](https://img-blog.csdnimg.cn/20200401094216298.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDI1NDI0Mw==,size_16,color_FFFFFF,t_70#pic_center)
![大概样式](https://img-blog.csdnimg.cn/20200401094238845.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDI1NDI0Mw==,size_16,color_FFFFFF,t_70#pic_center)
==零外还可以加入日程列表== 
# 2.上代码
需要创建一个vue脚手架，不会的可以百度下，这里就不说了，直接上主题。
### (1).安装依赖

```bash
npm install vue-full-calendar
```
安装好此依赖，如果提示安装jquery，请安装下，因为这个插件依赖了，jquery

```bash
npm install jquery
```
因为这是日历插件用到了时间工具类 ===   moment

```bash
npm install moment
```
### (2).文件中导入依赖
在想要用此插件的文件中导入依赖
```javascript
import { FullCalendar } from 'vue-full-calendar'
import "fullcalendar/dist/fullcalendar.css";
```
注册到组件中

```javascript
components: { FullCalendar },
```
这时候我们需要在主js（main.js）入口引入全局的moment

```javascript
Vue.prototype.$moment = moment;//赋值使用
Vue.config.productionTip = false
```
### (3).开发
在导入依赖的文件中（html模板）

```javascript
<template>
  <div>
    <full-calendar
      ref="calendar"
      :config="config"
      :events="events"
    ></full-calendar>
  </div>
</template>
```
在js中

```javascript
<script>
import { FullCalendar } from 'vue-full-calendar'
import "fullcalendar/dist/fullcalendar.css";
export default {
  name:'hello',
  components: { FullCalendar },
  data() {
      return {
        config: {
         header:{
            left: 'prev,next today',
            center: 'title',
            right: 'month,agendaWeek,agendaDay,list'
          },
          buttonText: {today: "今天", month: "月", week: "周", day: "日",list: "日程" },
          locale: "zh-cn",
          defaultView: "month", //显示默认视图
          //weekMode: 'liquid',
          // weekNumbers: true,
          // height: 'auto',
          timeFormat: 'HH:mm',
          navLinks: true,       // can click day/week names to navigate views
          eventLimit: 3,        // 限制一天中显示的事件数，默认false
          allDayText: '排班',   // 日历上显示全天的文本
          selectable: true,     // 允许用户通过单击或拖动选择日历中的对象，包括天和时间。
          selectHelper: false,  // 当点击或拖动选择时间时，显示默认加载的提示信息，该属性只在周/天视图里可用。
          unselectAuto: true,   // 当点击页面日历以外的位置时，自动取消当前的选中状态。
          eventBackgroundColor: '#3a87ad',    // 设置日程事件的背景色
          select: this.selectHandler,
          eventClick:this.eventClick  
       },
       events: [{
          title: '事件内容',  // 事件内容
          start: '2020-03-23 09:00:00', // 事件开始时间
          end: '2020-03-23 12:00:00',   // 事件结束时间
          color: 'rgba(9, 9, 9, 0.2)'       // 事件的显示颜色
        }],
     }
  },
  methods: {
    selectHandler(start, end, allDay){
      let startFormat = this.$moment(start).format('YYYY-MM-DD');
      let endFormat = this.$moment(end).format('YYYY-MM-DD');
      console.log('from === ' +startFormat + '====to === '+endFormat +'====allDay===='+allDay);

      //添加日历
      var json = {
        title: "张三" + ' - ' + "夜班",
        text: "张三",
        allDay: allDay,
        backgroundColor: "#3a87ad",
        start: start.format('YYYY-MM-DD'),
        end: end.format('YYYY-MM-DD')
      };
      this.events.push('renderEvent', json, true);
    // 更新排班
    eventClick(calEvent, jsEvent, view) {

      
      console.log('calEvent === ' +calEvent + '====jsEvent === '+jsEvent +'====view===='+view);
    }
  }
}
</script>
```
### (3). 开始运行
  如果没有安装其他依赖执行
  

```bash
npm install
```
如果安装好那么启动

```bash
npm run dev
```
如果有什么错误，谢谢指出。
