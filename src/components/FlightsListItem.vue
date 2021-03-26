<template>
  <li class="flight">
    <div class="flight__info">
      <div>
        <img src="" alt="">
        <span></span>
        <span>Детали перелета</span>
      </div>
      <div></div>
      <div></div>
      <div></div>
    </div>
    <div class="flight__price price-block">
      <span class="price-block__price">{{flight.price}}</span>
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
};
</script>

<style scoped>
.flight {
  background-color: #fff;
  border-radius: 4px;
  display: flex;
  margin-bottom: 12px;
}
.flight__info {
  padding: 20px;
}
.flight__price {
  width: 240px;
  display: flex;
  flex-direction: column;
  padding: 20px;
  background-color: #F5F5F5;
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
.flight__info {
  flex: 1;
}
</style>