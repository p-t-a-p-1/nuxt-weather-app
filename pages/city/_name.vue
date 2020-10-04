<template>
  <div class="c-main_content">
    <div class="c-card" :class="weatherName">
      <div class="c-card_main">
        <div class="c-card_main_left">
          <p class="-temp">{{ nowData.main.temp }}°</p>
          <p class="-weather">
            {{ nowData.weather[0].description }}
          </p>
        </div>
        <div class="c-card_main_right">
          <p class="-area">{{ nowData.name }}</p>
        </div>
      </div>
      <ul class="c-card_week">
        <li
          v-for="(day, index) in fiveDayData"
          :key="index"
          class="c-card_week_date"
        >
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
    <div v-if="weatherName === 'rain'" class="c-rain">
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ params, error, $axios }) {
    try {
      let nowData = []
      const fiveDayData = []
      let weatherName = ''
      // OpenWeatherMapApiのベース
      const baseUrl = 'https://api.openweathermap.org/data/2.5/'
      await $axios
        .$get(
          `${baseUrl}weather?q=${params.name},jp&units=metric&lang=ja&appid=${process.env.WEATHER_API_KEY}`
        )
        .then((nowDataResult) => {
          nowData = nowDataResult
          weatherName = nowDataResult.weather[0].main.toLowerCase()
          console.log(weatherName)
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
        weatherName,
      }
    } catch (err) {
      error({
        statusCode: err.response.status,
        message: err.response.data.message,
      })
    }
  },
}
</script>

<style lang="scss">
.c {
  &-main {
    &_content {
      margin: 100px auto;
      height: 550px;
      display: flex;
      justify-content: center;
      text-align: center;
      position: relative;
    }
  }
  &-card {
    padding: 100px 0;
    width: 85%;
    position: absolute;
    top: 0;
    bottom: 0;
    margin: 0;
    z-index: 10;
    &.rain {
      color: #fff;
    }
    &_main {
      display: flex;
      justify-content: space-around;
      &_left {
        .-temp {
          font-size: 5.5rem;
        }
        .-weather {
          font-size: 2.4rem;
        }
      }
      &_right {
        display: flex;
        align-items: center;
        .-area {
          font-size: 3.5rem;
        }
      }
    }
    &_week {
      margin-block-start: 40px;
      display: flex;
      justify-content: space-around;
      &_date {
        font-size: 2rem;
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
  &-rain {
    $rain_drop_height: 50px;
    background-color: #102030;
    width: 100%;
    height: 100%;
    position: absolute;
    z-index: 5;
    border-radius: 20px;
    div {
      position: absolute;
      background-color: rgba(#fff, 0.3);
      top: -$rain_drop_height;
      left: 0;
      width: 1px;
      height: $rain_drop_height;
      transform-origin: center center;
      // アニメーションの名前（keyframes）
      animation-name: rain;
      // アニメーションが始まって終わるまでの時間
      animation-duration: 500ms;
      // 変化の度合い（linearは開始から終了まで一定）
      animation-timing-function: linear;
      // アニメーションの繰り返し回数（infiniteは無限）
      animation-iteration-count: infinite;
    }
    @for $i from 1 through 20 {
      & > div:nth-of-type(#{$i}) {
        // アニメーションが始まる時間を少しずつずらす
        animation-delay: #{$i * 100}ms;
        // 一つずつの雨粒の時間をランダムに
        // 後ろの数値を大きい数字にするほど緩やかな雨粒になる
        animation-duration: random(100) + 800ms;
        left: random(100) + vw;
      }
    }
    @keyframes rain {
      from {
        transform: rotate(-15deg) translateY(-$rain_drop_height);
      }
      to {
        transform: rotate(-20deg) translateY(500px + $rain_drop_height);
      }
    }
  }
}
</style>
