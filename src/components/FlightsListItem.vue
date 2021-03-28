<template>
  <li class="flight">
    <div class="flight__info-block info-block">
      <div class="info-block__main">
        <ul class="info-block__logos">
          <li v-for="segment of segments" :key="segment.arr_time_iso">
            <img
              v-bind:src="
                'https://aviata.kz/static/airline-logos/80x80/' +
                segment.carrier +
                '.png'
              "
              alt=""
            />
          </li>
        </ul>
        <div class="info-block__departure">
          <span>{{ depDate }}</span>
          <span>{{ depTime }}</span>
        </div>
        <div class="info-block__path">
          <ul class="info-block__progressbar">
            <li v-for="destination of segments" :key="destination.arr_time_iso">
              {{ destination.origin_code }}
            </li>
            <li v-if="segments.length">
              {{ segments[segments.length - 1].dest_code }}
            </li>
          </ul>
        </div>
        <div class="info-block__arrival">
          <span>{{ depDate }}</span>
          <span>{{ depTime }}</span>
        </div>
      </div>
      <div class="info-block__footer">
        <a href=""><span>Детали перелета</span></a>
        <a href=""><span>Условия тарифа</span></a>
        <a href=""><span>Невозвратный</span></a>
      </div>
    </div>
    <div class="flight__price price-block">
      <span class="price-block__price">{{ flight.price }}</span>
      <button class="price-block__btn">Выбрать</button>
      <span class="price-block__underbutton">цена за всех пассажиров</span>
      <div class="price-block__footer">
        <span></span>
        <button></button>
      </div>
    </div>
  </li>
</template>

<script>
export default {
  props: {
    flight: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      segments: [],
      depDate: "",
      depTime: "",
    };
  },
  mounted() {
    this.getDepartureData();
  },
  methods: {
    getDepartureData() {
      this.segments = this.flight.itineraries[0][0].segments;
      let editedDate = this.segments[0].dep_time.slice(0, -6).toLowerCase();
      let editedTime = this.segments[0].dep_time.slice(11);
      this.depDate = editedDate;
      this.depTime = editedTime;
    },
    getTravelData() {},
  },
};
</script>

<style scoped>
.flight {
  background-color: #fff;
  border-radius: 4px;
  display: flex;
  margin-bottom: 12px;
}
.flight__info-block {
  display: flex;
  flex-direction: column;
  padding: 20px 40px;
  display: flex;
}
.info-block__main {
  display: flex;
  flex: 1;
  align-items: center;
}
.info-block__logos {
  display: flex;
  flex-basis: 15%;
}
.info-block__logos li {
  margin-right: 5px;
}
.info-block__logos img {
  width: 35px;
  height: 35px;
}
.info-block__departure {
  display: flex;
  flex-direction: column;
  padding-left: 25px;
}
.info-block__departure span {
  text-align: center;
}
.info-block__departure span:first-child {
  font-size: 12px;
}
.info-block__departure span:last-child {
  font-size: 24px;
}
.info-block__path {
  flex: 1;
}
.info-block__progressbar {
  display: flex;
  justify-content: space-between;
}
.info-block__progressbar li {
  flex: 1;
  font-size: 12px;
  position: relative;
  text-align: center;
  text-transform: uppercase;
  color: #7d7d7d;
}
.info-block__progressbar li:before {
  width: 5px;
  height: 5px;
  content: "";
  line-height: 30px;
  border: 0.5px solid #7d7d7d;
  display: block;
  text-align: center;
  margin: 0 auto 10px auto;
  border-radius: 50%;
  background-color: white;
  z-index: 10;
}
.info-block__progressbar li:after {
  width: 100%;
  height: 1px;
  content: "";
  position: absolute;
  background-color: #7d7d7d;
  top: 2px;
  left: -50%;
  /* z-index: -1; */
}
.info-block__progressbar li:first-child:after {
  content: none;
}
.info-block__progressbar li.active {
  color: green;
}
.info-block__progressbar li.active:before {
  border-color: #55b776;
}
.info-block__progressbar li.active + li:after {
  background-color: #55b776;
}
.info-block__arrival {
  display: flex;
  flex-direction: column;
  padding-right: 25px;
}
.info-block__arrival span {
  text-align: center;
}
.info-block__arrival span:first-child {
  font-size: 12px;
}
.info-block__arrival span:last-child {
  font-size: 24px;
}
.info-block__footer {
  display: flex;
  height: 50px;
  align-items: flex-end;
}
.info-block__footer a {
  font-size: 12px;
  margin-right: 12px;
  border-bottom: 1px dashed;
  padding-bottom: 2px;
  color: #7284E4;
}
.flight__price {
  width: 240px;
  display: flex;
  flex-direction: column;
  padding: 20px;
  background-color: #f5f5f5;
}
.price-block__price {
  font-size: 26px;
  font-weight: 400;
}
.price-block__btn {
  background-color: #55bb06;
  border-radius: 4px;
  border: none;
  text-decoration: none;
  color: #fff;
  padding: 8px 25px;
  font-weight: 700;
  font-size: 18px;
  margin: 12px 0;
}
.price-block__underbutton {
  font-size: 12px;
  color: #707276;
}
.flight__price span {
  text-align: center;
}
.flight__info-block {
  flex: 1;
}
</style>