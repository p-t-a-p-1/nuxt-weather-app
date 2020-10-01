<template>
  <div class="c-main_content">
    <div class="c-main_content_card">
      <div class="c-main_content_card_main">
        <div class="-left">
          <p class="-temp">{{ nowData.main.temp }}°</p>
          <p class="-weather">
            {{ nowData.weather[0].description }}
          </p>
        </div>
        <div class="-right">
          <p class="-area">{{ nowData.name }}</p>
        </div>
      </div>
      <ul class="c-main_content_card_week">
        <li v-for="(day, index) in fiveDayData" :key="index" class="-date">
          <p class="-day">
            {{ day.dt_txt }}
            <span class="-str">{{ day.weekDay }}</span>
          </p>
          <font-awesome-icon :icon="day.icon" class="-icon" />
          <p class="-weather">{{ day.weather[0].description }}</p>
          <p class="-temp">
            気温<span class="-number">{{ day.main.temp }}°</span>
          </p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ params, error, $axios }) {
    try {
      let nowData = []
      const fiveDayData = []
      // OpenWeatherMapApiのベース
      const baseUrl = 'https://api.openweathermap.org/data/2.5/'
      await $axios
        .$get(
          `${baseUrl}weather?q=${params.name},jp&units=metric&lang=ja&appid=${process.env.WEATHER_API_KEY}`
        )
        .then((nowDataResult) => {
          nowData = nowDataResult
        })

      await $axios
        .$get(
          `${baseUrl}forecast?q=${params.name},jp&units=metric&lang=ja&appid=${process.env.WEATHER_API_KEY}`
        )
        .then((fiveDayResult) => {
          fiveDayResult.list.forEach((data) => {
            const checkedTime = data.dt_txt
            const weekDay = ['日', '月', '火', '水', '木', '金', '土']

            // 12時の天気情報のみ表示
            if (!checkedTime.match(/ 12:/)) {
              return
            } else {
              // 曜日取得
              const thisDay = new Date(checkedTime)
              data.weekDay = weekDay[thisDay.getDay()]
              // 2020-09-29 12:00:00 から時間以降削除
              data.dt_txt = data.dt_txt.split(' ')[0]
            }
            // 天気アイコンの表示
            if (data.weather[0].main === 'Rain') {
              data.icon = 'umbrella'
            } else if (data.weather[0].main === 'Clouds') {
              data.icon = 'cloud'
            } else if (data.weather[0].main === 'Clear') {
              data.icon = 'sun'
            }
            fiveDayData.push(data)
          })
        })
      return {
        nowData,
        fiveDayData,
      }
    } catch (error) {
      error({
        statusCode: error.response.status,
        message: error.response.data.message,
      })
    }
  },
}
</script>

<style lang="scss">
.c {
  &-main {
    &_content {
      margin: 100px auto 0;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      text-align: center;
      &_card {
        width: 85%;
        &_main {
          display: flex;
          justify-content: space-around;
          .-right {
            display: flex;
            align-items: center;
          }
          .-temp {
            font-size: 5.5rem;
          }
          .-weather {
            font-size: 2.4rem;
          }
          .-area {
            font-size: 3.5rem;
          }
        }
        &_week {
          margin-block-start: 40px;
          display: flex;
          justify-content: space-around;
          .-date {
            font-size: 2rem;
          }
          .-day {
            padding-block-end: 1rem;
          }
          .-str {
            display: block;
          }
          .-icon {
            font-size: 5rem;
            padding-block-end: 1rem;
          }
          .-weather {
            padding-block-end: 1rem;
          }
          .-temp {
            padding-block-end: 1rem;
            span {
              font-size: 2.4rem;
            }
          }
          .-number {
            margin-left: 10px;
          }
        }
      }
    }
  }
}
</style>
