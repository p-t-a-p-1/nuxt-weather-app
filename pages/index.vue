<template>
  <div class="c-contents">
    <div class="c-card">
      <div class="c-card_main">
        <div class="c-card_main_left">
          <p class="c-card_main_temp">18°</p>
          <p class="c-card_main_weather">SUNNY</p>
        </div>
        <div class="c-card_main_right">
          <p class="c-card_main_area">Sapporo</p>
        </div>
      </div>
      <ul class="c-card_week">
        <li class="c-card_date">
          <p class="c-card_date_day">MON</p>
          <font-awesome-icon icon="sun" class="c-card_date_icon" />
          <p class="c-card_date_weather">SUNNY</p>
          <p class="c-card_date_temp">High<span>18°</span></p>
          <p class="c-card_date_temp">Low<span>18°</span></p>
        </li>
        <li class="c-card_date">
          <p class="c-card_date_day">TUE</p>
          <font-awesome-icon icon="cloud" class="c-card_date_icon" />
          <p class="c-card_date_weather">SUNNY</p>
          <p class="c-card_date_temp">High<span>18°</span></p>
          <p class="c-card_date_temp">Low<span>18°</span></p>
        </li>
        <li class="c-card_date">
          <p class="c-card_date_day">WED</p>
          <font-awesome-icon icon="umbrella" class="c-card_date_icon" />
          <p class="c-card_date_weather">SUNNY</p>
          <p class="c-card_date_temp">High<span>18°</span></p>
          <p class="c-card_date_temp">Low<span>18°</span></p>
        </li>
        <li class="c-card_date">
          <p class="c-card_date_day">THU</p>
          <font-awesome-icon icon="sun" class="c-card_date_icon" />
          <p class="c-card_date_weather">SUNNY</p>
          <p class="c-card_date_temp">High<span>18°</span></p>
          <p class="c-card_date_temp">Low<span>18°</span></p>
        </li>
        <li class="c-card_date">
          <p class="c-card_date_day">FRI</p>
          <font-awesome-icon icon="sun" class="c-card_date_icon" />
          <p class="c-card_date_weather">SUNNY</p>
          <p class="c-card_date_temp">High<span>18°</span></p>
          <p class="c-card_date_temp">Low<span>18°</span></p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {}
</script>

<style lang="scss">
.c-contents {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.c-card {
  width: 85%;
}
</style>
