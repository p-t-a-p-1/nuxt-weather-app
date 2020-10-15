<template>
  <div class="c-main_content areaDetail">
    <pre>{{ isDayTime }}</pre>
    <div class="c-card" :class="{ day: isDayTime, night: !isDayTime }">
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
            <span class="-number">{{ day.main.temp }}°</span>
          </p>
        </li>
      </ul>
    </div>

    <div v-if="weatherName === 'clear'" class="c-clear">
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
    <div v-if="weatherName === 'clouds'" class="c-clouds">
      <figure class="c-clouds_first">
        <img src="~assets/img/cloud01.png" />
      </figure>
      <figure class="c-clouds_second">
        <img src="~assets/img/cloud01.png" />
      </figure>
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
      if (!params.name.match(/^[A-Za-z0-9]*$/)) {
        this.error()
      }
      // 時間取得
      const nowHours = new Date().getHours()
      // 昼かどうか
      const isDayTime = nowHours > 6 && nowHours < 17
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

            // 気温の四捨五入
            data.main.temp = Math.floor(data.main.temp)

            fiveDayData.push(data)
          })
        })
      return {
        nowData,
        fiveDayData,
        weatherName,
        isDayTime,
      }
    } catch (err) {
      error({
        statusCode: 404,
      })
    }
  },
}
</script>

<style lang="scss" scoped>
.c {
  &-card {
    padding: 100px 0;
    width: 85%;
    position: absolute;
    top: 0;
    bottom: 0;
    margin: 0;
    z-index: 5;
    color: #fff;
    border-radius: 20px;
    &.day {
      background-color: #007acc;
    }
    &.night {
      background-color: #102030;
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
      }
    }
  }
  &-clear {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    z-index: 10;
    overflow: hidden;
  }
  &-clouds {
    width: 85%;
    height: 100%;
    position: absolute;
    z-index: 10;
    overflow: hidden;
    border-radius: 20px;
    figure {
      width: auto;
      height: 100%;
      background-size: cover;
      margin: auto;
      position: absolute;
      top: 0;
      right: 0;
      bottom: 0;
      left: 0;
      margin: auto;
      overflow: hidden;
      width: 250%;
      height: 100%;
      img {
        border-radius: 20px;
        width: 100%;
        height: 100%;
      }
    }
    &_first {
      animation-name: loop;
      animation-duration: 30s;
      animation-timing-function: linear;
      animation-iteration-count: infinite;
    }
    &_second {
      animation-name: loop;
      animation-duration: 35s;
      animation-timing-function: linear;
      animation-iteration-count: infinite;
    }
    @keyframes loop {
      0% {
        -webkit-transform: translate3d(0, 0, 0);
        transform: translate3d(0, 0, 0);
      }
      100% {
        -webkit-transform: translate3d(-60%, 0, 0);
        transform: translate3d(-60%, 0, 0);
      }
    }
  }
  &-rain {
    $rain_drop_height: 50px;
    width: 100%;
    height: 100%;
    position: absolute;
    z-index: 10;
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
