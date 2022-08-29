<template>
  <div class="nav_bar">
    <div class="nav_bar_title">COLORS*</div>
    <div class="nav_bar_pages">
      <div class="nav_bar_page">Продукты</div>
      <div class="nav_bar_page">Цвета</div>
      <div class="nav_bar_page">Вдохновение</div>
      <div class="nav_bar_page">Советы</div>
      <div class="nav_bar_page">Найти магазин</div>
    </div>
    <div class="nav_bar_contact">
      <div class="nav_bar_contact_phone">+7 (495) 221-77-69</div>
      <div class="nav_bar_contact_text">Заказать звонок</div>
    </div>
    <div class="nav_bar_icons">
      <div class="nav_bar_icon"><search /></div>
      <div class="nav_bar_icon"><profile /></div>
      <div class="nav_bar_icon"><heart /></div>
      <div class="nav_bar_icon"><heart /></div>
    </div>
  </div>
</template>

<script>
import search from "./svg/navbar/search.vue";
import profile from "./svg/navbar/profile.vue";
import heart from "./svg/navbar/heart.vue";

export default {
  components: { search, profile, heart },
};
</script>

<style lang="scss" scoped>
.nav_bar {
  font-style: "Inter";
  margin: 0px;
  padding: 35px 20px;
  border: 1px solid #000;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  &_title {
    font-weight: 400;
    font-size: 30px;
  }
  &_pages {
    display: flex;
    align-items: center;
    gap: 24px;
  }
  &_page {
    font-weight: 400;
    font-size: 14px;
    line-height: 100%;
    letter-spacing: 0.06em;
    text-transform: uppercase;
    color: #1f2020;
    transition: 0.3s all ease;
    cursor: pointer;
    &:hover {
      opacity: 0.5;
    }
  }
  &_contact {
  }
  &_contact_phone {
    font-weight: 500;
    line-height: 100%;

    font-size: 16px;
  }
  &_contact_text {
    font-weight: 400;
    font-size: 14px;
    line-height: 100%;
    color: #1f2020;
    opacity: 0.3;
  }
  &_icons {
    display: flex;
    gap: 24px;
  }
  &_icon {
  }
}
</style>