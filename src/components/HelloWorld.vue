<template>
  <div>
    <full-calendar
      ref="calendar"
      :config="config"
      :events="events"
    ></full-calendar>
  </div>
</template>
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
          // editable: false, //是否允许修改事件
          // eventLimit: 4, //事件个数
          // eventLimitText:"更多",
          // allDaySlot: false, //是否显示allDay
          // eventClick: this.eventClick, //点击事件
          // dayClick: this.dayClick, //点击日程表上面某一天
          // selectable:true, // 开启多选
          // select:this.handleSelect,  //多选执行的方法
         
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
      //alert("1")
      //this.$refs.calendar.fireMethod("unselect");
      //alert("2")
      //获取当前日期，返回一个moment
      // this.View_title = this.$refs.calendar.fireMethod("getDate");
      // //上一个月（周）
      // this.$refs.calendar.fireMethod("prev");
      // //下一个月（周）
      // this.$refs.calendar.fireMethod("next");
      // //切换到月视图
      // this.$refs.calendar.fireMethod("changeView", "month");
      // //切换到basicWeek视图
      // this.$refs.calendar.fireMethod("changeView", "basicWeek");

    },
    // 更新排班
    eventClick(calEvent, jsEvent, view) {

      
      console.log('calEvent === ' +calEvent + '====jsEvent === '+jsEvent +'====view===='+view);
    }












    //  // 点击事件
    //  eventClick (event, jsEvent, pos) {
    //    console.log('eventClick', event, jsEvent, pos)
    //  },
    //  // 点击当天
    //  dayClick (day, jsEvent) {
    //     console.log('dayClick', day, jsEvent)
    //  },
    //  // 当选择结束的时候获取开始和结束时间
    // handleSelect(info) {
    //   console.log(info)
    //   alert("form" + info.startStr + " to " + info.endStr);
    //   console.log("form" + info.startStr + " to " + info.endStr);
    // }
  }
}
</script>
<style scoped>
</style>