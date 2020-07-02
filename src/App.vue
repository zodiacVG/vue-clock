<template>
  <div>
    <div class="mainBox">
      <header class="menu">
        <selectBox id="timezone" :list="timezones" @timezone1="getTimeZone"></selectBox>
        <switchButton id="switch" @switch1="damnswitch" @keydown="damnswitch">{{switchshow}}</switchButton>
      </header>
      <div class="timediv">
        <h1 class="time" id="time">{{timestr}}</h1>
      </div>
      <h2 class="ampm" id="period">{{period}}</h2>
      <h2 class="date" id="date">{{datestr}}</h2>
      <h2 class="day" id="day">{{weekday}}</h2>
    </div>
  </div>
</template>

<script>
import selectBox from './components/selectBox'
import switchButton from './components/switchButton'
var weeks = [
  '星期日',
  '星期一',
  '星期二',
  '星期三',
  '星期四',
  '星期五',
  '星期六'
]
var offGmt = new Date().getTimezoneOffset()

export default {
  name: 'Home',
  components: {
    selectBox,
    switchButton
  },
  data: function () {
    return {
      timestr: '',
      datestr: '',
      weekday: '',
      period: '',
      times: {
        // get time info
        hour: '',
        min: '',
        sec: '',
        year: '',
        mon: '',
        day: '',
        weekday: '',
        period: ''
      },
      timezones: {
        'UTC-8': 8,
        'UTC+1': 1,
        'UTC+2': 2,
        'UTC+3': 3,
        'UTC+4': 4,
        'UTC+5': 5,
        'UTC+6': 6,
        'UTC+7': 7,
        'UTC+8': 8,
        'UTC+9': 9,
        'UTC+10': 10,
        'UTC+11': 11,
        'UTC+12': 12,
        'UTC-11': -11,
        'UTC-10': -10,
        'UTC-9': -9,
        'UTC-7': -7,
        'UTC-6': -6,
        'UTC-5': -5,
        'UTC-4': -4,
        'UTC-3': -3,
        'UTC-2': -2,
        'UTC-1': -1
      },
      switchtime: '24',
      switchshow: '切换为12小时制',
      timezone: 8
    }
  },
  methods: {
    getTimeZone: function (value) {
      this.timezone = value
      console.log('shit i got' + value)
    },
    damnswitch: function () {
      if (this.switchshow === '切换为12小时制') {
        this.switchtime = '12'
        this.switchshow = '切换为24小时制'
      } else {
        this.switchtime = '24'
        this.switchshow = '切换为12小时制'
        this.period = ''
      }
      console.log(this.switchtime)
    }
  },
  created () {
    document.onkeydown = function () {
      var key = window.event.keyCode
      if (key === 32) {
        window.switch2()
      }
    }
  },
  mounted: function () {
    window.switch2 = this.damnswitch
    setInterval(() => {
      const nowTime = new Date().getTime()
      const time = new Date(
        nowTime + offGmt * 60 * 1000 + this.timezone * 60 * 60 * 1000
      ) // get diftimezone time
      this.times = {
        hour: time.getHours(),
        min: time.getMinutes(),
        sec: time.getSeconds(),
        year: time.getFullYear(),
        mon: time.getMonth() + 1,
        day: time.getDate(),
        weekday: time.getDay(),
        period: ' '
      }
      if (this.switchtime === '12') {
        // switch12/24
        if (this.times.hour === 0) {
          this.times.hour = 12
          this.period = '上午'
        } else if (this.times.hour < 12) {
          this.period = '上午'
        } else if (this.times.hour === '12') {
          this.period = '下午'
        } else {
          this.times.hour -= 12
          this.period = '下午'
          console.log('should be -12')
        }
      }
      if (this.times.hour < 10) {
        // change to 2 chars fmt
        this.times.hour = '0' + this.times.hour
      }
      if (this.times.min < 10) {
        this.times.min = '0' + this.times.min
      }
      if (this.times.sec < 10) {
        this.times.sec = '0' + this.times.sec
      }
      if (this.times.mon < 10) {
        this.times.mon = '0' + this.times.mon
      }
      if (this.times.day < 10) {
        this.times.day = '0' + this.times.day
      }
      this.timestr =
        this.times.hour + ':' + this.times.min + ':' + this.times.sec
      this.datestr =
        this.times.year + '年' + this.times.mon + '月' + this.times.day + '日'
      this.weekday = weeks[this.times.weekday]
    }, 100)
  }
}
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
}

h1,
h2 {
  color: #fff;
}

h1 {
  font-size: 100px;
  align-self: center;
}

h2 {
  height: 25px;
  font-size: 18px;
  font-family: PingFang SC, Verdana, Helvetica Neue, Microsoft Yahei,
    Hiragino Sans GB, Microsoft Sans Serif, WenQuanYi Micro Hei, sans-serif;
}

.mainBox {
  width: 600px;
  height: 350px;
  margin-top: 130px;
  margin-left: auto;
  margin-right: auto;
  background-color: #000;
  border-radius: 10px;
  position: relative;
}

.menu {
  height: 60px;
  width: 600px;
  background-color: #797979;
  border-radius: 10px 10px 0 0;
  font-size: 0;
}

.timediv {
  width: 482px;
  height: 140px;
  margin-top: 55px;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 0;
  text-align: center;
  color: #fff;
  font-family: Courier, "Courier New", monospace;
  display: flex;
}

.ampm {
  text-align: center;
  height: 28px;
  margin-left: auto;
  margin-right: auto;
  font-size: 20px;
  color: #fff;
  bottom: 65px;
  font-family: PingFang SC, Verdana, Helvetica Neue, Microsoft Yahei,
    Hiragino Sans GB, Microsoft Sans Serif, WenQuanYi Micro Hei, sans-serif;
}

.date {
  height: 25px;
  font-size: 18px;
  font-family: PingFang SC, Verdana, Helvetica Neue, Microsoft Yahei,
    Hiragino Sans GB, Microsoft Sans Serif, WenQuanYi Micro Hei, sans-serif;
  float: left;
  left: 14px;
  bottom: 14px;
  position: absolute;
}

.day {
  height: 25px;
  font-size: 18px;
  font-family: PingFang SC, Verdana, Helvetica Neue, Microsoft Yahei,
    Hiragino Sans GB, Microsoft Sans Serif, WenQuanYi Micro Hei, sans-serif;
  float: right;
  right: 14px;
  bottom: 14px;
  position: absolute;
}
h1,
h2 {
  color: #fff;
}

h1 {
  font-size: 100px;
  align-self: center;
}

h2 {
  height: 25px;
  font-size: 18px;
  font-family: PingFang SC, Verdana, Helvetica Neue, Microsoft Yahei,
    Hiragino Sans GB, Microsoft Sans Serif, WenQuanYi Micro Hei, sans-serif;
}
</style>
