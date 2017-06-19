<template>
  <div id="app">
    <header>
      <span>Ayın Kalan İş Günü</span>
    </header>
    <main>
      <h1>
        {{RemainingWorkDay}}
      </h1>
      <h2>Gün Kaldı</h2>
      <span>Bugün hariç</span>
  
      <div>
        bugün: {{Today}}
      </div>
  
    </main>
  </div>
</template>

<script>

import Moment from 'moment'
import 'moment-business-days'

Moment.locale('tr', {
  workingWeekdays: [0, 1, 2, 3, 4]
})
export default {
  name: 'app',
  components: {},
  computed: {
    isWorkday: function () {
      return Moment(new Date()).isBusinessDay()
    },
    RemainingWorkDay: function () {
      let now = Moment(new Date())
      let nextMonth = Moment([now.year(), now.month() + 1])
      console.log('Next month: ', nextMonth)
      console.log('Now: ', now)
      return now.businessDiff(nextMonth)
    },
    Today: function () {
      return Moment(new Date()).format('L')
    }
  }
}
</script>

<style>
body {
  margin: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

main {
  text-align: center;
  margin-top: 40px;
}

header {
  margin: 0;
  height: 56px;
  padding: 0 16px 0 24px;
  background-color: #4fc08d;
  color: #ffffff;
}

header span {
  display: block;
  position: relative;
  font-size: 20px;
  line-height: 1;
  letter-spacing: .02em;
  font-weight: 400;
  box-sizing: border-box;
  padding-top: 16px;
}
</style>
